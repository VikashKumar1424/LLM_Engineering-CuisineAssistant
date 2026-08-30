# LLM Engineering - Cuisine Assistant

A comprehensive LLM engineering project demonstrating advanced AI application development with specialized focus on authentic Bihari cuisine.

---

## 📋 Project Overview

This repository showcases LLM (Large Language Model) engineering practices and contains practical applications built with modern AI frameworks. The main focus is on **MyTaste**, an intelligent Bihari Cuisine Assistant that leverages AI-powered conversational interfaces and structured data management.

---

## 🍲 MyTaste: Bihari Cuisine Assistant

### Overview
MyTaste is an LLM-powered interactive application that serves as a specialized assistant for authentic Bihari cuisine. It combines Google's Gemini AI with a SQLite database and Gradio UI to provide users with detailed information about traditional Bihari dishes, recipes, ingredients, and cooking methods.

### 🎯 Key Features

1. **AI-Powered Chat Interface**
   - Leverages Google Gemini 3.6 Flash LLM (via OpenAI-compatible API)
   - Specialized system prompt focused exclusively on Bihari cuisine
   - Maintains conversation history for contextual responses
   - Politely redirects non-Bihari food queries

2. **Database Integration**
   - SQLite database (`food.db`) storing authentic Bihari dishes
   - Structured data includes: dish name, description, ingredients, preparation methods, and regional information
   - Function calling mechanism for LLM to query food details

3. **Interactive Web UI**
   - Built with Gradio for user-friendly chatbot interface
   - Local deployment on `http://127.0.0.1:7860`
   - Real-time chat with the Bihari cuisine assistant

4. **LLM Function Calling**
   - Implements OpenAI-compatible tool calling
   - `get_bihari_food_details()` function allows the LLM to retrieve specific dish information
   - Enables context-aware responses with accurate data

### 📁 Project Structure

```
CuisineAssitant/MyTaste/
├── Cuisine/
│   ├── Taste.ipynb          # Main Jupyter notebook with full implementation
│   └── food.db              # SQLite database with Bihari food data
├── src/
│   └── mytaste/
│       └── __init__.py      # Package entry point
├── pyproject.toml           # Project configuration and dependencies
├── uv.lock                  # Dependency lock file
└── README.md                # Project documentation
```

### 📦 Dependencies

- **gradio** (>=6.26.0) - Web UI framework for interactive interfaces
- **openai** (>=3.6.0) - LLM API client for Gemini integration
- **python-dotenv** (>=1.2.3) - Environment variable management
- **ipykernel** (>=7.3.0) - Jupyter kernel support
- **Python** >= 3.12

### ⚙️ How It Works

1. **Initialization**: Loads Google Gemini API key from `.env` file
2. **System Prompt**: Sets up the LLM with strict Bihari cuisine specialization
3. **Database Setup**: Creates/initializes SQLite table for food data
4. **Chat Flow**:
   - User sends a message through Gradio interface
   - LLM processes the message and may call `get_bihari_food_details()` function
   - Function queries the database for dish information
   - LLM generates informed response with retrieved data
   - Response displays in chat interface

### 🔧 Configuration

- **LLM API**: Google Gemini via OpenAI-compatible endpoint
- **Base URL**: `https://generativelanguage.googleapis.com/v1beta/openai/`
- **Authentication**: Requires `.env` file with `GOOGLE_API_KEY`

### 🚀 Getting Started

#### Prerequisites
- Python 3.12 or higher
- Google Gemini API key (get from [Google AI Studio](https://aistudio.google.com))

#### Installation

1. Clone the repository:
```bash
git clone https://github.com/VikashKumar1424/LLM_Engineering-CuisineAssistant.git
cd LLM_Engineering-CuisineAssistant
```

2. Navigate to MyTaste project:
```bash
cd CuisineAssitant/MyTaste
```

3. Set up environment variables:
```bash
echo "GOOGLE_API_KEY=your_api_key_here" > .env
```

4. Install dependencies using UV:
```bash
uv sync
```

#### Running the Application

1. Open the Jupyter notebook:
```bash
jupyter notebook Cuisine/Taste.ipynb
```

2. Run all cells to initialize the application

3. The Gradio interface will launch at `http://127.0.0.1:7860`

4. Start asking questions about Bihari cuisine!

### 📚 Example Queries

- "What is Litti Chokha?"
- "How do you make Sattu Paratha?"
- "Tell me about the regional variations of Bihari cuisine"
- "What are the traditional ingredients used in Bihari cooking?"

### 💾 Database Schema

The `food.db` SQLite database contains the following table:

```sql
CREATE TABLE bihari_food (
    dish TEXT PRIMARY KEY,
    description TEXT,
    ingredients TEXT,
    preparation TEXT,
    region TEXT
)
```

### 🛠️ Technology Stack

| Component | Technology |
|-----------|-----------|
| LLM | Google Gemini 3.6 Flash |
| Backend | Python 3.12+ |
| Frontend | Gradio |
| Database | SQLite |
| Package Manager | UV |
| Notebook | Jupyter |

### 📝 Implementation Details

#### System Prompt
The assistant operates with a specialized system prompt that restricts responses to authentic Bihari cuisine only:

```
You are a helpful assistant specializing exclusively in authentic Bihari cuisine.
You provide detailed information only about traditional Bihari food, including:
- Bihari dishes
- Ingredients
- Recipes
- Cooking methods
- Regional variations
- Food history and traditions
- Serving methods
```

#### Tool Definition
```python
food_function = {
    "name": "get_bihari_food_details",
    "description": "Get detailed information about an authentic Bihari dish",
    "parameters": {
        "type": "object",
        "properties": {
            "dish": {
                "type": "string",
                "description": "The authentic Bihari dish for which the user wants information."
            }
        },
        "required": ["dish"]
    }
}
```

### 🎓 Learning Outcomes

This project demonstrates:
- **LLM Integration**: Using OpenAI-compatible APIs with Google Gemini
- **Function Calling**: Implementing tool calling for LLM-to-database interaction
- **Prompt Engineering**: Creating specialized system prompts
- **UI Development**: Building interactive interfaces with Gradio
- **Database Management**: SQLite integration with Python
- **Best Practices**: Professional project structure with pyproject.toml
- **Jupyter Notebooks**: Exploratory development and documentation

### 📖 Repository Language Composition

- **Jupyter Notebook**: 99.8%
- **Python**: 0.2%

### 🤝 Contributing

Contributions are welcome! Feel free to:
- Add more Bihari dishes to the database
- Enhance the UI/UX
- Improve documentation
- Suggest new features

### 📄 License

This project is open source and available under the MIT License.

### 👤 Author

**Vikash Kumar**
- GitHub: [@VikashKumar1424](https://github.com/VikashKumar1424)

### 🔗 Resources

- [Google Gemini API Documentation](https://ai.google.dev/)
- [Gradio Documentation](https://www.gradio.app/docs/)
- [OpenAI Python Client](https://github.com/openai/openai-python)
- [SQLite Documentation](https://www.sqlite.org/docs.html)

---

## 🙏 Acknowledgments

- Google for Gemini API
- Gradio team for the UI framework
- Python community for excellent libraries

---

**Last Updated**: August 30, 2026
