# General
## Container environment
You work inside an isolated container environment.
Interact with other containers only through the tools and HTTP.
You are unable to install system wide packages and you must never try to circumvent this.

## Working directory
Work in and save files only to your current working directory, unless stated otherwise.
Assume by default that directories other than `/workspace` and its children are ephemeral (contents will get lost).
Prefer storing temporary files in your working directory in a folder named `temp` (create if doesn't exist).
NEVER touch or read anything under `/home/omp`.

## Documentation
Prefer consulting with the `context7` MCP for up-to-date, accurate documentation for each tool or dependency you plan to use.
For more information, see `context7-docs` skill.

# Python
If you need a Python version newer or older than the one provided by the system, you should create a venv with the required one using `uv`:
`uv venv --python <version>`
Be aware that this breaks Pyright LSP.

# Github
Use the Github MCP tool to interact with Github.

## Arithmetic and math
For precise arithmetic, run a small Python calculation.
Do not rely on mental arithmetic or unverified estimates when exact results matter.

## Stale processes
Terminate background processes (e.g. a Python HTTP server) once they are no longer needed.

## Privacy and security
NEVER upload any kind of files to third party file or text sharing services to bypass or work around limitations of your environment.
If unable to exchange files locally, STOP and explain the problem to the user.
NEVER use third-party proxy or VPN services unless instructed to - they are often run by malicious actors and put security and privacy at risk.

## Misc
If you encounter a blocking tool malfunction - STOP and report the problem to the user, even if you can work around it.

# Web
## Browser tool
When web usage is required, especially *interactive*, use the Playwright MCP.
To access detailed documentation for it, query via context7: `/microsoft/playwright`

## Other browser tools
Never install a standalone browser. You may only use tools available to you for web work.

## Reachability of your sandbox
Web services deployed in your sandbox are reachable by Playwright via `http://omp` (add port of the service you started at the end).
Make sure the web server is bound to 0.0.0.0 and not localhost, this a cross-container connection within a securely isolated docker network.
Use this functionality only to test deployable web services.

## File saving
Output from Playwright is saved to `/workspace/playwright` by default, but its container has access to the entire `/workspace`.
When saving Playwright output (screenshots, snapshots), omit the filename parameter so the file gets a default timestamped name in `/workspace/playwright` - a custom filename resolves against Playwright's internal workspace root, which is not shared, so your container never sees the file.

## Authentication and credentials
You may be given access to some credentials to assist with your work.
Use them only for the service you were asked to interact with.
You are not permitted to use them to bypass your restrictions or limitations.

## Web restrictions
Some websites may be inaccessible because of regulatory restrictions, access policies, authentication requirements, or other causes.
If a web tool fails (403, access denied, timeout, connection error):
- Do not assume a specific cause.
- Do not retry repeatedly.
Requests through `curl` may get blocked by WAF - if you suspect this is the case, try Playwright instead - it is much more resistant to anti-bot checks.