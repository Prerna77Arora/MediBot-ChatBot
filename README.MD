# 🧠 MediBot — AI-Powered Chatbot for Q&A over Medical PDFs

MediBot is an AI-powered medical chatbot that leverages state-of-the-art language models and vector search to answer user queries based on a curated set of medical PDF documents. It uses [Streamlit](https://streamlit.io/) for the user interface, [LangChain](https://python.langchain.com/) for LLM orchestration, and [FAISS](https://faiss.ai/) for efficient vector search.

---

## 📚 Table of Contents

- [Features](#features)
- [Project Structure](#project-structure)
- [Setup Instructions](#setup-instructions)
  - [1. Clone the Repository](#1-clone-the-repository)
  - [2. Install Dependencies](#2-install-dependencies)
  - [3. Prepare Environment Variables](#3-prepare-environment-variables)
  - [4. Prepare Data](#4-prepare-data)
  - [5. Create Vector Store](#5-create-vector-store)
  - [6. Run the Chatbot](#6-run-the-chatbot)
- [How It Works](#how-it-works)
- [Customization](#customization)
- [Troubleshooting](#troubleshooting)
- [Disclaimer](#disclaimer)
- [License](#license)

---

## ✨ Features

- **📄 Medical PDF Knowledge Base:** Answers are grounded in the provided medical PDFs.
- **🤖 Modern LLM Integration:** Uses HuggingFace's Mistral-7B-Instruct-v0.3 for high-quality responses.
- **🔎 Semantic Search:** FAISS-powered vector search for relevant context retrieval.
- **🖥️ Streamlit UI:** Simple, interactive chat interface.
- **🧩 Custom Prompting:** Easily modify the prompt template for different behaviors.

---

## 📁 Project Structure

```
.
├── .env
├── connect_memory_with_llm.py
├── create_memory_for_llm.py
├── MediBot.py
├── Pipfile
├── Pipfile.lock
├── data/
│   ├── clinical_medicine_ashok_chandra.pdf
│   ├── ...
│   └── vectorstore/
│       └── db_faiss/
└── ...
```

- **MediBot.py**: Main Streamlit app for the chatbot.
- **create_memory_for_llm.py**: Script to process PDFs and build the FAISS vector store.
- **connect_memory_with_llm.py**: Script to test the QA chain in the terminal.
- **data/**: Folder containing all source PDFs.
- **vectorstore/**: Stores the FAISS vector database.

---

## ⚙️ Setup Instructions

### 1. Clone the Repository

```sh
git clone <your-repo-url>
cd medical_chatBot
```

### 2. Install Dependencies

It's recommended to use [pipenv](https://pipenv.pypa.io/en/latest/) (or you can use `pip`):

```sh
pipenv install
pipenv shell
```
Or, using pip:
```sh
pip install -r requirements.txt
```

### 3. Prepare Environment Variables

Create a `.env` file in the project root with your HuggingFace API token:

```
HF_TOKEN=your_huggingface_token_here
```

Alternatively, set the environment variable in your shell:

```sh
export HF_TOKEN=your_huggingface_token_here
```

### 4. Prepare Data

- Place all your medical PDF files inside the `data/` directory.

### 5. Create Vector Store

Run the following script to process PDFs and build the FAISS vector store:

```sh
python create_memory_for_llm.py
```

This will:
- Load all PDFs from `data/`
- Split them into text chunks
- Generate embeddings using the HuggingFace model
- Store the embeddings in `vectorstore/db_faiss`

### 6. Run the Chatbot

Start the Streamlit app:

```sh
streamlit run MediBot.py
```

Open the provided local URL in your browser to interact with MediBot.

---

## 🔍 How It Works

1. **Document Loading:** All PDFs in `data/` are loaded and split into manageable text chunks.
2. **Embedding Generation:** Each chunk is embedded using the `sentence-transformers/all-MiniLM-L6-v2` model.
3. **Vector Store:** Embeddings are stored in a FAISS vector database for efficient similarity search.
4. **Query Handling:** When a user asks a question, the most relevant chunks are retrieved from FAISS.
5. **LLM Response:** The context and question are sent to the Mistral-7B-Instruct-v0.3 model via HuggingFace Inference API.
6. **Answer Display:** The answer is shown in the Streamlit chat interface, along with the source documents if needed.

---

## 🛠️ Customization

- **Prompt Template:**  
  Modify the prompt in [`MediBot.py`](MediBot.py) or [`connect_memory_with_llm.py`](connect_memory_with_llm.py) to change the chatbot's behavior.
- **Model Selection:**  
  Change the `HUGGINGFACE_REPO_ID` variable to use a different HuggingFace model.
- **Chunk Size:**  
  Adjust `chunk_size` and `chunk_overlap` in [`create_memory_for_llm.py`](create_memory_for_llm.py) for different granularity.

---

## 🐞 Troubleshooting

- **FAISS Not Found:**  
  Ensure you have run `create_memory_for_llm.py` before starting the chatbot.
- **API Token Issues:**  
  Double-check your HuggingFace token in `.env` or your environment.
- **Dependency Errors:**  
  Make sure all dependencies are installed. Use `pipenv` or `pip` as described above.
- **CUDA/CPU Issues:**  
  If running on a machine without GPU, ensure models are set to run on CPU.

---

## ⚠️ Disclaimer

This chatbot provides AI-generated information and should **not** be considered a substitute for professional medical advice. Always consult a qualified doctor for medical concerns.

---

## 📄 License

This project is for educational and research purposes only. Please check the licenses of the models and datasets you use.

---