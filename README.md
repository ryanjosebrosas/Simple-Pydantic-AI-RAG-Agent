# Simple Pydantic AI RAG Agent

A powerful AI agent built with Pydantic AI that combines Agentic RAG (Retrieval Augmented Generation) with semantic search capabilities using Supabase vector database.

## Screenshots

### Terminal - Running the Agent
![Terminal](screenshot/Screenshot%202025-11-26%20235756.png)

### Streamlit Chat Interface
![Streamlit UI](screenshot/Screenshot%202025-11-26%20235841.png)

### Project Structure in VS Code
![VS Code](screenshot/Screenshot%202025-11-26%20235905.png)

## Agent Capabilities

- **Agentic RAG**: Query your documents with context-aware intelligence
- **Web Search**: Search the internet for up-to-date information
- **Multi-LLM Support**: Works with OpenAI, OpenRouter, or local Ollama models
- **Streaming UI**: Real-time response streaming in Streamlit interface

## Project Structure

```
Simple-Pydantic-AI-RAG-Agent/
├── .env.example               # Example environment variables
├── requirements.txt           # Project dependencies
├── agent.py                   # Main Pydantic AI agent implementation
├── clients.py                 # Client config for LLMs and databases
├── prompt.py                  # System prompt template
├── tools.py                   # Agent tool implementations
├── streamlit_ui.py            # Streamlit user interface
├── RAG_Pipeline/              # RAG Pipeline components
│   ├── common/                # Common RAG functionality
│   │   ├── db_handler.py      # DB operations for RAG
│   │   ├── text_processor.py  # Functions to prep text for vector DB
│   ├── Local_Files/           # Local file processing
│   │   ├── main.py            # Entrypoint for local file RAG pipeline
│   │   ├── file_watcher.py    # Logic for local file processing
├── sql/                       # SQL scripts for database setup
├── tests/                     # Test suite
```

## Setup Instructions

### Prerequisites

- Python 3.11+
- Supabase project (cloud or local)
- API keys for LLM provider (OpenAI or OpenRouter)

### Environment Setup

1. Clone the repository:
```bash
git clone https://github.com/ryanjosebrosas/SIMPLE-PYDANTIC-AI-RAG-AGENT.git
cd SIMPLE-PYDANTIC-AI-RAG-AGENT
```

2. Create and activate a virtual environment:
```bash
# Create a virtual environment
python -m venv venv

# Activate the virtual environment
# On Windows:
venv\Scripts\activate
# On macOS/Linux:
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt
```

3. Create a `.env` file by copying the example:
```bash
# Windows
copy .env.example .env
# macOS/Linux
cp .env.example .env
```

4. Configure your `.env` file with your API keys and settings.

### Environment Configuration

#### LLM Configuration

```
LLM_PROVIDER=openai
LLM_BASE_URL=https://api.openai.com/v1
LLM_API_KEY=your_api_key_here
LLM_CHOICE=gpt-4o-mini
```

#### Embedding Configuration

```
EMBEDDING_PROVIDER=openai
EMBEDDING_BASE_URL=https://api.openai.com/v1
EMBEDDING_API_KEY=your_api_key_here
EMBEDDING_MODEL_CHOICE=text-embedding-3-small
```

#### Database Configuration

```
SUPABASE_URL=your_supabase_url
SUPABASE_SERVICE_KEY=your_supabase_service_key
```

## Database Setup

1. Create a Supabase project at [https://supabase.com](https://supabase.com)

2. Run the SQL scripts in the `sql` directory:
   - `sql/documents.sql`: Creates the documents table with vector embeddings
   - `sql/document_metadata.sql`: Creates the document metadata table
   - `sql/document_rows.sql`: Creates the table for tabular data
   - `sql/execute_sql_rpc.sql`: Creates the RPC function for executing SQL queries

## Running the RAG Pipeline

The RAG Pipeline processes documents and stores them in the vector database.

### Local Files Pipeline

1. Configure the pipeline by editing `RAG_Pipeline/Local_Files/config.json`:
```json
{
  "watch_directory": "your/folder/to/watch"
}
```

2. Activate the RAG Pipeline virtual environment:
```bash
cd RAG_Pipeline
python -m venv venv
venv\Scripts\activate  # Windows
# source venv/bin/activate  # macOS/Linux
pip install -r requirements.txt
```

3. Run the pipeline:
```bash
python Local_Files/main.py
```

The script monitors for new, updated, or deleted files and syncs with Supabase.

## Running the Agent

1. Activate the virtual environment:
```bash
venv\Scripts\activate  # Windows
# source venv/bin/activate  # macOS/Linux
```

2. Run the Streamlit UI:
```bash
streamlit run streamlit_ui.py
```

3. Open your browser to http://localhost:8501

## Troubleshooting

- **Vector Dimensions Mismatch**: Ensure embedding dimensions match your model (OpenAI: 1536, Ollama nomic-embed-text: 768)
- **Function Calling Support**: Use models that support function calling (GPT-4, Qwen, etc.)
