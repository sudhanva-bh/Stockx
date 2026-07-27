# Stockx - Supply Chain Agentic AI Platform

[![Gilhari](https://img.shields.io/badge/Gilhari-ORM%20Microservice-blue?style=for-the-badge)](https://www.softwaretree.com/v1/products/gilhari/gilhari.php)
[![ORMCP](https://img.shields.io/badge/ORMCP-MCP%20Server-8A2BE2?style=for-the-badge)](https://pypi.org/project/ormcp-server/)
![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![Java](https://img.shields.io/badge/java-%23ED8B00.svg?style=for-the-badge&logo=openjdk&logoColor=white)
![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)
![Flutter](https://img.shields.io/badge/Flutter-%2302569B.svg?style=for-the-badge&logo=Flutter&logoColor=white)
![LangChain](https://img.shields.io/badge/LangChain-1C3C3C?style=for-the-badge&logo=langchain&logoColor=white)
![LangGraph](https://img.shields.io/badge/LangGraph-FF6B35?style=for-the-badge&logo=langchain&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-005571?style=for-the-badge&logo=fastapi)
![MicrosoftSQLServer](https://img.shields.io/badge/Microsoft%20SQL%20Server-CC2927?style=for-the-badge&logo=microsoft%20sql%20server&logoColor=white)


## What This Project Does

This repository demonstrates a complete, production-grade **Agentic Supply Chain Management** system. It is designed to showcase the full power of [Gilhari](https://www.softwaretree.com/v1/products/gilhari/gilhari.php) — a zero-boilerplate Object-Relational Mapping (ORM) microservice — paired with [ORMCP](https://pypi.org/project/ormcp-server/), a semantic gateway that exposes any Gilhari-managed database with a set of structured **Model Context Protocol (MCP)** tools that AI agents can understand and call directly.

In practical terms: you run this project and you get a **web dashboard** where a supply chain manager can either manually manage inventory, suppliers, and purchase orders through standard data grids, or simply type a natural-language question such as:

> "Show me a Kanban board of all purchase orders grouped by delivery status, sorted by total cost."

To answer a natural language question, the AI agent will then autonomously query the database through MCP tool calls, aggregate the data, and respond with a fully rendered, interactive UI component — a Kanban board, a bar chart, a KPI card, a data table — drawn directly inside the chat panel. No custom API endpoints. No hand-written SQL in the frontend. No glue code.

---

<table>
  <tr>
    <td width="240" valign="middle">
      <a href="https://youtu.be/TO6EByhE_u4">
        <img src="https://img.youtube.com/vi/TO6EByhE_u4/hqdefault.jpg" alt="Stockx Video Demo" width="180" />
      </a>
    </td>
    <td valign="middle">
      🎬 <b><a href="https://youtu.be/TO6EByhE_u4">Watch the Stockx Video Article on YouTube</a></b><br/>
    </td>
  </tr>
</table>

---

### Core Technologies

- **JDX**: A lightweight and non-intrusive Object-Relational Mapping (ORM) framework that maps relational data to Java/JSON objects. JDX is a Java ORM engine that reverse-engineers relational database schemas into a curated Java/JSON object model — the foundational data-access layer beneath Gilhari.
- **Gilhari**: A RESTful microservice framework, built on JDX, that turns a database into a governed object API. Gilhari packages a JDX object model as a RESTful microservice — exposing your database as a curated, object-oriented REST API with no hand-written server code.
- **ORMCP**: An MCP server that connects AI agents to a relational database via the Model Context Protocol. ORMCP bridges AI agents to your database through Gilhari, giving them a governed, object-oriented view of your data — not raw SQL or table rows — via natural language. As an MCP-compliant semantic layer, ORMCP exposes enterprise data as intuitive, business-oriented objects (e.g., Customers, Orders, Products), rather than requiring agents to interact with schemas and SQL directly. This simplifies how AI applications interact with structured data by improving reasoning clarity, reducing token usage, and introducing a cleaner governance boundary.

### Why This Matters

- **Zero SQL in your AI layer.** The ORMCP server provides an object-model agnostic set of flexible MCP tools that operate on any type of governed business objects exposed through the RESTful Gilhari microservice. The LLM never writes raw SQL for standard CRUD — it calls safe, schema-validated functions.
- **Generative UI, not just text.** The agent's response is a structured JSON payload that the Flutter frontend parses and renders as a live UI widget. The model decides the correct visualization for the data it just retrieved.
- **Swappable LLM backend.** The system works with both OpenAI (GPT-5, GPT-5-mini) and Google (Gemini Flash, Gemini Flash Lite) with a single environment variable change.
- **Fully containerized infrastructure.** SQL Server and the Gilhari microservice run in Docker with a single command.
- **Stable MCP tool surface across business domains.** ORMCP exposes a small, stable set of generic MCP tools rather than generating new tools per business class. Whether the attached Gilhari microservice defines five object types or five hundred, the MCP interface remains essentially unchanged. As new business classes are introduced — or an entirely different domain is deployed — the same generic MCP tools immediately work with the newly exposed object types.
- **Separation of concerns.** The Gilhari microservice defines the business domain declaratively through its object model. ORMCP provides a generic AI interface over that model. The object model changes; the MCP surface does not.

---

### Stable MCP Tools over Dynamic Business Models

Traditional MCP servers typically expose tools that are specific to the application they front. Add a new capability, and someone usually has to implement and register another MCP tool.

ORMCP takes a fundamentally different approach.

ORMCP exposes a small, stable set of generic MCP tools that operate over business objects rather than application-specific APIs. The attached Gilhari microservice defines the business domain declaratively through its object model. Whether that model contains five classes or five hundred, the MCP interface remains essentially unchanged.

As new business classes are introduced — or an entirely different domain such as healthcare, retail, insurance, or manufacturing is deployed — the same generic MCP tools immediately work with the newly exposed object types.

In effect, **the object model changes. The MCP surface does not.**

This separation is what makes ORMCP reusable across applications rather than tied to a particular business domain.

## Architectural Overview

![Architectural Overview](./reports/images/arch_overview.png)

| Layer | Technology | Role |
|---|---|---|
| Frontend | Flutter Web | Admin dashboard with manual CRUD views and an AI chat panel that renders Generative UI widgets |
| AI Orchestration | FastAPI + LangGraph + LangChain | Receives chat requests, runs the agentic tool-calling loop, streams structured JSON responses |
| Semantic Gateway | ORMCP (`ormcp-server`) | Exposes the object model and data access operations as MCP tools (e.g., object model discovery, querying, aggregation) |
| Data Abstraction | Gilhari (Docker) | Automatic REST API generation from JDX ORM mappings; no hand-written data access code |
| Database | Microsoft SQL Server 2022 | Persistent relational store for the six-table supply chain schema |
| ORM Mapping | JDX + Java/JSON Container Classes | Declarative mapping of Java/JSON objects to SQL tables; compiled into the Gilhari container |

---

## Repository Structure

| Directory / File | Type | Description |
|---|---|---|
| [`backend/`](./backend/) | Python Service | FastAPI agentic AI backend. Runs the LangGraph agent loop, connects to ORMCP, and streams Generative UI responses. See [Backend README](./backend/README.md). |
| [`admin_dashboard/`](./admin_dashboard/) | Flutter Web App | Single-page web dashboard with six CRUD views and an AI Analytics chat panel. See [Frontend README](./admin_dashboard/README.md). |
| [`src/`](./src/) | Java Source | Container model classes (`Supplier`, `InventoryItem`, etc.) extending `JDX_JSONObject`. Compiled into `bin/` and packaged into the Gilhari Docker image. |
| [`bin/`](./bin/) | Compiled Classes | Pre-compiled Java `.class` files for the Gilhari ORM. Produced by `compile.cmd`. |
| [`config/`](./config/) | ORM Configuration | `supply_chain.jdx` — JDX grammar file mapping Java/JSON object attributes to SQL columns and defining foreign-key relationships. The `JDX_DATABASE` directive at the top must be updated with your actual database connection URL, credentials, and driver settings before this file can be used in a live Gilhari microservice. The `OBJECT_MODEL_OVERVIEW` field provides the LLM with a high-level description of the business domain and can be expanded to improve agent reasoning. Also contains `classnames_map.json` — maps short entity names (e.g., `InventoryItem`) to their fully-qualified Java class names; used by Gilhari to resolve object types at runtime. |
| [`sql/`](./sql/) | SQL Scripts | `init.sql` — creates the six-table schema and inserts a baseline dataset into the SQL Server instance. |
| [`Dockerfile`](./Dockerfile) | Docker Build | Extends `softwaretree/gilhari`, downloads the Microsoft SQL Server JDBC driver, and packages the compiled models and JDX config. |
| [`docker-compose.yml`](./docker-compose.yml) | Docker Compose | Defines and links the `sqlserver` and `gilhari-service` containers. SQL Server on port `1433`, Gilhari on port `80`. |
| [`gilhari_service.config`](./gilhari_service.config) | Gilhari Config | JSON config read by the Gilhari REST server at startup — points to the JDX spec, JDBC driver, and compiled class directory. |
| [`seed.py`](./seed.py) / [`seed_lite.py`](./seed_lite.py) | Python Scripts | Populates the database with randomized supply chain data via the Gilhari REST API. |
| [`reports/`](./reports/) | LaTeX Reports | Academic and technical report sources for the project, including `report.tex`, bibliography (`ref.bib`), and supporting assets. Not required for running the application. |
| [`start_ormcp.bat`](./start_ormcp.bat) | Batch Script | Standalone launcher for the ORMCP server — for use with Claude Desktop or any other MCP-compatible client. |
| [`test_mcp_client.py`](./test_mcp_client.py) | Test Script | Validates that ORMCP connects to Gilhari and exposes the expected MCP tools. Dumps tool schemas to `mcp_tools_output.log`. |
| [`compile.cmd`](./compile.cmd) | Build Script | Compiles Java container model classes in `src/` into `bin/`. Only required when modifying Java source files. |

---

## Database Schema

The system manages six normalized tables representing a complete supply chain:

| Table | Purpose | Key Relationships |
|---|---|---|
| `Suppliers` | Vendor profiles: company name, contact email, geographic region | One-to-Many with `InventoryItems` |
| `ItemCategories` | Product category classifications with descriptions | One-to-Many with `InventoryItems` |
| `InventoryItems` | Central product catalog with stock quantities and unit prices | Many-to-One with `Suppliers` and `ItemCategories` |
| `PurchaseOrders` | Order headers with date, total cost, and delivery status | One-to-Many with `PurchaseOrderItems` |
| `PurchaseOrderItems` | Junction table mapping items and quantities to purchase orders, recording negotiated prices | Many-to-One with `PurchaseOrders` and `InventoryItems` |
| `StockTransactions` | Immutable audit log of all stock movements (RESTOCK, SALE, ADJUSTMENT) | Many-to-One with `InventoryItems` |

---

## Prerequisites

| Dependency | Required For |
|---|---|
| Docker Desktop | Running SQL Server and the Gilhari microservice containers |
| Python 3.12+ | FastAPI backend, ORMCP server, and seeding scripts |
| Flutter SDK 3.x | Admin dashboard web application |
| Java JDK 8+ | Only needed to recompile Java ORM container classes (`compile.cmd`) |
| Google Gemini API key or OpenAI API key | AI agent functionality |

---

## Setup and Running

Choose the guide that matches your situation:

- [Brand New Setup](#brand-new-setup) — First time running, or after deleting Docker volumes
- [Resuming an Existing Setup](#resuming-an-existing-setup) — Starting everything back up after a prior session
- [Shutting Everything Down](#shutting-everything-down) — Safely stopping all components

---

### Brand New Setup

#### Step 1 — Configure the Environment

Create a `.env` file from the example and configure your API keys and database credentials:
```cmd
copy .env.example .env
```
Open `.env` and fill in your values (e.g., `GEMINI_API_KEY` or `OPENAI_API_KEY`).

Then, run the setup script to generate the secure database configuration (`config/supply_chain.jdx`) and the backend configuration:
```cmd
python setup_env.py
```
*(Note: You must do this before starting Docker, as the Gilhari container requires the generated `.jdx` file!)*

> **Important:** After running `setup_env.py`, open `config/supply_chain.jdx` and verify that the `JDX_DATABASE` line contains the correct database URL, port, database name, username, and password for your environment. The `OBJECT_MODEL_OVERVIEW` value can also be expanded with a richer description of your data domain to improve LLM reasoning quality.

#### Step 2 — Start the Docker Infrastructure

**Compile the Java container classes** (required on first setup and whenever you modify `.java` files in `src/`):
```cmd
.\compile.cmd
```
This compiles the Java/JSON container classes (e.g., `Supplier.java`, `InventoryItem.java`) from `src/` into `bin/`, which are then packaged into the Gilhari Docker image.

**Build and start the Gilhari microservice and SQL Server:**
```cmd
docker-compose up -d --build
```
This builds the Gilhari Docker image (via `build.cmd` internally) and starts both the `gilhari-service` and `sqlserver` containers.

Wait approximately 15-20 seconds for SQL Server to finish initializing on port `1433`.

#### Step 3 — Initialize the Database Schema

Copy and execute the schema initialization script inside the SQL Server container:
```cmd
docker cp sql\init.sql sqlserver:/init.sql
docker exec -it sqlserver /opt/mssql-tools18/bin/sqlcmd -S localhost -U sa -P "YourStrong!Passw0rd" -C -i /init.sql
```

#### Step 4 — Seed the Database

Install dependencies and run the seeding script:
```cmd
pip install requests python-dotenv
python seed.py
```

For a smaller, faster dataset, use `python seed_lite.py` instead.

#### Step 5 — Start the Agentic Backend

```cmd
cd backend
python -m venv .venv --system-site-packages
.\.venv\Scripts\activate
pip install -r requirements.txt
uvicorn main:app --port 8001 --reload
```

#### Step 6 — Start the Frontend Dashboard

Open a new terminal:
```cmd
cd admin_dashboard
flutter run -d chrome --web-browser-flag "--disable-web-security"
```

---

### Resuming an Existing Setup

Your database is stored in a persistent Docker volume (`sqlserver_data`). Do not re-run initialization or seeding scripts.

```cmd
# Terminal 1 — Infrastructure
docker-compose up -d

# Terminal 2 — Backend
cd backend
.\.venv\Scripts\activate
uvicorn main:app --port 8001 --reload

# Terminal 3 — Frontend
cd admin_dashboard
flutter run -d chrome --web-browser-flag "--disable-web-security"
```

---

### Shutting Everything Down

```cmd
# Frontend: press 'q' in the Flutter terminal

# Backend: press Ctrl+C in the uvicorn terminal (also terminates the background ORMCP process)

# Docker infrastructure
docker-compose down
```

---

## Cloud Deployment

This project is fully ready for deployment on Microsoft Azure (Azure SQL, Azure Container Apps, Azure App Service, and Azure Static Web Apps). 

For a comprehensive, step-by-step guide on how to host this platform in the cloud, refer to the [Azure Deployment Guide](./DEPLOYMENT.md).

---

## Component Verification

### 1. SQL Server Database
```cmd
docker exec -it sqlserver /opt/mssql-tools18/bin/sqlcmd -S localhost -U sa -P "YourStrong!Passw0rd" -Q "SELECT @@VERSION"
```

### 2. Gilhari REST Microservice
```cmd
curl.exe -X GET "http://localhost/gilhari/v1/health/check"
```
Expected: `{"status":"ok"}`

### 3. ORMCP Semantic Gateway
```cmd
python test_mcp_client.py
```
Performs a handshake with the ORMCP server and dumps all available tool schemas to `mcp_tools_output.log`.

### 4. FastAPI Agentic Backend

Open the Swagger UI: [http://localhost:8001/docs](http://localhost:8001/docs)

Or via PowerShell:
```powershell
Invoke-RestMethod -Method Post -Uri "http://localhost:8001/api/agentic-chat" `
  -Headers @{"Content-Type"="application/json"; "X-App-Password"="secret123"} `
  -Body '{"message": "How many inventory items are below 100 units in stock?"}'
```

### 5. Flutter Admin Dashboard

Open the Chrome instance launched by `flutter run` and navigate to the **AI Analytics** tab in the left sidebar to verify Generative UI rendering.

---

## Standalone MCP Integration (Claude Desktop)

The ORMCP server can be connected to any MCP-compatible client independently of the full backend stack. This lets you query and manipulate the supply chain database directly from Claude Desktop:

```cmd
.\start_ormcp.bat
```

Configure your MCP client to invoke `start_ormcp.bat` as its server command. The ORMCP server will connect to the running Gilhari microservice and expose its stable set of generic MCP tools, giving the client immediate access to the supply chain object model.

---

## Generative UI Response Types

The AI agent returns a structured `AgentResponse` JSON payload. The Flutter frontend inspects the `response_type` field and renders the corresponding widget:

| Response Type | Rendered Widget |
|---|---|
| `text_only` | Plain markdown text response |
| `table_view` | Static data table with columns and rows |
| `direct_fetch_table` | Live data table fetched on demand from Gilhari |
| `metric_kpi_view` | KPI summary cards with values, trend direction, and color coding |
| `chart_view` | Bar, pie, or line chart rendered with `fl_chart` |
| `timeline_view` | Chronological event timeline |
| `kanban_view` | Multi-column Kanban board with color-coded status cards |
| `regional_view` | SVG world map with regional data overlays |
| `actionable_form_view` | Dynamic form for creating or updating records through the agent |
| `alert_anomaly_view` | Severity-ranked alert cards for detected anomalies |
| `confirmation_view` | Pre-execution confirmation dialog before a destructive mutation |

---

## Component Documentation

- [Backend README](./backend/README.md) — FastAPI service, LangGraph agent, ORMCP integration, API reference, and environment configuration
- [Frontend README](./admin_dashboard/README.md) — Flutter architecture, Generative UI widget system, CRUD view structure, and theming

## External References

- [Gilhari Product Page](https://www.softwaretree.com/v1/products/gilhari/gilhari.php) — Official documentation for the Gilhari ORM microservice
- [ORMCP on PyPI](https://pypi.org/project/ormcp-server/) — The Python package powering the MCP semantic gateway
- [ORMCP Documentation](https://github.com/SoftwareTree/ormcp-docs) — Full documentation for the ORMCP MCP server, including tool reference and configuration guide
- [Model Context Protocol Specification](https://modelcontextprotocol.io/) — The open protocol standard for connecting LLMs to external tools
