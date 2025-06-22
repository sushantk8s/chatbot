# CrewAI Chatbot with Ollama

A fully-featured chatbot application that combines CrewAI for agent-based AI processing with Ollama for local language models, wrapped in a clean, responsive user interface.

## Features

- **FastAPI Backend**: Robust API with both REST and WebSocket endpoints
- **CrewAI Integration**: Uses agent-based AI framework for collaborative problem-solving
- **Ollama Integration**: Local LLM support with various models
- **Real-time Communication**: WebSocket for instant message delivery
- **Responsive UI**: Clean, modern interface that works on all devices
- **Configurable**: Select different models and toggle CrewAI functionality
- **Docker Support**: Containerized application that connects to Ollama running on the host


## Prerequisites

- Docker and Docker Compose (for containerized setup)
- Ollama installed and running on your host machine (https://ollama.com/)
- At least one model pulled in Ollama (e.g., `ollama pull llama2`)

## Quick Start

1. **Clone this repository**:
   ```bash
   git clone https://github.com/yourusername/crewai-chatbot.git
   cd crewai-chatbot
   ```

2. **Start Ollama on your host machine**:
   ```bash
   ollama serve
   ```

3. **Pull required models**:
   ```bash
   ollama pull llama2
   # Optional: Pull additional models
   ollama pull mistral
   ollama pull phi
   ollama pull gemma
   ```

4. **Start the application with Docker**:
   ```bash
   docker-compose up --build
   ```

5. **Access the chatbot** at http://localhost:8000 or direct open html page on browser

## Usage

### Basic Chat

1. Type your question or message in the input box
2. Press Enter or click the Send button
3. Receive a response from the AI model

### Advanced Features

- **Change the Model**: Click the settings gear icon (⚙️) and select a different model
- **Use CrewAI**: Enable multi-agent processing by checking "Use CrewAI" in settings
  - This mode is slower but provides more comprehensive responses
  - Great for complex queries or when you need multiple perspectives

## Project Structure

```
├── main.py                  # FastAPI backend application with integrated HTML frontend
├── requirements.txt         # Python dependencies
├── Dockerfile               # Docker configuration for the application
├── docker-compose.yml       # Docker Compose configuration
└── static/                  # Auto-generated directory for static files
    └── index.html           # Auto-generated frontend HTML file
```

## Docker Configuration

The Docker setup is configured to connect to Ollama running on your host machine:

- For macOS and Windows: Uses `host.docker.internal` to connect to the host
- For Linux: May require using host network mode or host IP address

You can adjust these settings in the `docker-compose.yml` file.

## Development

### Running Without Docker

1. Create a virtual environment:
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

3. Start the application:
   ```bash
   uvicorn main:app --reload --host 0.0.0.0 --port 8000
   ```

### Customizing the Frontend

The frontend HTML is generated from the template in `main.py`. To customize:

1. Modify the `get_html_content()` function in `main.py`
2. Restart the application
3. Alternatively, edit the generated `static/index.html` file directly

### Adding New Models

1. Pull the model in Ollama:
   ```bash
   ollama pull new-model-name
   ```

2. Add the model to the dropdown in the HTML template (in `get_html_content()` function)

## How It Works

### CrewAI Integration

The application uses CrewAI to create a multi-agent system:

1. **Research Specialist**: Finds and analyzes information
2. **Content Creator**: Crafts engaging and accurate responses

These agents work together to process complex queries when CrewAI mode is enabled.

### WebSocket Communication

Real-time communication is handled through WebSockets:

1. User sends a message
2. Server processes it with Ollama or CrewAI
3. Status updates are sent back to the client
4. Final response is displayed in the chat interface

## Troubleshooting

### Connection Issues

If the Docker container can't connect to Ollama:

1. Ensure Ollama is running on your host with `ollama serve`
2. Check your Docker network configuration
3. For Linux users, you may need to use host network mode

### Model Loading

If models are slow to respond initially:

- This is normal as Ollama loads the model into memory
- Subsequent queries will be faster

### CrewAI Mode Not Working

If CrewAI mode fails with connection errors:

1. Check your Docker network configuration
2. Ensure the OLLAMA_HOST environment variable is set correctly
3. Try using direct host IP instead of host.docker.internal

