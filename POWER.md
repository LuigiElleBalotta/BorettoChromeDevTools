---
name: "BorettoChromeDevTools"
displayName: "Boretto's Chrome DevTools"
description: "Control and inspect a live Chrome browser with full DevTools access for automation, debugging, performance analysis, and web scraping using the Chrome DevTools Protocol"
keywords: ["chrome", "browser", "automation", "devtools", "puppeteer", "performance", "debugging", "screenshot", "scraping"]
author: "LuigiElleBalotta"
---

# Chrome DevTools

## Overview

Chrome DevTools MCP lets your coding agent control and inspect a live Chrome browser through the Model Context Protocol. It provides access to the full power of Chrome DevTools for reliable browser automation, in-depth debugging, performance analysis, and web scraping.

This power enables you to:
- Automate browser interactions with reliable waiting mechanisms
- Capture performance traces and extract actionable insights
- Debug web applications by analyzing network requests, console messages, and taking screenshots
- Scrape web content with full JavaScript execution support
- Emulate different devices and network conditions

The server uses Puppeteer under the hood for reliable automation and automatically waits for action results.

## Onboarding

### Prerequisites

- Node.js v20.19 or newer (latest maintenance LTS version)
- Chrome stable version or newer
- npm package manager

### Installation

The Chrome DevTools MCP server is installed via npx and doesn't require separate installation. The MCP configuration will automatically download and run the latest version when needed.

### Configuration

The basic configuration is already set up in the mcp.json file. The server will automatically start a Chrome instance when you first use a tool that requires the browser.

**Default behavior:**
- Starts Chrome with a dedicated profile at `$HOME/.cache/chrome-devtools-mcp/chrome-profile-stable`
- Profile persists between runs (not cleared automatically)
- Browser starts automatically when first tool is invoked

**Optional configurations** (add to args in mcp.json):
- `--headless=true` - Run Chrome without UI
- `--isolated=true` - Use temporary profile that's cleaned up after browser closes
- `--channel=canary` - Use Chrome Canary instead of stable
- `--viewport=1920x1080` - Set initial viewport size
- `--no-usage-statistics` - Opt out of Google's usage statistics collection

### Verification

After installation, test with this prompt:
```
Check the performance of https://developers.chrome.com
```

The browser should open automatically and record a performance trace.

## Common Workflows

### Workflow 1: Performance Analysis

**Goal:** Analyze website performance and get actionable insights

**Steps:**
1. Start a performance trace
2. Navigate to the target URL
3. Stop the trace and analyze results

**Example:**
```
Start a performance trace, navigate to https://example.com, stop the trace and analyze the performance insights
```

**Tools used:**
- `performance_start_trace` - Begin recording performance data
- `navigate_page` - Load the target page
- `performance_stop_trace` - Stop recording and get trace data
- `performance_analyze_insight` - Extract actionable performance recommendations

**Common Errors:**
- Error: "No active trace"
  - Cause: Trying to stop a trace that wasn't started
  - Solution: Always call `performance_start_trace` before `performance_stop_trace`

### Workflow 2: Web Scraping

**Goal:** Extract data from websites with JavaScript execution

**Steps:**
1. Navigate to the target page
2. Wait for content to load
3. Execute JavaScript to extract data
4. Optionally take screenshots for verification

**Example:**
```
Navigate to https://news.ycombinator.com, wait for the page to load, and extract the titles of the top 10 stories
```

**Tools used:**
- `navigate_page` - Load the page
- `wait_for` - Wait for specific elements or conditions
- `evaluate_script` - Run JavaScript to extract data
- `take_screenshot` - Capture visual confirmation

**Common Errors:**
- Error: "Element not found"
  - Cause: Trying to interact with elements before page loads
  - Solution: Use `wait_for` to ensure elements are present

### Workflow 3: Automated Testing

**Goal:** Test user interactions and verify application behavior

**Steps:**
1. Navigate to the application
2. Fill forms and click buttons
3. Verify results through console messages or screenshots
4. Check network requests for API calls

**Example:**
```
Navigate to https://example.com/login, fill in the login form with test credentials, submit it, and verify successful login
```

**Tools used:**
- `navigate_page` - Load the application
- `fill` - Enter text into input fields
- `click` - Click buttons and links
- `list_console_messages` - Check for errors or success messages
- `list_network_requests` - Verify API calls
- `take_screenshot` - Visual verification

**Common Errors:**
- Error: "Dialog not handled"
  - Cause: Browser dialog (alert/confirm) blocking automation
  - Solution: Use `handle_dialog` to accept or dismiss dialogs

### Workflow 4: Network Debugging

**Goal:** Analyze network requests and responses

**Steps:**
1. Navigate to the page
2. List all network requests
3. Inspect specific requests for headers, status, and response data

**Example:**
```
Navigate to https://api.example.com/dashboard and show me all failed network requests
```

**Tools used:**
- `navigate_page` - Load the page
- `list_network_requests` - Get all network activity
- `get_network_request` - Inspect specific request details

**Common Errors:**
- Error: "Request not found"
  - Cause: Trying to get details of a request that doesn't exist
  - Solution: Use `list_network_requests` first to get valid request IDs

### Workflow 5: Device Emulation

**Goal:** Test responsive design and mobile experiences

**Steps:**
1. Set device emulation parameters
2. Navigate to the page
3. Take screenshots to verify layout
4. Test touch interactions

**Example:**
```
Emulate an iPhone 13 Pro, navigate to https://example.com, and take a screenshot
```

**Tools used:**
- `emulate` - Set device type, user agent, and viewport
- `navigate_page` - Load the page
- `take_screenshot` - Capture the mobile view
- `resize_page` - Adjust viewport dimensions

**Common Errors:**
- Error: "Invalid device descriptor"
  - Cause: Incorrect emulation parameters
  - Solution: Use standard device names or provide valid viewport dimensions

### Workflow 6: Form Automation

**Goal:** Fill and submit complex forms efficiently

**Steps:**
1. Navigate to the form page
2. Use fill_form to populate multiple fields at once
3. Handle any dialogs or confirmations
4. Verify submission success

**Example:**
```
Navigate to https://example.com/contact, fill out the contact form with name "John Doe", email "john@example.com", and message "Test message", then submit it
```

**Tools used:**
- `navigate_page` - Load the form page
- `fill_form` - Fill multiple fields efficiently
- `click` - Submit the form
- `handle_dialog` - Handle confirmation dialogs
- `list_console_messages` - Check for validation errors

**Common Errors:**
- Error: "Form field not found"
  - Cause: Selector doesn't match form fields
  - Solution: Inspect the page to get correct selectors

## Available Tools

The Chrome DevTools MCP server provides 26 tools organized into 6 categories:

### Input Automation (8 tools)
- `click` - Click on elements
- `drag` - Drag and drop operations
- `fill` - Fill text into input fields
- `fill_form` - Fill multiple form fields at once
- `handle_dialog` - Accept or dismiss browser dialogs
- `hover` - Hover over elements
- `press_key` - Press keyboard keys
- `upload_file` - Upload files to file inputs

### Navigation Automation (6 tools)
- `close_page` - Close browser tabs
- `list_pages` - List all open tabs
- `navigate_page` - Navigate to URLs
- `new_page` - Open new tabs
- `select_page` - Switch between tabs
- `wait_for` - Wait for elements or conditions

### Emulation (2 tools)
- `emulate` - Emulate devices and network conditions
- `resize_page` - Change viewport size

### Performance (3 tools)
- `performance_analyze_insight` - Get performance recommendations
- `performance_start_trace` - Start recording performance data
- `performance_stop_trace` - Stop recording and get trace

### Network (2 tools)
- `get_network_request` - Get details of specific requests
- `list_network_requests` - List all network activity

### Debugging (5 tools)
- `evaluate_script` - Execute JavaScript in the page
- `get_console_message` - Get specific console message
- `list_console_messages` - List all console messages
- `take_screenshot` - Capture page screenshots
- `take_snapshot` - Take DOM snapshots

## Best Practices

- Always use `wait_for` before interacting with dynamic content to ensure elements are ready
- Start performance traces before navigating to capture complete loading metrics
- Use `list_console_messages` to catch JavaScript errors during automation
- Enable `--isolated=true` for testing to avoid polluting your browser profile
- Use `fill_form` instead of multiple `fill` calls for better performance
- Take screenshots at key points for debugging failed automation
- Check network requests to verify API calls and catch failed requests
- Use specific selectors (IDs or data attributes) instead of generic ones for reliability

## Troubleshooting

### MCP Server Connection Issues

**Problem:** MCP server won't start or connect
**Symptoms:**
- Error: "Connection refused"
- Server not responding
- Browser doesn't start

**Solutions:**
1. Verify Node.js version: `node --version` (should be v20.19+)
2. Check Chrome is installed and accessible
3. Try running manually: `npx -y chrome-devtools-mcp@latest`
4. Check for port conflicts (default debugging port 9222)
5. Restart Kiro and try again

### Browser Launch Failures

**Problem:** Chrome fails to start
**Symptoms:**
- Error: "Failed to launch browser"
- Timeout waiting for browser

**Solutions:**
1. Close all Chrome instances and try again
2. Check user data directory permissions: `$HOME/.cache/chrome-devtools-mcp/`
3. Try with `--isolated=true` flag to use temporary profile
4. On Windows: Ensure Chrome path is correct, may need `--executablePath` flag
5. Check for Chrome updates

### Automation Timing Issues

**Problem:** Elements not found or interactions fail
**Symptoms:**
- Error: "Element not found"
- Error: "Node is detached from document"

**Solutions:**
1. Add `wait_for` before interacting with elements
2. Increase wait timeout if page loads slowly
3. Use more specific selectors
4. Check if element is in an iframe (may need special handling)
5. Verify element is visible and not covered by other elements

### Performance Trace Errors

**Problem:** Performance trace fails or returns incomplete data
**Symptoms:**
- Error: "No active trace"
- Missing performance metrics

**Solutions:**
1. Ensure `performance_start_trace` is called before navigation
2. Wait for page to fully load before stopping trace
3. Check network connectivity (CrUX data requires internet)
4. Use `--no-performance-crux` if CrUX API is blocked
5. Verify page actually loaded (check for navigation errors)

### Network Request Issues

**Problem:** Network requests not captured or incomplete
**Symptoms:**
- Empty network request list
- Missing request details

**Solutions:**
1. Ensure requests are made after page navigation starts
2. Check if requests are blocked by CORS or CSP
3. Verify network category is enabled (not disabled via `--category-network=false`)
4. Some requests may be cached - clear cache if needed
5. Check browser console for network errors

### Dialog Handling Errors

**Problem:** Browser dialogs block automation
**Symptoms:**
- Error: "Dialog not handled"
- Automation hangs

**Solutions:**
1. Use `handle_dialog` before triggering actions that show dialogs
2. Set up dialog handler with `accept` or `dismiss` action
3. Check console messages for dialog text
4. Some dialogs may be custom (not native) - use regular element interaction

### Sandboxing Issues

**Problem:** MCP server can't start Chrome in sandboxed environments
**Symptoms:**
- Error: "Failed to launch browser"
- Sandbox permission errors

**Solutions:**
1. Disable sandboxing for chrome-devtools-mcp in your MCP client
2. Use `--browser-url` to connect to manually started Chrome instance
3. Start Chrome outside sandbox with remote debugging enabled
4. See "Connecting to a running Chrome instance" section in documentation

## Advanced Configuration

### Connecting to Running Chrome Instance

If you need to connect to an existing Chrome instance instead of starting a new one:

**Method 1: Automatic Connection (Chrome 144+)**
1. In Chrome, navigate to `chrome://inspect/#remote-debugging`
2. Enable remote debugging and allow connections
3. Add `--autoConnect` to mcp.json args:
```json
{
  "mcpServers": {
    "chrome-devtools": {
      "command": "npx",
      "args": ["-y", "chrome-devtools-mcp@latest", "--autoConnect"]
    }
  }
}
```

**Method 2: Manual Connection via Port**
1. Start Chrome with remote debugging:
   ```
   chrome.exe --remote-debugging-port=9222 --user-data-dir="%TEMP%\chrome-profile"
   ```
2. Add `--browser-url` to mcp.json args:
```json
{
  "mcpServers": {
    "chrome-devtools": {
      "command": "npx",
      "args": ["-y", "chrome-devtools-mcp@latest", "--browser-url=http://127.0.0.1:9222"]
    }
  }
}
```

### Custom Chrome Configuration

Add these flags to args array in mcp.json for custom behavior:

**Headless mode:**
```json
"args": ["-y", "chrome-devtools-mcp@latest", "--headless=true"]
```

**Custom viewport:**
```json
"args": ["-y", "chrome-devtools-mcp@latest", "--viewport=1920x1080"]
```

**Use Chrome Canary:**
```json
"args": ["-y", "chrome-devtools-mcp@latest", "--channel=canary"]
```

**Proxy configuration:**
```json
"args": ["-y", "chrome-devtools-mcp@latest", "--proxyServer=http://proxy.example.com:8080"]
```

**Disable usage statistics:**
```json
"args": ["-y", "chrome-devtools-mcp@latest", "--no-usage-statistics"]
```

### Disabling Tool Categories

If you don't need certain tool categories, disable them to reduce context:

```json
{
  "mcpServers": {
    "chrome-devtools": {
      "command": "npx",
      "args": [
        "-y",
        "chrome-devtools-mcp@latest",
        "--category-performance=false",
        "--category-emulation=false"
      ]
    }
  }
}
```

Available categories:
- `--category-emulation` (default: true)
- `--category-performance` (default: true)
- `--category-network` (default: true)

## Privacy and Data Collection

### Usage Statistics

Google collects usage statistics (tool invocation success rates, latency, environment information) to improve reliability and performance. This is enabled by default.

**To opt out**, add to args:
```json
"args": ["-y", "chrome-devtools-mcp@latest", "--no-usage-statistics"]
```

Or set environment variable: `CHROME_DEVTOOLS_MCP_NO_USAGE_STATISTICS=1`

### CrUX Performance Data

Performance tools may send trace URLs to the Google CrUX API to fetch real-user experience data for comparison with lab data.

**To disable**, add to args:
```json
"args": ["-y", "chrome-devtools-mcp@latest", "--no-performance-crux"]
```

### Security Considerations

- The MCP server exposes browser content to MCP clients
- Avoid browsing sensitive sites while the debugging port is open
- Use `--isolated=true` for temporary profiles that are automatically cleaned
- Be cautious with `--accept-insecure-certs` flag (only use for testing)

## Configuration

**No additional configuration required** - works after MCP server is installed in Kiro.

The server uses standard npm package installation via npx and will automatically download the latest version when first invoked.

**Optional environment variables:**
- `CHROME_DEVTOOLS_MCP_NO_USAGE_STATISTICS` - Set to disable usage statistics
- `DEBUG` - Set to `*` for verbose logging (useful for bug reports)

**Optional command-line flags** (add to args in mcp.json):
- See "Advanced Configuration" section above for common flags
- Run `npx chrome-devtools-mcp@latest --help` for complete list

---

**Package:** `chrome-devtools-mcp@latest`
**MCP Server:** chrome-devtools
**Repository:** https://github.com/ChromeDevTools/chrome-devtools-mcp
