# MCP Server Practice

This repository contains implementations of Model Context Protocol (MCP) servers for LinkedIn profile scraping and weather data retrieval. The MCP framework facilitates seamless integration and communication between AI services.

## Overview

- **LinkedIn Profile Scraper**: Fetches LinkedIn profile data using the Fresh LinkedIn Profile Data API.
- **Weather Data Service**: Retrieves weather alerts and forecasts using the National Weather Service (NWS) API.

## Prerequisites

- Python 3.7+
- `httpx` for asynchronous HTTP requests
- `python-dotenv` for environment variable management
- `mcp` for MCP server implementation

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/mybarefootstory/MCP-Server-Practice-2.git
   cd MCP-Server-Practice-2
   ```

2. Install dependencies:
   ```bash
   pip install httpx python-dotenv mcp
   ```

3. Set up environment variables:
   - Create a `.env` file in the root directory.
   - Add your RapidAPI key:
     ```
     RAPIDAPI_KEY=your_rapidapi_key_here
     ```

## LinkedIn Profile Scraper

### Description

Fetches LinkedIn profile data using the Fresh LinkedIn Profile Data API. The server is initialized with `FastMCP` and listens for requests to retrieve profile information.

### Code Snippet

```python
from mcp.server.fastmcp import FastMCP
import httpx
import os
from dotenv import load_dotenv

load_dotenv()
RAPIDAPI_KEY = os.getenv("RAPIDAPI_KEY")

mcp = FastMCP("linkedin_profile_scraper")

async def get_linkedin_data(linkedin_url: str) -> dict:
    # Fetch LinkedIn profile data
    ...

@mcp.tool()
async def get_profile(linkedin_url: str) -> str:
    # Get LinkedIn profile data
    ...

if __name__ == "__main__":
    mcp.run(transport="stdio")
```

## Weather Data Service

### Description

Retrieves weather alerts and forecasts using the NWS API. The server is initialized with `FastMCP` and provides tools for fetching alerts and forecasts.

### Code Snippet

```python
from mcp.server.fastmcp import FastMCP
import httpx

mcp = FastMCP("weather")

async def make_nws_request(url: str) -> dict:
    # Make a request to the NWS API
    ...

@mcp.tool()
async def get_alerts(state: str) -> str:
    # Get weather alerts for a US state
    ...

@mcp.tool()
async def get_forecast(latitude: float, longitude: float) -> str:
    # Get weather forecast for a location
    ...

if __name__ == "__main__":
    mcp.run(transport='stdio')
```

## Usage

- **LinkedIn Profile Scraper**: Run the server and use the `get_profile` tool to fetch LinkedIn data.
- **Weather Data Service**: Run the server and use the `get_alerts` and `get_forecast` tools to retrieve weather information.
