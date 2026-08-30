# LLM Engineering - Cuisine Assistant

A comprehensive LLM engineering project demonstrating advanced AI application development with specialized focus on authentic Bihari cuisine.

---

## 📋 Project Overview

This repository showcases LLM (Large Language Model) engineering practices and contains practical applications built with modern AI frameworks. The main focus is on **MyTaste**, an intelligent Bihari cuisine assistant.

---

## 🏗️ Project Architecture

### High-Level Architecture Diagram

```
┌─────────────────────────────────────────────────────────────────┐
│                        User Interface Layer                       │
│                   (Gradio Web Interface)                          │
│              http://127.0.0.1:7860                                │
└────────────────────────┬────────────────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────────────────┐
│                    Application Logic Layer                        │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │           Chat Handler & Message Processing              │   │
│  │  - Conversation History Management                       │   │
│  │  - Message Routing                                       │   │
│  │  - Response Formatting                                   │   │
│  └──────────────────────────────────────────────────────────┘   │
└────────┬───────────────────────────────┬───────────────────────┘
         │                               │
         ▼                               ▼
┌──────────────────────────┐  ┌──────────────────────────┐
│   LLM Integration Layer  │  │   Database Layer         │
│  (Google Gemini API)     │  │   (SQLite)               │
│                          │  │                          │
│ ┌──────────────────────┐ │  │ ┌────────────────────┐  │
│ │ OpenAI-Compatible   │ │  │ │  bihari_food table │  │
│ │ API Client          │ │  │ │                    │  │
│ └──────────────────────┘ │  │ │ - dish             │  │
│ ┌──────────────────────┐ │  │ │ - description      │  │
│ │ Function Calling     │ │  │ │ - ingredients      │  │
│ │ (Tool Execution)     │ │  │ │ - preparation      │  │
│ └──────────────────────┘ │  │ │ - region           │  │
└──────────────┬───────────┘  │ └────────────────────┘  │
               │              └──────────────┬───────────┘
               │                             │
               └─────────────────┬───────────┘
                                 ▼
                    ┌──────────────────────────┐
                    │   External Services      │
                    │ (Google Gemini API)      │
                    │ (with API Key Auth)      │
                    └──────────────────────────┘
```

### Component Architecture

#### 1. **Presentation Layer (Frontend)**
- **Technology**: Gradio
- **Responsibility**: 
  - Provides user-friendly chat interface
  - Manages user input and output display
  - Maintains UI state and session context
  - Real-time communication with backend

#### 2. **Application Layer (Core Logic)**
- **Components**:
  - **Chat Engine**: Handles message processing and routing
  - **Conversation Manager**: Maintains chat history for context
  - **Response Handler**: Formats and processes LLM responses
  - **Error Handler**: Manages exceptions and edge cases

#### 3. **LLM Integration Layer**
- **Technology**: Google Gemini 3.6 Flash
- **Integration Method**: OpenAI-compatible API
- **Key Features**:
  - System prompt management (Bihari cuisine specialization)
  - Function calling mechanism
  - Token management
  - Response parsing

#### 4. **Data Layer**
- **Database**: SQLite (`food.db`)
- **Schema**: Single table `bihari_food` with structured food data
- **Operations**: 
  - Read-only queries for food details
  - LLM-triggered function calls
  - Data retrieval and formatting

### Data Flow Architecture

```
1. USER INPUT
   └─> Gradio Interface
       
2. MESSAGE PROCESSING
   └─> Chat Engine receives message
       └─> Adds to conversation history
           
3. LLM PROCESSING
   └─> Sends to Google Gemini API
       └─> With system prompt (Bihari cuisine focus)
           └─> With conversation context
               
4. FUNCTION CALLING DECISION
   ├─> If LLM decides data is needed:
   │   └─> Calls get_bihari_food_details()
   │       └─> Queries SQLite database
   │           └─> Returns dish information
   │               └─> Feeds back to LLM
   │
   └─> LLM generates final response
       
5. RESPONSE DELIVERY
   └─> Formats response for display
       └─> Sends back to Gradio UI
           └─> USER SEES RESPONSE
```

### Technology Stack Architecture

```
┌─────────────────────────────────────────┐
│       Jupyter Notebook Environment      │
│  (Development & Experimentation)        │
└──────────────┬──────────────────────────┘
               │
       ┌───────┴────────┐
       │                │
       ▼                ▼
┌────────────────┐ ┌──────────────────┐
│   Python 3.12+ │ │  Virtual Env     │
│                │ │  (UV Package     │
│                │ │   Manager)       │
└────────────────┘ └──────────────────┘
       │
       ▼
┌─────────────────────────────────────────┐
│        Core Dependencies                 │
├─────────────────────────────────────────┤
│ - Gradio (>=6.26.0)      → UI/UX       │
│ - OpenAI (>=3.6.0)       → LLM Client  │
│ - python-dotenv (>=1.2.3)→ Env Config  │
│ - ipykernel (>=7.3.0)    → Notebook    │
│ - sqlite3                → Database    │
│ - requests               → HTTP Calls  │
└─────────────────────────────────────────┘
       │
       ▼
┌──────────────────────────────────────────┐
│    External APIs & Services              │
├──────────────────────────────────────────┤
│ Google Gemini API (OpenAI compatible)   │
│ Authentication: API Key via .env         │
│ Base URL: generativelanguage.googleapis  │
└──────────────────────────────────────────┘
```

### File Organization Architecture

```
LLM_Engineering-CuisineAssistant/
│
├── CuisineAssitant/                    # Main project directory
│   └── MyTaste/                        # Bihari Cuisine Assistant
│       ├── Cuisine/
│       │   ├── Taste.ipynb            # Main implementation notebook
│       │   └── food.db                # SQLite database
│       ├── src/
│       │   └── mytaste/
│       │       └── __init__.py        # Package initialization
│       ├── pyproject.toml             # Project metadata & deps
│       ├── uv.lock                    # Locked dependencies
│       └── README.md                  # Sub-project documentation
│
├── .env                               # Environment variables
├── README.md                          # Main documentation
└── .gitignore                         # Git configuration
```

### Execution Flow Sequence Diagram

```
User
  │
  ├─> Types message in Gradio UI
  │
  ▼
┌────────────────────────────┐
│  Gradio Interface          │
│  - Captures user input     │
│  - Displays conversation   │
└────────────┬───────────────┘
             │
             ▼
┌────────────────────────────┐
│  Chat Handler              │
│  - Prepares message        │
│  - Loads conversation hist │
└────────────┬───────────────┘
             │
             ▼
┌────────────────────────────┐
│  System Setup              │
│  - System prompt injected  │
│  - Function tools loaded   │
│  - Context prepared        │
└────────────┬───────────────┘
             │
             ▼
┌────────────────────────────┐
│  Google Gemini API Call    │
│  - Message + history sent  │
│  - System prompt included  │
└────────────┬───────────────┘
             │
             ▼ (Decision Tree)
        ┌────┴────┐
        │          │
    Uses Data   No Data Needed
        │          │
        ▼          │
┌─────────────┐    │
│  Function   │    │
│  Calling    │    │
│  get_bihari_│    │
│  food_      │    │
│  details()  │    │
└────┬────────┘    │
     │             │
     ▼             │
┌──────────────┐   │
│  Query SQLite│   │
│  Database    │   │
└────┬─────────┘   │
     │             │
     ▼             │
┌──────────────┐   │
│  Return Food │   │
│  Details     │   │
└────┬─────────┘   │
     │             │
     └──────┬──────┘
            │
            ▼
┌────────────────────────────┐
│  LLM Response Generation   │
│  (with or without data)    │
└────────────┬───────────────┘
             │
             ▼
┌────────────────────────────┐
│  Response Formatting       │
│  - Parse response          │
│  - Add to history          │
└────────────┬───────────────┘
             │
             ▼
┌��───────────────────────────┐
│  Display in Gradio         │
│  - Show assistant response │
└────────────┬───────────────┘
             │
             ▼
           User sees answer
```

### Interaction Matrix

| Component | Interacts With | Method | Purpose |
|-----------|---|---|---|
| Gradio UI | Chat Handler | Function calls | I/O handling |
| Chat Handler | LLM Layer | API calls | Message processing |
| Chat Handler | Database Layer | Function calling | Data retrieval |
| LLM Layer | Google Gemini | REST API | LLM inference |
| Database Layer | SQLite DB | SQL queries | Data operations |
| Config | .env file | Environment vars | Authentication |

---

## 🍲 MyTaste: Bihari Cuisine Assistant

### Overview
MyTaste is an LLM-powered interactive application that serves as a specialized assistant for authentic Bihari cuisine. It combines Google's Gemini AI with a SQLite database and Gradio UI to provide an engaging culinary experience.

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
