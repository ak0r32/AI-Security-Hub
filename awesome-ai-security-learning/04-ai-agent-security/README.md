
# AI Agent Security

A curated learning roadmap for understanding, testing, and securing AI agents, autonomous workflows, tool-using LLMs, and multi-agent systems.

## Table of Contents

- [1. Learning Objectives](#1-learning-objectives)
- [2. AI Agent Fundamentals](#2-ai-agent-fundamentals)
- [3. AI Agent Architecture](#3-ai-agent-architecture)
- [4. AI Agent Attack Surface](#4-ai-agent-attack-surface)
- [5. Major AI Agent Security Risks](#5-major-ai-agent-security-risks)
- [6. Essential Security Concepts](#6-essential-security-concepts)
- [7. Tools and Frameworks](#7-tools-and-frameworks)
- [8. Hands-On Labs](#8-hands-on-labs)
- [9. Secure AI Agent Development](#9-secure-ai-agent-development)
- [10. Multi-Agent Security](#10-multi-agent-security)
- [11. Research and Learning Resources](#11-research-and-learning-resources)
- [12. Practical Security Checklist](#12-practical-security-checklist)
- [13. Knowledge Check](#13-knowledge-check)
- [14. Suggested Learning Path](#14-suggested-learning-path)

---

## 1. Learning Objectives

After completing this section, you should be able to:

- Explain how AI agents differ from traditional chatbots.
- Understand tool calling, planning, memory, and autonomous execution.
- Identify common attack paths in agentic AI applications.
- Test agents for unauthorized tool use and excessive permissions.
- Understand indirect prompt injection and memory poisoning.
- Secure APIs, tools, credentials, and agent execution environments.
- Design human approval controls for sensitive actions.
- Evaluate the security of single-agent and multi-agent systems.

## 2. AI Agent Fundamentals

### What is an AI agent?

An AI agent is a system that uses an AI model to interpret inputs, decide what to do, and potentially execute actions through tools or external systems.

Unlike a basic chatbot, an agent may interact with databases, APIs, browsers, files, code interpreters, or other agents.

### Core concepts

| Concept | Description |
|---|---|
| LLM | Language model used for reasoning and generating outputs |
| Tool calling | Mechanism for requesting external functions or services |
| Planning | Breaking a goal into smaller steps |
| Memory | Storing information for current or future tasks |
| State | Information describing the current workflow |
| Orchestration | Coordinating tools, models, and workflow steps |
| Autonomy | Degree to which an agent acts without human approval |
| Human-in-the-loop | Human review before or during sensitive actions |
| Multi-agent system | Multiple agents collaborating on a task |

### Recommended prerequisites

Before studying agent security, understand:

- Python programming
- REST APIs and authentication
- LLM fundamentals and prompt injection
- RAG and vector databases
- OAuth, API keys, and access control
- Docker and basic application security

## 3. AI Agent Architecture

A typical agentic application can be represented as:

```text
                  User Request
                       |
                       v
                 Input Validation
                       |
                       v
                  Agent / LLM
                       |
              Planning and Decisions
                       |
                       v
                 Policy Gateway
                       |
             +---------+---------+
             |         |         |
             v         v         v
          Search      API      Database
             |         |         |
             +---------+---------+
                       |
                       v
                Result Validation
                       |
                       v
                  Final Response
```

Security controls should exist at every boundary, not only inside the LLM prompt.

### Important components

- **Model layer:** Processes requests and generates decisions.
- **Orchestration layer:** Manages workflow execution.
- **Tool layer:** Provides access to APIs, files, browsers, and other services.
- **Memory layer:** Stores conversation history and task information.
- **Identity layer:** Determines which user or agent is making a request.
- **Policy layer:** Enforces permissions and approval requirements.
- **Execution layer:** Runs code or performs external actions.
- **Monitoring layer:** Records relevant security events.

## 4. AI Agent Attack Surface

An agent can introduce security risks across several components.

| Component | Example attack surface |
|---|---|
| User input | Malicious instructions or crafted requests |
| Retrieved content | Instructions hidden in documents or web pages |
| Model output | Untrusted tool arguments or generated code |
| Tools | Unauthorized API calls or destructive operations |
| Memory | Poisoned or cross-user information |
| Credentials | Exposed API keys or excessive OAuth scopes |
| Planning | Unsafe action sequences |
| Workflow | Missing approval or validation steps |
| Agent communication | Forged or manipulated messages |
| Execution environment | Insecure file access or code execution |

**Key principle:** An LLM should not be treated as a security boundary. Enforce security requirements in trusted application code.

## 5. Major AI Agent Security Risks

### 5.1 Excessive Agency

An agent has more permissions or autonomy than required for its task.

**Example:** A support agent that only needs to read order details can also issue refunds and delete customer accounts.

**Security controls:**
- Apply least privilege.
- Separate read and write permissions.
- Restrict high-impact actions.
- Require approval for sensitive operations.
- Set transaction and action limits.

### 5.2 Indirect Prompt Injection

An agent processes untrusted content containing instructions intended to manipulate its behavior.

**Example:** A browsing agent reads a web page containing hidden instructions that attempt to redirect the agent or disclose private data.

**Security controls:**
- Treat retrieved content as untrusted data.
- Separate instructions from external content.
- Restrict tools available during retrieval.
- Validate actions independently of model reasoning.
- Test with adversarial documents and web pages.

Prompt wording alone cannot reliably prevent every prompt-injection attack.

### 5.3 Tool Misuse

An agent calls a legitimate tool with an unauthorized target, argument, or action.

**Example:** An agent with access to an email tool sends confidential information to an unintended recipient.

**Security controls:**
- Validate arguments using strict schemas.
- Authorize every action server-side.
- Allowlist permitted operations and destinations.
- Verify user identity and resource ownership.
- Require confirmation for external or irreversible actions.

### 5.4 Memory Poisoning

An attacker causes malicious or incorrect information to be stored in an agent's persistent memory.

**Example:** An agent stores a fabricated instruction that influences future tasks.

**Security controls:**
- Validate information before storing it.
- Track the source and time of memory entries.
- Separate user-specific memory.
- Prevent untrusted content from becoming privileged instructions.
- Support review, correction, and deletion of stored data.
- Test whether poisoned memory affects future decisions.

### 5.5 Unauthorized Data Access

An agent retrieves or exposes information outside the current user's permissions.

**Example:** A customer-support agent returns another customer's order details because a database query lacks ownership checks.

**Security controls:**
- Enforce authorization in the data layer.
- Apply tenant and user filters server-side.
- Avoid relying on model-generated filters alone.
- Test cross-user and cross-tenant access.
- Minimize sensitive information in prompts and logs.

### 5.6 Insecure Code Execution

An agent generates code and executes it in an unsafe environment.

**Example:** A data-analysis agent executes untrusted Python with access to environment variables and local files.

**Security controls:**
- Use isolated execution environments.
- Restrict filesystem and network access.
- Avoid exposing host credentials.
- Apply CPU, memory, and execution-time limits.
- Use disposable containers or sandboxes where appropriate.
- Require review before deploying generated code.

### 5.7 Goal Hijacking and Unsafe Planning

An agent follows a manipulated objective or creates an unsafe sequence of actions.

**Example:** An agent is asked to summarize a document but instead attempts to upload files to an external service.

**Security controls:**
- Define explicit task boundaries.
- Restrict available actions by task.
- Validate every action against the original authorized objective.
- Stop workflows when policy violations occur.
- Limit action count and execution time.

### 5.8 Credential and Secret Exposure

An agent may reveal or misuse API keys, tokens, passwords, or internal configuration.

**Security controls:**
- Store secrets in a dedicated secret manager.
- Avoid placing credentials in prompts.
- Use short-lived credentials when practical.
- Restrict credential scope.
- Redact secrets from logs.
- Rotate exposed credentials immediately.

### 5.9 Denial of Service and Resource Abuse

An agent can enter loops, make repeated tool calls, or trigger expensive model requests.

**Security controls:**
- Set maximum tool-call counts.
- Apply timeouts and rate limits.
- Set token and spending budgets.
- Detect repeated or circular actions.
- Add circuit breakers and cancellation mechanisms.

### 5.10 Multi-Agent Trust Failures

Agents may pass malicious instructions or unverified claims to other agents.

**Security controls:**
- Authenticate agent-to-agent requests.
- Define clear trust boundaries.
- Validate messages and tool results.
- Limit permissions independently for each agent.
- Preserve provenance for information passed between agents.
- Require independent policy checks before consequential actions.

For additional risk categories, consult the current OWASP GenAI and agentic security resources in the learning section below.

## 6. Essential Security Concepts

### 6.1 Least Privilege

Give each agent and tool only the permissions needed for its specific task.

For example:

```text
Research Agent:
- Read approved public websites
- No access to private customer records
- No permission to send emails

Email Drafting Agent:
- Read approved message context
- Draft emails
- Cannot send without authorization
```

### 6.2 Zero Trust for Tool Calls

Do not automatically trust a tool call because the model generated it.

For every tool invocation, check:

1. Who initiated the request?
2. Is the user authorized?
3. Is the tool allowed for this task?
4. Are the arguments valid?
5. Is the target resource permitted?
6. Does the action require human approval?
7. Can the action be audited?

### 6.3 Human Approval

Require explicit approval for high-impact actions, such as:

- Sending sensitive emails
- Making financial transactions
- Deleting records
- Changing access permissions
- Publishing content publicly
- Executing production changes

Approval must be enforced by the application, not merely requested through a model-generated message.

### 6.4 Provenance and Trust Labels

Track where information originated.

Useful labels include:

- Trusted application configuration
- Authenticated user input
- External web content
- Retrieved documents
- Tool output
- Unverified agent-generated content

Trust labels are useful only when application logic enforces the relevant security rules.

## 7. Tools and Frameworks

Use these tools in authorized testing environments. Their capabilities and licensing may vary by version.

| Tool or framework | Learning purpose | Official resource |
|---|---|---|
| LangChain | Build tool-using agents and workflows | https://docs.langchain.com/ |
| LangGraph | Build stateful, controlled agent workflows | https://docs.langchain.com/oss/python/langgraph/overview |
| Microsoft PyRIT | Assess generative AI system risks | https://github.com/Azure/PyRIT |
| garak | Test LLMs for vulnerabilities | https://github.com/NVIDIA/garak |
| Promptfoo | Evaluate prompts, agents, and LLM applications | https://www.promptfoo.dev/docs/ |
| OWASP GenAI Security Project | Study GenAI and agentic security guidance | https://genai.owasp.org/ |
| Docker | Isolate application components and workloads | https://docs.docker.com/ |
| Open Policy Agent | Implement policy-based authorization | https://www.openpolicyagent.org/docs/latest/ |

**Important:** A framework is not automatically secure because it includes guardrails or supports human approval. Verify how controls are configured and enforced.

## 8. Hands-On Labs

Perform these exercises only against systems you own or have explicit permission to test.

### Lab 1: Build a Read-Only Research Agent

**Goal:** Create an agent that searches approved public sources and summarizes results.

Tasks:
- Define a small set of permitted tools.
- Validate tool arguments.
- Prevent access to local secrets.
- Log tool invocations.
- Test malicious instructions in retrieved content.

**Success criteria:** The agent completes normal research tasks while refusing unauthorized operations through application-enforced controls.

### Lab 2: Test Excessive Agency

**Goal:** Determine whether an agent can perform actions beyond its intended role.

Tasks:
- Define the agent's intended permissions.
- Create mock read, update, and delete tools.
- Attempt unauthorized actions in a controlled test.
- Add server-side permission checks.
- Repeat the tests.

**Success criteria:** Unauthorized actions are blocked even if the model requests them.

### Lab 3: Test Indirect Prompt Injection

**Goal:** Evaluate how an agent handles untrusted retrieved content.

Tasks:
- Create a test document containing benign task instructions and a simulated malicious instruction.
- Ask the agent to summarize the document.
- Observe whether it attempts unauthorized tool calls.
- Add tool restrictions and action validation.
- Repeat the test with different document formats.

**Success criteria:** The agent treats the document as content to analyze, and security controls block any prohibited actions.

### Lab 4: Test Memory Isolation

**Goal:** Check whether one user's information can influence another user's session.

Tasks:
- Create two synthetic users.
- Store separate, harmless test memories.
- Query each session independently.
- Attempt cross-user retrieval.
- Add server-side access controls and tenant filters.

**Success criteria:** Each user can access only authorized memory.

### Lab 5: Test Tool Argument Validation

**Goal:** Verify that a tool rejects malformed or unauthorized requests.

Tasks:
- Define a tool with a strict input schema.
- Test missing, unexpected, and invalid arguments.
- Test unauthorized resource identifiers.
- Enforce resource ownership checks.
- Record rejected calls.

**Success criteria:** Invalid and unauthorized requests fail safely.

### Lab 6: Build a Human-in-the-Loop Workflow

**Goal:** Prevent high-impact actions from executing without approval.

Tasks:
- Create a mock email-sending tool.
- Allow the agent to prepare a draft.
- Require explicit approval before sending.
- Verify that approval is linked to the intended action and recipient.
- Reject changes made after approval until reviewed again.

**Success criteria:** Drafting is permitted, but sending cannot occur without valid approval.

## 9. Secure AI Agent Development

### 9.1 Example: Policy-Gated Tool Execution

The following Python example demonstrates the basic principle of checking a tool call before execution. It is an educational example, not a complete production authorization system.

```python
from typing import Any

ALLOWED_TOOLS = {"search_public_docs"}

def execute_tool(
    tool_name: str,
    arguments: dict[str, Any],
    user_authorized: bool
) -> dict[str, Any]:
    if not user_authorized:
        return {"error": "Unauthorized request"}

    if tool_name not in ALLOWED_TOOLS:
        return {"error": "Tool is not permitted"}

    if set(arguments) != {"query"}:
        return {"error": "Invalid arguments"}

    query = arguments["query"]

    if not isinstance(query, str) or not query.strip():
        return {"error": "Query must be a non-empty string"}

    # Call a real, separately secured search implementation here.
    return {
        "status": "approved",
        "query": query
    }

result = execute_tool(
    tool_name="search_public_docs",
    arguments={"query": "AI agent security"},
    user_authorized=True
)

print(result)
```

In production, authorization must be based on authenticated identity, server-side policy, resource ownership, and the current task. Do not accept a client-supplied Boolean as proof of authorization.

### 9.2 Security Engineering Checklist

- [ ] Authenticate users and services.
- [ ] Authorize each tool call independently.
- [ ] Enforce least privilege.
- [ ] Validate arguments with strict schemas.
- [ ] Treat external content as untrusted.
- [ ] Separate user data and agent memory.
- [ ] Isolate code execution.
- [ ] Protect secrets and credentials.
- [ ] Apply timeouts, rate limits, and budget limits.
- [ ] Require approval for sensitive operations.
- [ ] Log security-relevant actions without unnecessarily storing sensitive data.
- [ ] Test failure paths and adversarial inputs.
- [ ] Provide safe cancellation and recovery.
- [ ] Review dependencies and third-party tools.
- [ ] Reassess controls when models, tools, or workflows change.

## 10. Multi-Agent Security

Multi-agent systems introduce additional trust and authorization boundaries.

### Common architecture

```text
                  User Request
                       |
                       v
                 Coordinator Agent
                  /      |      \
                 v       v       v
             Research  Analysis  Reporting
               Agent    Agent     Agent
                 \       |       /
                  v      v      v
                Policy Enforcement
                       |
                       v
                 Final Response
```

### Security questions

- Can one agent invoke tools assigned to another?
- Can an untrusted agent change the task of the coordinator?
- Are messages authenticated and validated?
- Can agents share confidential memory?
- Are permissions enforced independently?
- Can a compromised agent trigger an irreversible action?
- Are tool results checked before being passed to another agent?

### Recommended controls

1. Give each agent a clearly defined role.
2. Restrict tools and data by role.
3. Validate messages between agents.
4. Keep secrets outside model-visible context.
5. Enforce authorization at the service boundary.
6. Limit recursion, delegation, and tool-call counts.
7. Require approval for sensitive actions.
8. Test failures and compromised-agent scenarios.

## 11. Research and Learning Resources

### Official security guidance

- [OWASP GenAI Security Project](https://genai.owasp.org/)
- [OWASP Top 10 for LLM Applications](https://genai.owasp.org/llm-top-10/)
- [NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework)
- [MITRE ATLAS](https://atlas.mitre.org/)
- [Google Secure AI Framework (SAIF)](https://saif.google/)

Check each project's current publications and versions before relying on a specific taxonomy or recommendation.

### Agent frameworks and documentation

- [LangGraph documentation](https://docs.langchain.com/oss/python/langgraph/overview)
- [Microsoft AutoGen](https://microsoft.github.io/autogen/)
- [CrewAI documentation](https://docs.crewai.com/)
- [OpenAI API documentation](https://platform.openai.com/docs/)

### Research topics to explore

Search academic papers and technical reports on:

- Indirect prompt injection in tool-using agents
- Excessive agency and least-privilege enforcement
- Persistent memory poisoning
- Agent identity and authorization
- Secure sandboxing for AI-generated code
- Multi-agent trust and communication
- Automated red teaming of agentic systems
- Evaluation of human approval mechanisms

Useful research sources:

- [arXiv](https://arxiv.org/)
- [Google Scholar](https://scholar.google.com/)
- [USENIX Security](https://www.usenix.org/conferences)
- [IEEE Xplore](https://ieeexplore.ieee.org/)

## 12. Practical Security Checklist

Use this checklist when reviewing an AI agent.

### Identity and permissions
- [ ] Does every user have a verified identity?
- [ ] Are permissions enforced outside the model?
- [ ] Are tools restricted to necessary operations?

### Input and retrieval
- [ ] Is untrusted content clearly separated from trusted instructions?
- [ ] Are retrieved documents and tool results validated?
- [ ] Are cross-user data boundaries enforced?

### Execution
- [ ] Are code execution and file access isolated?
- [ ] Are destructive operations gated?
- [ ] Are timeouts and resource limits configured?

### Memory and privacy
- [ ] Is memory scoped to the correct user or tenant?
- [ ] Can untrusted content alter privileged configuration?
- [ ] Are secrets and sensitive data protected?

### Monitoring and response
- [ ] Are security-relevant tool calls logged?
- [ ] Can suspicious workflows be stopped?
- [ ] Are tests repeated after major changes?

## 13. Knowledge Check

1. What makes an AI agent different from a standard chatbot?
2. Why should an LLM not be the only authorization mechanism?
3. What is excessive agency?
4. How can indirect prompt injection affect an agent?
5. Why is memory isolation important?
6. What security controls should protect tool calls?
7. When should a human approve an agent's action?
8. Why is sandboxing important for code-executing agents?
9. What additional risks appear in multi-agent systems?
10. How can you test whether an agent follows least privilege?

### Suggested answers

1. An agent can use tools and execute multi-step workflows.
2. Model outputs are not a reliable enforcement boundary; trusted application code must enforce permissions.
3. Excessive agency means an agent has more permissions or autonomy than necessary.
4. Malicious retrieved content may influence the agent's decisions or tool use.
5. It prevents unauthorized disclosure or influence between users.
6. Authentication, authorization, schema validation, resource checks, and auditing.
7. Before high-impact, sensitive, external, or irreversible actions.
8. It limits the damage caused by unsafe generated code.
9. Trust failures, unauthorized delegation, message manipulation, and permission leakage.
10. Attempt prohibited actions in a controlled environment and verify that server-side controls block them.

## 14. Suggested Learning Path

Follow this sequence to build practical skills:

1. Learn Python, APIs, authentication, and access control.
2. Build a simple tool-using agent.
3. Add strict tool schemas and server-side authorization.
4. Study prompt injection and untrusted retrieval.
5. Test memory isolation and data access controls.
6. Add sandboxing, resource limits, and human approval.
7. Build a small multi-agent workflow.
8. Create an adversarial test suite.
9. Document findings, mitigations, and remaining limitations.
10. Publish a portfolio project using synthetic data and a safe test environment.

---

## Contribution Guidelines

Contributions are welcome!

You can contribute by adding:

- New agent-security research papers
- Secure coding examples
- Open-source testing tools
- Authorized lab exercises
- Threat models and defensive checklists
- Case studies with reliable sources

Please verify links, provide source references, and avoid publishing real credentials, private data, or instructions for attacking systems without authorization.
