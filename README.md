# Docker MCP Servers


```json
{
    "mcpServers": {
        "slack": {
            "command": "docker",
            "args": [
                "run",
                "-i",
                "--rm",
                "-e",
                "SLACK_BOT_TOKEN=your-slack-bot-token",
                "-e",
                "SLACK_TEAM_ID=your-slack-team-id",
                "ghcr.io/tatsuiman/docker-mcp-notion-server-slack:main"
            ]
        },
        "notion": {
            "command": "docker",
            "args": [
                "run",
                "-i",
                "--rm",
                "-e",
                "NOTION_API_TOKEN=your-integration-token",
                "ghcr.io/tatsuiman/docker-mcp-notion-server-notion-server:main"
            ]
        },
        "github": {
            "command": "docker",
            "args": [
                "run",
                "-i",
                "--rm",
                "-e",
                "GITHUB_PERSONAL_ACCESS_TOKEN=your-github-token",
                "ghcr.io/tatsuiman/docker-mcp-notion-server-github:main"
            ]
        }
    }
}
```