# Retail Insights Assistant (GenAI)

A GenAI-powered Retail Insights Assistant that enables business users to analyze large-scale retail sales data using natural language. The system supports automated performance summarization and conversational Q&A, backed by a scalable, multi-agent architecture.

This project was built as part of a GenAI system design and implementation assignment, with a strong focus on data engineering, LLM orchestration, and scalability to 100GB+ datasets.

---

## Key Capabilities

### 1. Summarization Mode
- Generates concise, executive-friendly summaries of sales performance
- Example:
  > “Overall sales grew 12% YoY, driven by strong performance in the West region and the Electronics category.”

### 2. Conversational Q&A Mode
- Accepts ad-hoc business questions in natural language
- Converts questions into structured queries over retail sales data
- Example:
  > “Which category saw the highest YoY growth in Q3 in the North region?”

---

## System Architecture (High Level)

The solution is built using a **multi-agent GenAI architecture**:

1. **Language-to-Query Agent**
   - Interprets natural language questions
   - Translates intent into structured query logic (filters, metrics, aggregations)

2. **Data Extraction Agent**
   - Executes queries on structured data (CSV / DuckDB / Pandas)
   - Returns relevant, scoped results

3. **Validation Agent**
   - Validates query results for consistency and completeness
   - Prevents hallucinations and flags low-confidence responses

The final response is generated using an LLM with prompt templates designed for clarity, consistency, and business relevance.

---

## Tech Stack

- **Language:** Python 3.9+
- **LLM:** OpenAI / Gemini (pluggable)
- **Agent Framework:** LangChain / LangGraph (agent orchestration)
- **Data Layer:** Pandas, DuckDB
- **Optional UI:** Streamlit
- **Optional Vector Store:** FAISS / ChromaDB (for retrieval and context)

---

## Repository Structure

retail-insights-assistant-genai/
│
├── data/
│ ├── raw/ # Raw input datasets (CSV)
│ └── processed/ # Cleaned / transformed data
│
├── agents/
│ ├── query_agent.py # Language → query resolution
│ ├── data_agent.py # Data extraction & execution
│ └── validation_agent.py # Result validation & confidence checks
│
├── prompts/
│ ├── summarization.txt
│ ├── qa.txt
│ └── system_instructions.txt
│
├── app/
│ ├── main.py # Entry point
│ └── ui.py # Streamlit UI (optional)
│
├── architecture/
│ └── Retail_Insights_Assistant_Architecture.pdf
│
├── screenshots/
│ ├── summary_output.png
│ └── qa_example.png
│
├── requirements.txt
└── README.md

---
 ## Example Queries

“Which region had the highest sales growth YoY?”

“Which product category underperformed in Q4?”

“Summarize overall sales performance for the last year.”

---
## Scalability Design (100GB+ Data)

While the local implementation runs on CSV data, the architecture is designed to scale:

Ingestion & Processing: PySpark / Dask for batch or streaming ingestion

Storage: Data Lake (S3 / ADLS / GCS) + Warehouse (Snowflake / BigQuery)

Query Layer: DuckDB / BigQuery / Delta Lake

Retrieval: Metadata filtering + RAG for LLM grounding

Optimization: Prompt caching, query result caching, and cost controls

Detailed architecture and data flow are documented in the architecture presentation.

---

## Assumptions & Limitations

Sample dataset size is small and used for demonstration

Validation agent uses rule-based confidence checks (can be extended with statistical tests)

LLM responses depend on the quality of structured query translation

---

## Future Improvements

Add automated metric anomaly detection

Introduce role-based access control

Fine-tune LLM on retail-specific query patterns

Add observability (latency, accuracy, cost dashboards)
