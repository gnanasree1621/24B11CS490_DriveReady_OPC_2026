# ShopMate AI – Fashion Shopping Assistant

## About the Project

ShopMate AI is an AI-powered fashion shopping assistant designed to make online shopping easier and more convenient. It helps customers explore fashion products, check prices, find available sizes and colours, and get product recommendations based on their budget.

Customers can interact with the assistant using natural language in English or Telugu. Instead of searching through a product catalog manually, they can simply describe what they are looking for and receive suitable suggestions.

The application also supports order collection and stores confirmed customer orders in Google Sheets for easy tracking and management.

## Features

- **Product Information:** Provides details about available fashion products.
- **Price Checking:** Calculates product prices based on the selected quantity.
- **Product Availability:** Displays available sizes and colours.
- **Budget-Based Recommendations:** Suggests products according to the customer's budget.
- **Order Management:** Collects customer details and validates order information before saving.
- **Google Sheets Integration:** Automatically stores confirmed orders in a Google Sheet.
- **Conversation History:** Maintains previous messages to support continuous conversations.
- **Multilingual Support:** Allows customers to interact in English and Telugu.

## Technologies Used

| Technology | Purpose |
|---|---|
| Python | Main programming language |
| LangChain | Agent creation and tool integration |
| ChatGroq | Language model integration |
| GPT-OSS-20B | Model used for generating responses |
| Pydantic | Order data validation |
| Google Colab | Development and execution environment |
| Google Sheets | Customer order storage |
| gspread | Connecting Python with Google Sheets |

## Project Workflow

1. The customer sends a shopping-related message.
2. ShopMate AI understands the customer's request.
3. The agent selects the appropriate tool based on the request.
4. Product details, prices, sizes and colours are retrieved from the catalog.
5. Suitable recommendations are provided to the customer.
6. When a customer wants to place an order, the assistant collects the required details.
7. The customer reviews and confirms the order.
8. The order is validated and saved to Google Sheets.
9. The assistant displays the order summary and total amount.

## Available Shopping Tools

The project uses four main tools:

**1. get_price()**

Calculates the total price of a selected product based on quantity.

**2. check_product()**

Checks product details, including price, available colours and sizes.

**3. recommend_products()**

Suggests products that fit within the customer's specified budget.

**4. log_order()**

Validates the customer's order details and saves confirmed orders to Google Sheets.

## Sample Product Catalog

The current project includes the following sample products:

| Product | Price |
|---|---:|
| Kurti | ₹599 |
| Anarkali Dress | ₹899 |
| Saree | ₹1,299 |
| Jeans | ₹799 |
| Top | ₹499 |
| Handbag | ₹699 |

The product catalog can be modified to include additional products, prices, sizes and colours.

## Installation and Setup

### 1. Install Required Libraries

```bash
pip install langchain langchain-groq gspread
```

### 2. Configure API Key

Create a Groq API key and store it securely in Google Colab Secrets using the name:

```text
GROQ_API_KEY
```

### 3. Google Sheets Authentication

Authenticate your Google account and authorize access using `gspread`.

The application creates or opens a Google Sheet named **ShopMate AI Orders** to store customer orders.

### 4. Run the Application

Execute the notebook cells in the following order:

1. Library installation and API configuration.
2. Google Sheets authentication.
3. Product catalog creation.
4. Pydantic order validation.
5. Shopping tool definitions.
6. Agent creation.
7. Conversation history and chat function.
8. Test the chatbot.

## Example Interaction

**Customer:** Hi, I am looking for a kurti.

**ShopMate AI:** Sure! We have kurtis available for ₹599. Would you like to know the available colours and sizes?

**Customer:** What colours are available?

**ShopMate AI:** We have Black, Pink and Blue. Available sizes are S, M, L and XL.

**Customer:** My budget is ₹700. Can you suggest something?

**ShopMate AI:** You can choose a Kurti for ₹599 or a Top for ₹499. Both are within your budget.

**Customer:** I want to order two black kurtis in size M.

**ShopMate AI:** Please share your name and preferred delivery date so I can prepare your order.

## Future Enhancements

The following features can be added to improve the application:

- Integration with a real product database.
- Product image display and visual search.
- Shopping cart functionality.
- User registration and login.
- Order tracking and delivery status.
- Payment gateway integration.
- Admin dashboard for managing products and orders.
- Web-based interface using Streamlit or React.
- Integration with real-time inventory management.

## Conclusion

ShopMate AI provides a conversational approach to fashion shopping. It combines an AI-powered agent with product information tools and Google Sheets integration to simplify product discovery and order collection.

The project demonstrates how Large Language Models, tool calling, data validation and external services can work together to build a practical shopping assistant.

---

**Project Name:** ShopMate AI – Fashion Shopping Assistant  
**Category:** Artificial Intelligence / E-Commerce  
**Development Environment:** Google Colab  
**Primary Language:** Python
