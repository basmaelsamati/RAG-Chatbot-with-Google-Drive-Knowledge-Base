<img width="2000" height="961" alt="Screenshot_٢٠٢٦٠٨٢٤_٠٢٠٨٢٧_Samsung Browser" src="https://github.com/user-attachments/assets/94e42428-01d2-4241-8c8e-9c326ee5691a" />

0# RAG Chatbot with Google Drive Knowledge Base

## Overview

This project implements a **Retrieval-Augmented Generation (RAG) chatbot** using n8n. The system allows documents stored in Google Drive to be downloaded, processed, converted into embeddings, stored in a Qdrant vector database, and then retrieved by an AI-powered chatbot to answer user questions based on the available knowledge base.

The workflow is divided into two main parts:

1. **Knowledge Base Ingestion**
2. **RAG Chatbot**

---

## Architecture

### 1. Knowledge Base Ingestion

The knowledge-base workflow processes documents from Google Drive and stores them in Qdrant.

**Workflow:**

`Manual Trigger → Search Files and Folders → Edit Fields → Download File → Qdrant Vector Store`

The Qdrant Vector Store is connected to:

* **Google Gemini Embeddings**
* **Default Data Loader**
* **Recursive Character Text Splitter**

### Process

1. Trigger the workflow manually.
2. Search for files and folders in Google Drive.
3. Edit and prepare the file information.
4. Download the selected file.
5. Load the document using the Default Data Loader.
6. Split the document into smaller chunks using the Recursive Character Text Splitter.
7. Generate embeddings using Google Gemini.
8. Store the resulting vectors and document chunks in Qdrant.

---

## 2. RAG Chatbot

The chatbot receives a user's question and uses an AI Agent to generate an answer based on the stored knowledge.

**Workflow:**

`When Chat Message Is Received → AI Agent → Answer`

The AI Agent is connected to:

* **Google Gemini Chat Model**
* **Qwen Cloud Chat Model**
* **Simple Memory**
* **Qdrant Vector Store**
* **Google Gemini Embeddings**
* **Answer Questions with a Vector Store Tool**

### Chat Process

1. The user sends a question through the chat interface.
2. The message is received by the chat trigger.
3. The AI Agent analyzes the question.
4. The agent uses the vector-store tool to search the knowledge base.
5. Qdrant retrieves the most relevant document chunks.
6. Google Gemini embeddings are used for semantic similarity search.
7. The retrieved context is provided to the AI model.
8. The AI Agent generates an answer using the retrieved information.
9. Simple Memory maintains conversation context.

---

## Technologies Used

* **n8n** — Workflow automation and AI orchestration
* **Google Drive** — Document storage and source knowledge base
* **Qdrant** — Vector database
* **Google Gemini** — Embeddings and chat model
* **Qwen Cloud** — Additional chat model
* **LangChain / n8n AI Agent** — RAG and agent orchestration
* **Recursive Character Text Splitter** — Document chunking

---

## RAG Pipeline

```text
Google Drive
     ↓
Search Files
     ↓
Download File
     ↓
Document Loader
     ↓
Text Splitter
     ↓
Google Gemini Embeddings
     ↓
Qdrant Vector Store
     ↓
     ┌─────────────────────┐
     │     User Question   │
     └──────────┬──────────┘
                ↓
           AI Agent
                ↓
      Vector Store Search
                ↓
        Relevant Documents
                ↓
          Chat Model
                ↓
             Answer
```

## Key Features

* 📄 Google Drive-based knowledge management
* 🔎 Semantic document search
* 🧠 Retrieval-Augmented Generation
* 💬 Conversational chatbot
* 🗃️ Qdrant vector database
* ✂️ Automatic document chunking
* 🔢 Gemini-powered embeddings
* 🧠 Conversation memory
* 🤖 AI Agent-based question answering

## Purpose

The system can be adapted for:

* Internal company knowledge bases
* Document Q&A
* Educational assistants
* Technical documentation assistants
* Customer-support knowledge bases
* Personal document assistants
* Research and information retrieval systems

