# Model Context Protocol (MCP) Documentation

## What is MCP?

**Model Context Protocol (MCP)** is an open standard protocol created by Anthropic that enables AI applications to securely connect to external data sources, tools, and services. It provides a universal interface for AI models like Claude to interact with your local and remote resources.

### Core Concept
MCP acts as a bridge between AI applications and the tools/data they need to access. Instead of each AI tool implementing custom integrations, MCP provides a standardized way to:
- Read and write files
- Query databases
- Call APIs
- Execute commands
- Access web services

## Architecture

```
┌─────────────┐          ┌─────────────┐          ┌──────────────┐
│   Claude    │ ◄─────── │ MCP Client  │ ◄─────── │  MCP Server  │
│    Code     │          │  (Claude)   │          │ (Filesystem) │
└─────────────┘          └─────────────┘          └──────────────┘
                                │
                                │
                         ┌──────▼───────┐
                         │  MCP Server  │
                         │  (Database)  │
                         └──────────────┘
```

### Components

1. **MCP Hosts** - Applications that want to use AI (e.g., Claude Code CLI, IDEs)
2. **MCP Clients** - Protocol clients that maintain connections to servers
3. **MCP Servers** - Lightweight programs exposing specific capabilities
4. **Local Data Sources** - Your files, databases, services

## Most Useful MCP Servers

### 1. Filesystem MCP ⭐
**Purpose:** Access local files and directories

**Use cases:**
- Reading configuration files
- Processing markdown documentation
- Analyzing codebases
- Generating static websites from markdown

**Example capabilities:**
- Read file contents
- List directory contents
- Search for files
- Watch for file changes

### 2. Git MCP
**Purpose:** Interact with Git repositories

**Use cases:**
- Check repository status
- View commit history
- Create commits
- Manage branches

**Why useful:** Essential for version controlling your documentation and website code.

### 3. GitHub MCP
**Purpose:** Interact with GitHub API

**Use cases:**
- Manage issues and PRs
- Access repository information
- GitHub Pages deployment
- Workflow automation

**Why useful:** Perfect if hosting your developer website on GitHub Pages.

### 4. SQLite MCP
**Purpose:** Query SQLite databases

**Use cases:**
- Content management
- Metadata storage for static sites
- Local data analysis
- Configuration storage

### 5. PostgreSQL MCP
**Purpose:** Query PostgreSQL databases

**Use cases:**
- Advanced content management
- Multi-user systems
- Complex data relationships

### 6. Web Search MCP
**Purpose:** Perform web searches

**Use cases:**
- Research while coding
- Fact-checking documentation
- Finding code examples
- Staying current with technologies

### 7. Brave Search MCP
**Purpose:** Privacy-focused web search

**Use cases:**
- Similar to Web Search but privacy-focused
- API-based search integration

### 8. Puppeteer MCP
**Purpose:** Browser automation

**Use cases:**
- Testing static website output
- Web scraping for content
- Screenshot generation
- Automated browser interactions

## How to Use MCPs with Claude Code

### Installation
MCP servers are typically installed via npm:

```bash
npm install -g @modelcontextprotocol/server-filesystem
npm install -g @modelcontextprotocol/server-github
npm install -g @modelcontextprotocol/server-sqlite
```

### Configuration
MCP servers are configured in Claude Code's settings file. Configuration specifies:
- Which servers to use
- Server-specific parameters (paths, credentials, etc.)
- Permission levels

### Example Use Cases for Your Goals

#### Static Website Generation
1. **Filesystem MCP** reads your markdown files
2. **Git MCP** manages version control
3. **GitHub MCP** deploys to GitHub Pages
4. **SQLite MCP** (optional) stores metadata like tags, categories, dates

#### Documentation Management
1. **Filesystem MCP** organizes documentation files
2. **Git MCP** tracks documentation changes
3. **Web Search MCP** researches topics while writing

## MCP vs Traditional Integrations

### Traditional Approach
- Each tool builds custom integrations
- Inconsistent interfaces
- Security concerns with broad access
- Difficult to maintain

### MCP Approach
- Standardized protocol
- Consistent security model
- Easy to add new capabilities
- Vendor-neutral

## Security Considerations

MCP servers operate with specific permissions:
- **Filesystem access** - Limited to configured directories
- **Database access** - Specific connection credentials
- **API access** - Uses your provided tokens/keys
- **Sandboxing** - Servers run in isolated contexts

Always review MCP server permissions before enabling them.

## Getting Started

1. **Identify your needs** - What data/tools do you want Claude to access?
2. **Choose relevant servers** - Start with filesystem and Git
3. **Install servers** - Use npm or other package managers
4. **Configure Claude Code** - Add servers to settings
5. **Test access** - Verify Claude can interact with your resources
6. **Expand gradually** - Add more servers as needed

## Resources

- **Official MCP Documentation:** https://modelcontextprotocol.io
- **MCP Specification:** https://spec.modelcontextprotocol.io
- **Claude Code MCP Guide:** Use `/help` in Claude Code CLI or ask Claude directly
- **Community Servers:** Explore the MCP ecosystem on GitHub

## For Your Static Website Project

### Recommended MCP Setup
1. **Filesystem MCP** - Read markdown files from `Q:\HomeLabDev\Documentation`
2. **Git MCP** - Version control for website repository
3. **GitHub MCP** - Deploy to GitHub Pages (if applicable)

### Workflow
1. Write documentation in markdown
2. Claude (via Filesystem MCP) reads and processes markdown
3. Python script converts markdown to HTML
4. Git MCP commits changes
5. GitHub MCP triggers deployment

## Next Steps

- [ ] Install Filesystem MCP server
- [ ] Configure MCP in Claude Code settings
- [ ] Test reading markdown files via MCP
- [ ] Plan Python static site generator with MCP integration
- [ ] Consider Git MCP for version control automation
