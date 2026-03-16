# GitHub Repository Analyzer

An intelligent **AI-powered system that analyzes GitHub repositories using multi-agent workflows**.
Users can ask natural language questions about a repository and the system will explore the codebase, retrieve relevant files, and generate contextual answers.

This project combines **LangGraph multi-agent orchestration, GitHub MCP tools, vector embeddings, and semantic code search** to understand repositories efficiently.

Repository:
https://github.com/Tarun-428/Github-repository-analyzer

---

## Project Goal

The aim of this project is to build an **AI Software Engineering Assistant** capable of:

* Understanding large repositories
* Explaining code implementations
* Searching code semantically
* Debugging errors
* Suggesting feature implementations
* Assisting developers in navigating complex codebases

---

## Features Implemented

### Multi-Agent Workflow

The system uses **LangGraph** to orchestrate multiple specialized AI agents.

Agents implemented:

* Router Agent – Classifies user queries
* Summary Agent – Explains repository architecture
* Bug Solver Agent – Investigates errors and stack traces
* Feature Agent – Suggests feature implementations
* Code Search Agent – Finds implementation locations
* GitHub Tool Agent – Uses tools to interact with repositories

---

### GitHub MCP Tool Integration

The system interacts with GitHub using **MCP tools** that expose repository operations.

Available tools:

* get_repo_tree – Retrieve repository file structure
* read_file – Read repository files
* search_repo_code – Search code inside repository
* get_readme – Retrieve repository documentation

These tools allow agents to dynamically explore repositories.

---

### Semantic Code Search

Instead of keyword search, the system performs **vector-based semantic search** on repository code.

Workflow:

1. Repository files are fetched
2. Files are split into chunks
3. Each chunk is converted into embeddings
4. Embeddings are stored in a vector database
5. User queries retrieve relevant code chunks

---

### Code Chunking

Large files are divided into overlapping chunks before embedding.

Benefits:

* Better semantic retrieval
* Improved code reasoning
* More accurate context for AI responses

Example structure:

```
file.py
 ├ chunk_1
 ├ chunk_2
 ├ chunk_3
```

---

### Vector Database

The system uses **ChromaDB** to store code embeddings.

Stored metadata:

* repository owner
* repository name
* file path
* chunk index

This enables fast semantic search across repository code.

---

### Repository Indexing

When a repository is queried for the first time:

1. Repository tree is fetched
2. Files are retrieved
3. Files are chunked
4. Embeddings are generated
5. Chunks are stored in ChromaDB

Future queries reuse the existing index.

---

## System Architecture

```
User Query
   │
   ▼
FastAPI API Layer
   │
   ▼
LangGraph Router Agent
   │
   ├── Summary Agent
   ├── Bug Solver Agent
   ├── Feature Agent
   └── Code Search Agent
           │
           ▼
      GitHub MCP Tools
           │
           ▼
     Vector Search Tool
           │
           ▼
        ChromaDB
           │
           ▼
      Relevant Code
           │
           ▼
      LLM Reasoning
           │
           ▼
       Final Answer
```

---

## Technology Stack

Python
FastAPI
LangGraph
LangChain
ChromaDB
Sentence Transformers
GitHub API
Model Context Protocol (MCP)

---

## Example Request

POST `/query`

```
{
  "repo_url": "https://github.com/username/repository",
  "question": "Where is authentication implemented?"
}
```

The system will:

1. Classify the query
2. Perform semantic code search
3. Retrieve relevant code
4. Analyze the implementation
5. Generate a structured explanation

---

## Installation

Clone the repository

```
git clone https://github.com/Tarun-428/Github-repository-analyzer.git
```

Install dependencies

```
pip install -r requirements.txt
```

Run the API server

```
uvicorn api.main:app --reload
```

Open API documentation

```
http://127.0.0.1:8000/docs
```

---

## Current Capabilities

* Analyze GitHub repositories using natural language
* Perform semantic search on repository code
* Explain repository structure
* Locate implementations across large codebases
* Retrieve and analyze files dynamically

---

## Planned Improvements

Upcoming features:

* Planning agent for complex engineering tasks
* Automatic bug detection from stack traces
* Code patch generation using git style diffs
* AST-based code chunking
* Redis caching for faster retrieval
* Autonomous debugging workflow
* Automated pull request generation

---

## Future Vision

The long-term vision is to create a **fully autonomous AI software engineer** that can:

* Understand entire codebases
* Detect bugs automatically
* Implement features
* Refactor code
* Generate pull requests

---

