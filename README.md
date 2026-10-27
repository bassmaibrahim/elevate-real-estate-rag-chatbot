# Elevate Real Estate — RAG Chatbot

**An agentic, document-grounded chatbot built with Flowise, Google Gemini, and Exa Search.**

Elevate Real Estate is a fictional Egyptian real estate brokerage used to demonstrate Retrieval-Augmented Generation (RAG) and tool-augmented AI orchestration. The chatbot answers questions about a company annual report, supports general questions, and can use external web search through Exa Search.

> **Disclaimer:** Elevate Real Estate and all company figures, people, and projects in the sample report are fictional and created for demonstration purposes.

## Demo

| Resource | Link |
|---|---|
| Live demo | https://drive.google.com/file/d/1Q2nKoPdjRtxyStUK-WtJTn_8CBBwExaw/view?usp=drive_link |
| Flowise workflow | [`flowise/elevate-real-estate-chatflow.json`](flowise/elevate-real-estate-chatflow.json) |
| System architecture | [`docs/architecture.md`](docs/architecture.md) |

## Screenshots

### Workflow

Flowise workflow https://drive.google.com/file/d/1i6oCCqnsWmHO7SPSGDKkzeZ0GNkcFXkT/view?usp=sharing 


## Key Features

- **RAG-based question answering:** Retrieves relevant information from a PDF annual report.
- **Semantic search:** Uses Gemini embeddings and an in-memory vector store.
- **Agentic tool calling:** A Tool Agent can select between available tools based on the question.
- **External web search:** Integrates Exa Search for information outside the document.
- **General question answering:** Supports questions that do not require company-specific retrieval.
- **Conversation memory:** Connects Buffer Memory to the Tool Agent.
- **Visual orchestration:** Uses Flowise to build and inspect the AI workflow.

## Architecture

The application consists of two primary paths that can be used by the agent.

**Document retrieval**

Annual Report PDF → Character Text Splitter → Gemini Embeddings and In-Memory Vector Store → Retriever Tool

**Question answering**

User Query → Tool Agent → Retriever Tool and/or Exa Search → Gemini-powered Response

Buffer Memory supplies conversational context to the agent.

For the full component breakdown and request lifecycle, see [`docs/architecture.md`](docs/architecture.md).

## Technology Stack

| Technology | Role |
|---|---|
| Flowise | Visual AI workflow orchestration |
| Google Gemini | Chat model and agent reasoning |
| `gemini-embedding-001` | Document embeddings |
| In-Memory Vector Store | Semantic retrieval |
| Character Text Splitter | Document chunking |
| Retriever Tool | Knowledge-base retrieval |
| Exa Search | External web search |
| Buffer Memory | Conversational context |

The workflow screenshot shows `gemini-3.1-flash-lite-preview` as the configured chat model. Model availability and compatibility may change over time.

## RAG Configuration

The visible workflow settings include:

| Setting | Value |
|---|---:|
| Chunk size | 1,000 characters |
| Chunk overlap | 200 characters |
| Vector-store Top K | 4 |
| Chat model temperature | 0.9 |
| Embedding model | `gemini-embedding-001` |

These values describe the demonstrated configuration. Retrieval quality depends on the document, chunk boundaries, query, embedding model, and retrieval behavior.

## Example Interaction

**Question:** What was Elevate Real Estate's total sales value in 2024, and how much did it grow compared with 2023?

**Demonstrated response:**

- Total sales value in 2024: EGP 2.85 billion
- Total sales value in 2023: EGP 2.10 billion
- Year-over-year growth: 35.7%

The chatbot successfully returned these figures from the provided annual report in the demonstrated interaction.

## Try These Questions

**1. Document retrieval**

What were Elevate Real Estate's total sales value and year-over-year growth in 2024?

**2. General knowledge**

What is the difference between buying a property directly from a developer and purchasing a resale property?

**3. External information**

What is the current average price per square meter for apartments in the New Administrative Capital, Egypt?

The third question can be used to test whether the agent invokes Exa Search. Its routing behavior and the accuracy of any current market information should be verified during testing.

## Getting Started

### Prerequisites

- A compatible Flowise installation.
- Google Gemini credentials for the configured chat and embedding integrations.
- Exa Search credentials.
- The annual report PDF or a compatible replacement document.

Docker is optional unless you are using a containerized setup. The exported chatflow JSON does not, by itself, include every infrastructure or deployment setting.

### 1. Clone the repository

```bash
git clone https://github.com/YOUR_USERNAME/elevate-real-estate-rag-chatbot.git
cd elevate-real-estate-rag-chatbot
```

### 2. Import the workflow

1. Open your Flowise instance.
2. Import `flowise/elevate-real-estate-chatflow.json` using the import option supported by your Flowise version.
3. Inspect the nodes and connections.
4. Configure the required credentials.
5. Verify the PDF source and vector-store setup.
6. Save the chatflow and run a test query.

### 3. Verify the integrations

Test a question whose answer appears explicitly in the annual report. Then test a general-knowledge question and a question requiring external information.

The in-memory vector store may require the document to be indexed again after a restart, depending on how the workflow is configured.

**Security:** Never commit API keys or credential-bearing files to the repository. Review the exported JSON before publishing it.

## Evaluation Considerations

A successful demonstration confirms that the workflow can answer at least one tested question. A more comprehensive evaluation should measure:

- Retrieval relevance
- Answer groundedness
- Factual accuracy
- Tool-selection correctness
- Source attribution
- Latency and API failures

No aggregate evaluation score is claimed in this repository.

## Limitations

- In-memory vector storage may not persist across restarts.
- PDF extraction and chunking can affect retrieval quality.
- Agent tool selection may vary across queries.
- Web search results can be incomplete or outdated.
- Model quotas, availability, and compatibility may change.

## Future Improvements

- Introduce persistent vector storage.
- Build a repeatable RAG evaluation dataset.
- Improve source citations and traceability.
- Add logging, error handling, and latency measurements.
- Document a reproducible containerized deployment.
- Test tool routing and failure scenarios systematically.

## Repository Structure

```text
elevate-real-estate-rag-chatbot/
├── assets/
│   ├── flowise-workflow.png
│   └── chatbot-demo.png
├── docs/
│   └── architecture.md
├── flowise/
│   └── elevate-real-estate-chatflow.json
├── .gitignore
├── LICENSE
└── README.md
```

## Author

[Bassma Ibrahim]

[LinkedIn](https://www.linkedin.com/in/bassma-ibrahim/) · [GitHub](https://github.com/bassmaibrahim)

## License

Specify a license only after confirming your rights to distribute the workflow and all included assets. The fictional report and third-party materials may have separate licensing considerations.