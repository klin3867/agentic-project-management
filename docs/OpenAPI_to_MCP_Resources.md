# OpenAPI to MCP Conversion Resources

## Overview

Model Context Protocol (MCP) is a standardized protocol that enables AI agents and Large Language Models (LLMs) to communicate with external APIs and tools. Converting existing OpenAPI specifications to MCP servers allows AI assistants like Claude, ChatGPT, and others to seamlessly interact with your APIs.

This guide provides a comprehensive list of repositories and tools for converting OpenAPI specifications into MCP-compatible servers.

## What is MCP?

**Model Context Protocol (MCP)** is a protocol that allows LLMs and AI agents to:
- Discover available tools and operations
- Invoke API operations with proper parameters
- Handle authentication and authorization
- Process responses and errors in a standardized way
- Render resources and widgets using JSON Schema contracts

MCP uses standardized transport layers (stdio, HTTP, SSE) to facilitate robust communication between AI agents and external services.

## Why Convert OpenAPI to MCP?

- **Rapid Integration**: Automatically expose your existing APIs to AI agents without writing custom wrappers
- **Standardization**: Use a consistent protocol across different AI platforms
- **Reduced Development Time**: Generate production-ready code instantly
- **Better Agent Experience**: Provide structured, well-documented tools that AI agents can easily understand and use
- **Enhanced APM Workflows**: When integrated with APM, MCP tools enable agents to interact with external systems, databases, and APIs during task execution

## Available Tools and Repositories

### 1. JavaScript/TypeScript: `openapi-mcp-generator`

**Repository**: [github.com/harsha-iiiv/openapi-mcp-generator](https://github.com/harsha-iiiv/openapi-mcp-generator)

A powerful CLI tool for generating MCP servers from OpenAPI 3.0+ specifications.

**Features**:
- CLI tool for quick conversion
- Supports stdio, Streaming HTTP, and SSE transports
- Authentication support: API keys, Bearer tokens, Basic Auth, OAuth2
- Runtime schema validation with Zod
- Configurable via environment variables

**Installation**:
```bash
npm install -g openapi-mcp-generator
```

**Usage**:
```bash
# Generate with stdio transport
openapi-mcp-generator --input path/to/openapi.json --output path/to/output/dir

# Generate with HTTP transport
openapi-mcp-generator --input path/to/openapi.json --output path/to/output/dir --transport=web --port=3000

# Generate with SSE transport
openapi-mcp-generator --input path/to/openapi.json --output path/to/output/dir --transport=sse
```

**Best For**: Node.js/TypeScript projects, developers familiar with npm ecosystem

---

### 2. Python: `openapi-to-mcp`

**Repository/Package**: [pypi.org/project/openapi-to-mcp](https://pypi.org/project/openapi-to-mcp/)

A Python library that integrates seamlessly with frameworks like FastAPI.

**Features**:
- Dynamic OpenAPI spec configuration
- Endpoint filtering capabilities
- Authentication header forwarding
- SSRF protection
- Easy integration with FastAPI and other Python frameworks

**Installation**:
```bash
pip install openapi-to-mcp
```

**FastAPI Example**:
```python
from fastapi import FastAPI
from openapi_to_mcp.fastapi import add_mcp_route

app = FastAPI()

# Add MCP route with OpenAPI spec
add_mcp_route(
    app, 
    openapi_url="https://petstore.swagger.io/v2/swagger.json",
    allowed_domains=["petstore.swagger.io"]
)
```

**Best For**: Python projects, FastAPI applications, projects requiring custom integration logic

---

### 3. Go: `openapi-mcp`

**Repository**: [github.com/jedisct1/openapi-mcp](https://github.com/jedisct1/openapi-mcp)  
**Homepage**: [jedisct1.github.io/openapi-mcp](https://jedisct1.github.io/openapi-mcp/)

A comprehensive Go tool for instant MCP conversion with advanced features.

**Features**:
- Validation and linting of OpenAPI specs
- Endpoint filtering
- Interactive client for testing
- Safety features and security controls
- Comprehensive authentication support (API keys, OAuth2, Basic Auth)
- AI-optimized structured responses
- Supports stdio and HTTP transports

**Installation**:
```bash
go install github.com/jedisct1/openapi-mcp@latest
```

**Usage**:
```bash
# Convert OpenAPI spec to MCP
openapi-mcp convert --input api-spec.yaml --output mcp-server

# Run MCP server
openapi-mcp serve --spec api-spec.yaml --port 8080
```

**Best For**: Go projects, performance-critical applications, projects requiring robust validation

---

### 4. Universal Web-Based Converter: `convertmcp.com`

**Website**: [convertmcp.com](https://convertmcp.com/)

A free, open-source, client-side web tool for converting OpenAPI to MCP in multiple languages.

**Features**:
- **No installation required** - works entirely in your browser
- **Supports 10+ languages**: Python, TypeScript, Go, Rust, Java, Kotlin, C#, PHP, Ruby, Swift
- Client-side processing (no server uploads, complete privacy)
- Choose specific endpoints and SDK options
- Instant download of production-ready code
- Visual interface for easy configuration

**Usage**:
1. Visit [convertmcp.com](https://convertmcp.com/)
2. Upload your OpenAPI specification file
3. Select target language and endpoints
4. Configure authentication and transport options
5. Download generated MCP server code

**Best For**: Quick conversions, evaluating multiple language options, privacy-sensitive projects

---

### 5. Official Integration Examples: `OpenAPI-MCP`

**Repository**: [github.com/gujord/OpenAPI-MCP](https://github.com/gujord/OpenAPI-MCP)

Official examples and reference implementation for OpenAPI to MCP conversion.

**Features**:
- Built with FastMCP framework
- Supports stdio, SSE, and HTTP transports
- Prompt generation for AI agents
- Resource registration
- Robust error handling
- Well-documented reference implementation

**Best For**: Learning MCP protocol details, understanding best practices, reference implementation

---

## Integration with APM

When using APM (Agentic Project Management), MCP tools can significantly enhance agent capabilities. Here's how to integrate OpenAPI-based MCP tools:

### 1. Generate Your MCP Server

Use one of the tools above to convert your API's OpenAPI spec to an MCP server:

```bash
# Example with openapi-mcp-generator
openapi-mcp-generator --input ./my-api-spec.yaml --output ./my-mcp-server
```

### 2. Configure in Claude Desktop (or other MCP-compatible IDE)

Add the generated server to your MCP configuration file:

**For Claude Desktop** (`~/Library/Application Support/Claude/claude_desktop_config.json` on macOS):

```json
{
  "mcpServers": {
    "my-api": {
      "command": "node",
      "args": ["path/to/my-mcp-server/index.js"],
      "env": {
        "API_KEY": "your-api-key",
        "BASE_URL": "https://api.example.com"
      }
    }
  }
}
```

### 3. Reference in APM Agent Guides

Update your APM agent guides to reference available MCP tools. For example, in `.apm/guides/Implementation_Agent_Guide.md`:

```markdown
### Available MCP Tools

**My API MCP Server**:
- Operations: `getUser`, `createUser`, `updateUser`, `deleteUser`
- Authentication: Configured via environment variable
- Use this tool to interact with our user management system
```

### 4. Use in Agent Workflows

APM agents can now leverage your MCP-enabled API during task execution:

```markdown
**Implementation Agent**: I'll use the My API MCP server to create a new user account:
- Tool: `my-api.createUser`
- Parameters: { "name": "John Doe", "email": "john@example.com" }
```

## Choosing the Right Tool

| Scenario | Recommended Tool |
|----------|------------------|
| Node.js/TypeScript project | `openapi-mcp-generator` |
| Python/FastAPI project | `openapi-to-mcp` |
| Go project or need high performance | `openapi-mcp` |
| Quick evaluation or multiple language support | `convertmcp.com` |
| Learning MCP protocol | `OpenAPI-MCP` |
| Privacy-sensitive specs | `convertmcp.com` (client-side only) |

## Best Practices

1. **Validate Your OpenAPI Spec**: Ensure your OpenAPI specification is valid before conversion
2. **Security First**: 
   - Never commit API keys or secrets to your repository
   - Use environment variables for sensitive configuration
   - Enable SSRF protection when exposing APIs to AI agents
3. **Document Available Operations**: Provide clear descriptions in your OpenAPI spec to help AI agents understand what each operation does
4. **Test Before Production**: Use interactive clients to test generated MCP servers before deploying
5. **Version Control**: Keep your OpenAPI specs in version control and regenerate MCP servers when specs change
6. **Monitor Usage**: Implement logging and monitoring for MCP server calls to track AI agent API usage
7. **Set Rate Limits**: Configure appropriate rate limits to prevent excessive API usage by AI agents

## Additional Resources

- **MCP Protocol Documentation**: [modelcontextprotocol.io](https://modelcontextprotocol.io/)
- **OpenAPI Specification**: [swagger.io/specification](https://swagger.io/specification/)
- **APM MCP Integration Guide**: See [Modifying_APM.md](Modifying_APM.md#mcp-tool-integration)

## Contributing

If you know of additional OpenAPI to MCP conversion tools or have experience with the tools listed here, contributions to this documentation are welcome. Please see [CONTRIBUTING.md](../CONTRIBUTING.md) for details on how to contribute.

---

**Note**: This resource guide is part of the APM documentation but focuses on external tools and repositories. The information about specific repositories and tools was current as of the last update but may change as these projects evolve.
