Here’s a clear, beginner-friendly `README.md` for your RAG project, designed to explain what it does, how it works, and how someone can run it from scratch.

---

## 📄 `README.md`

````markdown
# 🧠 RAG-Food: Simple Retrieval-Augmented Generation with ChromaDB + Ollama

This is a **minimal working RAG (Retrieval-Augmented Generation)** demo using:

- ✅ Local LLM via [Ollama](https://ollama.com/)
- ✅ Local embeddings via `mxbai-embed-large`
- ✅ [ChromaDB](https://www.trychroma.com/) as the vector database
- ✅ A simple food dataset in JSON (Indian foods, fruits, etc.)

---

## 🎯 What This Does

This app allows you to ask questions like:

- “Which Indian dish uses chickpeas?”
- “What dessert is made from milk and soaked in syrup?”
- “What is masala dosa made of?”

It **does not rely on the LLM’s built-in memory**. Instead, it:

1. **Embeds your custom text data** (about food) using `mxbai-embed-large`
2. Stores those embeddings in **ChromaDB**
3. For any question, it:
   - Embeds your question
   - Finds relevant context via similarity search
   - Passes that context + question to a local LLM (`llama3.2`)
4. Returns a natural-language answer grounded in your data.

---

## 📦 Requirements

### ✅ Software

- Python 3.8+
- Ollama installed and running locally
- ChromaDB installed

### ✅ Ollama Models Needed

Run these in your terminal to install them:

```bash
ollama pull llama3.2
ollama pull mxbai-embed-large
````

> Make sure `ollama` is running in the background. You can test it with:
>
> ```bash
> ollama run llama3.2
> ```

---

## 🛠️ Installation & Setup

### 1. Clone or download this repo

```bash
git clone https://github.com/yourname/rag-food
cd rag-food
```

### 2. Install Python dependencies

```bash
pip install chromadb requests
```

### 3. Run the RAG app

```bash
python rag_run.py
```

If it's the first time, it will:

* Create `foods.json` if missing
* Generate embeddings for all food items
* Load them into ChromaDB
* Run a few example questions

---

## 📁 File Structure

```
rag-food/
├── rag_run.py       # Main app script
├── foods.json       # Food knowledge base (created if missing)
├── README.md        # This file
```

---

## 🧠 How It Works (Step-by-Step)

1. **Data** is loaded from `foods.json`
2. Each entry is embedded using Ollama's `mxbai-embed-large`
3. Embeddings are stored in ChromaDB
4. When you ask a question:

   * The question is embedded
   * The top 1–2 most relevant chunks are retrieved
   * The context + question is passed to `llama3.2`
   * The model answers using that info only

---

## 🔍 Try Custom Questions

You can update `rag_run.py` to include your own questions like:

```python
print(rag_query("What is tandoori chicken?"))
print(rag_query("Which foods are spicy and vegetarian?"))
```

---

## 🚀 Next Ideas

* Swap in larger datasets (Wikipedia articles, recipes, PDFs)
* Add a web UI with Gradio or Flask
* Cache embeddings to avoid reprocessing on every run

---

## 👨‍🍳 Credits

Made by Callum using:

* [Ollama](https://ollama.com)
* [ChromaDB](https://www.trychroma.com)
* [mxbai-embed-large](https://ollama.com/library/mxbai-embed-large)
* Indian food inspiration 🍛

# 🥗 Custom Food RAG System
**A specialized Retrieval-Augmented Generation (RAG) agent for international culinary data.**

## 📌 Project Overview
This repository contains a functional RAG system that allows users to query a custom-built dataset of 15 international food items. By integrating a local Large Language Model (LLM) with a vector database, the system provides accurate, context-aware information regarding ingredients, cultural history, and nutritional value.

## 🛠️ Technical Implementation
- **LLM:** Llama 3.2 (via Ollama)
- **Vector Database:** ChromaDB
- **Embedding Model:** mxbai-embed-large
- **Data Source:** Custom `foods.json` (15 items)

## 🧠 Core AI Concepts Demonstrated

### 1. Vector Embeddings
I have demonstrated the use of **Vector Embeddings** by transforming raw text descriptions into numerical vectors. This mathematical representation allows the system to calculate the distance between concepts, enabling the AI to understand the context of a query beyond simple keyword matching.

### 2. Semantic Search
Unlike traditional search engines, this system utilizes **Semantic Search**. When a user asks for a "spicy Malaysian meal," the system retrieves items like *Nasi Lemak* and *Sarawak Laksa* because their embeddings are semantically similar to the intent of the query, even if the user's exact words aren't in the database.


## 🚀 How to Run
1. Ensure **Ollama** is running with `llama3.2` and `mxbai-embed-large`.
2. Install dependencies: `pip install chromadb langchain-community ollama`.
3. Run the application: `python rag_run.py`.

## 🌱 Reflection: AI Builder Growth Mindset
Through this project, I evolved from an AI user to an AI builder. I successfully navigated technical challenges, such as resolving `KeyError` exceptions by aligning data schemas with script requirements. I learned that the effectiveness of an LLM is significantly enhanced when grounded in a structured, specialized vector database, which effectively prevents hallucinations.

---

# ☁️ Phase 2: Cloud Migration (Week 3)

## 🏗️ Architecture Upgrade
I have migrated the system from a local-only setup to a production-ready cloud infrastructure.
- **Database:** [Upstash Vector](https://upstash.com/)
- **LLM:** [Groq Cloud](https://groq.com/) (Model: `llama-3.1-8b-instant`)
- **Data:** Expanded `food_data.json` to 35+ items with 75+ word comprehensive descriptions.

## 📊 Local vs. Cloud Comparison
| Feature | Local (Week 2) | Cloud (Week 3) |
| :--- | :--- | :--- |
| **Response Time** | ~8 seconds | **< 1 second** |
| **Vector DB** | ChromaDB (Local) | Upstash Vector (Cloud) |
| **LLM Provider** | Ollama (Local CPU) | Groq (Cloud API) |
| **Setup Complexity** | High (Requires Ollama) | **Low (Serverless)** |

## 🚀 Cloud Setup Instructions
1. **Environment Variables:**
   Ensure your `.env` file contains:
   - `UPSTASH_VECTOR_REST_URL`
   - `UPSTASH_VECTOR_REST_TOKEN`
   - `GROQ_API_KEY`
2. **Sync the Data:**
   Run `python cloud-version/sync_data.py` to populate the cloud index.
3. **Run the RAG System:**
   Run `python cloud-version/rag_cloud.py` to ask questions.

## 🧪 Advanced Query Examples
- "Suggest a healthy Mediterranean dish with heart benefits."
- "What is a spicy Asian vegetarian option?"
- "Tell me the cultural history of Pho."