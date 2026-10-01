# 🤖 AI Data Agent

An Agentic AI-based Data Assistant that allows users to interact with structured and external data using natural-language queries.

The system uses a **Router Agent** to understand the user's request and delegate it to the appropriate specialized agent.

Currently, the system supports:

- 🗄️ **SQL Analyst Agent** — Database querying and analysis using PostgreSQL
- 🔄 **ETL Analyst Agent** — Data extraction and transformation from external sources

---

## 🚀 Project Overview

Working with data often requires knowledge of multiple technologies such as SQL, APIs, Python, and data-processing libraries.

The goal of this project is to provide a **natural-language interface for data analysis**, allowing users to ask questions without manually writing SQL queries or implementing data-processing logic.

For example, instead of manually writing an SQL query such as:

```sql
SELECT SUM(sales)
FROM sales
WHERE city = 'Mumbai';
```

the user can simply ask:

> **"What were the total sales in Mumbai?"**

The AI agent determines the appropriate workflow, performs the required operation, and returns the result in an understandable form.

---

## 🧠 Architecture

The project follows a **multi-agent architecture** in which a Router Agent delegates user requests to specialized agents.

```text
                         User
                           |
                           ↓
                  Natural Language Query
                           |
                           ↓
                    Router Agent
                      /       \
                     /         \
                    ↓           ↓
              SQL Agent      ETL Agent
                  |               |
                  ↓               ↓
             PostgreSQL      External APIs
                  |               |
                  ↓               ↓
             SQL Result      Data Processing
                  \               /
                   \             /
                    ↓           ↓
                    Final Response
```

### Workflow

1. The user provides a natural-language query.
2. The Router Agent analyzes the request.
3. The request is delegated to the appropriate specialized agent.
4. The selected agent performs the required operation.
5. The result is processed and returned as a natural-language response.

---

# ✨ Features

## 🧠 Intelligent Query Routing

The Router Agent acts as the central component of the system.

It analyzes the user's request and determines whether the query should be handled by the SQL Analyst Agent or the ETL Analyst Agent.

For example:

```text
Database-related question
        ↓
SQL Analyst Agent
```

```text
External data / API task
        ↓
ETL Analyst Agent
```

---

## 🗄️ SQL Data Analysis

The SQL Analyst Agent handles questions related to structured data stored in PostgreSQL.

Its workflow includes:

1. Understanding the user's question
2. Gathering relevant database schema information
3. Generating an SQL query
4. Validating the generated query
5. Executing the query
6. Processing the result
7. Generating a natural-language response

### Example

> "What are the total sales for each department?"

The agent can generate the required SQL query, execute it against PostgreSQL, and return the result in an understandable form.

---

## 🔄 ETL Data Processing

The ETL Analyst Agent handles tasks involving external data sources and data transformation.

ETL stands for:

- **E — Extract:** Obtain data from an external source such as an API
- **T — Transform:** Clean, filter, aggregate, or modify the data
- **L — Load:** Prepare the processed data for further analysis or use

Python and Pandas are used for data processing and transformation.

### Example

> "Fetch weather data from an API and calculate the average temperature."

The workflow can be represented as:

```text
External API
     ↓
Extract Data
     ↓
Transform using Python/Pandas
     ↓
Process / Analyze
     ↓
Return Result
```

---

# 🤖 Agents

## 1. Router Agent

The Router Agent is responsible for understanding the user's request and selecting the appropriate specialized agent.

### Responsibilities

- Analyze user intent
- Determine the type of task
- Route the request
- Connect the user query with the appropriate workflow

The Router Agent helps keep the system modular by allowing different agents to handle different types of tasks.

---

## 2. SQL Analyst Agent

The SQL Analyst Agent is responsible for database-related tasks.

### Responsibilities

- Understand natural-language database questions
- Inspect relevant database schema
- Generate SQL queries
- Validate generated SQL
- Execute queries against PostgreSQL
- Process query results
- Generate natural-language responses

### SQL Workflow

```text
User Question
      ↓
Understand Query
      ↓
Gather Database Schema
      ↓
Generate SQL
      ↓
Validate SQL
      ↓
Execute Query
      ↓
Process Result
      ↓
Final Answer
```

---

## 3. ETL Analyst Agent

The ETL Analyst Agent handles external data extraction and transformation tasks.

### Responsibilities

- Extract data from external sources
- Process external data
- Transform data using Python/Pandas
- Perform required calculations or filtering
- Prepare the processed result
- Return the final result

### ETL Workflow

```text
User Request
      ↓
Understand Requirement
      ↓
Extract Data
      ↓
Transform Data
      ↓
Process Data
      ↓
Return Result
```

---

# 🛠️ Technology Stack

| Technology | Purpose |
|------------|---------|
| **Python** | Core programming language |
| **LangGraph** | Agent workflow and orchestration |
| **LangChain** | LLM and agent integration |
| **OpenAI / Claude** | Large Language Models |
| **PostgreSQL** | Relational database |
| **Pandas** | Data processing and transformation |
| **Pydantic** | Data validation and structured data |
| **psycopg2** | PostgreSQL database connectivity |
| **python-dotenv** | Environment variable management |

---

# 📁 Project Structure

```text
AI_Data_Agent/
│
├── agents/
│   ├── SQL Analyst Agent
│   └── ETL Analyst Agent
│
├── data/
│
├── Models/
│
├── utils/
│
├── main.py
├── feed_db.py
│
├── .env.example
├── .gitignore
├── .python-version
├── pyproject.toml
├── requirements.txt
├── test_schema_details.txt
├── uv.lock
└── README.md
```

> The exact filenames and folders may vary depending on the current implementation.

---

# ⚙️ Installation

## 1. Clone the Repository

```bash
git clone <your-repository-url>
cd AI_Data_Agent
```

---

## 2. Create a Virtual Environment

### Windows

```bash
python -m venv .venv
```

Activate the environment:

```bash
.venv\Scripts\activate
```

### Linux / macOS

```bash
python3 -m venv .venv
```

Activate the environment:

```bash
source .venv/bin/activate
```

---

## 3. Install Dependencies

```bash
pip install -r requirements.txt
```

---

# 🔑 Configuration

Create a `.env` file in the project root directory.

Example:

```env
OPENAI_API_KEY=your_api_key
DATABASE_URL=your_database_url
```

The exact environment variables depend on the configured LLM provider and database setup.

> ⚠️ **Never commit your `.env` file or API keys to GitHub.**

Use `.env.example` as a reference for the required environment variables.

---

# 🗄️ PostgreSQL Setup

The SQL Analyst Agent uses PostgreSQL as the database backend.

The database connection requires the appropriate:

- Host
- Port
- Username
- Password
- Database name

Once the database is configured, the SQL Analyst Agent can use schema information to understand the available tables and columns before generating queries.

---

# ▶️ Running the Project

After completing the installation and configuration:

```bash
python main.py
```

The application can then process natural-language queries through the agent workflow.

---

# 💡 Usage Examples

## Example 1 — SQL Analysis

### User Query

```text
What are the total sales for each department?
```

### Workflow

```text
User
 ↓
Router Agent
 ↓
SQL Analyst Agent
 ↓
PostgreSQL
 ↓
SQL Result
 ↓
Natural Language Response
```

---

## Example 2 — Database Ranking

### User Query

```text
Show me the top users based on their ratings.
```

The SQL Analyst Agent can determine the relevant table and columns, generate the SQL query, execute it, and return the result.

---

## Example 3 — External Data Processing

### User Query

```text
Fetch weather data from an API and calculate the average temperature.
```

### Workflow

```text
User
 ↓
Router Agent
 ↓
ETL Analyst Agent
 ↓
External API
 ↓
Pandas Processing
 ↓
Result
```

---

# 🔐 Safety

The SQL workflow contains a validation step before executing generated queries.

This provides an additional layer between the generated SQL and the PostgreSQL database.

Sensitive information such as:

- API keys
- Database passwords
- Database connection strings

should be stored using environment variables rather than being written directly into the source code.

---

# 📊 Data Processing

The ETL Analyst Agent uses Python and Pandas for data-processing operations.

Depending on the requested task, the data can be:

- Extracted
- Filtered
- Cleaned
- Transformed
- Aggregated
- Analyzed
- Prepared for further use

This allows users to perform common data-processing tasks using natural-language instructions.

---

# 🎯 Learning Objectives

This project provides practical exposure to:

- Agentic AI
- Multi-agent architecture
- LLM-based applications
- Natural-language data querying
- SQL generation
- PostgreSQL integration
- SQL validation
- API-based data extraction
- ETL workflows
- Pandas data processing
- Structured data validation
- Agent routing and orchestration

---

# 🔮 Future Scope

Possible improvements to the project include:

- 📊 Adding data visualization capabilities
- 📁 Supporting CSV and Excel files
- 🧠 Adding conversation memory
- 🌐 Building a web-based interface
- 🔐 Adding authentication
- 🗃️ Supporting additional databases
- 🔌 Integrating additional external APIs
- ⚡ Improving error handling and recovery

---

# 📌 Project Status

**Status:** 🚧 Active Development

The project is being developed as an Agentic AI-based data assistant and can be extended with additional agents and data-processing capabilities.

---

# 👨‍💻 Author

**Tanveer Singh Naruka**

GitHub:

```text
https://github.com/boolwood
```

---

# 📄 License

This project is maintained by **Tanveer Singh Naruka**.

The project is intended for learning, experimentation, and development in the areas of Agentic AI, data analysis, database interaction, and automated data processing.