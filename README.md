# Financial Datasets MCP Server

## Introduction

This is a Model Context Protocol (MCP) server that provides access to stock market data from [Financial Datasets](https://www.financialdatasets.ai/). 

It allows Claude and other AI assistants to retrieve financial information like income statements, balance sheets, cash flow statements, and stock prices directly through the MCP interface.

## Available Tools

This MCP server provides the following tools:

- **get_income_statements**: Retrieve income statements for a stock
- **get_balance_sheets**: Retrieve balance sheets for stock
- **get_cash_flow_statements**: Retrieve cash flow statements for a stock
- **get_current_price**: Get the latest price information for a stock
- **get_prices**: Get historical stock prices with customizable date ranges and intervals
- **get_news**: Get the latest news for a stock

## Setup

### Prerequisites

- Python 3.10 or higher
- [uv](https://github.com/astral-sh/uv) package manager

### Installation

1. Clone this repository:
   ```bash
   git clone https://github.com/financial-datasets/mcp-server
   cd mcp-server
   ```

2. If you don't have uv installed, install it:
   ```bash
   # macOS/Linux
   curl -LsSf https://astral.sh/uv/install.sh | sh
   
   # Windows
   curl -LsSf https://astral.sh/uv/install.ps1 | powershell
   ```

3. Install dependencies:
   ```bash
   # Create virtual env and activate it
   uv venv
   source .venv/bin/activate  # On Windows: .venv\Scripts\activate
   
   # Install dependencies
   uv add "mcp[cli]" httpx  # On Windows: uv add mcp[cli] httpx

   ```

4. Set up environment variables:
   ```bash
   # Create .env file for your API keys
   cp .env.example .env

   # Set API key in .env
   FINANCIAL_DATASETS_API_KEY=your-financial-datasets-api-key
   ```

5. Run the server:
   ```bash
   uv run server.py
   ```

## Connecting to Claude Desktop

1. Install [Claude Desktop](https://claude.ai/desktop) if you haven't already

2. Create or edit the Claude Desktop configuration file:
   ```bash
   # macOS
   mkdir -p ~/Library/Application\ Support/Claude/
   nano ~/Library/Application\ Support/Claude/claude_desktop_config.json
   ```

3. Add the following configuration:
   ```json
   {
     "mcpServers": {
       "financial-datasets": {
         "command": "/path/to/uv",
         "args": [
           "--directory",
           "/absolute/path/to/financial-datasets-mcp",
           "run",
           "server.py"
         ]
       }
     }
   }
   ```
   
   Replace `/path/to/uv` with the result of `which uv` and `/absolute/path/to/financial-datasets-mcp` with the absolute path to this project.

4. Restart Claude Desktop

5. You should now see the financial tools available in Claude Desktop's tools menu (hammer icon)

6. Try asking Claude questions like:
   - "What are Apple's recent income statements?"
   - "Show me the current price of Tesla stock"
   - "Get historical prices for MSFT from 2024-01-01 to 2024-12-31"
