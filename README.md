# Cloud Architect MCP Server

A Model Context Protocol (MCP) server that provides cloud architecture design assistance through an iterative questioning process. This tool helps determine optimal Azure architectures by gathering requirements, constraints, and goals systematically.

## Project Structure

```
├── cloud_arch.ts          # Main TypeScript source file
├── dist/
│   └── cloud_arch.js      # Compiled JavaScript output
├── package.json           # Node.js dependencies and scripts
├── tsconfig.json          # TypeScript configuration
├── run_cloud_arch_server.sh  # Shell script for easy server startup
└── README.md             # This file
```

## Features

- **Iterative requirement gathering**: Systematically collect cloud architecture requirements through guided questions
- **Azure component suggestions**: Get recommendations for specific Azure services with detailed configuration options
- **Multi-tier architecture design**: Design comprehensive solutions covering infrastructure, platform, application, data, security, and operations tiers
- **Tracking architecture completeness**: Monitor design progress with metrics for each architecture tier
- **Design pattern recommendations**: Receive suggestions for architectural patterns appropriate to your requirements
- **Follow-up questions**: Dynamic questioning that adapts based on previous answers
- **Visualization**: Console-based visualization of architecture progress

## Requirements

- Node.js (v14 or higher)
- npm (v6 or higher)

## Installation

1. Clone this repository:
   ```
   git clone <repository-url>
   cd cloud_architect_mcp
   ```

2. Install dependencies:
   ```
   npm install
   ```

3. Build the TypeScript code:
   ```
   npm run build
   ```
   
   Or if you don't have a build script, compile manually:
   ```
   npx tsc
   ```

## Usage

You can run the server in multiple ways:

### Using Node.js directly (Recommended)

```bash
# With default settings (stdio transport)
node dist/cloud_arch.js

# With SSE transport on specific port
node dist/cloud_arch.js --sse --port=8015
```

### Using the provided shell script

```bash
# With default settings (stdio transport)
./run_cloud_arch_server.sh

# With SSE transport on specific port
./run_cloud_arch_server.sh --sse --port=8123
```

### Command Line Arguments

- `--sse`: Use Server-Sent Events (SSE) transport instead of stdio
- `--port=<number>`: Specify the port number for the SSE server (default: 8015)

### Server Modes

The server supports two transport modes:

1. **stdio**: Default mode for terminal-based interactions
2. **SSE (Server-Sent Events)**: For web-based applications and integration with AI platforms

### Examples

```bash
# Run with stdio transport (default)
node dist/cloud_arch.js

# Run with SSE on default port (8015)
node dist/cloud_arch.js --sse

# Run with SSE on custom port
node dist/cloud_arch.js --sse --port=8123

# Run with custom port specified in your example
node dist/cloud_arch.js --sse --port=801
```

## Development

### Building the Project

To compile the TypeScript source to JavaScript:

```bash
# Compile TypeScript to JavaScript
npx tsc

# Or if you have a build script in package.json
npm run build
```

### Running in Development Mode

For development with automatic recompilation:

```bash
# Run TypeScript directly (if ts-node is installed)
npx ts-node-esm cloud_arch.ts

# Or watch mode compilation
npx tsc --watch
```

## API Documentation

### Tool: `design_azure_architecture`

This tool facilitates the design of Azure cloud architectures through an interactive process.

#### Parameters

- `question`: The current question being asked
- `questionNumber`: Current question number in sequence
- `totalQuestions`: Estimated total questions needed
- `answer`: The user's response to the question (optional)
- `nextQuestionNeeded`: Whether another question is needed
- `requirementCategory`: Category for organizing requirements (optional)
- `isFollowUp`: Whether this is a follow-up to a previous question (optional)
- `followsQuestionNumber`: Question number this follows up on (optional)
- `architectureSuggested`: Whether this suggests an architecture component (optional)
- `architectureComponent`: Specific Azure component being suggested (optional)
- `detailLevel`: Level of detail for this component or question (high, medium, low) (optional)
- `domainSpecific`: Whether this relates to a specific domain (optional)
- `requirementIdentified`: Specific requirement identified from user responses (optional)
- `technicalConstraint`: Technical constraint identified that impacts architecture (optional)
- `designPatternSuggested`: Architectural pattern being recommended (optional)
- `serviceDetails`: Detailed information about a specific Azure service (optional)
- `architectureTier`: Which architectural tier this component belongs to (optional)

#### Response

The server returns JSON with the following structure:

```json
{
  "display_text": "The question text for display",
  "questionNumber": 1,
  "totalQuestions": 10,
  "nextQuestionNeeded": true,
  "followUpQuestions": [1, 2],
  "questionHistoryLength": 5,
  "architectureStatus": {
    "componentsCount": 8,
    "requirementsCount": 10,
    "constraintsCount": 3,
    "designPatternsCount": 2,
    "completenessPercentage": 67,
    "emptyTiers": ["operations"],
    "tierComponentCounts": {
      "infrastructure": 2,
      "platform": 1,
      "application": 3,
      "data": 2,
      "security": 1,
      "operations": 0
    }
  }
}
```

## Examples

### Starting the Architecture Design Process

```json
{
  "question": "What is the primary business goal for your cloud solution?",
  "questionNumber": 1,
  "totalQuestions": 10,
  "nextQuestionNeeded": true
}
```

### Following Up on a Specific Requirement

```json
{
  "question": "You mentioned high availability is important. What is your specific Recovery Time Objective (RTO) requirement?",
  "questionNumber": 3,
  "totalQuestions": 10,
  "nextQuestionNeeded": true,
  "isFollowUp": true,
  "followsQuestionNumber": 2,
  "requirementCategory": "reliability"
}
```

### Suggesting an Architecture Component

```json
{
  "question": "Based on your requirements for high data throughput and need for eventual consistency, I recommend using Azure Cosmos DB with the following configuration.",
  "questionNumber": 6,
  "totalQuestions": 10,
  "nextQuestionNeeded": true,
  "architectureSuggested": true,
  "architectureComponent": "Azure Cosmos DB",
  "architectureTier": "data",
  "serviceDetails": {
    "name": "Azure Cosmos DB",
    "purpose": "Global distributed NoSQL database with multiple consistency levels",
    "configuration": "Multi-region write with Session consistency",
    "alternatives": ["Azure Table Storage", "MongoDB"]
  }
}
```

## Troubleshooting

### Common Issues

1. **Connection Errors**: If experiencing 404 errors with SSE connections, ensure the port is not in use and CORS is properly configured.
2. **Tool Execution Errors**: Check the server logs for detailed error messages.

### Server Logs

The server outputs detailed logs to the console for debugging purposes. Look for error messages and connection status information to troubleshoot issues.

## License

[MIT License](LICENSE) 
