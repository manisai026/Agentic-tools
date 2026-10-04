# Agentic Tools MCP Server

[![npm version](https://badge.fury.io/js/@pimzino%2Fagentic-tools-mcp.svg)](https://badge.fury.io/js/@pimzino/agentic-tools-mcp)
[![npm downloads](https://img.shields.io/npm/dm/@pimzino/agentic-tools-mcp.svg)](https://www.npmjs.com/package/@pimzino/agentic-tools-mcp)
[![GitHub stars](https://img.shields.io/github/stars/manisai026/Agentic-tools.svg)](https://github.com/manisai026/Agentic-tools/stargazers)
[![GitHub license](https://img.shields.io/github/license/manisai026/Agentic-tools.svg)](https://github.com/manisai026/Agentic-tools/blob/main/LICENSE)
[![Node.js Version](https://img.shields.io/node/v/@pimzino/agentic-tools-mcp.svg)](https://nodejs.org/)

A comprehensive Model Context Protocol (MCP) server providing AI assistants with powerful **advanced task management** and **agent memories** capabilities with **project-specific storage**.

## 🔗 Ecosystem

This MCP server is part of a complete task and memory management ecosystem:

- **🖥️ [VS Code Extension](https://github.com/manisai026/Agentic-tools)** - GUI interface for managing tasks and memories directly in VS Code
- **⚡ MCP Server** (this repository) - Advanced AI agent tools and API for intelligent task management

> **💡 Pro Tip**: Use both together for the ultimate productivity experience! The VS Code extension provides a visual interface while the MCP server enables AI assistant integration with advanced features like PRD parsing, task recommendations, and research capabilities.

## Features

### 🎯 Advanced Task Management System with Unlimited Hierarchy (v1.8.0)

- **Projects**: Organize work into distinct projects with descriptions
- **Unified Task Model**: Single task interface supporting unlimited nesting depth
- **Unlimited Hierarchy**: Tasks → Subtasks → Sub-subtasks → infinite depth nesting
- **Rich Features at All Levels**: Every task gets priority, complexity, dependencies, tags, and time tracking
- **Parent-Child Relationships**: Flexible hierarchy organization with `parentId` field
- **Level Tracking**: Automatic hierarchy level calculation and visual indicators
- **Tree Visualization**: Comprehensive hierarchical tree display with unlimited depth
- **Intelligent Dependencies**: Task dependency management with validation across hierarchy
- **Priority & Complexity**: 1-10 scale prioritization and complexity estimation at every level
- **Enhanced Status Tracking**: pending, in-progress, blocked, done status workflow
- **Tag-Based Organization**: Flexible categorization and filtering
- **Time Tracking**: Estimated and actual hours for project planning
- **Automatic Migration**: Seamless upgrade from old 3-level to unlimited depth model
- **Progress Tracking**: Monitor completion status at all hierarchy levels
- **Project-Specific Storage**: Each working directory has isolated task data
- **Git-Trackable**: Task data can be committed alongside your code

### 🧠 Agent Memories System

- **Persistent Memory**: Store and retrieve agent memories with titles and detailed content
- **Intelligent Search**: Multi-field text search with relevance scoring across titles, content, and categories
- **Smart Ranking**: Advanced scoring algorithm prioritizes title matches (60%), content matches (30%), and category bonuses (20%)
- **Rich Metadata**: Flexible metadata system for enhanced context
- **JSON Storage**: Individual JSON files organized by category, named after memory titles
- **Project-Specific**: Isolated memory storage per working directory

### 🔧 MCP Tools Available

#### Project Management

- `list_projects` - View all projects in a working directory
- `create_project` - Create a new project in a working directory
- `get_project` - Get detailed project information
- `update_project` - Edit project name/description
- `delete_project` - Delete project and all associated data

#### Task Management (Unlimited Hierarchy v1.8.0)

- `list_tasks` - View tasks in hierarchical tree format with unlimited depth visualization
- `create_task` - Create tasks at any hierarchy level with `parentId` (supports unlimited nesting)
- `get_task` - Get detailed task information including hierarchy relationships
- `update_task` - Edit tasks, metadata, or move between hierarchy levels with `parentId`
- `delete_task` - Delete task and all child tasks recursively
- `move_task` - Dedicated tool for moving tasks within hierarchy structure
- `migrate_subtasks` - Automatic migration tool for converting legacy subtasks to unified model

#### Advanced Task Management (AI Agent Tools)

- `parse_prd` - Parse Product Requirements Documents and automatically generate structured tasks
- `get_next_task_recommendation` - Get intelligent task recommendations based on dependencies, priorities, and complexity
- `analyze_task_complexity` - Analyze task complexity and suggest breaking down overly complex tasks
- `infer_task_progress` - Analyze codebase to infer task completion status from implementation evidence
- `research_task` - Guide AI agents to perform comprehensive web research with memory integration
- `generate_research_queries` - Generate intelligent, targeted web search queries for task research

#### Legacy Subtask Management (Backward Compatibility)

- `list_subtasks` - View child tasks (legacy compatibility, now uses unified Task model)
- `create_subtask` - Create child tasks (legacy compatibility, creates tasks with `parentId`)
- `get_subtask` - Get task information (legacy compatibility for existing subtasks)
- `update_subtask` - Edit child tasks (legacy compatibility, uses unified Task operations)
- `delete_subtask` - Delete child tasks (legacy compatibility, deletes tasks recursively)

#### Agent Memory Management

- `create_memory` - Store new memories with title and detailed content
- `search_memories` - Find memories using intelligent multi-field search with relevance scoring
- `get_memory` - Get detailed memory information
- `list_memories` - List memories with optional filtering
- `update_memory` - Edit memory title, content, metadata, or categorization
- `delete_memory` - Delete a memory (requires confirmation)

**Important**: All tools require a `workingDirectory` parameter to specify where the data should be stored. This enables project-specific task and memory management.

## Installation

### Quick Start

```bash
npx -y @pimzino/agentic-tools-mcp
```

### Global Installation

```bash
npm install -g @pimzino/agentic-tools-mcp
```

## Usage

### Storage Modes

The MCP server supports two storage modes:

#### 📁 Project-Specific Mode (Default)

Data is stored in `.agentic-tools-mcp/` subdirectories within each project's working directory.

```bash
npx -y @pimzino/agentic-tools-mcp
```

#### 🌐 Global Directory Mode

Use the `--claude` flag to store all data in a standardized global directory:

- **Windows**: `C:\Users\{username}\.agentic-tools-mcp\`
- **macOS/Linux**: `~/.agentic-tools-mcp/`

```bash
npx -y @pimzino/agentic-tools-mcp --claude
```

**When to use `--claude` flag:**

- With Claude Desktop client (non-project-specific usage)
- When you want a single global workspace for all tasks and memories
- For AI assistants that work across multiple projects

**Note**: When using `--claude` flag, the `workingDirectory` parameter in all tools is ignored and the global directory is used instead.

### With Claude Desktop

#### Project-Specific Mode (Default)

```json
{
  "mcpServers": {
    "agentic-tools": {
      "command": "npx",
      "args": ["-y", "@pimzino/agentic-tools-mcp"]
    }
  }
}
```

#### Global Directory Mode

```json
{
  "mcpServers": {
    "agentic-tools": {
      "command": "npx",
      "args": ["-y", "@pimzino/agentic-tools-mcp", "--claude"]
    }
  }
}
```

**Note**: The server now includes both task management and agent memories features.

### With AugmentCode

#### Project-Specific Mode (Default)

1. Open Augment Settings Panel (gear icon)
2. Add MCP server:
   - **Name**: `agentic-tools`
   - **Command**: `npx -y @pimzino/agentic-tools-mcp`
3. Restart VS Code

#### Global Directory Mode

1. Open Augment Settings Panel (gear icon)
2. Add MCP server:
   - **Name**: `agentic-tools`
   - **Command**: `npx -y @pimzino/agentic-tools-mcp --claude`
3. Restart VS Code

**Features Available**: Task management, agent memories, and text-based search capabilities.

### With VS Code Extension

For the best user experience, use the [Agentic Tools MCP Companion](https://github.com/manisai026/Agentic-tools) VS Code extension.

1. Clone the repository
2. Open it in VS Code and press `F5` to run in development mode
3. Use the GUI interface for task and memory management

**Benefits of using both together:**

- 🎯 **Visual Task Management**: Rich forms with priority, complexity, status, tags, and time tracking
- 🎨 **Enhanced UI**: Status emojis, priority badges, and visual indicators
- 🔄 **Real-time Sync**: Changes in VS Code instantly available to AI assistants
- 📁 **Project Integration**: Seamlessly integrated with your workspace
- 🤖 **AI Collaboration**: Human planning with AI execution for optimal productivity

### With Other MCP Clients

The server uses STDIO transport and can be integrated with any MCP-compatible client.

#### Project-Specific Mode

```bash
npx -y @pimzino/agentic-tools-mcp
```

#### Global Directory Mode

```bash
npx -y @pimzino/agentic-tools-mcp --claude
```

## Data Models

### Project

```typescript
{
  id: string;
  name: string;
  description: string;
  createdAt: string;
  updatedAt: string;
}
```

### Task (Unified Model v1.8.0 - Unlimited Hierarchy)

```typescript
{
  id: string;
  name: string;
  details: string;
  projectId: string;
  completed: boolean;
  createdAt: string;
  updatedAt: string;

  // Unlimited hierarchy fields
  parentId?: string;
  level?: number;

  // Enhanced metadata fields
  dependsOn?: string[];
  priority?: number;
  complexity?: number;
  status?: string;
  tags?: string[];
  estimatedHours?: number;
  actualHours?: number;
}
```

### Legacy Subtask

The separate Subtask interface has been replaced by the unified Task model. Legacy subtasks are automatically migrated to tasks with the `parentId` field. This ensures unlimited hierarchy depth while maintaining rich features at every level.

### Memory

```typescript
{
  id: string;
  title: string;
  content: string;
  metadata: Record<string, any>;
  createdAt: string;
  updatedAt: string;
  category?: string;
}
```

## Example Workflow

### 1. Create a Project

```text
Use create_project with:
- workingDirectory="/path/to/your/project"
- name="Website Redesign"
- description="Complete overhaul of company website"
```

### 2. Add Enhanced Tasks

```text
Use create_task with:
- workingDirectory="/path/to/your/project"
- name="Design mockups"
- details="Create wireframes and high-fidelity designs"
- projectId="[project-id-from-step-1]"
- priority=8
- complexity=6
- status="pending"
- tags=["design", "ui", "mockups"]
- estimatedHours=16
```

### 3. Break Down Tasks

```text
Use create_subtask with:
- workingDirectory="/path/to/your/project"
- name="Create wireframes"
- details="Sketch basic layout structure"
- taskId="[task-id-from-step-2]"
```

### 4. Track Progress

```text
Use update_task and update_subtask to mark items as completed.

Use list_projects, list_tasks, and list_subtasks to view progress.

All tools require the workingDirectory parameter.
```

### Agent Memories Workflow

#### 1. Create a Memory

```text
Use create_memory with:
- workingDirectory="/path/to/your/project"
- title="User prefers concise technical responses"
- content="The user has explicitly stated they prefer concise responses with technical explanations. They value brevity but want detailed technical information when relevant."
- metadata={"source": "conversation", "confidence": 0.9}
- category="user_preferences"
```

#### 2. Search Memories

```text
Use search_memories with:
- workingDirectory="/path/to/your/project"
- query="user preferences responses"
- limit=5
- threshold=0.3
- category="user_preferences"
```

#### 3. List and Manage

```text
Use list_memories to view all memories.
Use update_memory to modify existing memories.
Use delete_memory to remove outdated memories.

All tools require the workingDirectory parameter.
```

📖 **Quick Start**: See `docs/QUICK_START_MEMORIES.md` for a step-by-step guide to agent memories.

## Data Storage

- **Project-specific**: Each working directory has its own isolated task and memory data
- **File-based**: Task data stored in `.agentic-tools-mcp/tasks/`, memory data in `.agentic-tools-mcp/memories/`
- **Git-trackable**: All data can be committed alongside your project code
- **Persistent**: All data persists between server restarts
- **Atomic**: All operations are atomic to prevent data corruption
- **JSON Storage**: Simple file-based storage for efficient memory organization
- **Backup-friendly**: Simple file-based storage for easy backup and migration

### Storage Structure

```text
your-project/
├── .agentic-tools-mcp/
│   ├── tasks/
│   │   └── tasks.json
│   └── memories/
│       ├── preferences/
│       │   └── User_prefers_concise_technical_responses.json
│       ├── technical/
│       │   └── React_TypeScript_project_with_strict_ESLint.json
│       └── context/
│           └── User_works_in_healthcare_needs_HIPAA_compliance.json
├── src/
├── package.json
└── README.md
```

### Working Directory Parameter

All MCP tools require a `workingDirectory` parameter that specifies:

- Where to store the `.agentic-tools-mcp/` folder in project-specific mode
- Which project's task and memory data to access
- How multiple projects can have separate task lists and memory stores

**Note**: When the server is started with the `--claude` flag, the `workingDirectory` parameter is ignored and a global user directory is used instead.

### Benefits of Project-Specific Storage

- **Git Integration**: Task and memory data can be committed with your code
- **Team Collaboration**: Share task lists and agent memories via version control
- **Project Isolation**: Each project has its own task management and memory system
- **Multi-Project Workflow**: Work on multiple projects simultaneously with isolated memories
- **Backup & Migration**: File-based storage travels with your code
- **Text Search**: Simple content-based memory search for intelligent context retrieval
- **Agent Continuity**: Persistent agent memories across sessions and deployments

## Error Handling

- **Validation**: All inputs are validated with comprehensive error messages
- **Directory Validation**: Ensures working directory exists and is accessible
- **Referential Integrity**: Prevents orphaned tasks/subtasks with cascade deletes
- **Unique Names**: Enforces unique names within scope
- **Confirmation**: Destructive operations require explicit confirmation
- **Graceful Degradation**: Detailed error messages for troubleshooting
- **Storage Errors**: Clear messages when storage initialization fails

## Development

### Building from Source

```bash
git clone https://github.com/manisai026/Agentic-tools.git
cd Agentic-tools
npm install
npm run build
npm start
```

### Project Structure

```text
src/
├── features/
│   ├── task-management/
│   │   ├── tools/
│   │   │   ├── projects/
│   │   │   ├── tasks/
│   │   │   └── subtasks/
│   │   ├── models/
│   │   └── storage/
│   └── agent-memories/
│       ├── tools/
│       │   └── memories/
│       ├── models/
│       └── storage/
├── server.ts
└── index.ts
```

## Troubleshooting

### Common Issues

**"Working directory does not exist"**

- Ensure the path exists and is accessible
- Use absolute paths for reliability
- Check directory permissions

**"Text search returns no results"**

- Try using different keywords or phrases
- Check that memories contain the search terms
- Verify that the query content matches memory content

**"Memory files not found"**

- Ensure the working directory exists and is writable
- Check that the `.agentic-tools-mcp/memories` directory was created

## Version History

See `CHANGELOG.md` for detailed version history and release notes.

### Current Version: 1.8.0

- 🚀 **NEW: Unified Task Model**: Single task interface supporting unlimited nesting depth
- 🚀 **NEW: Unlimited Hierarchy**: Tasks → Subtasks → Sub-subtasks → infinite depth nesting
- 🚀 **NEW: Automatic Migration**: Seamless upgrade from 3-level to unlimited depth model
- 🚀 **NEW: Enhanced Tree Display**: Hierarchical visualization with level indicators and unlimited depth
- 🚀 **NEW: Hierarchy Tools**: `move_task`, `migrate_subtasks` for unlimited depth management
- ✅ **Rich Features at All Levels**: Every task gets priority, complexity, dependencies, tags, and time tracking
- ✅ **Enhanced Task Management**: Rich metadata with dependencies, priority, complexity, status, tags, and time tracking
- ✅ **Advanced AI Agent Tools**: PRD parsing, task recommendations, complexity analysis, progress inference, and research guidance
- ✅ **Intelligent Task Dependencies**: Dependency validation and workflow management across hierarchy
- ✅ **Priority & Complexity System**: 1-10 scale prioritization and complexity estimation at every level
- ✅ **Enhanced Status Workflow**: pending → in-progress → blocked → done status tracking
- ✅ **Tag-Based Organization**: Flexible categorization and filtering system
- ✅ **Time Tracking**: Estimated and actual hours for project planning
- ✅ **Hybrid Research Integration**: Web research with memory caching for AI agents
- ✅ **Complete task management system** with unlimited hierarchical organization
- ✅ **Agent memories** with title/content architecture and JSON file storage
- ✅ **Intelligent multi-field search** with relevance scoring
- ✅ **Project-specific storage** with comprehensive MCP tools
- ✅ **Global directory mode** with `--claude` flag for Claude Desktop
- ✅ **VS Code extension ecosystem** integration

## Acknowledgments

We're grateful to the open-source community and the following projects that make this MCP server possible:

### Core Technologies

- **[@modelcontextprotocol/sdk](https://github.com/modelcontextprotocol/typescript-sdk)** - The foundation for MCP server implementation
- **[Node.js File System](https://nodejs.org/api/fs.html)** - Reliable file-based storage for memory persistence
- **[TypeScript](https://www.typescriptlang.org/)** - Type-safe JavaScript development
- **[Node.js](https://nodejs.org/)** - JavaScript runtime environment

### Development & Validation

- **[Zod](https://zod.dev/)** - TypeScript-first schema validation for robust input handling
- **[ESLint](https://eslint.org/)** - Code quality and consistency
- **[Prettier](https://prettier.io/)** - Code formatting

### File Storage & Search

- **JSON** - Simple, human-readable data format for memory storage
- **Text Search** - Efficient content-based search across memory files

### Special Thanks

- **Open Source Community** - For creating the tools and libraries that make this MCP server possible

## License

MIT License - see LICENSE file for details.

## Contributing

Contributions are welcome! Please feel free to submit issues and pull requests.

### Development Setup

```bash
git clone https://github.com/manisai026/Agentic-tools.git
cd Agentic-tools
npm install
npm run build
npm start
```

## Related Projects

### 🖥️ VS Code Extension

**[Agentic Tools MCP Companion](https://github.com/manisai026/Agentic-tools)** - A VS Code interface for this MCP server.

**Key Features:**

- 🎯 **Visual Task Management**: Rich GUI with enhanced task metadata forms
- 📝 **Enhanced Forms**: Priority, complexity, status, tags, and time tracking
- 🎨 **Visual Indicators**: Status emojis, priority badges, and complexity indicators
- 📊 **Rich Tooltips**: Complete task information on hover
- 🔄 **Real-time Sync**: Instant synchronization with MCP server data
- 📱 **Responsive Design**: Adaptive forms that work on different screen sizes

**Perfect for:**

- Visual task management and planning
- Teams who prefer GUI interfaces
- Project managers who need rich task metadata
- Anyone who wants beautiful task organization in VS Code

## Support

For issues and questions, please use the GitHub issue tracker.

### Documentation

- 📖 **[API Reference](docs/API_REFERENCE.md)** - Complete tool documentation
- 🧠 **[Agent Memories Guide](docs/AGENT_MEMORIES.md)** - Comprehensive memory system guide
- 🚀 **[Quick Start: Memories](docs/QUICK_START_MEMORIES.md)** - Get started with agent memories
- 📋 **[Changelog](CHANGELOG.md)** - Version history and release notes

### Getting Help

- 🐛 Report bugs via GitHub issues
- 💡 Request features via GitHub discussions
- 🖥️ **VS Code Extension Issues**: Report extension-specific issues through the repository's GitHub issues
