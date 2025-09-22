# Shared Data Directory

This directory is mounted as `/data/shared` in the N8N container and can be used to:

- Store files that need to be accessed by N8N workflows
- Share data between different workflows
- Store temporary files and outputs

## Usage in N8N

You can access this directory in your N8N workflows using the path: `/data/shared/`

Example workflow nodes that can use this directory:
- Read/Write File nodes
- HTTP Request nodes (for file downloads)
- Code nodes (for file operations)
