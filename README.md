# NAPAS: Smoke Haze & Wildfire AI Assistant

**NAPAS** is a Retrieval-Augmented Generation (RAG) assistant designed to help people in Indonesia understand and respond to haze and forest fire (*karhutla*) issues.

Built with Langflow, NAPAS retrieves relevant information from official Indonesian Ministry of Health documents to provide answers grounded in trusted references rather than relying solely on the language model's general knowledge.

<p align="center">
  <img src="assets/mainFlow.png" alt="NAPAS Main Flow" width="100%">
</p>

## How It Works

NAPAS consists of two main flows in Langflow.

### 1. Data Ingestion

The ingestion flow processes reference documents and stores their vector embeddings for retrieval.

1. Reads the reference PDF.
2. Splits the document into smaller text chunks.
3. Generates embeddings using Google's Gemini Embedding model (`gemini-embedding-001`).
4. Stores the embeddings in DataStax Astra DB.

### 2. Chat & Retrieval

The chat flow retrieves relevant information to answer user questions.

1. Accepts questions through the chat input.
2. Searches Astra DB for relevant document chunks.
3. Parses the retrieved text.
4. Passes the retrieved context and user question to a structured prompt template.
5. Generates a context-grounded response using Google's Gemini model.

## Key Features & Guardrails

- **Grounded Responses:** Uses retrieved reference documents to keep answers relevant to the available sources.
- **Emergency Guidance:** Recognizes critical symptoms, such as severe breathing difficulties, chest pain, and fainting, and prioritizes urgent medical guidance, including contacting emergency services at 112.
- **Medical Safety:** Does not provide medication dosages or definitive medical diagnoses.
- **Scope Control:** Restricts responses to haze, wildfire, and related health concerns.
- **AI Disclaimer:** Reminds users that NAPAS is an AI assistant, not a substitute for professional medical advice.

## Tech Stack

| Component | Technology |
|---|---|
| Workflow Orchestration | Langflow |
| Large Language Model | Google Gemini |
| Embedding Model | `gemini-embedding-001` |
| Vector Database | DataStax Astra DB |

## Getting Started

### Prerequisites

Before running NAPAS, make sure you have:

- [Langflow](https://www.langflow.org/) installed and running.
- A Google Gemini API key.
- A DataStax Astra DB database and application token.
- The reference PDF included in the `docs/` directory.

### Installation

**1. Clone the repository**

```bash
git clone https://github.com/raaihansvg/NAPAS.git
cd NAPAS
```

**2. Import the Langflow workflow**

Open your Langflow dashboard, select **Import**, and import the workflow file:

```text
src/NAPAS.json
```

**3. Configure credentials**

Set up your own Google Gemini API key and DataStax Astra DB credentials in the appropriate Langflow components.

**4. Run the ingestion flow**

Load the reference PDF from the `docs/` directory into the Read File component, then execute the ingestion flow to generate and store the document embeddings.

**5. Test the assistant**

Open the Langflow Playground and start asking questions about haze, wildfire, and related health concerns.

## Project Structure

```text
NAPAS/
├── docs/           # Reference documents
├── src/
│   └── NAPAS.json  # Langflow workflow
├── assets/
│   └── mainFlow.png
└── README.md
```

## Disclaimer

NAPAS provides informational guidance based on its configured reference documents. It is not a medical diagnostic tool and does not replace professional medical care.

For severe or life-threatening symptoms, seek immediate medical attention.


