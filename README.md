# Multi-Actor-Applications-Using-Langgraph
A chatbot application built using the LangGraph framework that integrates external tools — enabling the bot to call out to functions/APIs (tools) as part of its conversational flow.

## Table of Contents  
1. [About the Project](#about-the-project)  
2. [Key Capabilities](#key-capabilities)  
3. [Getting Started](#getting-started)  
   - Prerequisites  
   - Setup  
   - Running the Chatbot  
4. [How It Works](#how-it-works)  
   - Conversation Flow with Tools  
   - Tool Integration Examples  
5. [Project Structure](#project-structure)  
6. [Future Enhancements](#future-enhancements)  
7. [Contributing](#contributing)  
8. [License](#license)  
9. [Contact](#contact)  

---

## About the Project  
This repository demonstrates how to build a chatbot with LangGraph that doesn’t just respond using an LLM, but also *uses tools* — for example, web search, weather lookup, database queries, or any custom function. The underlying architecture uses LangGraph’s graph-based orchestration of states and nodes to embed tool calls into the conversation flow.  

It acts as a blueprint for building conversational agents where you want:  
- Tool-aware responses (the bot can invoke a function/tool as part of its answer)  
- Clean orchestration of when the bot uses a tool vs when it answers directly  
- Graph-based structure so conversations can branch, call tools, resume, and decide next steps.

---

## Key Capabilities  
- Conversational interface (chat) with user and bot  
- Integration of external tools/functions (e.g., search tool, info lookup, data retrieval)  
- Decision logic: based on user intent, decide whether to use a tool or just answer  
- Orchestrated flow using LangGraph graphs: nodes represent states/tasks, edges represent transitions  
- Extensible: you can add your own tools, change graph definitions, swap LLMs or tool behaviour  

---

## Getting Started

### Prerequisites  
- Python 3.8+  
- Access to a Large Language Model (LLM) API or local model  
- Any API keys required by the tools you integrate (e.g., search API, weather API)  
- Basic knowledge of LangGraph and LangChain concepts  

### Setup  
- ```bash
  git clone https://github.com/ShivamMitra/Chatbot-With-Tools-Using-Langgraph.git
  cd Chatbot-With-Tools-Using-Langgraph


- (Optional) Create and activate a virtual environment:
  ```bash
  python3 -m venv venv
  source venv/bin/activate  # On Windows: .\venv\Scripts\activate
- Install dependencies:
  ```bash
  pip install -r requirements.txt
Set environment variables / API keys (if any).

### Running the Chatbot
- Run the main script (for example):
  ```bash
  python main.py --mode chat
- This will start the chatbot session. You can type your prompt, and depending on the user input the bot may call a tool or directly respond.
- You can also modify graph configuration (e.g., graph.yaml or graph_definition.py) to change which tools are available, and how the conversation flows.

## How It Works

### Conversation Flow with Tools
1. The chatbot receives a user message.
2. The graph (built using LangGraph) begins at a start node, and based on the message, decides whether to invoke a tool node or proceed to an answer node.
3. If a tool is invoked:
   - The tool node executes a function (e.g., search_web(query))
   - The result of the tool is appended to state/context

4. The next node (often an LLM node) uses the augmented state (including tool results) to generate the final response.
5. The state is updated, conversation history is preserved, and the graph may loop for multi-turn dialogues.

### Tool Integration Examples
- Web Search Tool: The user asks a factual question → Graph routes to tool_web_search → the tool runs a query → result returned → LLM node generates an answer using the result.
- Weather Tool: The user asks “What’s the weather in Mumbai?” → Graph routes to tool_weather_lookup → tool fetches weather → answer given.
- Custom DB Lookup: A tool could query a database for user account information (in a mock setup).
You can add more tools by defining a function and wiring it into the graph’s node list.

## Project Structure

```graphql
Chatbot-With-Tools-Using-Langgraph/
├── README.md
├── requirements.txt
├── main.py                   # Entry point for chat interface  
├── graph_definition.py       # Defines the LangGraph nodes, edges, and tools  
├── tools/                    # Directory containing tool implementations  
│   ├── web_search.py  
│   ├── weather_lookup.py  
│   └── custom_tool.py  
├── agents/                   # (Optional) wrappers or agent definitions  
│   └── chat_agent.py  
├── config/                   # Configuration files (e.g., tool settings, API keys)  
│   └── config.yaml  
└── utils/                    # Utility modules  
    └── state_manager.py  
```
(Adjust folder names & filenames to reflect actual code.)

## Future Enhancements
- Add streaming responses from the LLM (token-by-token streaming)
- Add multi-turn tool context: track tool usage across multiple turns and maintain tool results in memory
- Create a UI (web frontend) for interactive chat instead of command line
- Add human-in-the-loop fallback: if the bot is unsure, escalate to a human or ask clarifying questions
- Persist conversation memory across sessions (long-term memory)
- Add more advanced tools (file upload & processing, PDF/document ingestion, RAG retrieval)
- Logging, monitoring and metrics on tool usage and chatbot performance

## Contributing
Contributions are welcome! If you’d like to add a new tool, improve graph definitions, create UI, or enhance code quality:
- Fork the repository
- Create a feature branch: git checkout -b feature/YourFeature
- Commit your changes: git commit -m "Add tool XYZ"
- Push to your branch: git push origin feature/YourFeature
- Open a Pull Request describing your changes
- Please ensure your code is documented and tests (if any) are included.

## License
This project is licensed under the MIT License – see the LICENSE file for details.

