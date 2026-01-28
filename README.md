AI-Powered Stock & ETF Signal Generation Platform
Version 2.3.0 - Hybrid Signal Intelligence Update
Updated: January 13, 2026

A comprehensive trading signal platform that combines Machine Learning (Random Forest + XGBoost) with Technical Analysis (RSI, MACD, SMA) to generate high-confidence stock predictions. Features a modern Glassmorphism dashboard, smart email alerts, and a resilient microservices architecture.

🚀 Quick Start
Windows (Recommended)
The easiest way to start all services (Dashboard + API + Alerts + Backtesting):

./run_project.ps1
This script automatically starts the backend API, the alerts scheduler, and the Streamlit dashboard in the correct order.

Manual Start
If you prefer running components individually:

# Terminal 1: Start Backend API
python signals/api.py

# Terminal 2: Start Dashboard
streamlit run 0_Overview.py
Access Points:

📊 Dashboard: http://localhost:8501
📡 Signals API: http://localhost:8000
🔔 Alerts Service: http://localhost:8001
🧪 Backtesting: http://localhost:8002
💎 Key Features
🧠 Hybrid AI Architecture
We don't just rely on one model. Our system synthesizes data from multiple sources:

Deep Learning: Random Forest & XGBoost models trained on 5 years of historical data.
Technical Validation: Signals are cross-referenced with live RSI, MACD, and Moving Averages.
Explainable AI: Every signal comes with a specific "Why" (e.g., "RSI Oversold + Strong Uptrend").
🖥️ Modern Dashboard
Glassmorphism Design: Beautiful, responsive UI with dark mode aesthetics.
Real-Time Analysis: Live price updates and instant signal generation.
Interactive Charts: Technical indicators (RSI, MACD) visualized dynamically.
🛡️ Resilience & Safety
Circuit Breakers: Automatically handles API failures or delisted stocks without crashing.
Smart Fallback: If ML models are unreachable, the system gracefully switches to a robust Heuristic Expert System.
No-Flicker Logic: Signal consistency checks to prevent "flashing" predictions.
🔔 Smart Alerts
HTML Emails: Receive beautiful, formatted email alerts.
Details: Includes Confidence Score, Signal Strength, and Current Price.
🏛️ Architecture Overview
The platform operates on a microservices architecture, ensuring scalability and resilience:

+-------------------+       +-------------------+       +-------------------+
|     Frontend      |       |     Backend API   |       |    ML Engine      |
| (Streamlit/Pages) | <---> |   (FastAPI)       | <---> | (Models/Predictor)|
+-------------------+       +-------------------+       +-------------------+
         ^                          ^     ^
         |                          |     |
         |                          |     v
         |                          |   +-------------------+
         |                          |   |  Data Layer       |
         |                          |   | (Fetcher/Pipeline)|
         |                          v   +-------------------+
         |                  +-------------------+
         +----------------->|  Alerts Service   |
                            | (Email Notifications) |
                            +-------------------+
Frontend (Streamlit Dashboard): User interface for interaction, data visualization, and signal display.
Backend API (FastAPI): Serves as the central hub, handling requests from the dashboard, orchestrating data fetching, and interacting with the ML Engine.
ML Engine: Contains the core machine learning models and prediction logic.
Data Layer: Responsible for fetching raw market data and processing it for the ML Engine.
Alerts Service: A background service for sending email notifications based on generated signals.
📂 Project Structure Guide
Here is a detailed breakdown of the codebase organization:

AI POWERED SIGNALS/
│
├── 0_Overview.py          # 🏠 Main Entry Point for the Dashboard
├── run_project.ps1        # 🚀 One-Click Startup Script for Windows
│
├── alerts/                # 🔔 Notifications Service
│   └── main.py           # Background scheduler for email alerts
│
├── backtesting/           # 🧪 Strategy Validation
│   └── main.py           # Backtesting engine to verify model performance
│
├── contracts/             # 📝 Data Schemas
│   └── schema.py         # Pydantic models (MLSignal, StockData) used across apps
│
├── data/                  # 💾 Data Layer
│   ├── fetcher.py        # Connects to Yahoo Finance (YFinance)
│   └── pipeline.py       # Data cleaning and feature engineering pipeline
│
├── ml/                    # 🧠 Machine Learning Core
│   ├── models/           # Stores trained model files (*.pkl)
│   └── predictor.py      # The "Brain": Logic for Hybrid Prediction (ML + Technicals)
│
├── pages/                 # 📄 Dashboard Screens
│   ├── 1_📊_AI_Signals.py # Main Analysis Page
│   └── 2_🧪_Backtesting.py # Historic Performance Page
│
├── signals/               # 📡 Backend API Service
🎯 Features
✅ One-Command Startup - Everything auto-starts
✅ Background API Server - Starts automatically with dashboard
✅ 8 REST API Endpoints - Supabase-ready
✅ Auto-dependency Management - No manual setup
✅ ML Models - Random Forest + XGBoost ensemble
✅ Interactive Dashboard - Real-time stock analysis
✅ Smart Port Detection - Auto-finds available ports
📡 API Endpoints
Base URL: http://127.0.0.1:8000

System & Pipeline
GET /health - Health check
POST /run-pipeline - Trigger data pipeline
Stock Data & Charts
GET /supabase/recent/{ticker}?days=30 - Recent data
GET /supabase/ticker/{ticker}?start_date=2024-01-01&limit=100 - Historical data
Market Overview
GET /supabase/latest?limit=10 - Latest market data
GET /supabase/top-performers?top_n=10 - Top performers
Analysis
GET /supabase/stats/{ticker}?start_date=2024-01-01 - Statistics
GET /supabase/rsi-search?min_rsi=0&max_rsi=30 - RSI-based search
🧪 Testing
# Test all API endpoints
python test_api_endpoints.py
📡 Core API Endpoints
Predictions
POST /api/v1/ml/signal/live - Generate real-time hybrid signal.
POST /api/v1/ml/signal/historical - Get 5-year signal history for backtesting.
Market Data
GET /supabase/recent/{ticker} - Get clean historical OHLCV data.
GET /supabase/top-performers - Get market movers.
⚡ How It Works (The Flow)
User Search: You enter a ticker (e.g., AAPL) on the Dashboard.
Data Fetch: System pulls live market data via yfinance.
Hybrid Analysis:
Layer 1: ML Models calculate probability.
Layer 2: Technical Rules validate the trend.
Signal Generation: A final BUY/SELL/HOLD signal is generated with a Confidence Score.
Display: Results are shown on the Dashboard and sent via Email (if configured).
HOW TO RUN OLLAMA
. Install Ollama
Download and install Ollama from the official website:

Windows/Mac/Linux: https://ollama.com/download

2. Download the Model
Open your terminal (Command Prompt, PowerShell, or Bash) and run the following command to download the OLlama model:



ollama pull mistral

(run this once,i.e the first time)

3. Start the Ollama Server
Ensure the Ollama application is running. You can verify this by checking your system tray (Windows/Mac) or by running:


ollama serve

(Note: The server must be active on http://localhost:11434 for the MLEngine to generate summaries.)

4. Verify the Connection (Optional)
You can test if the model is responsive by running:


ollama run mistral 

License: MIT
