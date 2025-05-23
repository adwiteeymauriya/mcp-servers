
### Run the Container

```bash
# Run the container, passing in your credentials
docker run -d \
  -e TURSO_API_TOKEN="your-turso-api-token" \
  -e TURSO_ORGANIZATION="your-organization-name" \
  -e TURSO_DEFAULT_DATABASE="optional-default-database" \
  --name mcp-turso-cloud \
  mcp-turso-cloud:latest
```

### Environment Variables

| Variable | Description | Required |
|----------|-------------|----------|
| `TURSO_API_TOKEN` | Your Turso API token | ✅ Yes |
| `TURSO_ORGANIZATION` | Your Turso organization name | ✅ Yes |
| `TURSO_DEFAULT_DATABASE` | Default database to connect to | ❌ Optional |

> **Security Note**: Never include sensitive data like API tokens in your Dockerfile. Always pass them at runtime using the `-e` flag or environment files.

## IDE Integration

### Cursor / VS Code Configuration

Update your `.cursor/config.json` (or VS Code settings) to use the Docker container:

```jsonc
{
  "mcpServers": {
    "mcp-turso-cloud": {
      "command": "docker",
      "args": [
        "run", "-i", "--rm",
        "-e", "TURSO_API_TOKEN=your-turso-api-token",
        "-e", "TURSO_ORGANIZATION=your-organization-name",
        "-e", "TURSO_DEFAULT_DATABASE=optional-default-database",
        "mcp-turso-cloud:latest"
      ]
    }
  }
}
```

Now your IDE's MCP subsystem will spin up the container just as easily as it ran `npx mcp-turso-cloud`.

## Alternative: Using Environment Files

For better security and management of environment variables, you can use an environment file:

### Create `.env` file

```bash
TURSO_API_TOKEN=your-turso-api-token
TURSO_ORGANIZATION=your-organization-name
TURSO_DEFAULT_DATABASE=optional-default-database
```

### Run with environment file

```bash
docker run -d --env-file .env --name mcp-turso-cloud mcp-turso-cloud:latest
```

## Docker Compose (Optional)

For more complex setups, you can use Docker Compose:

```yaml
version: '3.8'
services:
  mcp-turso-cloud:
    build: .
    environment:
      - TURSO_API_TOKEN=${TURSO_API_TOKEN}
      - TURSO_ORGANIZATION=${TURSO_ORGANIZATION}
      - TURSO_DEFAULT_DATABASE=${TURSO_DEFAULT_DATABASE}
    restart: unless-stopped
```

Run with:
```bash
docker-compose up -d
```

## Troubleshooting

### Check Container Logs

```bash
docker logs mcp-turso-cloud
```

### Interactive Shell Access

```bash
docker exec -it mcp-turso-cloud sh
```

### Stop and Remove Container

```bash
docker stop mcp-turso-cloud
docker rm mcp-turso-cloud
```

## Benefits of Docker Deployment

- **Isolation**: Dependencies are contained within the container
- **Consistency**: Same environment across development, testing, and production
- **Portability**: Runs anywhere Docker is supported
- **Easy Updates**: Simply rebuild and restart the container
- **Resource Management**: Better control over CPU and memory usage

---

*For more information about the MCP Turso Cloud package, visit the [official documentation](https://github.com/your-repo/mcp-turso-cloud).*
