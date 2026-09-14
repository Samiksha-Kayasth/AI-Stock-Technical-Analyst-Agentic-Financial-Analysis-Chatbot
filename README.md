# AI Stock Technical Analyst

An agentic stock technical-analysis chatbot built with **n8n**, **Google Gemini 2.5 Flash**, and the **Chart-IMG REST API**.

## What it does

The system accepts a natural-language stock request such as `Analyze Reliance stock`, extracts the stock ticker, generates a TradingView-style technical chart, and sends the chart image to Gemini for visual technical analysis.

The final analysis includes:
- Candlestick and price-action observations
- Trend and momentum analysis
- MACD and histogram interpretation
- Volume analysis
- Support and resistance levels
- Breakout/pullback observations
- An overall BUY / SELL / HOLD signal

## Architecture

```text
User stock request
       ↓
Technical_Analyst (AI Agent)
       ↓
Extract ticker with $fromAI("ticker")
       ↓
Call Main_analysis sub-workflow
       ↓
Chart-IMG REST API
       ↓
TradingView-style chart image
       ↓
Download chart
       ↓
Gemini 2.5 Flash Vision
       ↓
Technical analysis + BUY/SELL/HOLD
```

## Workflows

### `Technical_Analyst.json`
The main agent workflow. It receives the user's request, uses Gemini as the language model, maintains conversational memory, extracts the ticker, and calls the `Main_analysis` workflow as an AI tool.

### `Main_analysis.json`
The analysis sub-workflow. It receives the ticker, generates a weekly NSE chart with Volume and MACD using Chart-IMG, downloads the chart, and passes the image to Gemini for technical analysis.

## Technologies

- n8n — workflow automation and agent orchestration
- LangChain / n8n AI Agent — tool calling
- Google Gemini 2.5 Flash — language and vision analysis
- Chart-IMG API — chart generation
- REST APIs — external service integration

## Setup

1. Install and run n8n locally.
2. Import both JSON files from the `workflows/` folder.
3. Create your own Gemini credential in n8n.
4. Add your own Chart-IMG API key.
5. In `Technical_Analyst`, make sure the `Call 'Main_analysis'` tool points to your imported `Main_analysis` workflow.
6. Execute the workflow with a stock request such as `Analyze RELIANCE stock`.

> **Important:** The exported workflows in this repository contain placeholders instead of real API keys or credentials. Add your own secrets inside n8n and never commit them to GitHub.

## Project result

The workflow automates the chart-generation and visual-analysis steps of technical stock analysis, reducing a multi-step manual process to an automated n8n pipeline.

## Disclaimer

This project is for educational and demonstration purposes. The BUY/SELL/HOLD output is model-generated technical analysis and is not financial advice.
