# Monday.com MCP Server

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

A lightweight MCP Server for seamless integration with Monday.com, enabling MCP clients to interact with boards, items and other Monday.com resources. Developed by [sofias tech](https://github.com/xxx/mcp-server-monday/).

## Features

This server provides a clean interface to Monday.com resources through the Model Context Protocol (MCP), with built-in caching for improved performance.

### Tools

The server implements the following tools:

- `Get_Board_Schema`: Retrieves the schema of a Monday.com board including columns, groups, and tags
- `Get_Item_Details`: Fetches detailed information about a specific item by its ID
- `Get_Items_by_Column_Value`: Searches for items based on a specific column value
- `Create_Item`: Creates a new item in a specified group within a board
- `Update_Item`: Updates column values for an existing item
- `Delete_Item`: Removes an item from a board

## Architecture

The server is built with resource efficiency in mind:

- Clear separation between resource management and tool implementation
- Simple and maintainable codebase under 30 lines per module

## Setup

1. Create a personal API token in Monday.com by following the instructions in the [Monday.com API documentation](https://developer.monday.com/api-reference/docs/authentication#personal-api-tokens)
2. Identify your board ID from the URL of your Monday.com board (e.g., if the URL is `https://your-workspace.monday.com/boards/12345678`, the board ID is `12345678`)

## Environment Variables

The server requires these environment variables:

- `MONDAY_API_KEY`: Your Monday.com personal API token
- `MONDAY_BOARD_ID`: The ID of your default board

## Quickstart

### Installation

```bash
pip install -e .
```

Or install from PyPI once published:

```bash
pip install mcp-monday-server
```

Using uv:

```bash
uv pip install mcp-monday-server
```

### Claude Desktop Integration

To integrate with Claude Desktop, update the configuration file:

On Windows: `%APPDATA%/Claude/claude_desktop_config.json`
On macOS: `~/Library/Application\ Support/Claude/claude_desktop_config.json`

#### Standard Integration

```json
"mcpServers": {
  "monday": {
    "command": "mcp-monday-server",
    "env": {
      "MONDAY_API_KEY": "your-monday-api-key",
      "MONDAY_BOARD_ID": "your-default-board-id"
    }
  }
}
```

#### Using uvx

```json
"mcpServers": {
  "monday": {
    "command": "uvx",
    "args": [
      "mcp-monday-server"
    ],
    "env": {
      "MONDAY_API_KEY": "your-monday-api-key",
      "MONDAY_BOARD_ID": "your-default-board-id"
    }
  }
}
```

## Development

### Requirements

- Python 3.10+
- Dependencies listed in `requirements.txt` and `pyproject.toml`

### Local Development

1. Clone the repository
2. Create a virtual environment:
   ```bash
   python -m venv .venv
   source .venv/bin/activate  # On Windows: .venv\Scripts\activate
   ```
3. Install development dependencies:
   ```bash
   pip install -e .
   ```
4. Create a `.env` file with your Monday.com credentials:
   ```
   MONDAY_API_KEY=your-monday-api-key
   MONDAY_BOARD_ID=your-default-board-id
   ```
5. Run the server:
   ```bash
   python -m mcp_monday_server
   ```

### Debugging

For debugging the MCP server, you can use the [MCP Inspector](https://github.com/modelcontextprotocol/inspector):

```bash
npx @modelcontextprotocol/inspector -- python -m mcp_monday_server
```

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

Copyright (c) 2025 sofias tech
