ShopMate AI
ShopMate AI is a conversational shopping assistant built with
Python, Groq API, and the OpenAI Python SDK. It helps users
explore a small product catalog, check product prices and colors, and
find items based on their budget and preferences.

The chatbot supports English and Telugu responses and maintains recent
conversation context while the notebook session is running.
Features
- Conversational shopping: Ask questions naturally, just like
  chatting with a shopping assistant.
- Product catalog: Includes sample products with prices,
  categories, and available colors.
- Budget-based suggestions: Ask for products within a particular
  budget.
- Product information: Ask about product prices and available
  colors.
- Conversation history: Uses recent messages to maintain context
  during a chat session.
- English and Telugu: The system prompt instructs the assistant to
  respond in the customer's language.
- Prompt instructions: The assistant is instructed not to invent
  products, prices, or discounts.
- Basic error handling: Displays friendly messages for API
  rate-limit and connection errors.
Technologies Used
- Python
- Google Colab
- Groq API
- OpenAI Python SDK
- openai/gpt-oss-20b language model
Sample Product Catalog
The notebook currently contains the following sample products:

  Product             Price Category      Available Colors
  Kurti                ₹599 Fashion       Black, Pink, Blue
Anarkali dress       ₹899 Fashion       Red, Blue
Jeans                ₹799 Fashion       Black, Blue
Sneakers           ₹1,299 Footwear      White, Black
Handbag              ₹499 Accessories   Brown, Black

These are example catalog entries defined directly in the notebook. They
are not live store inventory or real-time product listings.
Getting Started
1. Open the notebook
Open the project notebook in Google
Colab.
2. Install the required package
Run the following cell:
!pip install openai
3. Get a Groq API key
1. Visit the Groq Console and create an
   API key.
2. In Google Colab, open the Secrets panel from the left sidebar.
3. Add a secret named GROQ_API_KEY.
4. Paste your Groq API key as its value and allow notebook access.
4. Configure the Groq client
The notebook uses the OpenAI SDK with Groq's OpenAI-compatible API
endpoint:
from openai import OpenAI
from google.colab import userdata

client = OpenAI(
    api_key=userdata.get("GROQ_API_KEY"),
    base_url="https://api.groq.com/openai/v1"
)
Security: Never hard-code your API key or commit it to GitHub. Store
it in Colab Secrets.
How to Run
Run the notebook cells in order. The main chatbot configuration defines
the model and sample product catalog:
MODEL = "openai/gpt-oss-20b"

PRODUCTS = {
    "kurti": {"price": 599, "category": "Fashion", "color": ["Black", "Pink", "Blue"]},
    "anarkali dress": {"price": 899, "category": "Fashion", "color": ["Red", "Blue"]},
    "jeans": {"price": 799, "category": "Fashion", "color": ["Black", "Blue"]},
    "sneakers": {"price": 1299, "category": "Footwear", "color": ["White", "Black"]},
    "handbag": {"price": 499, "category": "Accessories", "color": ["Brown", "Black"]}
}
The system prompt includes the product catalog and gives the assistant
instructions about product recommendations, prices, customer
preferences, language, and response style.

The notebook stores the system prompt and recent chat messages in a
conversation history:
history = [{"role": "system", "content": SYSTEM}]
MAX_TURNS = 8
To start chatting, run the final cell. You can enter shopping questions
at the You: prompt.

Type bye, exit, or quit to end the chat.
Example Conversation
Welcome to ShopMate AI!

You: hi
ShopMate: Hey there! How can I help you find something special today?

You: i want pink kurti for my birthday under the budget
ShopMate: The pink kurti is ₹599. What's your budget range?

You: 1000
ShopMate: The pink kurti is ₹599, well under your ₹1,000 budget.

You: tell me the cost of all items
ShopMate: Here's the price list for all items in our catalog:
- Kurti – ₹599
- Anarkali dress – ₹899
- Jeans – ₹799
- Sneakers – ₹1,299
- Handbag – ₹499

You: bye
ShopMate: Happy shopping! Visit again!
Example output is taken from a sample run; responses may vary.
Additional Functions in the Notebook
The notebook defines two helper functions with a logging decorator:
- get_product_price(item, qty=1): Calculates the total price for a
  product and quantity.
- search_products(category): Returns products matching a category.
The @log_call decorator prints the function name and returned result
when either helper is called.

Current implementation note: These helper functions are defined
separately but are not connected as automatic tools in the chatbot's
chat() request. The chatbot currently receives the catalog through its
system prompt.
Current Limitations
- The product catalog is hard-coded in the notebook; there is no
  database or live store connection.
- Product prices and colors are sample data and may need updating.
- Conversation history exists only in the running Python session and
  is not saved permanently.
- The chatbot uses the product catalog in its prompt, but the code
  does not enforce every answer through programmatic product lookup.
- The helper functions for price calculation and category search are
  not yet called automatically by the language model.
- The chatbot handles rate-limit and API-connection errors, but other
  API or input errors may still need handling.
Future Improvements
- Connect a real product database or store API.
- Integrate product search and price functions into the chatbot's
  tool-calling flow.
- Add stricter validation so product recommendations and prices always
  come directly from catalog data.
- Save conversation history between sessions.
- Add product filters for size, ratings, discounts, and availability.
- Build a simple web-based chat interface.
Project Structure
ShopMate-AI/
│
├── ShopMate_AI.ipynb
└── README.md
The notebook filename shown above is an example. Use the actual
filename when adding it to your GitHub repository.
Author
ShopMate AI --- LLM-based conversational shopping assistant
prototype.
This project was created for learning and experimentation with LLMs and
API-based chatbot development.
