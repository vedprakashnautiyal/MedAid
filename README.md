<h1 align="center"><strong>MedAid 🩺 <h6 align="center">A Bi-Modal Multi-Agent Medical Assistant</h6></strong></h1>

## Table of Contents

- [Overview](#overview)
- [Flow Chart](#flow-chart)
- [Features](#features)
- [Technology Stack](#technology-used)
- [Project Setup](#project-setup)
- [References](References.md)

---

## Overview 

**MedAid** is an **AI-powered assistant** designed to assist with **medical diagnosis, research, and patient interactions**.

This project integrates LLMs, CV Models, RAG, Web Search and Human-in-the-loop validation for AI based medical diagnosis and research.

---

## Flow Chart

![Flowchart](assets/flowchart.svg)

---

## Features

* **Modular Multi-Agent System** : Specialized agents for diagnosis, retrieval, reasoning, and image analysis.
* **Agentic RAG Pipeline** :
  * PDF parsing via Docling (text, tables, images)
  * Structural-aware semantic chunking
  * Domain-specific query expansion
  * Hybrid search with BM25 + dense vectors (Qdrant)
  * Cross-encoder reranking for relevance
  * Guardrails and source linking
  * Confidence-based switch to Web Search to reduce hallucinations
* **Medical Imaging Module** :
  * COVID-19 chest X-ray classification
  * Skin lesion segmentation
* **Live Research Agent** : Real-time retrieval of current medical literature.
* **Confidence Scoring** : Log-probability–based accuracy verification.
* **Voice Interface** : Speech-to-text and TTS via Eleven Labs API.
* **Expert Review** : Human-in-the-loop validation by medical professionals.
* **Safety Filters** : Robust I/O guardrails for trustworthy and ethical responses.
* **User-Friendly UI** : Accessible design tailored for medical practitioners.

---

## Technology Used

| Component                        | Technologies                                    |
| -------------------------------- | ----------------------------------------------- |
| **Backend**                | FastAPI                                         |
| **Agent Orchestration**    | LangGraph                                       |
| **Document Parsing**       | Docling                                         |
| **Knowledge Storage**      | Qdrant Vector Database                          |
| **Medical Image Analysis** | Computer Vision Models                          |
|                                  | • Chest X-Ray: Image Classification (PyTorch)  |
|                                  | • Skin Lesion: Semantic Segmentation (PyTorch) |
| **Guardrails**             | LangChain                                       |
| **Speech Processing**      | Eleven Labs API                                 |
| **Frontend**               | HTML, CSS, JavaScript                           |

---

## Project Setup

### 1️⃣ Clone the Repository

```bash
git clone https://github.com/vedprakashnautiyal/MedAid.git
cd MedAid
```

### 2️⃣ Create Environment File

- Create a `.env` file in the root directory and add API keys or other environment variables:

```bash
# Speech API Key 
ELEVEN_LABS_API_KEY=

# Web Search API Key
TAVILY_API_KEY=

# Hugging Face Token (For ReRanker Model -  "ms-marco-TinyBERT-L-6" )
HUGGINGFACE_TOKEN=

# For Gemini API (Can use other LLMs like Ollama Based or OpenAI but need code modification)
GOOGLE_API_KEY=
```

### 3️⃣ Create & Activate Virtual Environment

```bash
python -m venv .medaid
source .medaid/bin/activate  # For Mac/Linux
.medaid\Scripts\activate     # For Windows  
```

### 4️⃣ Install Dependencies

> **[NOTE]**
> ffmpeg is required for speech service to work.

```bash
winget install ffmpeg
```

```bash
pip install -r requirements.txt  
```

### 5️⃣ Ingest Data into Vector DB

- To ingest one document at a time:

```bash
python ingest_rag_data.py --file ./data/raw/brain_tumors_ucni.pdf
```

- To ingest multiple documents from a directory:

```bash
python ingest_rag_data.py --dir ./data/raw
```

### 6️⃣ Run the Project

```bash
python app.py
```

The application will be available at: [http://localhost:8000](http://localhost:8000)

[**🔝 Return**](#top)

---
