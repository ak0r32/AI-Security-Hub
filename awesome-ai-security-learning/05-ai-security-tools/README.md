
# AI Security Tools

A curated collection of open-source tools, frameworks, and resources for testing, evaluating, and securing AI applications, large language models (LLMs), retrieval-augmented generation (RAG) systems, and AI agents.

## Table of Contents

- [1. Introduction](#1-introduction)
- [2. AI Security Testing Categories](#2-ai-security-testing-categories)
- [3. LLM Red Teaming Tools](#3-llm-red-teaming-tools)
- [4. Prompt Injection Testing](#4-prompt-injection-testing)
- [5. AI Application Evaluation](#5-ai-application-evaluation)
- [6. RAG Security Tools](#6-rag-security-tools)
- [7. AI Agent Security](#7-ai-agent-security)
- [8. Guardrails and Defensive Frameworks](#8-guardrails-and-defensive-frameworks)
- [9. Privacy and Data Protection](#9-privacy-and-data-protection)
- [10. Infrastructure and Deployment Security](#10-infrastructure-and-deployment-security)
- [11. Practical Labs](#11-practical-labs)
- [12. Building an AI Security Testing Pipeline](#12-building-an-ai-security-testing-pipeline)
- [13. Tool Selection Guide](#13-tool-selection-guide)
- [14. Learning Roadmap](#14-learning-roadmap)
- [15. References](#15-references)

---

## 1. Introduction

AI security tools help security engineers identify weaknesses in systems that use machine learning, LLMs, RAG, and autonomous agents.

Traditional application security tools remain important, but AI applications introduce additional risks, including:

- Prompt injection
- Sensitive information disclosure
- Insecure output handling
- Training data and knowledge-base poisoning
- Excessive agent permissions
- Unsafe tool execution
- Model denial of service
- Privacy and data leakage
- Insecure AI supply chains

No single tool detects every AI security issue. Combine automated testing, manual review, threat modeling, and application-level security controls.

## 2. AI Security Testing Categories

| Category | Purpose |
|---|---|
| LLM red teaming | Probe models for security weaknesses |
| Prompt injection testing | Test whether malicious instructions influence behavior |
| Vulnerability scanning | Identify known classes of AI application weaknesses |
| Model evaluation | Measure model behavior and response quality |
| RAG evaluation | Test retrieval quality, grounding, and information boundaries |
| Agent security | Test tools, permissions, memory, and action execution |
| Guardrails | Apply input, output, and workflow controls |
| Privacy testing | Assess sensitive-data exposure and memorization risks |
| Infrastructure security | Protect APIs, containers, dependencies, and deployment environments |

## 3. LLM Red Teaming Tools

### 3.1 Microsoft PyRIT

**Purpose:** Assess generative AI systems through automated and structured red-teaming workflows.

Useful for:
- Designing adversarial test scenarios
- Evaluating model responses
- Organizing red-team experiments
- Assessing risks across AI application workflows

Repository: https://github.com/Azure/PyRIT

Documentation: https://azure.github.io/PyRIT/

### 3.2 garak

**Purpose:** Probe LLMs for vulnerabilities and undesirable behaviors.

Useful for:
- Running model vulnerability probes
- Testing different failure categories
- Generating structured assessment results
- Comparing model behavior across tests

Repository: https://github.com/NVIDIA/garak

### 3.3 Inspect AI

**Purpose:** Evaluate AI systems using structured tasks, solvers, and scorers.

Useful for:
- Creating repeatable model evaluations
- Testing model behavior against defined tasks
- Developing security evaluation benchmarks
- Recording results for comparison

Repository: https://github.com/UKGovernmentBEIS/inspect_ai

Documentation: https://inspect.aisi.org.uk/

### 3.4 When to use red-teaming tools

Use red-teaming tools when you need to systematically test model or application behavior. Select probes based on your threat model and verify whether the test covers the complete application, including its tools, retrieval system, and authorization logic.

## 4. Prompt Injection Testing

Prompt injection occurs when malicious instructions influence an AI system through user input, retrieved content, documents, or tool outputs.

### Recommended tools

| Tool | Main use | Official resource |
|---|---|---|
| Promptfoo | LLM application testing and red teaming | https://www.promptfoo.dev/ |
| garak | Model probing and vulnerability testing | https://github.com/NVIDIA/garak |
| PyRIT | Structured generative AI red teaming | https://github.com/Azure/PyRIT |

### What to test

- Direct prompt injection through user input
- Indirect prompt injection through retrieved documents
- Instructions embedded in web pages
- Attempts to disclose system instructions
- Unauthorized tool calls
- Unsafe handling of model-generated output
- Cross-user data exposure
- Attempts to bypass application policies

### Example test scenario

Build a small document-question-answering application using synthetic documents.

1. Add a normal document containing factual information.
2. Add a test document containing a simulated malicious instruction.
3. Ask the application to summarize both documents.
4. Observe whether the application follows the injected instruction.
5. Verify that application-level controls block prohibited actions.
6. Record the result and repeat after implementing mitigations.

**Important:** A model refusing an attack in one test does not prove the application is secure. Test multiple inputs, workflows, and permission boundaries.

## 5. AI Application Evaluation

Security testing should be combined with functional and quality evaluation.

### 5.1 Promptfoo

Useful for:
- Creating repeatable test cases
- Comparing models and prompts
- Testing LLM applications
- Evaluating adversarial inputs
- Integrating evaluations into development workflows

Website: https://www.promptfoo.dev/

Documentation: https://www.promptfoo.dev/docs/

### 5.2 Giskard

Useful for:
- Evaluating AI and machine-learning systems
- Identifying potential model weaknesses
- Testing LLM application behavior
- Organizing evaluation results

Website: https://www.giskard.ai/

Repository: https://github.com/Giskard-AI/giskard

Check the current documentation for supported features and maintenance status before selecting it for a new project.

### 5.3 Evaluation dimensions

Evaluate your application across multiple dimensions:

| Dimension | Example question |
|---|---|
| Security | Can an attacker trigger an unauthorized action? |
| Privacy | Can one user retrieve another user's data? |
| Reliability | Does the system behave consistently? |
| Grounding | Are responses supported by retrieved evidence? |
| Robustness | Does behavior change under adversarial inputs? |
| Authorization | Are access controls enforced for every request? |
| Resource usage | Can repeated requests exhaust available resources? |

## 6. RAG Security Tools

Retrieval-augmented generation systems combine an LLM with a retrieval pipeline that searches external documents or databases.

RAG security requires testing both retrieval behavior and the permissions governing access to documents.

### 6.1 Ragas

Useful for:
- Evaluating retrieval and generation quality
- Measuring faithfulness and relevance
- Building repeatable RAG evaluations

Repository: https://github.com/explodinggradients/ragas

Documentation: https://docs.ragas.io/

**Security note:** High retrieval or answer-quality scores do not establish that a RAG application enforces authorization or prevents data leakage.

### 6.2 DeepEval

Useful for:
- Testing LLM application behavior
- Creating repeatable evaluation suites
- Evaluating RAG pipelines and other LLM workflows

Repository: https://github.com/confident-ai/deepeval

Documentation: https://deepeval.com/docs/

### 6.3 RAG security test cases

Test the following:

- Unauthorized document retrieval
- Cross-tenant information leakage
- Malicious instructions in retrieved content
- Poisoned or misleading documents
- Incorrect document permissions
- Retrieval of stale or revoked information
- Sensitive data in prompts and logs
- Incorrect access filters in vector database queries

### 6.4 Example RAG security test matrix

| Test | Expected result |
|---|---|
| User asks about an authorized document | Only permitted information is returned |
| User asks about another user's private document | Access is denied |
| Retrieved text contains malicious instructions | Instructions do not override application policy |
| A document is revoked | It is no longer accessible through retrieval |
| A query attempts to bypass tenant filtering | Server-side authorization still blocks access |

## 7. AI Agent Security

AI agents can call APIs, execute code, browse websites, and perform multi-step tasks. Their security testing must include tool authorization and action execution, not only model responses.

### 7.1 Agent framework resources

| Resource | Purpose | Link |
|---|---|---|
| LangGraph | Stateful agent workflows | https://docs.langchain.com/oss/python/langgraph/overview |
| AutoGen | Multi-agent application framework | https://microsoft.github.io/autogen/ |
| CrewAI | Agent orchestration | https://docs.crewai.com/ |
| Open Policy Agent | Policy-based authorization | https://www.openpolicyagent.org/docs/latest/ |

These frameworks are not all dedicated security scanners. They provide implementation or policy capabilities that can support a security architecture.

### 7.2 Agent security test cases

- Attempt to call a tool outside the agent's role.
- Attempt to access an unauthorized resource.
- Supply invalid or unexpected tool arguments.
- Attempt to access another user's memory.
- Insert malicious instructions into retrieved content.
- Attempt to exceed tool-call or spending limits.
- Attempt a sensitive action without approval.
- Verify that rejected actions cannot execute through an alternate path.

### 7.3 Core security controls

- Server-side authorization
- Least-privilege tool permissions
- Strict argument validation
- Execution sandboxing
- Resource and time limits
- Human approval for high-impact actions
- Secure credential storage
- Audit logging and incident response

## 8. Guardrails and Defensive Frameworks

Guardrails can help enforce application policies, but they should be used alongside traditional security controls.

### 8.1 NVIDIA NeMo Guardrails

Useful for implementing configurable conversational and workflow controls in LLM applications.

Repository: https://github.com/NVIDIA/NeMo-Guardrails

Documentation: https://docs.nvidia.com/nemo/guardrails/

### 8.2 Guardrails AI

Provides a framework for validating and structuring LLM outputs.

Repository: https://github.com/guardrails-ai/guardrails

Documentation: https://guardrailsai.com/

### 8.3 Open Policy Agent (OPA)

OPA is a general-purpose policy engine that can enforce application authorization decisions independently of the LLM.

Documentation: https://www.openpolicyagent.org/docs/latest/

### 8.4 Defense-in-depth approach

Use multiple layers:

1. Validate input formats.
2. Apply authentication and authorization.
3. Restrict tool availability.
4. Validate model-generated arguments.
5. Enforce business rules in trusted code.
6. Review or approve sensitive actions.
7. Validate output before rendering or executing it.
8. Log relevant security events.
9. Monitor for repeated failures and abuse.

**Remember:** Guardrails may fail or be bypassed. Critical authorization decisions must be enforced outside the model.

## 9. Privacy and Data Protection

AI systems may process personal information, internal documents, customer records, or confidential source code.

Security testing should cover:
- Sensitive information exposure
- Insecure storage of prompts and responses
- Cross-user memory leakage
- Excessive retention of conversation logs
- Unintended disclosure through tool outputs
- Access to secrets through execution environments
- Data sharing with third-party model providers

### Recommended controls

- Minimize sensitive data sent to models.
- Apply access controls to logs and stored conversations.
- Redact credentials and other secrets.
- Establish appropriate retention and deletion policies.
- Restrict access to datasets and model artifacts.
- Review provider data-handling settings and contractual terms.
- Test privacy boundaries with synthetic data.

Use synthetic records for initial security labs. Do not upload real customer data or confidential records to third-party testing tools without appropriate authorization.

## 10. Infrastructure and Deployment Security

AI application security also depends on the underlying software and infrastructure.

### Recommended resources

| Tool | Purpose | Official resource |
|---|---|---|
| Bandit | Python code security checks | https://github.com/PyCQA/bandit |
| Semgrep | Static analysis and security rules | https://semgrep.dev/ |
| Gitleaks | Detect secrets in repositories | https://github.com/gitleaks/gitleaks |
| Trivy | Scan containers and dependencies | https://github.com/aquasecurity/trivy |
| OWASP ZAP | Web application security testing | https://www.zaproxy.org/ |
| Docker | Containerization and isolation | https://docs.docker.com/ |

These tools are not substitutes for AI-specific testing. Use them to address the conventional application, API, dependency, and infrastructure risks surrounding an AI system.

### Infrastructure checklist

- Scan dependencies and container images.
- Protect API keys and credentials.
- Enforce API authentication and rate limits.
- Restrict network access where possible.
- Use least-privilege service accounts.
- Secure vector databases and document stores.
- Separate development, testing, and production environments.
- Monitor application and infrastructure logs.
- Patch vulnerable dependencies.
- Avoid exposing internal services to untrusted networks.

## 11. Practical Labs

Complete these exercises in a local environment or an authorized test system.

### Lab 1: LLM Red-Team Baseline

**Objective:** Establish a baseline for an LLM application's security behavior.

Tasks:
1. Create a simple LLM application.
2. Define its intended use and security boundaries.
3. Prepare normal and adversarial test cases.
4. Run an evaluation using a suitable testing framework.
5. Document failures and limitations.
6. Repeat after adding mitigations.

Deliverable: `reports/llm-red-team-baseline.md`

### Lab 2: Prompt Injection Evaluation

**Objective:** Test how the application handles malicious instructions in user input and retrieved content.

Tasks:
1. Create synthetic test documents.
2. Add simulated malicious instructions.
3. Observe the application's behavior.
4. Check whether prohibited tool calls are blocked.
5. Implement and test mitigations.

Deliverable: `reports/prompt-injection-results.md`

### Lab 3: RAG Authorization Testing

**Objective:** Verify document access boundaries.

Tasks:
1. Create two synthetic users or tenants.
2. Store separate test documents.
3. Implement server-side authorization.
4. Test normal retrieval and unauthorized retrieval.
5. Verify that revoked documents cannot be retrieved.

Deliverable: `reports/rag-authorization-tests.md`

### Lab 4: Agent Tool Permission Testing

**Objective:** Verify that an agent cannot exceed its assigned permissions.

Tasks:
1. Create mock read and write tools.
2. Give the agent only read access.
3. Attempt a write operation through the agent.
4. Confirm that trusted application code rejects the action.
5. Add audit logging and repeat the test.

Deliverable: `reports/agent-permission-tests.md`

### Lab 5: AI Application Security Pipeline

**Objective:** Combine conventional and AI-specific testing.

Tasks:
1. Run static analysis on the application.
2. Scan for exposed secrets.
3. Run dependency and container scans where applicable.
4. Execute an LLM evaluation suite.
5. Test authentication and authorization.
6. Record findings and assign remediation priorities.

Deliverable: `reports/ai-security-pipeline.md`

## 12. Building an AI Security Testing Pipeline

A repeatable pipeline helps detect regressions when prompts, models, dependencies, or application code change.

```text
            Code / Prompt Changes
                     |
                     v
              Static Analysis
                     |
                     v
              Secret Detection
                     |
                     v
           Dependency / Container Scan
                     |
                     v
            AI Security Evaluation
                     |
                     v
         Authorization and Tool Tests
                     |
                     v
             Review Test Results
                     |
                     v
          Remediate and Re-test
```

### Suggested test stages

**Stage 1: Application security**
- Static analysis
- Dependency checks
- Secret detection

**Stage 2: AI behavior**
- Prompt-injection test cases
- Output validation
- Model behavior evaluation

**Stage 3: Access control**
- User authorization
- Tenant isolation
- Tool permissions
- Resource ownership

**Stage 4: Operational security**
- Rate limits
- Timeouts
- Audit logs
- Secret protection

**Stage 5: Release review**
- Review failed tests.
- Fix critical issues.
- Re-run relevant tests.
- Document accepted residual risks.

Do not treat a passing automated test suite as proof of security. Combine automated tests with manual review and threat modeling.

## 13. Tool Selection Guide

Choose tools based on the problem you are trying to solve.

| Requirement | Tools to investigate |
|---|---|
| General LLM red teaming | PyRIT, garak |
| Repeatable prompt and application tests | Promptfoo |
| Model task evaluations | Inspect AI |
| RAG quality evaluation | Ragas, DeepEval |
| Output validation | Guardrails AI |
| Configurable conversational controls | NeMo Guardrails |
| Policy-based authorization | Open Policy Agent |
| Python static analysis | Bandit, Semgrep |
| Secret detection | Gitleaks |
| Container and dependency scanning | Trivy |
| Web application testing | OWASP ZAP |

Before adopting a tool, check:
- Current maintenance activity
- Supported models and integrations
- Installation and runtime requirements
- Licensing and usage restrictions
- Data-handling and privacy implications
- Suitability for your specific threat model

## 14. Learning Roadmap

### Beginner

- Learn Python and REST APIs.
- Understand LLM, RAG, and agent architecture.
- Run a basic evaluation with Promptfoo.
- Learn common LLM security risks.
- Practice conventional application security.

### Intermediate

- Use garak or PyRIT to organize security tests.
- Build a RAG application with synthetic documents.
- Test indirect prompt injection.
- Evaluate access-control boundaries.
- Use Semgrep, Gitleaks, and dependency scanning.

### Advanced

- Build repeatable adversarial evaluations.
- Test tool-using agents and multi-agent workflows.
- Integrate security tests into CI/CD.
- Develop custom checks for your application's threat model.
- Analyze false positives, false negatives, and residual risks.
- Publish reproducible research with documented limitations.

## 15. References

### AI security guidance

- [OWASP GenAI Security Project](https://genai.owasp.org/)
- [OWASP Top 10 for LLM Applications](https://genai.owasp.org/llm-top-10/)
- [NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework)
- [MITRE ATLAS](https://atlas.mitre.org/)
- [Google Secure AI Framework](https://saif.google/)

### Research and publications

- [arXiv](https://arxiv.org/)
- [Google Scholar](https://scholar.google.com/)
- [USENIX Security](https://www.usenix.org/conferences)
- [IEEE Xplore](https://ieeexplore.ieee.org/)

### Contribution guidelines

Contributions are welcome!

You can contribute by adding:
- New AI security tools
- Verified documentation links
- Reproducible test cases
- Defensive code examples
- Research papers and technical reports
- Authorized hands-on labs

For each contribution, include the tool's purpose, official link, installation or usage notes where appropriate, and known limitations.

Only test systems you own or are explicitly authorized to assess. Do not publish credentials, private datasets, or confidential results.

