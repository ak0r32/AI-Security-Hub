# LLM Security

Study prompt injection, jailbreaks, sensitive information disclosure, and LLM defenses.

## Learning Objectives

# 🔐 LLM Security

A practical learning hub for understanding, testing, and securing Large Language Model (LLM) applications.

This section covers common LLM vulnerabilities, attack surfaces, security testing methodologies, defensive techniques, research papers, and hands-on exercises.

The goal is to understand how LLM applications fail, how attackers may exploit those weaknesses, and how developers can implement effective security controls.

---

## 📚 Table of Contents

- [Learning Objectives](#-learning-objectives)
- [LLM Security Fundamentals](#1-llm-security-fundamentals)
- [LLM Architecture and Attack Surface](#2-llm-architecture-and-attack-surface)
- [OWASP Top 10 for LLM Applications](#3-owasp-top-10-for-llm-applications)
- [Core LLM Vulnerabilities](#4-core-llm-vulnerabilities)
- [LLM Security Tools](#5-llm-security-tools)
- [Hands-On Labs](#6-hands-on-labs)
- [Defensive Security Engineering](#7-defensive-security-engineering)
- [Research Papers and Further Reading](#8-research-papers-and-further-reading)
- [Security Checklist](#9-llm-security-checklist)
- [Knowledge Check](#10-knowledge-check)
- [Next Steps](#11-next-steps)

---

## 🎯 Learning Objectives

After completing this section, learners should be able to:

- Explain the security challenges associated with LLM applications.
- Identify common LLM attack surfaces and trust boundaries.
- Understand direct and indirect prompt injection.
- Explain jailbreaks and their relationship to model safety controls.
- Identify sensitive information disclosure risks.
- Understand insecure output handling and unsafe tool integration.
- Perform authorized security evaluations against local test applications.
- Implement appropriate security mitigations.
- Create repeatable tests to verify security controls.
- Document vulnerabilities and communicate security findings.

---

## 1. LLM Security Fundamentals

### What Is LLM Security?

LLM security focuses on protecting language models and applications built around them from manipulation, unauthorized access, data exposure, unsafe actions, and other security failures.

Security depends on more than the model itself. It also depends on application code, prompts, data sources, permissions, external tools, APIs, and deployment infrastructure.

### Core Concepts

- LLM Threat Modeling
- AI Application Attack Surfaces
- Trusted and Untrusted Inputs
- System Instructions and User Inputs
- Model and Application Security
- Data Confidentiality and Integrity
- Authorization and Access Control
- Security Evaluation and Monitoring

### Learning Resources

| Resource | Description | Link |
|---|---|---|
| OWASP GenAI Security Project | AI application security guidance | https://genai.owasp.org/ |
| OWASP LLM Top 10 | Common LLM application risks | https://github.com/GenAI-Security-Project/GenAI-LLM-Top10 |
| MITRE ATLAS | Adversarial AI threat knowledge base | https://atlas.mitre.org/ |
| NIST AI Risk Management Framework | AI risk management guidance | https://www.nist.gov/itl/ai-risk-management-framework |

Youtube Tutorial 
Ai Security By Krish Naik Academy
https://www.youtube.com/watch?v=rQE3w8Qjx98

AI Security Playlist By IBM Security
https://www.youtube.com/watch?v=5WlmyncEcNM&list=PLOspHqNVtKADin6JGozvzSvUQFTQRdum-

### Practical Exercise

Choose a simple chatbot architecture and identify:

1. User-controlled inputs.
2. Sensitive information.
3. External services and tools.
4. Trust boundaries.
5. Potential attack scenarios.
6. Security controls required to mitigate those risks.

---

## 2. LLM Architecture and Attack Surface

Understanding the architecture of an LLM application helps identify where security controls are needed.

### Typical Architecture

```text
                User Input
                    |
                    v
             Application API
                    |
                    v
             Input Processing
                    |
                    v
            Prompt Construction
                    |
                    v
                LLM Model
                    |
          +---------+---------+
          |                   |
          v                   v
    Direct Response       Tool Calling
          |                   |
          |             Authorization
          |                   |
          |             External Tools
          |                   |
          +---------+---------+
                    |
                    v
          Output Validation
                    |
                    v
               User Response
```

This is a simplified architecture. Real applications may include retrieval systems, moderation, memory, caching, multiple models, and additional security controls.

### Attack Surfaces

- User prompts and uploaded files
- System prompt construction
- Retrieved documents and external knowledge
- Model inputs and outputs
- Tool and function calling
- API authentication and authorization
- Application secrets and configuration
- Logging and monitoring systems
- Model hosting and third-party integrations

### Security Exercise

Draw the architecture of an LLM application and mark every component that processes untrusted input or accesses sensitive data.

For each component, document a possible threat and a corresponding mitigation.

---

## 3. OWASP Top 10 for LLM Applications

Use the official OWASP project to study the risks in the current published edition.

Official resource:

https://github.com/GenAI-Security-Project/GenAI-LLM-Top10

The following is a study index of commonly recognized LLM application risks. Always consult the official edition for its current categories and wording.

| Vulnerability | What to Learn |
|---|---|
| Prompt Injection | Manipulation of model instructions through untrusted input |
| Sensitive Information Disclosure | Exposure of confidential information |
| Supply Chain Vulnerabilities | Risks in models, datasets, packages, and dependencies |
| Data and Model Poisoning | Manipulation of training or other model-related data |
| Improper Output Handling | Unsafe processing of model-generated output |
| Excessive Agency | Unnecessary or insufficiently controlled model capabilities |
| System Prompt Leakage | Exposure of hidden application instructions |
| Vector and Embedding Weaknesses | Security issues in retrieval and embedding systems |
| Misinformation | Incorrect or misleading generated content |
| Unbounded Consumption | Excessive resource usage and associated costs |

Use the official OWASP documentation to confirm the categories, ordering, and definitions before publishing any version-specific claims.

---

## 4. Core LLM Vulnerabilities

### 4.1 Prompt Injection

Prompt injection occurs when untrusted input influences a model to behave contrary to the intended instructions or application policy.

Types:
- Direct Prompt Injection
- Indirect Prompt Injection
- Retrieved-Content Injection
- Tool-Output Injection

Study:
- Trust boundaries between instructions and data
- Untrusted content in retrieved documents
- Unauthorized tool invocation
- Input handling and policy enforcement

**Practice:** Create a local chatbot using synthetic data. Test whether untrusted text changes its behavior, then implement external authorization checks and regression tests.

### 4.2 Jailbreaks

Jailbreak attempts try to bypass a model's safety or behavioral restrictions.

Study:
- Model safety behavior
- Adversarial prompting
- Evaluation of safety controls
- Differences between model-level and application-level protections

**Practice:** Evaluate a local test model against benign policy-compliance scenarios and record whether the expected restrictions hold.

### 4.3 Sensitive Information Disclosure

Sensitive information disclosure occurs when an application exposes data that should remain confidential.

Potential causes:
- Incorrect access controls
- Sensitive information in model context
- Unsafe logging
- Inadequate output filtering
- Cross-user retrieval failures

**Practice:** Use synthetic secrets and multiple test users to verify that confidential records cannot be accessed by unauthorized users.

### 4.4 Insecure Output Handling

Model-generated content should not automatically be treated as safe for downstream use.

Risks may include:
- Cross-site scripting in web interfaces
- Unsafe HTML rendering
- Injection into downstream interpreters
- Unsafe execution of generated code
- Invalid or unexpected structured output

**Practice:** Create a test suite that checks HTML escaping, schema validation, and safe handling of untrusted generated content.

### 4.5 Excessive Agency

Excessive agency occurs when an AI application has more permissions or capabilities than it needs.

Risks:
- Unnecessary access to sensitive resources
- Unauthorized tool use
- Destructive actions without approval
- Overprivileged service accounts

**Practice:** Create a read-only tool and verify that the application rejects requests to perform actions outside the tool's permissions.

### 4.6 System Prompt Exposure

System prompts may contain internal instructions or implementation details that an application intends to keep private.

Important distinction: a system prompt is not a reliable place to store secrets or enforce authorization.

**Practice:** Build a local demonstration with a fictional internal prompt and document why access control must be implemented outside the model.

### 4.7 Supply Chain Vulnerabilities

AI applications depend on external packages, model files, datasets, and services.

Study:
- Dependency vulnerabilities
- Untrusted model artifacts
- Dataset provenance
- Package integrity
- Model licensing
- Version pinning and security updates

**Practice:** Inventory dependencies in a sample AI project and document how you would verify their provenance and update them securely.

### 4.8 Unbounded Resource Consumption

LLM applications may consume substantial resources when processing large inputs, generating long outputs, or repeatedly invoking expensive tools.

Study:
- Input and output token limits
- Request rate limiting
- Timeouts
- Concurrency controls
- Budget limits
- Abuse monitoring

**Practice:** Add input-size limits and request quotas to a local demo, then test that oversized requests are rejected.

---

## 5. LLM Security Tools

The following tools are useful starting points for authorized security research.

| Tool | Purpose | Official Repository |
|---|---|---|
| garak | LLM vulnerability probing | https://github.com/NVIDIA/garak |
| PyRIT | Generative AI red teaming | https://github.com/Azure/PyRIT |
| Giskard | AI model testing and evaluation | https://github.com/Giskard-AI/giskard |
| Promptfoo | LLM evaluation and red teaming | https://github.com/promptfoo/promptfoo |
| NeMo Guardrails | Programmable conversational guardrails | https://github.com/NVIDIA/NeMo-Guardrails |

### Tool Evaluation Checklist

Before using a tool, check:

- Official documentation and installation instructions
- Supported Python and dependency versions
- Model and provider compatibility
- Test environment requirements
- Output formats and reporting features
- Licensing and maintenance status
- Potential costs and data handling requirements

Do not assume a tool can prevent every vulnerability simply because it performs security tests or applies guardrails.

---

## 6. Hands-On Labs

All labs should use isolated environments, synthetic data, and models or systems you own or are authorized to test.

### Beginner Labs

- Lab 01: LLM Architecture and Attack Surface
- Lab 02: Direct Prompt Injection Demonstration
- Lab 03: Safe Output Rendering
- Lab 04: Token Limits and Resource Controls

### Intermediate Labs

- Lab 05: Indirect Prompt Injection in a Local RAG Application
- Lab 06: Synthetic Secret Leakage Tests
- Lab 07: LLM Security Testing with garak
- Lab 08: Automated Evaluation with Promptfoo

### Advanced Labs

- Lab 09: AI Agent Tool Authorization
- Lab 10: Automated Red-Team Evaluation
- Lab 11: Security Regression Testing Pipeline
- Lab 12: LLM Application Threat Modeling

### Recommended Lab Structure

```text
lab-name/
├── README.md
├── app/
├── tests/
├── solutions/
├── requirements.txt
└── SECURITY-NOTES.md
```

Each lab should include its objective, prerequisites, setup, expected results, defensive recommendations, and tests that verify the fix.

---

## 7. Defensive Security Engineering

Security controls should be implemented in the application architecture rather than relying entirely on model instructions.

### Recommended Practices

- Treat user input and retrieved content as untrusted.
- Enforce authentication and authorization in application code.
- Apply least-privilege permissions to tools and service accounts.
- Validate model outputs before using them in downstream systems.
- Escape untrusted content before rendering it in a browser.
- Restrict file access, network access, and code execution.
- Store API keys in environment configuration or a secrets manager.
- Apply request limits, timeouts, and cost controls.
- Log security-relevant events without unnecessarily storing sensitive data.
- Test security controls regularly.

### Security Validation

For every implemented defense:

1. Define the security requirement.
2. Create a test that reproduces the failure.
3. Implement the mitigation.
4. Repeat the test.
5. Add a regression test.
6. Document residual risks.

---

## 8. Research Papers and Further Reading

Use these sources to find technical research and authoritative documentation.

| Resource | Focus | Link |
|---|---|---|
| OWASP GenAI Security Project | LLM and AI application security | https://genai.owasp.org/ |
| MITRE ATLAS | Adversarial AI techniques | https://atlas.mitre.org/ |
| arXiv | Research papers | https://arxiv.org/ |
| USENIX Security | Security research publications | https://www.usenix.org/conferences |
| IEEE Xplore | Research on AI and cybersecurity | https://ieeexplore.ieee.org/ |

When adding a paper, record:
- Title and authors
- Publication year
- Research problem
- Main findings
- Limitations
- Official publication link
- Available implementation or dataset

Prefer original publications and verify claims against the paper itself.

---

## 9. LLM Security Checklist

Use this checklist when reviewing a test application.

### Architecture
- [ ] Identify application components and trust boundaries.
- [ ] Identify sensitive data and external integrations.
- [ ] Document model and tool permissions.

### Input and Output
- [ ] Treat user input and retrieved documents as untrusted.
- [ ] Validate structured outputs against expected schemas.
- [ ] Safely render model-generated content.
- [ ] Apply suitable input and output limits.

### Data Protection
- [ ] Enforce access control outside the model.
- [ ] Avoid placing secrets in prompts.
- [ ] Test for unauthorized cross-user data access.
- [ ] Review logging and retention practices.

### Tools and Agents
- [ ] Enforce least privilege.
- [ ] Validate tool arguments.
- [ ] Restrict sensitive actions.
- [ ] Require human approval for high-impact actions where appropriate.

### Operations
- [ ] Apply timeouts and rate limits.
- [ ] Monitor suspicious behavior.
- [ ] Pin and review dependencies.
- [ ] Maintain repeatable security tests.

---

## 10. Knowledge Check

1. What is the difference between direct and indirect prompt injection?
2. Why should retrieved documents be treated as untrusted?
3. Why is a system prompt not an effective security boundary?
4. How can an LLM application expose sensitive information?
5. Why should model-generated HTML be handled carefully?
6. What is excessive agency?
7. How can an application limit the impact of unsafe tool calls?
8. What is the role of security regression testing?
9. Why are token limits and rate limits important?
10. How would you design a secure LLM application?

Try to answer each question with an example and a mitigation.

---

## 11. Next Steps

Continue your AI security journey with:

- [RAG Security](../03-rag-security/README.md)
- [AI Agent Security](../04-ai-agent-security/README.md)
- [AI Security Tools](../05-ai-security-tools/README.md)
- [Research Papers](../06-research-papers/README.md)
- [Hands-On Labs](../07-hands-on-labs/README.md)

### Core References

- OWASP GenAI Security Project: https://genai.owasp.org/
- OWASP LLM Top 10: https://github.com/GenAI-Security-Project/GenAI-LLM-Top10
- MITRE ATLAS: https://atlas.mitre.org/
- NIST AI Risk Management Framework: https://www.nist.gov/itl/ai-risk-management-framework

---

**Learning Philosophy:** Understand the vulnerability, reproduce it safely, implement a defense, and verify that the defense works.

**Next Topic:** RAG Security

- Understand the core concepts.
- Explore official documentation and trusted resources.
- Practice in authorized, controlled environments.
- Document security findings and mitigations.

## Resources

Resources will be added here.

## Practical Exercises

Hands-on exercises will be added here.
