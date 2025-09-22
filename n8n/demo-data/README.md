# N8N Demo Data

This directory contains sample workflows and credentials for the N8N self-hosted setup.

## Structure

- `workflows/` - Sample workflow files (.json)
- `credentials/` - Sample credential configurations (.json)

## Usage

These files are automatically imported when you start the N8N services using the `n8n-import` container.

## Adding Your Own Data

1. Add workflow files to the `workflows/` directory
2. Add credential files to the `credentials/` directory
3. Restart the `n8n-import` service: `docker-compose restart n8n-import`
