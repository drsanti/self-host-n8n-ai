# Self-Hosted N8N with AI

A Docker Compose setup for running N8N (workflow automation) with AI capabilities using Ollama, backed by PostgreSQL.

## Features

- **N8N**: Latest version with workflow automation capabilities
- **PostgreSQL**: Database backend for N8N data persistence
- **Ollama**: Local AI model server supporting multiple GPU configurations
- **Pre-configured workflows**: Demo data and credentials included

## Quick Start

1. **Clone and setup environment**:
   ```bash
   git clone https://github.com/drsanti/self-host-n8n-ai.git
   cd self-host-n8n-ai
   cp .env.example .env
   ```

2. **Configure environment variables**:
   Edit `.env` file with your settings:
   ```
   POSTGRES_USER=your_postgres_user
   POSTGRES_PASSWORD=your_secure_password
   POSTGRES_DB=n8n
   N8N_ENCRYPTION_KEY=your_encryption_key
   N8N_USER_MANAGEMENT_JWT_SECRET=your_jwt_secret
   ```

3. **Start the services**:

   **CPU-only setup**:
   ```bash
   docker-compose --profile cpu up -d
   ```

   **NVIDIA GPU setup**:
   ```bash
   docker-compose --profile gpu-nvidia up -d
   ```

   **AMD GPU setup**:
   ```bash
   docker-compose --profile gpu-amd up -d
   ```

## Services

### Core Services
- **N8N**: Available at http://localhost:5678
- **PostgreSQL**: Available at localhost:5432
- **Ollama**: Available at http://localhost:11434

### AI Models
The setup automatically pulls the `mistral:latest` model for AI workflows.

## Configuration

### Profiles
- `cpu`: CPU-only Ollama setup
- `gpu-nvidia`: NVIDIA GPU acceleration
- `gpu-amd`: AMD GPU acceleration with ROCm

### Volumes
- `n8n_storage`: N8N workflow and configuration data
- `postgres_storage`: PostgreSQL database files
- `ollama_storage`: AI model storage

## Usage

1. Access N8N at http://localhost:5678
2. Create your first workflow or import demo workflows from `./n8n/demo-data/`
3. Use Ollama nodes in N8N to interact with AI models
4. Models are automatically downloaded on first startup

## File Structure

```
.
├── docker-compose.yml    # Main service configuration
├── .env.example          # Environment variables template
├── .gitignore           # Git ignore file for sensitive data
├── README.md            # Project documentation (English & Thai)
├── n8n/
│   └── demo-data/       # Sample workflows and credentials
│       ├── README.md    # Demo data documentation
│       ├── workflows/   # Sample workflow files (.json)
│       └── credentials/ # Sample credential configurations (.json)
└── shared/              # Shared data directory
    └── README.md        # Shared directory documentation
```

## Troubleshooting

### GPU Issues
- Ensure Docker has GPU support enabled
- For NVIDIA: Install nvidia-docker2
- For AMD: Ensure ROCm drivers are installed

### Port Conflicts
If ports are already in use, modify the port mappings in `docker-compose.yml`:
- N8N: `5678:5678`
- PostgreSQL: `5432:5432`
- Ollama: `11434:11434`

### Storage Issues
Check volume permissions and ensure Docker has access to the storage directories.

## Development

To modify workflows or add new demo data:
1. Edit files in `./n8n/demo-data/`
2. Restart the `n8n-import` service: `docker-compose restart n8n-import`

## License

This project is provided as-is for educational and development purposes.

---

