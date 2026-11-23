---
name: playwright-proxy-usage
description: Use when a target site must be reached through a specific proxy through Playwright MCP browser tools
---

## MCP config does not define Playwright's runtime capabilities
- `browser_get_config` reports the resolved server config after merging CLI arguments, environment variables and config files. Inspect `browser.launchOptions.proxy` and `browser.contextOptions.proxy`; absence of `--proxy-server` alone proves nothing. It does not report settings subsequently applied to runtime-created contexts.
- Microsoft's `browser_run_code_unsafe` receives a single `page` argument and exposes the full Playwright API. Use `page.context().browser()` to obtain the owning Browser (when available), then `await browser.newContext({ proxy: { server, username, password } })`. Create a new page in that context and use it; this does not change the MCP's existing page. Close the new context when finished.
- Before declaring any library feature unavailable, query official docs (Context7: `/microsoft/playwright`) for proxy configuration and authentication. Playwright supports HTTP(S) and SOCKS5 proxies; `username`/`password` authentication is supported for HTTP(S) proxies, not SOCKS5. Do not assume other MCP code-execution tools expose the same capabilities.

## Verify the proxy outside the browser first
- `curl -x http://<host>:<port> --proxy-user '<user>:<pass>' -v <url>` checks proxy connectivity and authentication. Compare with `curl --noproxy '*' -v <url>` to test direct connectivity. Inspect the CONNECT response and HTTP headers: a 403/451 alone cannot establish whether the proxy or destination denied access.
- Avoid putting real proxy credentials directly in shell history or command lines.