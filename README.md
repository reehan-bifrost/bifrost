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
  <a href="https://getmaxim.ai/llm-gateway">Bifrost LLM Gateway</a> |
  <a href="https://getmaxim.ai/mcp-gateway">Bifrost MCP Gateway</a> |
  <a href="https://getmaxim.ai/edge">Bifrost Edge</a> |
  <a href="https://www.getmaxim.ai/enterprise">Enterprise Tier</a> |
  <a href="https://docs.getbifrost.ai">Docs</a> |
  <a href="https://docs.getbifrost.ai/changelogs/v2.0.0">Changelogs</a> |
</p>

Bifrost, by Maxim AI, is an AI gateway with an Apache 2.0 open-source core, written in Go. It enables enterprises to route, govern, and secure every AI request its people and systems make all in one place.

Bifrost unifies LLM gateway, MCP gateway, and Agents gateway capabilities into a single platform.

<p align="center">
  <a href="#quick-start">Quick start</a> ·
  <a href="#connect-your-applications-and-agents">Integrations</a> ·
  <a href="#performance">Benchmarks</a> ·
  <a href="https://discord.gg/exN5KAydbU">Discord</a>
</p>

## Why Bifrost AI Gateway

Bifrost is built for enterprises running mission-critical AI workloads that require top-tier performance, scalability, and reliability

- Built in Go, it offers ultra low latency, with gateway overhead not exceeding microseconds
- Peer-to-peer node clusters guarantee high availability and uptime. Adding nodes scales horizontally without the cluster becoming a bottleneck
- Routing that adapts in real time with Adaptive Load Balancing
- Deploy via a single binary, anywhere. It is air-gapped, by default, runs entirely in your infrastructure and no data, not even telemetry leaves your environment

### Core capabilities

#### [LLM Gateway](https://getmaxim.ai/llm-gateway)

- **Drop-in replacement**: Existing OpenAI, Anthropic, Bedrock, Google GenAI, LangChain, and LiteLLM SDK code continues to work with just a base URL change. Also includes a [LiteLLM migration script](https://docs.getbifrost.ai/migration-guides/litellm).
- **Unified model access**: Access [10,000+ models across 30+ providers](https://docs.getbifrost.ai/providers/supported-providers/overview) through one OpenAI-compatible API, with routing rules, model aliases, retries, and fallback across providers and model families.

#### [MCP Gateway](https://getmaxim.ai/mcp-gateway)

- Connect MCP servers for [tool discovery and execution](https://docs.getbifrost.ai/mcp/overview), with per-user authentication and tool filtering.
- Combine multiple tools into Virtual MCPs with their own endpoints and use [Code Mode](https://docs.getbifrost.ai/mcp/code-mode) to orchestrate tools in a Starlark sandbox while keeping intermediate results out of the model’s context.

#### [AI Governance](https://www.getmaxim.ai/ai-governance)

- Control model and MCP access, enforce budgets and rate limits with virtual keys.
- [Bifrost Enterprise](https://getmaxim.ai/enterprise) connects the gateway to your identity provider for SSO, enables user provisioning via OIDC and/or inbound SCIM, offers role-based access, and reusable Access Profiles, so access follows the people and teams in your organization.

#### [Guardrails](https://www.getmaxim.ai/ai-guardrails)

- Apply [Enterprise guardrails](https://docs.getbifrost.ai/enterprise/guardrails) to requests and responses, with content safety checks, personal data and secrets detection, redaction, and integrations with external guardrail providers.
- Validate inputs and outputs in real time to detect, block, or redact sensitive information.

#### [Observability](https://www.getmaxim.ai/ai-observability)

- Inspect requests, token usage, costs, and latency through request logs, Prometheus metrics, and OpenTelemetry traces.
- Connect AI traffic to your existing monitoring and data systems through integrations with Datadog, Kafka, BigQuery, Pub/Sub, and Splunk.

#### [Deployment and extensibility](https://docs.getbifrost.ai/enterprise/overview)

- Self-host Bifrost as an HTTP gateway or embed its Go SDK, and extend request handling with plugins across the request lifecycle.
- Enterprise adds high-availability clustering and supports deployment in your VPC, on-premises, or in air-gapped environments.

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

| SDK, application or harness | Start here |
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

## Performance

Bifrost adds virtually zero overhead to your AI requests. In sustained 5,000 RPS benchmarks, the gateway added only **11 µs** of overhead per request.

| Metric | t3.medium | t3.xlarge | Improvement |
|--------|-----------|-----------|-------------|
| Added latency (Bifrost overhead) | 59 µs | **11 µs** | **-81%** |
| Success rate @ 5k RPS | 100% | 100% | No failed requests |
| Avg. queue wait time | 47 µs | **1.67 µs** | **-96%** |
| Avg. request latency (incl. provider) | 2.12 s | **1.61 s** | **-24%** |

**Key Performance Highlights:**

- **Perfect Success Rate** - 100% request success rate even at 5k RPS
- **Minimal Overhead** - Less than 15 µs additional latency per request
- **Efficient Queuing** - Sub-microsecond average wait times
- **Fast Key Selection** - ~10 ns to pick weighted API keys

**Complete Benchmarks:** [Performance Analysis](https://docs.getbifrost.ai/benchmarking/getting-started)

## Open source vs Enterprise

| | Open-source Gateway | Bifrost Enterprise |
|---|---|---|
| Model access | Provider integrations, SDK adapters, routing, retries, fallbacks, and weighted load balancing | Includes the open-source capabilities |
| MCP | Server connections, tool filtering, authentication, Agent Mode, and Code Mode | Adds organizational access policies and enterprise scoping |
| Governance | Virtual keys, budgets, and rate limits | Adds identity-provider integration, access profiles, roles, and projects |
| Security and operations | Self-hosted gateway with configurable access and logging | Adds guardrails, sensitive-data redaction, signed audit logs, external secret management, and high availability |
| Employee devices | Configure supported clients to use the Gateway | Extend coverage with Bifrost Edge |
| License | Apache 2.0 | Commercial enterprise license |

Both editions run in your infrastructure. See the [Enterprise documentation](https://docs.getbifrost.ai/enterprise/overview) for the full scope and deployment requirements.

## Open-source capabilities

### Route requests across models and providers

Connect to OpenAI, Anthropic, AWS Bedrock, Google Vertex, Azure, and other [supported providers](https://docs.getbifrost.ai/providers/supported-providers/overview) through a common API.

- **[Routing and model aliases](https://docs.getbifrost.ai/features/governance/routing)** - choose request destinations through routing rules and expose stable model names to applications.
- **[Retries and fallbacks](https://docs.getbifrost.ai/features/fallbacks)** - retry failed requests and configure alternative providers or models.
- **[Weighted load balancing](https://docs.getbifrost.ai/features/keys-management)** - distribute requests across configured keys and providers.
- **[Complexity routing](https://docs.getbifrost.ai/features/governance/complexity-router)** - classify prompt complexity and route requests to an appropriate model tier.
- **[Multimodal requests](https://docs.getbifrost.ai/quickstart/gateway/multimodal)** - work with text, images, audio, streaming, and reranking where supported.

### Connect and govern MCP tools

Bifrost [connects to MCP servers](https://docs.getbifrost.ai/mcp/overview) and can expose connected tools through a gateway endpoint for external MCP clients.

- **[Server connections](https://docs.getbifrost.ai/mcp/overview)** - connect over STDIO, HTTP, or SSE.
- **[Tool filtering](https://docs.getbifrost.ai/features/governance/mcp-tools)** - control which tools are available to clients and requests.
- **[Authentication](https://docs.getbifrost.ai/mcp/auth/overview)** - connect to upstream servers using shared credentials, OAuth, or per-user authentication.
- **[Agent Mode](https://docs.getbifrost.ai/mcp/agent-mode)** - configure automatic tool execution for the tools you allow.
- **[Code Mode](https://docs.getbifrost.ai/mcp/code-mode)** - let a model orchestrate tools through sandboxed code, reducing the need to carry every tool definition and intermediate result in context.

[Tool execution](https://docs.getbifrost.ai/mcp/tool-execution) and automatic approval are configurable. Connecting a server does not mean every tool should be available to every caller.

### Control spending and inspect traffic

- **[Virtual keys](https://docs.getbifrost.ai/features/governance/virtual-keys)** - issue keys with access restrictions, [budgets, and rate limits](https://docs.getbifrost.ai/features/governance/budget-and-limits).
- **[Semantic caching](https://docs.getbifrost.ai/features/semantic-caching)** - reuse responses for sufficiently similar requests where that fits your application.
- **[Request logs](https://docs.getbifrost.ai/features/observability/default)** - inspect token usage, cost, and latency through the built-in interface.
- **[Metrics and traces](https://docs.getbifrost.ai/features/observability/prometheus)** - export through [Prometheus](https://docs.getbifrost.ai/features/telemetry) and [OpenTelemetry](https://docs.getbifrost.ai/features/observability/otel), and configure which request and response content is recorded.

### Extend the Gateway and manage reusable assets

- **[Custom plugins](https://docs.getbifrost.ai/plugins/getting-started)** - add custom request and response handling.
- **[Prompt Repository](https://docs.getbifrost.ai/features/prompt-repository/playground)** - version prompts and test them in the playground.
- **[Skills Repository](https://docs.getbifrost.ai/features/skills-repository)** - create, version, and distribute reusable skills to compatible coding agents.

## Bifrost Enterprise

As AI usage spreads across teams, security and governance have to adapt to the organization's structure: users, roles, applications, and data boundaries.

[Bifrost Enterprise](https://getmaxim.ai/enterprise) provides the required controls to manage this while keeping the Gateway in your infrastructure.

### Govern access through your existing identity provider

- **[User provisioning](https://docs.getbifrost.ai/enterprise/advanced-governance)** - connect your identity provider for sign-in and provisioning.
- **[Access Profiles](https://docs.getbifrost.ai/enterprise/access-profiles)** - define reusable provider, model, MCP, budget, and rate-limit policies, then assign them to users directly or through roles and identity mappings.
- **[Role-based permissions](https://docs.getbifrost.ai/enterprise/rbac)** - control administration and apply enterprise access policies to Virtual MCPs.
- **[Projects](https://docs.getbifrost.ai/enterprise/projects)** - give work its own access scope, budget, and reporting.

### Apply security policies to requests and responses

- **[Guardrails](https://docs.getbifrost.ai/enterprise/guardrails)** - configure content safety, personal data, and secrets policies, and connect services including AWS Bedrock Guardrails, Azure Content Safety, and Google Model Armor.
- **[Redaction controls](https://docs.getbifrost.ai/enterprise/guardrails/redaction#redaction-strategies)** - block or redact content according to your policies, with separate controls for live payloads, stored logs, and exported traces.

### Keep an audit trail and control credentials

- **[Audit logs](https://docs.getbifrost.ai/enterprise/audit-logs)** - record administrative changes through signed, unalterable logs.
- **[Secret management](https://docs.getbifrost.ai/enterprise/secret-management)** - connect external secret stores for provider credentials.
- **[Log exports](https://docs.getbifrost.ai/enterprise/log-exports)** - fit exports to your existing storage and monitoring systems, including a native [Datadog connector](https://docs.getbifrost.ai/features/observability/datadog).

### Run across nodes and private environments

- **[Clustering](https://docs.getbifrost.ai/enterprise/clustering)** - run multiple nodes for high availability.
- **[Adaptive load balancing](https://docs.getbifrost.ai/enterprise/adaptive-load-balancing)** - respond to provider health, with circuit breakers to handle degradation.
- **[Private deployments](https://docs.getbifrost.ai/enterprise/invpc-deployments)** - deploy in your VPC, on-premises, or in an air-gapped environment. Upstream models and external services remain destinations you configure; an isolated deployment requires those dependencies to fit the same network boundary.

### Extend governance to employee devices with Bifrost Edge

Employees use AI through desktop applications, browsers, coding agents, and the MCP servers connected to those tools. AI traffic from these apps does not reach the Gateway, unless specifically configured.

[Bifrost Edge](https://getmaxim.ai/edge) is a lightweight service that runs on employee machines. It picks up AI traffic from the tools people already use and sends it through the Bifrost Gateway. This enables security and IT teams to discover applications and MCP servers, approve or block their use, and apply Gateway guardrails, budgets, and access controls to routed traffic.

Edge supports macOS, Windows, and Linux and can be deployed through existing device-management tools. It requires and works only with Bifrost Enterprise.

[Bifrost Edge documentation](https://docs.getbifrost.ai/edge/overview) · [Book a demo](https://www.getmaxim.ai/bifrost/book-a-demo)

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
