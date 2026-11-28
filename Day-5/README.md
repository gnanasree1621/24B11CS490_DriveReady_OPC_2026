# PDF Question Answering System using RAG

This project lets you ask questions about a PDF and get answers based on
the information found in that document.

It uses a Retrieval-Augmented Generation (RAG) approach. First, the PDF
content is extracted and divided into smaller chunks. Those chunks are
converted into embeddings and stored in a FAISS index. When a question
is entered, the system finds the most relevant chunks and sends them to
a Groq-hosted language model to generate an answer.

## What the project does

-   Accepts a PDF uploaded by the user.
-   Extracts selectable text from the PDF.
-   Uses OCR as a fallback when a page does not contain extractable
    text.
-   Splits the extracted content into overlapping chunks.
-   Converts the chunks into vector embeddings using Sentence
    Transformers.
-   Stores the embeddings in a FAISS index for similarity search.
-   Retrieves the three most relevant chunks for a question.
-   Uses the Groq API to generate an answer using the retrieved PDF
    context.

## Technologies used

-   **Python** -- main programming language.
-   **PyMuPDF** -- reads PDF pages and extracts text.
-   **Tesseract OCR and pytesseract** -- extracts text from scanned
    pages when normal text extraction returns no text.
-   **Pillow** -- handles page images created for OCR.
-   **Sentence Transformers** -- creates text embeddings using
    `all-MiniLM-L6-v2`.
-   **NumPy** -- handles embedding arrays.
-   **FAISS** -- indexes embeddings and retrieves similar content.
-   **Groq API** -- generates answers using the `openai/gpt-oss-20b`
    model.
-   **Google Colab** -- provides the notebook environment and PDF upload
    flow.

## How the system works

1.  **Upload a PDF**\
    The notebook uses the Google Colab file upload window to receive a
    PDF.

2.  **Extract text**\
    PyMuPDF attempts to extract text from each page. If a page has no
    extractable text, the page is rendered as an image and processed
    with Tesseract OCR.

3.  **Split the text into chunks**\
    The extracted text is divided into chunks of 500 characters, with an
    overlap of 100 characters. The overlap helps retain context between
    neighboring chunks.

4.  **Create embeddings**\
    The `all-MiniLM-L6-v2` Sentence Transformer model converts each
    chunk into a vector. The embeddings are normalized and converted to
    `float32` before being added to FAISS.

5.  **Build the FAISS index**\
    The notebook creates a `faiss.IndexFlatIP` index. Since the
    embeddings are normalized, inner-product search can be used to rank
    chunks by cosine similarity.

6.  **Retrieve relevant context**\
    When a question is entered, it is converted into an embedding. FAISS
    searches the index and returns up to three matching chunks.

7.  **Generate an answer**\
    The retrieved chunks and the question are sent to the Groq chat
    completion API. The system prompt instructs the model to answer only
    from the supplied PDF context and to say when the answer is not
    available in the PDF.

8.  **Ask more questions**\
    The notebook continues accepting questions until `exit` is entered.

## Setup and run

This notebook is designed to run in **Google Colab**.

1.  Open `Day_5.ipynb` in Google Colab.
2.  Run the notebook cells from top to bottom.
3.  Install the required packages when prompted. The notebook includes
    installation commands for its dependencies and OCR tools.
4.  Upload the PDF when the upload prompt appears.
5.  Wait for text extraction, chunking, embedding creation, and FAISS
    indexing to finish.
6.  Enter your Groq API key when prompted. The notebook uses `getpass`,
    so the key is entered without being displayed in the output.
7.  Start asking questions about the uploaded PDF.
8.  Enter `exit` to end the question-answering session.

### Main Python packages

The notebook installs or imports these packages for the workflow:

``` bash
pip install pymupdf sentence-transformers faiss-cpu groq numpy pillow pytesseract
```

The notebook also installs Tesseract OCR and uses Google Colab's
`google.colab.files` module for uploading the PDF.

## Example interaction

``` text
Ask a question (or 'exit'): What is the main topic of this document?

Best Matching PDF Content:
[Answer generated from the retrieved PDF context]

Ask a question (or 'exit'): exit
Session ended.
```

The answer will depend on the content of the PDF that was uploaded.

## Important notes

-   The notebook uses Google Colab-specific features, including
    `files.upload()`. It is not ready to run unchanged as a regular
    local Python script.
-   OCR is configured for English (`lang="eng"`).
-   The current chunking settings are 500 characters per chunk and 100
    characters of overlap.
-   The retriever requests up to three relevant chunks.
-   The model is instructed to stay within the retrieved PDF context.
    However, generated answers should still be checked against the
    original document.
-   A valid Groq API key is required. Do not hard-code or publish your
    API key.
-   The notebook contains an initial experiment comparing the output
    dimensions of `all-MiniLM-L6-v2` and `all-mpnet-base-v2`. The main
    retrieval pipeline uses `all-MiniLM-L6-v2`.

## Current scope

This is a notebook-based PDF question-answering prototype. It currently
handles one uploaded PDF per notebook run and uses a simple FAISS
similarity search pipeline. It does not include a web interface, user
accounts, persistent document storage, or multi-PDF management.

## Future improvements

-   Add support for uploading and searching multiple PDF files.
-   Add a simple Streamlit or web interface.
-   Display the source page or retrieved text with each answer.
-   Improve chunking by splitting on paragraphs or sentences.
-   Add support for more OCR languages.
-   Add checks for empty PDFs and pages where OCR cannot extract
    readable text.
