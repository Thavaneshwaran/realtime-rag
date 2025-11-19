# Real-Time AI Assistant Using RAG + LangChain + Ollama (Local LLM)

## 1. Project Overview

**This project is a fully local, real-time AI assistant that performs web searches at runtime and generates grounded answers using open-source tools—no paid APIs, no cloud dependencies.** With LangChain, DuckDuckGo Search, and the Ollama model "llama3.1:8b", the assistant demonstrates how to build a realistic Retrieval-Augmented Generation (RAG) pipeline that is privacy-friendly and cost-free.

- **What does this assistant do?**  
  It answers your questions by live-searching the web and using a local LLM, giving cited, detailed results—never hallucinating, never relying on proprietary APIs.

- **Why does real-time RAG matter?**  
  You get up-to-date, well-grounded answers—even on recent topics—while enjoying full transparency and source control.

- **Why only local tools?**  
  *Privacy, control, and accessibility.* You never send queries to a commercial cloud LLM; everything runs on your machine except the search.

- **Architecture Summary:**  
  **LLM (Ollama/Llama3.1:8b) → DuckDuckGo Search → RAG Chain (LangChain LCEL)**

---

## 2. Features

- **Local LLM:** Uses Ollama's `llama3.1:8b` model.
- **Real-time web search:** Integrates DuckDuckGo Search for current results.
- **LangChain LCEL pipeline:** Manages RAG and context injection.
- **Fully local/offline (except search):** Your data stays private.
- **No paid APIs:** 100% free, open-source stack.
- **Easy to extend:** Ready for vectorDB, custom UI, or plugins.

---

## 3. Tech Stack

- **Python**
- **LangChain**
- **langchain-ollama**
- **DuckDuckGo Search (`ddgs`)**
- **Ollama**
- **llama3.1:8b**

---

## 4. Project Folder Structure

- **realtime_rag/
- **assistant.py
- **requirements.txt
- **README.md
- **.venv/

---

## 5. Installation

1. **Create & activate a virtual environment** (recommended):
    ```
    python -m venv .venv
    source .venv/bin/activate      # On Linux/Mac
    .venv\Scripts\activate         # On Windows
    ```

2. **Install dependencies:**
    ```
    pip install -r requirements.txt
    pip install ddgs
    pip install -U langchain-ollama
    ```

3. **Install Ollama and download the model:**
    ```
    # Download and install Ollama from https://ollama.com/
    ollama pull llama3.1:8b
    ```

---

## 6. Running the Assistant

Run the assistant with:
python assistant.py
The assistant will greet you and wait for your queries. Type your question and hit enter!

---

## 7. Code Explanation

### **How the RAG Chain Works**
- **RunnablePassthrough:**   
  This LangChain primitive passes your user question down the chain while allowing intermediate steps (like search results) to be injected as `{context}`.

- **Search Integration:**  
  Uses DuckDuckGo Search (`DuckDuckGoSearchRun`) to retrieve real-time results for the input query.

- **Context Injection:**  
  Search results are passed as `{context}` to the prompt template, so the model sees only those facts.

- **Local LLM Grounding:**  
  The Ollama "llama3.1:8b" model generates answers using the supplied context **only**. If the search is empty, the assistant says so—never hallucinating, never making up citations.

### **Why this prevents hallucination**
- The LLM receives **only** what came from live search. If nothing is found, it must say "no info found".  
- Responses are always based on real web content, not guesses.

---

## 8. Troubleshooting

- **Module not found (ddgs/langchain-ollama):**
  - Run `pip install ddgs langchain-ollama`

- **Ollama import errors:**  
  - Update to the latest `langchain-ollama` and verify your Ollama setup.

- **Memory errors (model loading):**  
  - "llama3.1:8b" requires significant RAM—use swap, close other apps, or try smaller models.

- **Slow responses (CPU only):**  
  - Model inference is much faster with a GPU. If stuck on CPU, answers will be slower.

---

## 9. Future Improvements

- Add summarizers to condense search results before passing to the LLM.
- Integrate query rewriting for smarter search queries.
- Add vector DB support for persistent document retrieval.
- Build a UI using FastAPI, Gradio, or Streamlit for a better user experience.

---

_This repository shows you how to build an open, offline, real-time RAG assistant with full transparency, no paid APIs, and ready for future extensibility. Questions, issues, or improvement ideas welcome—just open an issue!_
