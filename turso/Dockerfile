# 1. Base image
FROM node:lts-slim

# 2. Install the MCP package globally
RUN npm install -g mcp-turso-cloud

# 3. (Optional) Provide default ENV values for non-sensitive data
#    For sensitive data like TURSO_API_TOKEN, pass at runtime with: docker run -e TURSO_API_TOKEN=your_token
ENV TURSO_ORGANIZATION=""
ENV TURSO_DEFAULT_DATABASE=""

# 4. Expose any ports if needed (MCP itself doesn't listen publicly)
#    but your package might open a port—check its docs.
# EXPOSE 4000

# 5. Default entrypoint: run the MCP server
ENTRYPOINT ["mcp-turso-cloud"]

