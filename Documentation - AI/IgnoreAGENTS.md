# AI Agents & Assistants Documentation

## Overview
This document describes how AI agents are used in this project, including best practices, guidelines, and tool-specific information.

## Current AI Tools in Use

### Claude Code (Primary)
**Official Anthropic VS Code Extension**

**Features:**
- Deep codebase understanding through Claude Sonnet 4.5
- Direct file editing and creation
- Terminal command execution
- Multi-file refactoring
- MCP (Model Context Protocol) integration

**Does NOT use:**
- `.clinerules` files
- `AGENTS.md` for automatic instructions
- `.cursorrules` files

**Configuration:**
- Settings managed through VS Code settings JSON
- MCP servers configured in Claude Code settings
- Context comes from conversation and open files

**Best practices:**
- Keep related files open for context
- Be specific about file paths
- Use markdown documentation for reference
- Leverage MCP servers for enhanced capabilities

### Model Context Protocol (MCP) Integration
See [MCP.md](MCP.md) for detailed documentation.

**Enabled MCP Servers:**
- [ ] Filesystem MCP
- [ ] Git MCP
- [ ] GitHub MCP
- [ ] Web Search MCP

## Agent Workflows

### Documentation Workflow
1. Write documentation in markdown
2. Store in `Q:\HomeLabDev\Documentation\`
3. Use Claude Code to help organize and structure
4. Version control with Git
5. Convert to static site (Python script)

### Development Workflow
1. Plan features with Claude Code
2. Implement with Claude's assistance
3. Review and refine code
4. Commit changes
5. Deploy/test

### Learning Workflow
1. Research topics with Claude
2. Document findings in markdown
3. Ask clarifying questions
4. Build examples/demos
5. Create reference documentation

## Project-Specific Guidelines

### File Organization
```
Q:\HomeLabDev\
├── AiBin\              # AI-related scripts and tools
│   └── TodaysTasks.md  # Daily task tracking
├── Documentation\       # All markdown documentation
│   ├── MCP.md          # MCP documentation
│   ├── AGENTS.md       # This file
│   └── [topic].md      # Topic-specific docs
└── [Other projects]
```

### Documentation Standards
- Use markdown for all documentation
- Include code examples where relevant
- Link between related documents
- Keep documentation up-to-date
- Use clear headings and structure

### When to Use AI Assistance
**Good use cases:**
- Code refactoring and optimization
- Documentation writing and organization
- Learning new technologies
- Debugging complex issues
- Planning project architecture
- Converting between formats (e.g., markdown to HTML)

**Less ideal use cases:**
- Simple syntax fixes (use IDE features)
- Bulk file operations (use scripts)
- Repetitive tasks (automate with scripts)

## AI Agent Comparison

### Claude Code vs Other Tools

| Feature | Claude Code | Cline | Cursor | GitHub Copilot |
|---------|-------------|-------|--------|----------------|
| File rules | No | Yes (.clinerules) | Yes (.cursorrules) | No |
| MCP Support | Yes | Limited | No | No |
| Multi-file edits | Yes | Yes | Yes | Limited |
| Terminal access | Yes | Yes | Yes | No |
| Code generation | Yes | Yes | Yes | Yes |
| Chat interface | Yes | Yes | Yes | Chat separately |

## Future Considerations

### Potential Enhancements
- [ ] Custom MCP servers for project-specific needs
- [ ] Automated documentation generation
- [ ] CI/CD integration with AI assistance
- [ ] Custom skills/commands for Claude Code
- [ ] Integration with issue tracking

### Feature Requests
If Claude Code adds configuration file support:
- Create `.claudecode` or similar
- Define project-specific context
- Set coding standards
- Configure preferred patterns

## Common Patterns & Prompts

### Effective Prompts
**Documentation:**
```
"Create comprehensive documentation for [topic] in Q:\HomeLabDev\Documentation\[topic].md
Include: overview, examples, best practices, and resources."
```

**Code Development:**
```
"Help me implement [feature] following these requirements:
1. [Requirement 1]
2. [Requirement 2]
Let's plan the approach first."
```

**Learning:**
```
"I want to learn about [topic]. Please:
1. Explain the core concepts
2. Show practical examples
3. Document in markdown format
4. Suggest next steps"
```

### Code Review Prompts
```
"Review this code for:
- Security vulnerabilities
- Performance issues
- Best practices
- Code clarity"
```

### Refactoring Prompts
```
"Refactor this code to:
- Improve readability
- Follow [language] best practices
- Add error handling
- Include documentation"
```

## MCP Integration Examples

### Filesystem MCP Usage
```python
# Claude can read markdown files
"Read all markdown files in Documentation folder and create an index"

# Claude can process files for static site generation
"Convert all markdown files to HTML using Python"
```

### Git MCP Usage
```bash
# Claude can help with version control
"Check git status and suggest what to commit"
"Create a commit for the documentation updates"
```

## Security & Privacy

### Best Practices
- Don't commit API keys or secrets
- Review AI-generated code before running
- Understand changes before accepting
- Keep sensitive data in `.gitignore`
- Use environment variables for config

### Data Handling
- Claude Code processes data locally where possible
- MCP servers operate with limited permissions
- Review MCP server configurations
- Understand what data is sent to AI services

## Troubleshooting

### Common Issues

**Claude doesn't understand context:**
- Open relevant files in editor
- Provide more specific instructions
- Reference file paths explicitly

**Changes not applied correctly:**
- Review proposed changes before accepting
- Check file paths are correct
- Ensure files aren't read-only

**MCP servers not working:**
- Check configuration in settings
- Verify server installation
- Review server permissions
- Check logs for errors

## Resources

### Documentation
- [MCP Documentation](MCP.md)
- [Claude Code Official Docs](https://claude.com/claude-code)
- [Model Context Protocol](https://modelcontextprotocol.io)

### Learning Resources
- Anthropic API documentation
- Claude Code examples
- MCP server repository
- Community forums

## Changelog

### 2025-12-26
- Initial AGENTS.md creation
- Added Claude Code guidelines
- Documented MCP integration
- Created workflow templates

---

**Note:** This file is for documentation and team reference. Claude Code does not automatically read this file. Include relevant context in conversations or configure MCP servers for extended capabilities.
