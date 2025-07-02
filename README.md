# Real-Time Analytics and Intelligence for Streaming Data

An AI-driven platform to monitor and analyze live data streams across IoT, Healthcare, and Finance — with real-time dashboards, conversational querying, and autonomous alert agents.

###  Tech Stack

* **Frontend**: React, Material UI, Recharts, EventSource (SSE)
* **Backend**: Node.js (Express), Kafka (producer/consumer), Supabase (PostgreSQL)
* **Agent Layer**: Python, LangGraph, LLaMA3-70B via Groq API
* **Data Streaming**: Server-Sent Events, Kafka simulation
* **Email Alerts**: Gmail OAuth2 integration

---

##  Features

###  Unified Realtime Dashboard

* Select between IoT, Healthcare, and Stock streams
* View live metrics, trend charts, and anomaly summaries
* Real-time updates using Server-Sent Events (SSE)

###  LangGraph ReAct Agent

* Converts natural language queries into SQL
* Executes SQL using Supabase RPC
* Summarizes results in plain English
* Falls back to LLM when SQL isn't possible
* Tools:

  * `handle_greeting_tool`
  * `generate_sql_tool`
  * `run_sql_tool`
  * `summarize_result_tool`
  * `fallback_llm_tool`

###  Autonomous Monitoring Agent

* Parses user alert instructions like “Notify me if temperature > 38”
* Monitors live streams from Kafka
* Sends Gmail alerts using OAuth2
* Tools:

  * `parse_alert_condition_tool`
  * `check_custom_condition_tool`
  * `send_email_tool`
* Alerts can be stopped dynamically using `/ask` with instructions like “stop alerting”

---

##  Architecture Overview

```text
rta-frontend      → React UI, chatbot, charts
rta-backend       → Node.js Express, API layer, SSE handlers
rta-datasource    → Kafka producer streams IoT, Healthcare, and Stock data
rta-agent-python  → Python LangGraph agents for SQL + Alerts
Supabase          → Real-time PostgreSQL backend
Groq API          → LLaMA3-70B for fast LLM response (SQL gen, alerts, summarization)
```

---

##  Performance & Testing

* **Dashboard latency**: <900ms end-to-end
* **LLM response time**: \~700ms via Groq
* **Kafka ingestion**: 10K+ messages/sec
* **SQL accuracy**: \~87% correct from natural language
* **Email alerts**: Triggered in real-time on valid conditions

---

##  Quick Start

### 1. Clone & Install

```bash
git clone https://github.com/jsalammagari/real-time-analytics-and-intelligence-for-streaming-data.git
cd rta-agent-python
pip install -r requirements.txt
```

### 2. Set up `.env`

```env
GROQ_API_KEY=your_groq_key
SUPABASE_URL=your_project_url
SUPABASE_ANON_KEY=your_supabase_key
ALERT_RECIPIENT=your_email@example.com
```

### 3. Start All Modules

```bash
# Terminal 1
cd rta-frontend
npm install && npm start

# Terminal 2
cd rta-backend
npm install && node server.js

# Terminal 3
cd rta-datasource
npm install && node server.js

# Terminal 4
cd rta-agent-python
uvicorn main:app --reload --port 8001
```

---

##  Usage Examples

### 1. Ask AI questions:

```
What is the average heart rate today?
Show me the latest fire alarm status.
What is the current AQI?
```

### 2. Trigger alerts via chat:

```
Alert me when temperature > 38
Notify me if oxygen_saturation < 94
Stop IOT alert monitoring
```

---

##  Project Structure

```bash
rta-agent-python/
main.py                # ReAct + Alert agents
alert_agent.py         # Autonomous agent logic
credentials.json       # Gmail OAuth2 creds
token.json             # Gmail refresh token

rta-frontend/              # React frontend with chatbot and charts
rta-backend/               # Express SSE and Kafka bridge
rta-datasource/            # Kafka producers for IoT/Stock/Healthcare
```

---

##  Report and Documentation

* [Abstract](https://drive.google.com/file/d/1FcaZSR0hYOO1WPnDcVZA1HHFJFavZzQd/view?usp=sharing)
* [Report](https://drive.google.com/file/d/1iad54FV-IYfvJHu-dUds60Lnr7passrD/view?usp=sharing)
* [Demo](https://drive.google.com/file/d/1Mz7-iwtIpYbw4qMDGRWy7wH0L9h70g5K/view?usp=sharing)

---