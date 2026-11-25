# ShopMate AI

ShopMate AI is a conversational shopping assistant built using **Python, LangChain, and Groq API**. It helps customers explore products, check prices, find available colors, and receive personalized shopping recommendations.

## Features

- Conversational shopping assistance.
- Product information and pricing.
- Available color details.
- Product recommendations based on customer preferences.
- Conversation history during the current session.
- Excel-based chatbot response testing.
- LangChain agent implementation.

## Technologies Used

- Python
- Google Colab
- LangChain
- LangChain-Groq
- Groq API
- Pandas
- OpenPyXL

## Product Catalog

| Product | Price | Available Colors |
|---|---:|---|
| Kurti | Rs 599 | Black, Pink, Blue |
| Anarkali Dress | Rs 899 | Red, Blue |
| Jeans | Rs 799 | Black, Blue |
| Sneakers | Rs 1299 | White, Black |
| Handbag | Rs 499 | Brown, Black |

## Installation and Setup

### 1. Install Required Libraries

```python
!pip install -q langchain langchain-groq pandas openpyxl
```

### 2. Configure Groq API Key

Add your `GROQ_API_KEY` in Google Colab Secrets.

```python
import os
from google.colab import userdata

os.environ["GROQ_API_KEY"] = userdata.get("GROQ_API_KEY")
```

### 3. Initialize the Language Model

```python
from langchain_groq import ChatGroq

llm = ChatGroq(
    model="openai/gpt-oss-120b",
    temperature=0.3
)
```

## How ShopMate AI Works

### 1. System Prompt

The system prompt defines the role and behavior of ShopMate AI.

It instructs the chatbot to:

- Help customers find suitable products.
- Provide correct product prices and colors.
- Avoid inventing products, prices, or discounts.
- Ask about customer budgets and preferences.
- Recommend products based on customer requirements.
- Remember customer preferences during conversations.
- Respond in English or Telugu based on the customer's language.
- Keep responses under 80 words.

### 2. Conversation Chain

ShopMate AI uses LangChain's `ChatPromptTemplate`, `MessagesPlaceholder`, and `StrOutputParser` to process customer questions.

The `ask()` function maintains conversation history so the chatbot can remember previous messages during the active session.

Example:

```python
print(ask("Hi, I'm Sree. Do you have kurtis?"))
print(ask("What's my name?"))
```

### 3. Excel-Based Testing

ShopMate AI is tested using an Excel file named `tests.xlsx`.

The Excel file contains two columns:

- `question` – Customer question.
- `must_include` – Expected information in the chatbot's answer.

Example:

| question | must_include |
|---|---|
| How much is a kurti? | Rs 599 |
| What colors are available in kurtis? | Black, Pink, Blue |
| How much is an Anarkali dress? | Rs 899 |
| Do you have sneakers? | Yes, Rs 1299 |
| Which products are available under Rs 600? | Kurti Rs 599, Handbag Rs 499 |

The testing function reads the Excel file using Pandas and checks whether the chatbot response contains the expected information.

It displays PASS or FAIL for each test and calculates the overall test score.

**Note:** The current testing method uses exact substring matching. Differences in currency symbols, whitespace, and wording may cause a correct answer to show FAIL.

### 4. LangChain Agent

ShopMate AI also uses LangChain's `create_agent()` function to initialize a conversational agent.

```python
from langchain.agents import create_agent

agent_order = create_agent(
    model=llm,
    tools=[],
    system_prompt=SYSTEM
)

result_order = agent_order.invoke({
    "messages": [
        {"role": "user", "content": "Do you have a pink kurti?"}
    ]
})

print(result_order["messages"][-1].content)
```

Currently, the agent is initialized without external tools. It responds using the system instructions and language model.

## Current Limitations

- Product information is predefined in the system prompt.
- No database integration.
- No live product availability checking.
- No cart or checkout functionality.
- Conversation history is not permanently stored.
- No external tools are connected to the agent.

## Future Enhancements

- Integrate a product database.
- Add product search and price-checking tools.
- Implement shopping cart functionality.
- Add order management.
- Store customer preferences and conversation history.
- Improve automated response evaluation.
- Develop a user-friendly web interface.

## Project Status

**Prototype / Learning Project**

ShopMate AI currently demonstrates conversational shopping assistance using LangChain and Groq. Additional integrations are required to make it a complete shopping application.
