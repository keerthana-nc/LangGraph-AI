# LangGraph-AI

This repo contains four small projects I built to get hands-on with LangGraph. Each one focuses on a different pattern — basic agent setup, pausing for human input, tracing runs, and RAG over PDFs with images.

They're independent of each other.

---

## Modules

**1. Basic Chatbot** — `1-BasicChatbot/`  
A minimal agent built with LangGraph's `StateGraph`. Sets up message state, connects a Groq LLM, and streams responses. Good starting point to understand how nodes and edges work.

**2. Human in the Loop** — `2-HumanAssistance/`  
Adds Tavily search and a custom tool to the agent. Uses `interrupt()` to pause the graph mid-run and wait for human input, then resumes with `Command(resume=...)`. State is saved across turns with `MemorySaver`.

**3. Debugging** — `3-Debugging/`  
Hooks up LangSmith tracing so you can inspect every step of a run. Also includes a simple tool-calling agent and shows how to serve it locally with LangGraph Studio.

```bash
cd 3-Debugging
langgraph dev
```

**4. Multimodal RAG** — `4-Multimodal/`  
Pulls text and images from a PDF using PyMuPDF, embeds them with CLIP, stores in FAISS, and answers queries using OpenAI. The interesting part here is handling both text and image content from the same document.

---

## Stack

- **Agent framework** — LangGraph, LangChain
- **LLMs** — Groq (Llama), OpenAI
- **Search** — Tavily
- **Tracing** — LangSmith
- **RAG / multimodal** — PyMuPDF, CLIP, FAISS, PyTorch
- **Python 3.13**, Jupyter notebooks

---

## Setup

```bash
git clone https://github.com/keerthana-nc/LangGraph-AI.git
cd LangGraph-AI

python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate

pip install -r requirements.txt
pip install ipykernel jupyter
```

For module 4 only, install the extra dependencies:

```bash
pip install pymupdf transformers torch pillow scikit-learn faiss-cpu langchain-community langchain-openai
```

---

## API Keys

Create a `.env` file at the root. You only need the keys for the modules you're running.

```env
GROQ_API_KEY=your_key
TAVILY_API_KEY=your_key
LANGCHAIN_API_KEY=your_key
OPENAI_API_KEY=your_key
```

| Key | Where to get it | Needed for |
|-----|----------------|------------|
| Groq | [console.groq.com](https://console.groq.com) | Modules 1, 2, 3 |
| Tavily | [app.tavily.com](https://app.tavily.com) | Module 2 |
| LangSmith | [smith.langchain.com](https://smith.langchain.com) | Module 3 |
| OpenAI | [platform.openai.com](https://platform.openai.com) | Module 4 |

---

## Running

```bash
jupyter notebook
```

Open the notebook for whichever module you want and run top to bottom.

---

## Structure

```
LangGraph-AI/
├── 1-BasicChatbot/
│   └── 1-basicchatbot.ipynb
├── 2-HumanAssistance/
│   └── humanintheloop.ipynb
├── 3-Debugging/
│   ├── agent.py
│   ├── debugging.ipynb
│   └── langgraph.json
├── 4-Multimodal/
│   ├── 1-multimodalopenai.ipynb
│   └── multimodal_sample.pdf
├── requirements.txt
├── pyproject.toml
└── README.md
```
