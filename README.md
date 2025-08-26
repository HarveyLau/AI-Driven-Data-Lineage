# AI-Driven-Data-Lineage

An AI-powered platform for visualizing data lineage from Control-M XML files, using multi-agent systems and Model Context Protocol (MCP) for automated extraction, analysis, and display. This tool helps data teams trace data flows securely and efficiently, addressing common challenges like accuracy and scalability.

[![License](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Build Status](https://img.shields.io/badge/Build-Passing-green.svg)](https://example.com/build)
[![Demo](https://img.shields.io/badge/Demo-Live-orange.svg)](https://example.com/demo)

## Motivation
Data lineage is essential for compliance, debugging, and trust in data-driven decisions, but manual tracing is error-prone. This platform automates the process with AI agents, inspired by industry needs in 2025.

## Features
- **Automated Parsing**: Extract jobs and dependencies from Control-M XML.
- **Script Analysis**: Read and mark data sources (DBs/files) via MCP.
- **Data Organization**: Categorize and store lineage in a graph database.
- **Interactive Visualization**: Custom portal for exploring bloodline graphs with filters and exports.
- **Enhanced Security**: RBAC, encryption, and auditing.
- **Scalability**: Distributed agents and caching for large workflows.
- **Integrations**: Compatible with OpenLineage, Neo4j, and more.

## Installation
### Prerequisites
- Python 3.10+
- Docker (for containerized deployment)
- API keys for AI models (e.g., Anthropic) and MCP connectors

### Steps
1. Clone the repo: `git clone https://github.com/yourusername/AI-MCP-DataLineage.git`
2. Install dependencies: `pip install -r requirements.txt`
3. Set environment variables in `.env` (e.g., DB_URL, AI_API_KEY)
4. Build and run: `docker-compose up`

For detailed setup, see [docs/install.md](docs/install.md).

## Usage
1. Upload Control-M XML via the portal or CLI: `python app.py --input path/to/xml`
2. Agents process automatically: Parse > Read Scripts > Mark Sources > Organize > Store.
3. View lineage: Access http://localhost:3000/dashboard for interactive graphs.
4. Customize: Edit `config.yaml` for agent behaviors or integrations.

Example output: A DAG visualization showing job triggers, script flows, and data sources.

For advanced usage, including API endpoints, see [docs/usage.md](docs/usage.md).

## Architecture
```mermaid
%%{init: {"themeVariables": {"fontSize": "16px", "fontFamily": "'Comic Sans MS', 'Comic Sans', 'Caveat', 'Bradley Hand', cursive"}} }%%
flowchart TD
    %% Styles
    classDef input fill:#e3f0ff,stroke:#0077b6,stroke-width:2px;
    classDef database fill:#ffe3e3,stroke:#d90429,stroke-width:2px;
    classDef visualize fill:#edfbf9,stroke:#11998e,stroke-width:2px;
    classDef agent fill:#f9ecd6,stroke:#fe9000,stroke-width:2px;
    classDef security fill:#f3e5f5,stroke:#8e24aa,stroke-width:2px,stroke-dasharray:5 5;
    classDef monitor fill:#f5f5f5,stroke:#1565c0,stroke-width:2px,stroke-dasharray:3 3;

    %% Main Nodes
    A@{ shape: lean-r, label: "User Input:\nControl-M XML File" }
    B@{ shape: rect, label: "Input Validator:\nxmlschema/Python Std Lib" }
    C@{ shape: stadium, label: "Orchestrator:\nLangChain/LangGraph" }
    D@{ shape: rounded, label: "Parser Agent:\nxml.etree + Hugging Face LLM" }
    E@{ shape: rounded, label: "Script Reader Agent:\nos/pathlib" }
    F@{ shape: rounded, label: "Data Source Marker Agent:\nregex/NLTK + LLM" }
    G@{ shape: rounded, label: "Data Organizer Agent:\nPandas" }
    H@{ shape: cyl, label: "DB Inserter Agent:\nNeo4j Driver" }
    I@{ shape: stadium, label: "Visualization Portal:\nStreamlit + Plotly" }
    L@{ shape: rect, label: "User Dashboard:\nInteractive Lineage Graphs" }

    %% Apply classes
    class A input;
    class B input;
    class C agent;
    class D,E,F,G agent;
    class H database;
    class I,L visualize;

    %% Connections
    A --> B
    B --> C
    subgraph "Data Processing Agents"
        direction TB
        C --> D
        D --> E
        E --> F
        F --> G
    end
    G --> H
    H --> I
    I --> L

    %% Security Subgraph
    subgraph "Open-Source Security"
        J@{ shape: hex, label: "PyJWT/Auth Libs" }
        class J security;
    end

    %% Monitoring Subgraph
    subgraph Monitoring
        K@{ shape: rect, label: "Prometheus/Grafana" }
        class K monitor;
    end

    %% Security Connections (dotted)
    C -.-> J
    E -.-> J
    F -.-> J
    H -.-> J

    %% Monitoring Connections
    C --> K
```

The system uses AI agents orchestrated via LangGraph, MCP for secure access, and Neo4j for storage. Shortcomings like AI errors are mitigated with hybrid validation.

## Contributing
We welcome contributions! Fork the repo, create a branch, and submit a pull request. Follow our [code of conduct](CODE_OF_CONDUCT.md).

- Report issues: https://github.com/yourusername/AI-MCP-DataLineage/issues
- Suggest features: Open a discussion.

## Related Projects
- OpenLineage: For standardized lineage capture[](https://openlineage.io/)
- Atlan: AI-driven metadata tools[](https://atlan.com/)
- Monte Carlo: Data observability[](https://www.montecarlodata.com/)

## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
