# Multi-Document Chat 🔎📚 (Streamlit · RAG · FAISS)

I built a Streamlit app that lets me ask questions across many PDFs and text files and get answers grounded in those sources. Under the hood it’s a Retrieval-Augmented Generation (RAG) pipeline using LangChain, FAISS, and an LLM (Gemini Pro by default; OpenAI/Anthropic/Llama are pluggable).

# ✨ What it does

📤 Upload one or more PDF/TXT files

🧩 Chunk content with an overlapping, windowed splitter

🧠 Embed + Index chunks in FAISS for fast similarity search

🤖 Answer questions with an LLM, guided by retrieved context

📎 (Optional) Show sources so I can see what supported the answer

# 💡 Why I built it

Jumping between pages is slow. I wanted a conversational interface that can pull evidence from multiple documents while keeping responses traceable to the original text.

# 🧱 Features

🗂️ Multi-file conversational QA: handles single-hop and multi-step questions across documents

🪟 Adjustable windowed chunking: balance local detail with broader context

🔌 Pluggable LLMs: Gemini Pro default; swap to OpenAI/Anthropic or local models with minimal code changes

🖥️ Simple UI: upload → process → chat, with Streamlit session state

📄 Formats: PDF (PyPDF2) and TXT

# 🛠️ Tech stack

App/UI: Streamlit

RAG: LangChain (splitters, retrievers, chains, memory)

Vector store: FAISS (CPU)

Parsing: PyPDF2

Models/Embeddings: langchain_google_genai (Gemini), optional OpenAI/Anthropic/Llama

Config: python-dotenv

# 🚀 Quickstart
1) Clone
git clone https://github.com/<your-username>/<your-repo>.git
cd <your-repo>

2) Install
pip install -r requirements.txt

3) Configure environment

Create a .env file in the project root:

Default provider (Gemini)
GOOGLE_API_KEY=<your-google-api-key>

Optional providers
OPENAI_API_KEY=<your-openai-key>
ANTHROPIC_API_KEY=<your-anthropic-key>

Optional selector used in code (gemini | openai | anthropic | llama)
LLM_PROVIDER=gemini

4) Run
streamlit run app.py


Open the local URL Streamlit prints to your terminal 🌐.

# 🧭 How it works (under the hood)

Load & normalize text from PDFs/TXT

Split into overlapping windows (tunable size/stride)

Embed & index chunks in FAISS

Retrieve top-k similar chunks per query

Generate an answer with the LLM using retrieved context (optionally display sources)

Design knobs

🔬 Chunking: bigger windows for narrative reports; smaller for dense technical docs

🎯 Top-k: raise for recall (more context), lower for cost/latency

🔁 Provider abstraction: switch vendors or go local without refactoring the app

# ❓ FAQ

Which file types are supported?
PDF and TXT.

Do I need a GPU?
No. FAISS-CPU plus hosted LLMs work fine. For local OSS models, a GPU helps.

Can I add citations?
Yes—enable the sources panel or add a citation step in the chain.

resources:
GURPREETKAURJETHRA
