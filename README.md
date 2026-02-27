# myweather

An MCP (Model Context Protocol) server that provides real-time weather data using the [National Weather Service (NWS) API](https://www.weather.gov/documentation/services-web-api). It exposes tools to fetch active weather alerts and forecasts for US locations.

## Features

- Get active weather alerts by US state
- Get weather forecasts by latitude and longitude
- Runs as an MCP server over stdio transport

## Requirements

- Python 3.12+
- [uv](https://github.com/astral-sh/uv) (recommended) or pip

## Installation

```bash
git clone https://github.com/GigCory/myweather.git
cd myweather
```

Using uv:

```bash
uv sync
```

Using pip:

```bash
pip install -r requirements.txt
```

## Usage

### Run as MCP server

```bash
python weather.py
```

The server communicates over stdio and exposes the following tools:

### Tools

#### `get_alerts(state: str)`

Returns active weather alerts for a given US state.

- `state` — Two-letter state code (e.g. `CA`, `NY`, `TX`)

**Example:**
```
get_alerts("CA")
```

#### `get_forecast(latitude: float, longitude: float)`

Returns the weather forecast for the next 5 periods for a given location.

- `latitude` — Latitude of the location (e.g. `37.7749`)
- `longitude` — Longitude of the location (e.g. `-122.4194`)

**Example:**
```
get_forecast(37.7749, -122.4194)
```

## MCP Client Configuration

To use this server with an MCP-compatible client (e.g. Claude Desktop), add the following to your client config:

```json
{
  "mcpServers": {
    "myweather": {
      "command": "python",
      "args": ["/path/to/myweather/weather.py"]
    }
  }
}
```

## Project Structure

```
myweather/
├── weather.py        # MCP server with NWS API tools
├── main.py           # Entry point
├── mcp_logger.py     # Logging utility
├── pyproject.toml    # Project metadata and dependencies
├── requirements.txt  # Pip-compatible dependency list
└── .python-version   # Python version pin
```

## License

MIT
