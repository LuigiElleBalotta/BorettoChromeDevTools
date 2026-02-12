# Boretto Chrome DevTools

A Kiro Power that wraps the Chrome DevTools MCP server, providing full browser automation, debugging, performance analysis, and web scraping capabilities.

## Overview

This power enables your AI coding assistant to control and inspect a live Chrome browser through the Model Context Protocol. It provides access to the full power of Chrome DevTools for:

- **Browser Automation** - Reliable automation with automatic waiting mechanisms
- **Performance Analysis** - Capture traces and extract actionable insights
- **Web Debugging** - Analyze network requests, console messages, and take screenshots
- **Web Scraping** - Extract data with full JavaScript execution support
- **Device Emulation** - Test responsive designs and mobile experiences

## Installation

### In Kiro

1. Open Kiro Settings
2. Navigate to Powers
3. Click "Add Custom Power"
4. Select "GitHub Repository"
5. Enter: `https://github.com/LuigiElleBalotta/BorettoChromeDevTools`
6. Click "Add"

### Prerequisites

- Node.js v20.19 or newer
- Chrome stable version or newer
- npm package manager

## Quick Start

After installation, test with this prompt:

```
Check the performance of https://developers.chrome.com
```

The browser should open automatically and record a performance trace.

## Features

### 26 Tools Across 6 Categories

- **Input Automation** (8 tools) - click, drag, fill, fill_form, handle_dialog, hover, press_key, upload_file
- **Navigation** (6 tools) - close_page, list_pages, navigate_page, new_page, select_page, wait_for
- **Emulation** (2 tools) - emulate, resize_page
- **Performance** (3 tools) - analyze_insight, start_trace, stop_trace
- **Network** (2 tools) - get_network_request, list_network_requests
- **Debugging** (5 tools) - evaluate_script, get_console_message, list_console_messages, take_screenshot, take_snapshot

## Common Workflows

### Performance Analysis
```
Start a performance trace, navigate to https://example.com, stop the trace and analyze the performance insights
```

### Web Scraping
```
Navigate to https://news.ycombinator.com, wait for the page to load, and extract the titles of the top 10 stories
```

### Automated Testing
```
Navigate to https://example.com/login, fill in the login form with test credentials, submit it, and verify successful login
```

### Network Debugging
```
Navigate to https://api.example.com/dashboard and show me all failed network requests
```

### Device Emulation
```
Emulate an iPhone 13 Pro, navigate to https://example.com, and take a screenshot
```

## Configuration

The basic configuration works out of the box. For advanced options, you can customize the MCP server by editing your mcp.json:

### Headless Mode
```json
"args": ["-y", "chrome-devtools-mcp@latest", "--headless=true"]
```

### Custom Viewport
```json
"args": ["-y", "chrome-devtools-mcp@latest", "--viewport=1920x1080"]
```

### Isolated Profile (Temporary)
```json
"args": ["-y", "chrome-devtools-mcp@latest", "--isolated=true"]
```

### Disable Usage Statistics
```json
"args": ["-y", "chrome-devtools-mcp@latest", "--no-usage-statistics"]
```

## Documentation

For complete documentation, workflows, troubleshooting, and best practices, see [POWER.md](POWER.md).

## About

This power wraps the official [Chrome DevTools MCP server](https://github.com/ChromeDevTools/chrome-devtools-mcp) maintained by the Chrome DevTools team.

**Author:** Luigi Ella Balotta (Boretto)  
**Repository:** https://github.com/LuigiElleBalotta/BorettoChromeDevTools  
**License:** GNU General Public License v3.0

## Support

For issues related to:
- **This power wrapper**: Open an issue in this repository
- **Chrome DevTools MCP server**: See the [official repository](https://github.com/ChromeDevTools/chrome-devtools-mcp)
- **Kiro Powers**: See [Kiro documentation](https://kiro.dev/docs)

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.
