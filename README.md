# [Wix MCP](https://mcp.wix.com)

Wix now provides a [Model Context Protocol](https://modelcontextprotocol.io/introduction) (MCP) server that allows you to work with Wix tools and services in your chosen AI client. By configuring the Wix MCP server, you enable your client to search the Wix documentation, write code for the Wix platform, and make API calls on Wix sites. This saves you the time and effort of finding and applying the information in the documentation yourself.

For examples on how to use the Wix MCP server, see our [sample prompts](https://dev.wix.com/docs/sdk/articles/use-the-wix-mcp/mcp-sample-prompts).

## Configure the Wix MCP

This section shows you the basic configuration you need to add to your AI tool to use the Wix MCP server.

### Before you begin

- Make sure you have [Node.js](https://nodejs.org/en) version 19.9.0 or higher installed.

### Required configuration

To add the Wix MCP server to your agent, include the following JSON object in your MCP server configuration:

```javascript
{
  "mcpServers": {
    "wix-mcp-remote": {
      "type": "http",
      "url": "https://mcp.wix.com/mcp"
    }
  }
}
```

Depending on your client, you may be able to configure the MCP server through the client settings, or even ask the client itself to add the configuration. See instructions on adding MCP servers for common AI tools:

- [Instructions for Claude Desktop](https://modelcontextprotocol.io/quickstart/user#2-add-the-filesystem-mcp-server)
- [Instructions for Claude Web](https://support.anthropic.com/en/articles/11175166-about-custom-integrations-using-remote-mcp)
- [Instructions for Cursor](https://docs.cursor.com/context/model-context-protocol#configuring-mcp-servers)
- [Instructions for Windsurf](https://docs.windsurf.com/windsurf/mcp)
- [Instructions for VS Code](https://code.visualstudio.com/docs/copilot/chat/mcp-servers#_add-an-mcp-server-to-your-workspace)
- [Instructions for Gemini CLI](https://geminicli.com/docs/extensions/#installing-an-extension)

## Wixel MCP

[Wixel](https://www.wix.com/wixel) is the AI design studio by Wix. Its MCP server lets your AI client create images, logos, slide decks, videos and documents, and run quick image edits such as background removal, upscaling and vectorizing.

[![Install in Cursor](https://cursor.com/deeplink/mcp-install-dark.svg)](https://cursor.com/en-US/install-mcp?name=wixel&config=eyJ1cmwiOiJodHRwczovL21jcC53aXguY29tL3dpeGVsP3JlZj1jdXJzb3IifQ%3D%3D)
[![Install in VS Code](https://img.shields.io/badge/VS_Code-Install_Wixel-0098FF?style=flat-square&logo=visualstudiocode&logoColor=white)](https://insiders.vscode.dev/redirect/mcp/install?name=wixel&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fmcp.wix.com%2Fwixel%3Fref%3Dvscode%22%7D)

For other clients, add this server to your MCP configuration:

```json
{
  "mcpServers": {
    "wixel": {
      "type": "http",
      "url": "https://mcp.wix.com/wixel?ref=github"
    }
  }
}
```

In Claude, add `https://mcp.wix.com/wixel?ref=github` as a custom connector. You sign in with your Wix account the first time you use it.

## Available tools

The Wix MCP server provides the following tools in the table below. All of these tools are enabled by default.

|                                |                                                                                      |
| ------------------------------ | ------------------------------------------------------------------------------------ |
| Tool                           | Description                                                                          |
| SearchWixWDSDocumentation      | Search the [Wix Design System](https://www.docs.wixdesignsystem.com/) documentation. |
| SearchWixRESTDocumentation     | Search the [Wix REST](https://dev.wix.com/docs/rest) documentation.                  |
| SearchWixSDKDocumentation      | Search the [Wix SDK](https://dev.wix.com/docs/sdk) documentation.                    |
| SearchBuildAppsDocumentation   | Search the [Wix Build Apps](https://dev.wix.com/docs/build-apps) documentation.      |
| SearchWixHeadlessDocumentation | Search the [Wix Headless](https://dev.wix.com/docs/go-headless) documentation.       |
| WixBusinessFlowsDocumentation  | Include complete step-by-step instructions for multi-step sample flows.              |
| ReadFullDocsArticle            | Fetch the full content of an article by article URL.                                 |
| ReadFullDocsMethodSchema       | Get the full request and response schema of an API method.                           |
| ListWixSites                   | Query the sites for a Wix account.                                                   |
| CallWixSiteAPI                 | Perform an action or query for a given account and selected site.                    |
| ManageWixSite                  | Perform a site-level action, such as creating a site.                                |
| SupportAndFeedback             | Prompt the user for feedback and send it to Wix.                                     |

## Troubleshooting

If you’re getting errors when running the MCP server, try the following:

1. Check the IDE logs.

1. Check if the error is related to your package manager. Make sure you have the latest node version as the default on the path.

1. Check that you entered the npx arguments correctly in the configuration. Make sure you included `-y` and the correct npm registry.

1. Include the full path to Node.

1. Restart the IDE.

1. Run the MCP server directly on the command line:

    ```bash
    npx -y @wix/mcp-remote https://mcp.wix.com/sse
    ```

1. The connection to the server may be lost after a long period of inactivity, or if you switch the Wix account you’re authenticating with. In that case, it may help to delete `~/.mcp-auth` (on Mac) or `C:\Users\<username>\.mcp-auth` (on Windows).

1. If the server still isn’t working, check the [MCP debugging guide](https://modelcontextprotocol.io/docs/tools/debugging#debugging-in-claude-desktop) for more help.
