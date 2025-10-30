# 🎥 Video Content Analyzer - Agentic AI System

## 📋 Table of Contents
1. [Project Overview](#project-overview)
2. [Problem Statement](#problem-statement)
3. [Solution Architecture](#solution-architecture)
4. [Agentic AI Concepts Implemented](#agentic-ai-concepts)
5. [System Components](#system-components)
6. [Tech Stack](#tech-stack)
7. [Setup Instructions](#setup-instructions)
8. [Usage Guide](#usage-guide)
9. [Demo Video](#demo-video)
10. [Future Enhancements](#future-enhancements)

---

## 🎯 Project Overview

The Video Content Analyzer is an intelligent multi-agent AI system that automatically processes video files to extract, analyze, and enable intelligent querying of video content. The system uses specialized AI agents working together to provide transcription, summarization, semantic search, and interactive Q&A capabilities.

---

## 🔍 Problem Statement

People spend hours watching lengthy videos (lectures, meetings, tutorials, interviews) to find specific information. Current challenges include:

- **Time-consuming:** Watching entire videos to find specific information
- **Inefficient:** No way to search video content semantically
- **Limited accessibility:** Difficulty reviewing or referencing video content later
- **Poor indexing:** Videos lack searchable transcripts and summaries

---

## 💡 Solution Architecture

Our system employs a multi-agent architecture where specialized AI agents collaborate to process and analyze video content:

### High-Level Architecture
```
User → Gradio Interface → Orchestrator → Multiple Specialized Agents → Results
```

### Agent Workflow

1. **Transcription Agent**: Extracts audio and converts speech to text
2. **Summary Agent**: Generates intelligent summaries and chapter markers
3. **Embedding Agent**: Creates semantic vectors and stores in vector database
4. **Q&A Agent**: Answers questions using RAG (Retrieval Augmented Generation)
5. **Frame Extractor**: Extracts key visual frames with timestamps

---

## 🤖 Agentic AI Concepts Implemented

### 1. **Multi-Agent System**
- Multiple specialized agents with distinct responsibilities
- Each agent focuses on one task (separation of concerns)
- Agents work independently but coordinate through orchestrator

### 2. **Agent Tools & Resources**
- **Tools**: AssemblyAI API, Gemini API, OpenCV, MoviePy
- **Resources**: Video files (MP4, MOV, AVI formats)
- **External APIs**: Cloud-based AI services for processing

### 3. **Agentic Workflows**
- **Sequential workflow**: Transcription → Summary → Embedding → Ready for Q&A
- **Parallel potential**: Frame extraction runs independently
- **Orchestration**: Central coordinator manages agent execution

### 4. **Agentic Patterns**

#### a) **Tool Use Pattern**
- Agents use external tools (APIs, libraries) to accomplish tasks
- AssemblyAI for transcription, Gemini for text generation

#### b) **RAG Pattern (Retrieval Augmented Generation)**
- Q&A Agent retrieves relevant context from vector DB
- Augments LLM prompts with retrieved information
- Generates grounded, accurate answers

#### c) **Memory & Context**
- Transcript stored for all agents to access
- Vector database maintains semantic memory
- Session persistence for continuous Q&A

### 5. **Handoffs Between Agents**
- Transcription Agent → passes transcript → Summary Agent
- Transcription Agent → passes transcript → Embedding Agent
- Embedding Agent → provides search capability → Q&A Agent

### 6. **Vector Storage & Semantic Search**
- ChromaDB stores embeddings of transcript chunks
- Enables semantic similarity search (not just keyword matching)
- Powers intelligent Q&A capabilities

### 7. **Guardrails**
- Error handling in each agent
- Input validation for video files
- API rate limiting awareness
- Context length management for LLMs

### 8. **Persistence**
- Transcript saved to file
- Summary saved to file
- Vector database persists embeddings
- Extracted frames saved to disk

---

## 🏗️ System Components

### 1. **Transcription Agent**
**Responsibility:** Convert video speech to text

**Process:**
- Extracts audio from video using MoviePy
- Sends audio to AssemblyAI for transcription
- Returns timestamped transcript

**Output:** Full text transcript with word-level timestamps

---

### 2. **Summary Agent**
**Responsibility:** Create intelligent summaries

**Process:**
- Analyzes full transcript using Gemini
- Generates structured summary with key points
- Creates logical chapter markers

**Output:** 
- Main topic summary
- Key points (bullet format)
- Chapter breakdown

---

### 3. **Embedding Agent**
**Responsibility:** Enable semantic search

**Process:**
- Chunks transcript into overlapping segments (500 words)
- Generates embeddings using Gemini embedding model
- Stores vectors in ChromaDB

**Output:** Populated vector database ready for queries

---

### 4. **Q&A Agent**
**Responsibility:** Answer user questions about video

**Process:**
- Receives user question
- Searches vector DB for relevant transcript chunks
- Uses retrieved context + Gemini to generate answer
- Implements RAG pattern

**Output:** Natural language answers with source attribution

---

### 5. **Frame Extractor**
**Responsibility:** Extract visual timeline

**Process:**
- Opens video file with OpenCV
- Extracts frames at regular intervals
- Saves frames with timestamps

**Output:** 5-10 key frames representing video timeline

---

## 🛠️ Tech Stack

### **Frontend**
- **Gradio**: Web interface for video upload and interaction
- Hosted in Google Colab for easy deployment

### **Backend & Orchestration**
- **Python**: Core programming language
- **Custom Orchestrator**: Coordinates agent workflows

### **AI/ML Services**
- **OpenAI Whisper (via AssemblyAI)**: Speech-to-text transcription
- **Google Gemini API**: 
  - Text generation (summaries, Q&A)
  - Embeddings generation
- **ChromaDB**: Vector database for semantic search

### **Video Processing**
- **MoviePy**: Audio extraction from video
- **OpenCV**: Frame extraction and processing

### **Additional Libraries**
- **LangChain**: Framework utilities
- **tiktoken**: Token counting for LLMs

### **Hosting**
- **Google Colab**: Development and testing
- **Hugging Face Spaces** (optional): Final deployment

---

## 🚀 Setup Instructions

### Prerequisites
- Google Account (for Colab)
- OpenAI API key or Google Gemini API key
- AssemblyAI API key (free tier available)

### Step 1: Clone Repository
```bash
git clone https://github.com/yourusername/
