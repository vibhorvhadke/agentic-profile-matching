# Agentic Profile Matching

An AI-powered recruiting assistant built with **LangGraph** that reads a job description, searches resumes using RAG (Retrieval-Augmented Generation), ranks candidates with LLM-based reasoning, and lets you refine requirements through natural conversation.

## Features

- **Parse & Extract**: Automatically splits a job description into must-have vs nice-to-have requirements.
- **RAG-based Resume Search**: Uses sentence embeddings + cosine similarity to find relevant candidates.
- **LLM-based Ranking**: Ranks candidates with clear, human-readable reasoning for each rank.
- **Explainability**: Generates a saved match report highlighting strengths/gaps per candidate.
- **Conversational Refinement**: Ask questions ("Why did John rank higher than Jane?") or change requirements mid-conversation ("Make TypeScript a must-have") — the agent re-ranks and explains changes.

## Architecture

Built as a LangGraph state machine:
START → Parse JD → Extract Requirements → Search Resumes →
Rank Candidates → Generate Report → Human Feedback Loop → END

The Human Feedback node uses conditional edges to loop back to Search/Rank (on requirement changes) or back to itself (to answer further questions), until the user signals they're done.

See `state_machine_diagram.png` for the visual graph.

## Project Structure

The Human Feedback node uses conditional edges to loop back to Search/Rank (on requirement changes) or back to itself (to answer further questions), until the user signals they're done.

See `state_machine_diagram.png` for the visual graph.

## Project Structure
matching_agent_project/
├── src/
│ └── matching_agent.py # Standalone agent implementation
├── data/
│ └── resumes/ # Candidate resume files (.txt)
├── reports/ # Generated match reports (auto-saved)
├── tests/
│ └── test_scenarios_output.txt # 5+ scripted conversation flow tests
└── state_machine_diagram.png # Visual graph of the agent's workflow

## Setup & Usage

1. Install dependencies:
pip install langgraph langchain langchain-openai sentence-transformers faiss-cpu
2. Set your OpenRouter API key as an environment variable:
export OPENROUTER_API_KEY=your_key_here
3. Run the agent:
python src/matching_agent.py

## Tech Stack

- **LangGraph** — agent workflow / state machine
- **LangChain** — LLM orchestration
- **OpenRouter** — LLM provider (model-agnostic)
- **Sentence Transformers** — resume embeddings for RAG search
- **NumPy** — cosine similarity scoring

## Author

Built by [vibhorvhadke](https://github.com/vibhorvhadke) as part of an Agentic AI assignment.
