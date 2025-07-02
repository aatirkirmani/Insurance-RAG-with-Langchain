# 📄 Insurance Documents RAG Pipeline

A Retrieval-Augmented Generation (RAG) pipeline to enable intelligent, grounded question answering over a corpus of insurance documents using OpenAI and Chroma.

---

## 🚀 Project Overview

Insurance providers and analysts often deal with lengthy, complex documents that are difficult to search through. End users or internal teams may need quick answers to natural language questions like:

- “What’s excluded under accidental damage?”
- “Does this policy cover pre-existing conditions?”
- “Which documents are required for claims?”
 
### Challenges
- 📄 Large unstructured text in PDFs  
- 🔍 Traditional search lacks contextual understanding  
- 🧠 Users need accurate, conversational responses  
- ⚙️ Difficult to maintain manual indexing at scale  

This project is an AI-powered question-answering system built using **LangChain**. It enables semantic search and natural language querying over unstructured insurance documents (e.g. policy PDFs, claim booklets). The project uses the following main components:


- 🧠 **OpenAI's LLMs** for language generation  
- 🔍 **Chroma** for efficient vector-based retrieval  
- 📄 **LangChain** for orchestrating the RAG pipeline  

The goal is to allow users to ask natural language questions and receive fact-based responses backed by insurance documents.

---

## ✅ Why LangChain?

LangChain is a powerful framework that helps orchestrate components in a **Retrieval-Augmented Generation (RAG)** pipeline — ideal for document-based Q&A systems.

---

## 📂 Data Sources

The insurance documents processed in this project include:

- **Motor Vehicle Insurance Policy Against Loss and Damage**  
- **Motor Vehicle Insurance Policy Against Third Party Liability**

These files were uploaded in PDF format and parsed using `PyPDFLoader` from LangChain, enabling structured extraction of text from scanned policies.

---

## 🛠️ Tech Stack

| Component      | Tool / Library                         |
|----------------|----------------------------------------|
| Language Model | OpenAI GPT via LangChain               |
| Embeddings     | `sentence-transformers/all-MiniLM-L6-v2` |
| Vector Store   | Chroma                                 |
| Document Parsing | `PyPDFLoader` (LangChain)           |
| Pipeline       | LangChain `RetrievalQA`                |
| Programming Language | Python                           |

---

## ⚙️ Design Choices

1. **Document Parsing**
   - Used `PyPDFLoader` for extracting structured text from PDFs.
   - Chosen due to its reliability with multi-page documents.

2. **Chunking Strategy**
   - Employed `RecursiveCharacterTextSplitter` to preserve semantic coherence.
   - Chunk size: `1000` characters with `200` character overlap to maintain contextual linkage between segments.

3. **Embedding Model**
   - Selected `all-MiniLM-L6-v2` from HuggingFace for its balance of speed and semantic precision.

4. **Vector Store**
   - Opted for **Chroma** as an easy-to-integrate, persistent vector database.
   - Chroma's simplicity and in-memory or persistent modes suited this POC well.

5. **Query Pipeline**
   - Leveraged `RetrievalQA` from LangChain to combine retrieval + OpenAI-based generation.
   - Retrieval grounded the answers in actual document text, reducing hallucinations.

---

## ⚠️ Challenges Faced

- **Chunking Trade-offs**  
  Determining the right chunk size and overlap was essential. Too small loses context; too large reduces retrieval accuracy.

- **Grounding Model Responses**  
  Without tight control of context, the language model might hallucinate. Using Chroma-based retrieval significantly reduced this risk by anchoring queries in real content.

- **Latency for Larger Docs**  
  While Chroma performs well, larger document sets may need batched processing for scaling.

---

## 📦 Setup Instructions


    # Clone the repository
    git clone https://github.com/aatirkirmani/Insurance-RAG-with-Langchain.git
    cd Insurance-RAG-with-Langchain
    
    # Create and activate a virtual environment
    python -m venv venv; .\venv\Scripts\Activate.ps1
    
    # Upgrade pip and install dependencies
    pip install --upgrade pip; pip install -r requirements.txt
    
    # Create .env file for OpenAI key
    "OPENAI_API_KEY=your_openai_api_key_here" | Out-File -Encoding ASCII .env
    
    # Launch the notebook
    jupyter notebook Insurance_Documents_RAG_Completed.ipynb

##  Flowchart
![Untitled diagram _ Mermaid Chart-2025-07-02-152408](https://github.com/user-attachments/assets/8ba48f10-891c-4876-bcfa-e6298faaacd7)

    
