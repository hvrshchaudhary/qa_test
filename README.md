# QA Agent Testing

This directory contains tests for the GitHub MCP server integration and QA Agent functionality.

## Test Files Overview

- `test_github_connection.py` - Tests for GitHub MCP server connection and basic API operations
- `mcp_conn_test_plan.md` - Detailed test plan document for GitHub MCP server integration

## Setup Instructions

### 1. Configuration

Create a `test_config.yaml` file in this directory with your test repository details:

```yaml
github:
  owner: "your-github-username"  # or organization name
  repo: "your-test-repository"
  file_path: "README.md"  # A file known to exist in your test repo
```

Alternatively, you can set environment variables:
- `TEST_GITHUB_OWNER`
- `TEST_GITHUB_REPO`
- `TEST_GITHUB_FILE_PATH`

### 2. Dependencies

Make sure you have the required dependencies installed:

```bash
pip install pytest pytest-asyncio pyyaml
```

### 3. GitHub MCP Server

Ensure the GitHub MCP server is running in Docker with appropriate configuration:

```bash
# The server should be running with:
docker run -p 4010:4010 -e GITHUB_TOKEN=YOUR_PAT_TOKEN ghcr.io/github/github-mcp-server
```

### 4. Running Tests

To run all QA tests:

```bash
pytest tests/qa/
```

To run with detailed logging:

```bash
pytest tests/qa/ -v --log-cli-level=DEBUG
```

To run a specific test file:

```bash
pytest tests/qa/test_github_connection.py
```

## Test Repository Requirements

Your test repository should include:
- A README.md file (or whatever is specified in your config)
- Some sample code files that can be accessed during tests
- Permissions configured to allow the GitHub token to:
  - Read repository contents
  - Create/update issues (if testing those features) 
