---
name: context7-docs
description: Use Context7 to retrieve current, version-specific documentation for tools, MCP-exposed capabilities, third-party libraries, frameworks, SDKs, and APIs when using, implementing or debugging software.
---

# Context7 Documentation

Use Context7 whenever a task involves using, configuring, implementing, or debugging an external tool, library, framework, SDK, or API and its usage, capabilities, parameters, or behavior may require documentation. This includes tools and capabilities exposed through MCP servers: look up their documentation before using unfamiliar tools or relying on undocumented behavior.

## Workflow

1. Identify the relevant tool, library, or API. Determine its version when available and relevant to documentation accuracy. For MCP-exposed tools, identify the underlying tool or service and consult its documentation; do not require version identification when unavailable.
2. Call `resolve-library-id` and select the matching official documentation.
3. Call `query-docs` with a focused question about the intended operation, API, tool usage, parameters, or behavior. Include the installed version when relevant.
4. Apply the documented usage and constraints; do not assume that similarly named tools or APIs behave identically or copy examples blindly.
5. Verify the result through relevant tests, type checks, tool execution, or other appropriate validation.

## Rules

- Prefer official documentation matching the installed version or exposed tool's implementation.
- Consult Context7 before using unfamiliar MCP-exposed tools or relying on their specific capabilities, arguments, workflows, or limitations.
- Do not guess library IDs or invent APIs, tool names, signatures, parameters, defaults, or compatibility claims.
- Avoid unnecessary lookups for routine operations or well-understood project-owned code.
- Never include secrets or unrelated private code in queries.
- If Context7 is unavailable or its documentation is insufficient, say so and use other reliable sources.
- Documentation lookup does not prove functionality; report only checks and operations actually performed.