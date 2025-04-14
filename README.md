# Docker Containerization Setup

## Docker Configuration

### Docker Compose Overview
The MCP Perplexity application uses Docker for containerization, providing an easy-to-deploy and consistent development environment.

#### docker-compose.yml Configuration
- **Version**: Uses Docker Compose file version 3.8
- **Service Name**: `mcp-perplexity`
- **Build Context**: Builds from the root directory using the Dockerfile
- **Container Name**: `mcp-perplexity`

### Environment Variables
The application uses environment variables for flexible configuration:

| Variable | Description | Default Value |
|----------|-------------|---------------|
| `LOG_LEVEL` | Logging verbosity | `INFO` |
| `PYTHONUNBUFFERED` | Ensures Python output is sent directly to the console | `1` |
| `PYTHONFAULTHANDLER` | Enables Python fault handler | `1` |
| `PERPLEXITY_API_KEY` | Perplexity API key for integration | *Required* |
| `PERPLEXITY_MODEL` | Perplexity model for general use | `sonar-pro` |
| `PERPLEXITY_MODEL_ASK` | Perplexity model for ask functionality | `sonar-pro` |
| `PERPLEXITY_MODEL_CHAT` | Perplexity model for chat functionality | `sonar-reasoning-pro` |
| `DATABASE_URL` | Database connection string | `sqlite:///mcp_perplexity.db` |
| `DB_PATH` | Path to the database file | `/app/data/perplexity.db` |
| `APP_PORT` | Port on which the application runs | `8000` |

### Docker Setup Instructions

#### Prerequisites
- Docker
- Docker Compose

#### Steps to Run

1. **Configure Environment**
   ```bash
   # Copy the example .env file and modify as needed
   cp .env.example .env
   ```

2. **Add API Keys**
   ⚠️ **IMPORTANT API KEY SECURITY NOTICE** ⚠️
   - Open the `.env` file
   - Replace `your_perplexity_api_key_here` with your actual Perplexity API key
   - NEVER share your API keys publicly or commit them to version control
   
   ##### Obtaining a Perplexity API Key
   - Visit the [Perplexity AI website](https://www.perplexity.ai/)
   - Create an account or log in
   - Navigate to API settings or developer section
   - Generate a new API key
   - Copy the key and paste it into the `.env` file

3. **Build and Run**
   ```bash
   # Build the Docker image
   docker-compose build

   # Start the application
   docker-compose up -d
   ```

4. **Access the Application**
   - Open a web browser and navigate to `http://localhost:8000`

#### Additional Configuration
- Modify `.env` file to change port, logging level, or database configuration
- Adjust `docker-compose.yml` for advanced Docker configurations

#### Stopping the Application
```bash
docker-compose down
```

### Volume Mapping
- Local `./data` directory is mapped to `/app/data` in the container
- Ensures data persistence between container restarts

### Restart Policy
- Container is configured to restart automatically unless explicitly stopped

### Security Recommendations
- Keep your `.env` file private
- Use strong, unique API keys
- Regularly rotate your API keys
- Consider using environment-specific configurations
