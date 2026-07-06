# AKI-Ex Project: AI-Powered Finance Manager (n8n)

An automated, self-hosted n8n workflow designed to ingest local receipt images, process them using an online Large Language Model (LLM), extract line-by-line spending items into a structured ledger format, and append the categorized results directly into a master Excel/CSV table.

## 📋 Project Overview
* **Goal**: Automate receipt ingestion to eliminate manual spreadsheet entries and gain clear, structural transparency over historical spending patterns.
* **Core Technology Stack**: n8n (Self-hosted via Docker), JavaScript Data Sanitization Engine, Google Gemini 2.5 Flash-Lite LLM.
* **Verifiability**: The workflow features built-in AI Confidence Scoring, allowing automated validation checkmarks before data persistence takes place.

## 🖼️ Workflow Architecture
![n8n Workflow Blueprint](images/workflow.png)

### Core Node Sequence:
1. **Manual Trigger**: Initiates batch-processing cycles on demand.
2. **Directory Scanner (`ls`) & JS Compiler**: Discovers raw files inside the input directory and structures them into separate processing threads.
3. **Loop Over Items**: Processes each receipt individually to prevent system overhead.
4. **AI Agent & Gemini 2.5 Flash-Lite**: Specialized vision processing running under a custom financial accountant prompt configuration to output clean, structured schemas.
5. **Data Sanitization (JS)**: Automatically strips formatting code blocks and structures numeric data entries.
6. **Data Appender**: Commits clean line items directly to a persistent CSV database file using native file appending protocols.
7. **Archive Router**: Moves finalized physical files out of the input cache into the archive directories to prevent duplicate iterations.

---

## 🛠️ Local Environment Installation Guide

### Prerequisites
* Windows 10/11 with **WSL 2** initialized (`wsl --install`).
* **Docker Desktop** installed and configured to use the WSL 2 based engine.

### Quick Start Deployment
1. Clone this repository to your local machine.
2. Ensure your directory structure matches the following tree layout:
   ```text
   Receipt_Manager/
   ├── docker-compose.yml
   ├── README.md
   ├── Receipt_Manager.json
   ├── n8n_data/
   └── local_files/
       ├── input/
       ├── processed/
       └── output/