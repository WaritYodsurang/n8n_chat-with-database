# System Architecture – ChatSQL Agent

```mermaid
---
config:
  layout: dagre
---

flowchart TD
  %% === USER INTERACTION ===
  subgraph User_Interaction["👤 User Interaction"]
    A1["User on Streamlit Frontend"]
    A2["Asks natural language question"]
  end

  %% === FRONTEND ===
  subgraph Frontend["💻 Streamlit App"]
    B1["Streamlit App"]
    B2["Send query via HTTP POST"]
    B3["Display: SQL + Result Table + Chart + Logs"]
  end

  %% === BACKEND ===
  subgraph Backend["🧠 n8n Backend"]
    C1["n8n Webhook Trigger – Chat"]
    C2["AI Agent – Langchain + OpenAI"]
    C3["Get Schema & Table List"]
    C4["Get Table Definition"]
    C5["Execute SQL Query"]
    C6["Return Results as JSON"]
    D1[("PostgreSQL DB")]
  end

  %% === Flow Connections ===
  A1 --> A2
  A2 --> B1
  B1 --> B2
  B2 --> C1
  C1 --> C2
  C2 --> C3
  C2 --> C4
  C2 --> C5
  C3 --> D1
  C4 --> D1
  C5 --> D1
  C5 --> C6
  C6 --> B3
  B3 --> A1

  %% === Subgraph Colors ===
  classDef UserInteraction fill:#E3F2FD,stroke:#90CAF9,stroke-width:1px;
  classDef Frontend fill:#F1F8E9,stroke:#AED581,stroke-width:1px;
  classDef Backend fill:#FFF3E0,stroke:#FFB74D,stroke-width:1px;

  class User_Interaction UserInteraction
  class Frontend Frontend
  class Backend Backend
