<p align="center">
  <a href="https://www.getmaxim.ai/bifrost">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="https://www.getmaxim.ai/bifrost/brand-assets/bifrost-logo-white.svg">
      <source media="(prefers-color-scheme: light)" srcset="https://www.getmaxim.ai/bifrost/brand-assets/bifrost-logo.svg">
      <img src="https://www.getmaxim.ai/bifrost/brand-assets/bifrost-logo.svg" alt="Bifrost by Maxim AI" width="240">
    </picture>
  </a>
</p>

<h3 align="center">Route, govern, and secure AI traffic across models, MCP tools, and agents</h3>

<p align="center">
  <a href="https://trendshift.io/repositories/14529?utm_source=repository-badge&amp;utm_medium=badge&amp;utm_campaign=badge-repository-14529" target="_blank" rel="noopener noreferrer"><img src="https://trendshift.io/api/badge/repositories/14529" alt="maximhq%2Fbifrost | Trendshift" width="250" height="55"/></a>
</p>

<p align="center">
  <a href="https://discord.gg/exN5KAydbU"><img src="https://img.shields.io/badge/Discord-Join%20Community-5865F2?logo=discord&amp;logoColor=white" alt="Discord badge"/></a>
  <img src="https://img.shields.io/docker/pulls/maximhq/bifrost" alt="Docker Pulls"/>
  <a href="https://app.getpostman.com/run-collection/31642484-2ba0e658-4dcd-49f4-845a-0c7ed745b916?action=collection%2Ffork&amp;source=rip_markdown&amp;collection-url=entityId%3D31642484-2ba0e658-4dcd-49f4-845a-0c7ed745b916%26entityType%3Dcollection%26workspaceId%3D63e853c8-9aec-477f-909c-7f02f543150e"><img src="https://run.pstmn.io/button.svg" alt="Run In Postman" width="95" height="21"/></a>
  <a href="https://artifacthub.io/packages/search?repo=bifrost"><img src="https://img.shields.io/endpoint?url=https://artifacthub.io/badge/repository/bifrost" alt="Artifact Hub"/></a>
  <a href="LICENSE"><img src="https://img.shields.io/github/license/maximhq/bifrost" alt="License"/></a>
</p>

<p align="center">
  <a href="https://www.getmaxim.ai">Website</a> |
  <a href="https://getmaxim.ai/llm-gateway">Bifrost AI Gateway</a> |
  <a href="https://getmaxim.ai/mcp-gateway">Bifrost MCP Gateway</a> |
  <a href="https://getmaxim.ai/edge">Bifrost Edge</a> |
  <a href="https://www.getmaxim.ai/enterprise">Enterprise Tier</a> |
  <a href="https://docs.getbifrost.ai">Docs</a> |
  <a href="https://docs.getbifrost.ai/changelogs/v2.0.0">Changelogs</a> |
</p>

Bifrost, by Maxim AI, is an enterprise AI gateway with an Apache 2.0 open-source core, written in Go. It connects applications to AI providers through an OpenAI-compatible API and brings MCP tool discovery and execution into the same gateway.

AI inside a company comes from several directions: production applications calling models, agents using tools, and employees working with AI on their own machines. We built Bifrost to give teams control over those requests without making the gateway a bottleneck.

Start with the open-source Gateway for model routing, failover, MCP tools, budgets, and observability. Bifrost Enterprise adds identity-based governance, guardrails, audit logs, and high availability. Bifrost Edge extends the Enterprise Gateway to supported AI tools on employee devices.

<p align="center">
  <a href="#quick-start">Quick start</a> ·
  <a href="#connect-your-applications-and-agents">Integrations</a> ·
  <a href="#performance">Benchmarks</a> ·
  <a href="https://discord.gg/exN5KAydbU">Discord</a>
</p>

## Why Bifrost

**Performance and reliability belong in the foundation.** The gateway sits in the critical path. Every policy check, routing decision, and log has to work without holding up the application. Bifrost is built in Go, with retries, fallbacks, and weighted load balancing in the open-source core. Enterprise adds clustering, adaptive load balancing, and circuit breakers.

**Model access and tool access need governance together.** An agent’s model requests are only part of its activity. It also calls tools that can read data and take actions. Bifrost provides routing and access controls for both, with enterprise policies that connect to the identity provider your organization already uses.

**Run it in infrastructure you control.** Self-host Bifrost as an HTTP gateway or embed its Go SDK. Choose your upstream providers, configure how content is logged, and extend request handling with plugins. Enterprise supports private and air-gapped deployment options.

## Open source and Enterprise

| | Open-source Gateway | Bifrost Enterprise |
|---|---|---|
| Model access | Provider integrations, SDK adapters, routing, retries, fallbacks, and weighted load balancing | Includes the open-source capabilities |
| MCP | Server connections, tool filtering, authentication, Agent Mode, and Code Mode | Adds organizational access policies and enterprise scoping |
| Governance | Virtual keys, budgets, and rate limits | Adds identity-provider integration, access profiles, roles, and projects |
| Security and operations | Self-hosted gateway with configurable access and logging | Adds guardrails, sensitive-data redaction, signed audit logs, external secret management, and high availability |
| Employee devices | Configure supported clients to use the Gateway | Extend coverage with Bifrost Edge |
| License | Apache 2.0 | Commercial enterprise license |

Both editions run in your infrastructure. See the [Enterprise documentation](https://docs.getbifrost.ai/enterprise/overview) for the full scope and deployment requirements.

## Quick start

Run Bifrost locally and send your first model request.

You’ll need Node.js with `npx`, or Docker, and credentials for the provider you want to use. This example uses OpenAI.

### 1. Start the Gateway

Using `npx`:

```bash
npx -y @maximhq/bifrost
```

Or using Docker, with local storage for configuration and logs:

```bash
docker run \
  -p 127.0.0.1:8080:8080 \
  -v bifrost-data:/app/data \
  maximhq/bifrost
```

### 2. Configure a provider

Open [http://localhost:8080](http://localhost:8080).

Navigate to **Model Providers**, select **OpenAI**, and add your OpenAI API key. Make sure the key has access to the model used below.

You can also configure providers through the API or a `config.json` file. See [Provider configuration](https://docs.getbifrost.ai/quickstart/gateway/provider-configuration).

### 3. Send a request

From another terminal:

```bash
curl http://localhost:8080/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model": "openai/gpt-4o-mini",
    "messages": [
      {
        "role": "user",
        "content": "Explain what an AI gateway does in one sentence."
      }
    ]
  }'
```

The response contains the model’s answer. Open the Gateway’s request logs to inspect the request, provider, token usage, and latency.

This example uses a local Gateway without virtual-key enforcement. For a shared deployment, configure authentication, TLS, and durable storage, and pin the version you deploy. Follow the [Gateway setup guide](https://docs.getbifrost.ai/quickstart/gateway/setting-up) and [deployment documentation](https://docs.getbifrost.ai/deployment-guides).

## Connect your applications and agents

Bifrost supports existing SDKs through documented integration endpoints.

### Use the OpenAI Python SDK

With your provider configured, create a [Bifrost virtual key](https://docs.getbifrost.ai/features/governance/virtual-keys) that permits the provider and model you want to call. Set it as the `BIFROST_VIRTUAL_KEY` environment variable.

Install the SDK:

```bash
pip install openai
```

Then point the client at Bifrost:

```python
import os
from openai import OpenAI

client = OpenAI(
    base_url="http://localhost:8080/openai",
    api_key=os.environ["BIFROST_VIRTUAL_KEY"],
)

response = client.chat.completions.create(
    model="openai/gpt-4o-mini",
    messages=[
        {"role": "user", "content": "Hello, Bifrost!"}
    ],
)

print(response.choices[0].message.content)
```

The application authenticates to Bifrost with its virtual key. Bifrost uses the provider credentials configured at the Gateway for the upstream request.

See the [OpenAI SDK guide](https://docs.getbifrost.ai/integrations/openai-sdk/overview) for authentication and supported request types.

### Choose your integration

| Your application or workflow | Start here |
|---|---|
| OpenAI SDK, Python or JavaScript/TypeScript | [OpenAI integration](https://docs.getbifrost.ai/integrations/openai-sdk/overview) |
| Anthropic SDK | [Anthropic integration](https://docs.getbifrost.ai/integrations/anthropic-sdk/overview) |
| AWS Bedrock SDK | [Bedrock integration](https://docs.getbifrost.ai/integrations/bedrock-sdk/overview) |
| Google GenAI SDK | [Google GenAI integration](https://docs.getbifrost.ai/integrations/genai-sdk/overview) |
| LangChain | [LangChain integration](https://docs.getbifrost.ai/integrations/langchain-sdk) |
| LiteLLM SDK | [LiteLLM SDK integration](https://docs.getbifrost.ai/integrations/litellm-sdk) |
| Go application embedding Bifrost | [Go SDK setup](https://docs.getbifrost.ai/quickstart/go-sdk/setting-up) |
| Claude Code, Codex CLI, Gemini CLI, or OpenCode | [Bifrost CLI](https://docs.getbifrost.ai/quickstart/cli/getting-started) |
| MCP clients and tool servers | [MCP Gateway](https://docs.getbifrost.ai/mcp/overview) |

Use the integration guide for your SDK’s endpoint and authentication settings. Supported request types vary by provider and integration.

## Open-source capabilities

### Route requests across models and providers

Connect to OpenAI, Anthropic, AWS Bedrock, Google Vertex, Azure, and other supported providers through a common API.

- **Routing and model aliases:** choose request destinations through routing rules and expose stable model names to applications.
- **Retries and fallbacks:** retry failed requests and configure alternative providers or models.
- **Weighted load balancing:** distribute requests across configured keys and providers.
- **Complexity routing:** classify prompt complexity and route requests to an appropriate model tier.
- **Multimodal requests:** work with text, images, audio, streaming, and reranking where supported.

[Supported providers](https://docs.getbifrost.ai/providers/supported-providers/overview) · [Retries and fallbacks](https://docs.getbifrost.ai/features/retries-and-fallbacks) · [Complexity Router](https://docs.getbifrost.ai/features/governance/complexity-router)

### Connect and govern MCP tools

Bifrost connects to MCP servers and can expose connected tools through a gateway endpoint for external MCP clients.

- **Server connections:** connect over STDIO, HTTP, or SSE.
- **Tool filtering:** control which tools are available to clients and requests.
- **Authentication:** connect to upstream servers using shared credentials, OAuth, or per-user authentication.
- **Agent Mode:** configure automatic tool execution for the tools you allow.
- **Code Mode:** let a model orchestrate tools through sandboxed code, reducing the need to carry every tool definition and intermediate result in context.

Tool execution and automatic approval are configurable. Connecting a server does not mean every tool should be available to every caller.

[MCP overview](https://docs.getbifrost.ai/mcp/overview) · [Authentication](https://docs.getbifrost.ai/mcp/auth/overview) · [Code Mode](https://docs.getbifrost.ai/mcp/code-mode)

### Control spending and inspect traffic

Issue virtual keys with access restrictions, budgets, and rate limits. Use semantic caching to reuse responses for sufficiently similar requests where that fits your application.

Inspect request logs, token usage, cost, and latency through the built-in interface. Export metrics and traces through Prometheus and OpenTelemetry, and configure which request and response content is recorded.

[Virtual keys](https://docs.getbifrost.ai/features/governance/virtual-keys) · [Budgets and limits](https://docs.getbifrost.ai/features/governance/budget-and-limits) · [Semantic caching](https://docs.getbifrost.ai/features/semantic-caching) · [Observability](https://docs.getbifrost.ai/features/observability/default)

### Extend the Gateway and manage reusable assets

Add custom request and response handling through plugins. Version prompts in the Prompt Repository and test them in the playground. Use the Skills Repository to create, version, and distribute reusable skills to compatible coding agents.

[Custom plugins](https://docs.getbifrost.ai/plugins/getting-started) · [Prompt Repository](https://docs.getbifrost.ai/features/prompt-repository/playground) · [Skills Repository](https://docs.getbifrost.ai/features/skills-repository)

## Performance

A gateway’s overhead matters because every request passes through it.

In our published tests at **5,000 requests per second**, Bifrost recorded the following results against mocked OpenAI calls:

| Metric | AWS t3.medium | AWS t3.xlarge |
|---|---:|---:|
| Request success rate | 100% | 100% |
| Reported Bifrost overhead | 59 μs | 11 μs |
| Average queue wait | 47.13 μs | 1.67 μs |

The t3.medium configuration used 2 vCPUs and 4 GB RAM; t3.xlarge used 4 vCPUs and 16 GB RAM. Payload sizes and tuning differed between the tests, so these results describe the published configurations rather than an isolated comparison of instance sizes. Gateway overhead is separate from end-to-end model response latency.

Read the [benchmark methodology and results](https://docs.getbifrost.ai/benchmarking/getting-started), including the linked instructions for running benchmarks in your environment.

## Bifrost Enterprise

As AI usage spreads across teams, security and governance have to follow the organization: its people, roles, applications, and data boundaries.

Bifrost Enterprise adds the controls to manage that centrally while keeping the Gateway in your infrastructure.

### Govern access through your existing identity provider

Connect your identity provider for sign-in and provisioning. Define reusable access profiles for provider, model, MCP, budget, and rate-limit policies, then assign them to users directly or through roles and identity mappings.

Use role-based permissions to control administration. Apply enterprise access policies to Virtual MCPs, and use Projects to give work its own access scope, budget, and reporting.

[User provisioning](https://docs.getbifrost.ai/enterprise/user-provisioning) · [Access Profiles](https://docs.getbifrost.ai/enterprise/access-profiles) · [RBAC](https://docs.getbifrost.ai/enterprise/rbac) · [Projects](https://docs.getbifrost.ai/enterprise/projects)

### Apply security policies to requests and responses

Configure guardrails for content safety, personal data, and secrets. Block or redact content according to your policies, with separate redaction controls for live payloads, stored logs, and exported traces.

Connect guardrail services including AWS Bedrock Guardrails, Azure Content Safety, Google Model Armor, and other supported providers.

[Guardrails](https://docs.getbifrost.ai/enterprise/guardrails) · [Redaction controls](https://docs.getbifrost.ai/enterprise/guardrails/redaction)

### Keep an audit trail and control credentials

Record administrative changes through signed audit logs. Connect external secret stores for provider credentials, and configure log exports to fit your existing storage and monitoring systems.

[Audit logs](https://docs.getbifrost.ai/enterprise/audit-logs) · [Secret management](https://docs.getbifrost.ai/enterprise/secret-management) · [Log exports](https://docs.getbifrost.ai/enterprise/log-exports)

### Run across nodes and private environments

Use clustering for high availability, adaptive load balancing to respond to provider health, and circuit breakers to handle degradation.

Deploy in your VPC, on-premises, or in an air-gapped environment. Upstream models and external services remain destinations you configure; an isolated deployment requires those dependencies to fit the same network boundary.

[Clustering](https://docs.getbifrost.ai/enterprise/clustering) · [Adaptive load balancing](https://docs.getbifrost.ai/enterprise/adaptive-load-balancing) · [Private deployments](https://docs.getbifrost.ai/enterprise/invpc-deployments)

### Extend governance to employee devices with Bifrost Edge

Employees use AI through desktop applications, browsers, coding agents, and the MCP servers connected to those tools. That activity can sit outside the paths a platform team has configured.

Bifrost Edge runs on employee devices and brings supported AI tools through the Enterprise Gateway. Security and IT teams can discover applications and MCP servers, approve or block their use, and apply Gateway guardrails, budgets, and access controls to routed traffic.

Edge supports macOS, Windows, and Linux and can be deployed through existing device-management tools. It is available in **public preview** and requires Bifrost Enterprise.

[Explore Bifrost Edge](https://docs.getbifrost.ai/edge/overview)

[Explore Enterprise](https://docs.getbifrost.ai/enterprise/overview) · [Book a demo](https://www.getmaxim.ai/bifrost/book-a-demo)

## Build with AI coding assistants

Using Claude Code, Codex, Cursor, or another coding assistant to integrate Bifrost? Give it the documentation for the task you are working on.

| Task | Reference |
|---|---|
| Find current documentation | [Machine-readable documentation index](https://docs.getbifrost.ai/llms.txt) |
| Start and configure a Gateway | [Gateway setup](https://docs.getbifrost.ai/quickstart/gateway/setting-up) |
| Connect an application | [SDK integrations](https://docs.getbifrost.ai/integrations/what-is-an-integration) |
| Configure provider credentials and routing | [Provider configuration](https://docs.getbifrost.ai/quickstart/gateway/provider-configuration) |
| Connect agents to MCP tools | [MCP documentation](https://docs.getbifrost.ai/mcp/overview) |
| Run coding agents through Bifrost | [Bifrost CLI](https://docs.getbifrost.ai/quickstart/cli/getting-started) |
| Modify Bifrost’s source code | [Contributor setup](https://docs.getbifrost.ai/contributing/setting-up-repo) and [repository agent guidance](https://github.com/maximhq/bifrost/blob/dev/AGENTS.md) |

Include your Bifrost version, SDK, provider, and deployment method when asking for implementation help. This gives the assistant the context to select the right endpoints, credentials, and configuration.

## Repository layout

Bifrost separates the core library, HTTP gateway, web interface, and plugins so they can be developed and extended independently.

| Directory | What lives here |
|---|---|
| `core/` | Core Go library, provider integrations, and MCP implementation |
| `transports/bifrost-http/` | HTTP gateway and API handlers |
| `framework/` | Shared infrastructure for configuration, logs, and storage |
| `plugins/` | Extensions for governance, logging, caching, and other request handling |
| `ui/` | Gateway web interface |

See the [contributing guide](https://docs.getbifrost.ai/contributing/setting-up-repo) for development setup and the [repository agent guidance](https://github.com/maximhq/bifrost/blob/dev/AGENTS.md) for a detailed codebase map.

## Community and contributing

Questions about setup, integrations, or operating Bifrost? Join the [Discord community](https://discord.gg/exN5KAydbU).

We welcome contributions to code, documentation, integrations, and examples. Start with the [contributing guide](https://docs.getbifrost.ai/contributing/setting-up-repo) for local setup, development conventions, and testing.

[Report a bug](https://github.com/maximhq/bifrost/issues) · [Join a discussion](https://github.com/maximhq/bifrost/discussions)

## Security

To report a vulnerability, follow our [security policy](https://github.com/maximhq/bifrost/blob/dev/SECURITY.md). Please use the reporting channel described there rather than posting sensitive details in a public issue.

## License

The open-source Bifrost Gateway is licensed under [Apache 2.0](https://github.com/maximhq/bifrost/blob/dev/LICENSE). Bifrost Enterprise is available under a separate commercial license.

Built and maintained by [Maxim AI](https://github.com/maximhq).
