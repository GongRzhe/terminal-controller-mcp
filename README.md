[![MseeP.ai Security Assessment Badge](https://mseep.net/pr/gongrzhe-terminal-controller-mcp-badge.png)](https://mseep.ai/app/gongrzhe-terminal-controller-mcp)

# Terminal Controller for MCP

A Model Context Protocol (MCP) server that enables secure terminal command execution, directory navigation, and file system operations through a standardized interface.

![](https://badge.mcpx.dev?type=server 'MCP Server')
[![smithery badge](https://smithery.ai/badge/@GongRzhe/terminal-controller-mcp)](https://smithery.ai/server/@GongRzhe/terminal-controller-mcp)

## Features

- **Command Execution**: Run terminal commands with timeout controls and comprehensive output capture
- **Directory Management**: Navigate and list directory contents with intuitive formatting
- **Security Measures**: Built-in safeguards against dangerous commands and operations
- **Command History**: Track and display recent command executions
- **Cross-Platform Support**: Works on both Windows and UNIX-based systems
- **File Operations**: Read, write, update, insert, and delete file content with row-level precision

## Installation

### Installing via Smithery

To install Terminal Controller for Claude Desktop automatically via [Smithery](https://smithery.ai/server/@GongRzhe/terminal-controller-mcp):

```bash
npx -y @smithery/cli install @GongRzhe/terminal-controller-mcp --client claude
```

### Prerequisites

- Python 3.11+
- An MCP-compatible client (such as Claude Desktop)
- UV/UVX installed (optional, for UVX method)

### Method 1: PyPI Installation (Recommended)

Install the package directly from PyPI:

```bash
pip install terminal-controller
```

Or if you prefer to use UV:

```bash
uv pip install terminal-controller
```

### Method 2: From Source

If you prefer to install from source:

1. Clone this repository:
   ```bash
   git clone https://github.com/GongRzhe/terminal-controller-mcp.git
   cd terminal-controller-mcp
   ```

2. Run the setup script:
   ```bash
   python setup_mcp.py
   ```

## Client Configuration

### Claude Desktop

There are two ways to configure Claude Desktop to use Terminal Controller:

#### Option 1: Using UVX (Recommended)

Add this to your Claude Desktop configuration file:

```json
"terminal-controller": {
  "command": "uvx",
  "args": ["terminal_controller"]
}
```

#### Option 2: Using Python Directly

```json
"terminal-controller": {
  "command": "python",
  "args": ["-m", "terminal_controller"]
}
```

The configuration path varies by operating system:
- **macOS**: `~/Library/Application Support/Claude/claude_desktop_config.json`
- **Windows**: `%APPDATA%\Claude\claude_desktop_config.json`

### Cursor

For Cursor, use similar configuration settings as Claude Desktop.

### Other MCP Clients

For other clients, refer to their documentation on how to configure external MCP servers.

## Usage

Once configured, you can use natural language to interact with your terminal through your MCP client:

- "Run the command `ls -la` in the current directory"
- "Navigate to my Documents folder"
- "Show me the contents of my Downloads directory"
- "Show me my recent command history"
- "Read the content of config.json"
- "Update line 5 in my script.py file with 'print(\"Hello World\")'"
- "Delete lines 10-15 from the log file"
- "Insert a new line at the beginning of my text file"

## API Reference

Terminal Controller exposes the following MCP tools:

### `execute_command`

Execute a terminal command and return its results.

**Parameters:**
- `command`: The command line command to execute
- `timeout`: Command timeout in seconds (default: 30)

**Returns:**
- Output of the command execution, including stdout, stderr, and execution status

### `get_command_history`

Get recent command execution history.

**Parameters:**
- `count`: Number of recent commands to return (default: 10)

**Returns:**
- Formatted command history record

### `get_current_directory`

Get the current working directory.

**Returns:**
- Path of current working directory

### `change_directory`

Change the current working directory.

**Parameters:**
- `path`: Directory path to switch to

**Returns:**
- Operation result information

### `list_directory`

List files and subdirectories in the specified directory.

**Parameters:**
- `path`: Directory path to list contents (default: current directory)

**Returns:**
- List of directory contents, formatted with icons for directories and files

### `write_file`

Write content to a file with overwrite or append options.

**Parameters:**
- `path`: Path to the file
- `content`: Content to write
- `mode`: Write mode ('overwrite' or 'append', default: 'overwrite')

**Returns:**
- Operation result information including verification of successful write

### `read_file`

Read content from a file with optional row selection.

**Parameters:**
- `path`: Path to the file
- `start_row`: Starting row to read from (0-based, optional)
- `end_row`: Ending row to read to (0-based, inclusive, optional)

**Returns:**
- File content or selected lines

### `insert_file_content`

Insert content at specific row(s) in a file.

**Parameters:**
- `path`: Path to the file
- `content`: Content to insert
- `row`: Row number to insert at (0-based, optional)
- `rows`: List of row numbers to insert at (0-based, optional)

**Returns:**
- Operation result information

### `delete_file_content`

Delete content at specific row(s) from a file.

**Parameters:**
- `path`: Path to the file
- `row`: Row number to delete (0-based, optional)
- `rows`: List of row numbers to delete (0-based, optional)

**Returns:**
- Operation result information

### `update_file_content`

Update content at specific row(s) in a file.

**Parameters:**
- `path`: Path to the file
- `content`: New content to place at the specified row(s)
- `row`: Row number to update (0-based, optional)
- `rows`: List of row numbers to update (0-based, optional)

**Returns:**
- Operation result information

## Security Considerations

Terminal Controller implements several security measures:

- Timeout controls to prevent long-running commands
- Blacklisting of dangerous commands (rm -rf /, format, mkfs)
- Proper error handling and isolation of command execution
- Access only to the commands and directories specifically granted

## Limitations

- Only commands that complete within the timeout period will return results
- By default, the server has access to the same file system permissions as the user running it
- Some interactive commands may not work as expected due to the non-interactive nature of the terminal interface

## Troubleshooting

If you encounter issues:

1. Check that your Python version is 3.11 or higher
2. Verify that your Claude Desktop configuration is correct
3. Try running the terminal controller directly to check for errors:
   ```bash
   python -m terminal_controller
   ```
4. For UVX-related issues, try:
   ```bash
   uvx terminal_controller
   ```
5. Review your MCP client's logs for connection errors

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

MIT
