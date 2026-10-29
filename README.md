
# 🛡️ Awesome AI Security Learning

<p align="center">
  <strong>Learn • Practice • Research • Secure AI</strong>
</p>

<p align="center">
  A curated, hands-on collection of resources for learning,
  practicing, and researching Artificial Intelligence Security.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Domain-AI%20Security-blue" alt="AI Security">
  <img src="https://img.shields.io/badge/Focus-LLM%20%7C%20RAG%20%7C%20AI%20Agents-purple" alt="Focus">
  <img src="https://img.shields.io/badge/Resources-Open%20Source-green" alt="Open Source">
  <img src="https://img.shields.io/badge/Contributions-Welcome-orange" alt="Contributions Welcome">
</p>

---

## 📌 About This Repository

**Awesome AI Security Learning** is an open-source knowledge hub designed
to help students, cybersecurity professionals, AI engineers, developers,
and security researchers understand and secure AI-powered systems.

This repository brings together carefully selected documentation,
research papers, security tools, practical labs, learning roadmaps,
and real-world security scenarios.

Whether you are starting your AI security journey or developing advanced
skills in LLM security and AI red teaming, this repository provides a
structured path for continuous learning and practical application.

### 🎯 Our Mission

Make AI security knowledge accessible through structured learning,
hands-on experimentation, defensive engineering, and community collaboration.

## 📚 Table of Contents

- [Learning Objectives](#-learning-objectives)
- [AI Security Domains](#-ai-security-domains)
- [Learning Roadmap](#-learning-roadmap)
- [Hands-On Labs](#-hands-on-labs)
- [Security Tools and Frameworks](#-security-tools-and-frameworks)
- [Research Papers](#-research-papers)
- [Portfolio Projects](#-portfolio-projects)
- [Books and Courses](#-books-and-courses)
- [Interview Preparation](#-interview-preparation)
- [Contribution Guidelines](#-contribution-guidelines)
- [Responsible Use](#-responsible-use)
- [License](#-license)

---

## 🎯 Learning Objectives

By exploring this repository, you will learn how to:

- Understand the architecture and security of modern AI systems.
- Identify common vulnerabilities in LLM-powered applications.
- Understand prompt injection, jailbreaks, and information disclosure.
- Analyze security risks in Retrieval-Augmented Generation (RAG).
- Identify threats affecting AI agents and tool integrations.
- Understand adversarial machine learning and model security.
- Perform authorized AI security assessments and red-team evaluations.
- Implement security controls and evaluate their effectiveness.
- Build practical AI security projects for your portfolio.
- Research emerging threats and defensive techniques.

---

## 🔐 AI Security Domains

### 1. AI and Machine Learning Fundamentals

Learn the technical foundations required to understand AI security.

Topics:
- Machine Learning and Deep Learning
- Neural Networks and Transformers
- Large Language Models (LLMs)
- Tokenization and Embeddings
- Vector Databases
- Retrieval-Augmented Generation (RAG)
- AI Agents and Tool Calling
- Model Training and Inference

### 2. LLM Security

Understand the security challenges introduced by LLM-powered applications.

Topics:
- Prompt Injection
- Jailbreaks and Safety Bypass
- Sensitive Information Disclosure
- Insecure Output Handling
- System Prompt Exposure
- Improper Input Validation
- Unsafe Tool Calling
- Denial of Service and Resource Abuse
- Model and Application Supply Chain Risks

### 3. RAG Security

Study security risks in systems that combine LLMs with external knowledge sources.

Topics:
- Document and Knowledge-Base Poisoning
- Retrieval Manipulation
- Embedding Security
- Vector Database Access Control
- Cross-User Data Leakage
- Indirect Prompt Injection
- Document Ingestion Security
- Secure Retrieval and Authorization

### 4. AI Agent Security

Learn how to secure AI agents that can use tools, access data, and execute tasks.

Topics:
- Agent Threat Modeling
- Excessive Agency and Permissions
- Tool Misuse and Unauthorized Actions
- Memory Poisoning
- Untrusted Tool Outputs
- Multi-Agent Security
- Human Approval and Authorization
- Secure Agent Sandboxing

### 5. Adversarial Machine Learning

Explore attacks and defenses affecting machine learning models.

Topics:
- Data Poisoning
- Adversarial Examples
- Evasion Attacks
- Model Extraction
- Membership Inference
- Model Inversion
- Backdoor Attacks
- Model Supply Chain Security
- Privacy-Preserving Machine Learning

### 6. AI Red Teaming

Learn systematic methods for evaluating AI system security.

Topics:
- AI Threat Modeling
- Attack Surface Analysis
- Adversarial Testing
- Prompt Injection Testing
- Data Leakage Evaluation
- Tool and Agent Security Testing
- Security Test Automation
- Risk Scoring and Reporting
- Remediation Verification

### 7. Defensive AI Security Engineering

Focus on building and operating safer AI applications.

Topics:
- Secure AI Architecture
- Input and Output Validation
- Least-Privilege Access
- Secure RAG Design
- Tool Authorization
- Secrets Management
- Guardrails and Security Testing
- Logging and Monitoring
- AI Risk Management
- Incident Response for AI Systems

---

## 🗺️ Learning Roadmap

Follow this suggested sequence to develop your AI security skills.

| Level | Focus | Goal |
|---|---|---|
| Beginner | AI fundamentals, LLM architecture, security basics | Understand AI systems |
| Intermediate | LLM vulnerabilities, RAG security, testing | Identify and reproduce risks |
| Advanced | AI agents, adversarial ML, AI red teaming | Assess complex systems |
| Professional | Secure AI architecture, automation, research | Build and defend AI products |

### Recommended Learning Sequence

1. Learn AI, ML, LLM, and RAG fundamentals.
2. Understand traditional web and application security.
3. Study common LLM vulnerabilities and threat models.
4. Practice in local, intentionally vulnerable AI applications.
5. Learn AI security testing and evaluation frameworks.
6. Implement defensive controls and regression tests.
7. Build end-to-end AI security projects.
8. Read research papers and contribute to open-source projects.

---

## 🧪 Hands-On Labs

Practical exercises are essential for understanding AI security.

The repository aims to organize labs into three difficulty levels.

### Beginner Labs
- Basic Prompt Injection Demonstration
- System Prompt Exposure in a Toy Application
- Insecure LLM Output Handling
- Sensitive Data Leakage Demonstration

### Intermediate Labs
- Indirect Prompt Injection in a Local RAG Application
- RAG Access-Control Testing
- Document Poisoning Simulation
- LLM Security Evaluation with Automated Tests

### Advanced Labs
- AI Agent Permission and Tool Abuse Testing
- Multi-Agent Trust Boundary Evaluation
- Adversarial Machine Learning Experiments
- Automated AI Red-Team Evaluation Pipelines

Each lab should include:

- Learning objectives
- Technical prerequisites
- Architecture and threat model
- Setup instructions
- Controlled attack demonstration
- Expected results
- Detection and mitigation
- Security validation tests
- Further reading

**Note:** Labs should use isolated environments, synthetic data, and systems
that you own or have explicit permission to test.

---

## 🧰 Security Tools and Frameworks

The following are starting points for exploring the AI security ecosystem.

| Resource | Purpose | Link |
|---|---|---|
| OWASP GenAI Security Project | AI application security guidance | [Website](https://genai.owasp.org/) |
| MITRE ATLAS | Adversarial AI threat knowledge base | [Website](https://atlas.mitre.org/) |
| NIST AI RMF | AI risk management | [Website](https://www.nist.gov/itl/ai-risk-management-framework) |
| garak | LLM vulnerability scanning and probing | [GitHub](https://github.com/NVIDIA/garak) |
| PyRIT | AI red-teaming automation | [GitHub](https://github.com/Azure/PyRIT) |
| Giskard | AI model testing and evaluation | [GitHub](https://github.com/Giskard-AI/giskard) |
| ART | Adversarial robustness research and testing | [GitHub](https://github.com/Trusted-AI/adversarial-robustness-toolbox) |

Always check each project's official documentation, supported versions,
license, and maintenance status before adopting it.

---

## 📄 Research Papers

This section will organize research papers by topic.

### LLM Security
- Prompt Injection and instruction hierarchy
- Jailbreak detection and mitigation
- LLM privacy and information leakage
- Security evaluation of language models

### RAG Security
- Knowledge-base poisoning
- Retrieval manipulation
- Indirect prompt injection
- Access control in retrieval pipelines

### Adversarial Machine Learning
- Adversarial examples
- Training data poisoning
- Model extraction and inference attacks
- Robustness evaluation

### AI Agent Security
- Agentic threat modeling
- Tool-use security
- Memory and context poisoning
- Secure autonomous systems

Where available, include the paper title, authors, publication year,
abstract summary, official publication link, and associated code.

---

## 🚀 Portfolio Projects

Build practical projects that demonstrate your understanding of AI security.

| Project | Description | Difficulty |
|---|---|---|
| Prompt Injection Evaluator | Test an LLM against a collection of controlled injection cases | Beginner |
| Secure RAG Chatbot | Build a RAG application with authorization and security tests | Intermediate |
| LLM Security Scanner | Automate security checks against a local AI application | Intermediate |
| AI Red-Team Test Suite | Run repeatable adversarial evaluations and generate reports | Advanced |
| AI Threat Model Generator | Assist in identifying risks from an AI system architecture | Advanced |

Each project should contain source code, setup instructions, a threat model,
test cases, security findings, and documented mitigations.

---

## 📚 Books and Courses

This section will collect learning resources covering:

- AI and Machine Learning Fundamentals
- LLM Engineering
- Application and API Security
- AI Security and Red Teaming
- Adversarial Machine Learning
- RAG and AI Agent Engineering
- Secure Software Development

Prefer official documentation, reputable educational materials,
research-backed publications, and legally accessible resources.

---

## 💼 Interview Preparation

Prepare for roles such as:

- AI Security Engineer
- AI Red Team Engineer
- LLM Security Engineer
- Product Security Engineer for AI
- Machine Learning Security Engineer
- AI Security Researcher

Practice the following:

- AI security fundamentals
- Threat modeling and attack-surface analysis
- LLM and RAG security scenarios
- AI agent authorization and sandboxing
- Security testing and mitigation strategies
- Python-based security automation
- Practical architecture reviews
- Research paper analysis

Interview preparation should emphasize explaining the risk, demonstrating
the issue safely, recommending a defense, and verifying that the defense works.

---

## 🤝 Contribution Guidelines

Contributions from learners, developers, security researchers, and AI
engineers are welcome.

You can contribute by:

- Adding high-quality learning resources
- Improving documentation
- Writing practical labs
- Contributing defensive code and tests
- Summarizing research papers
- Fixing broken links
- Adding interview questions
- Improving learning roadmaps

### Before Submitting a Contribution

1. Check whether the resource already exists.
2. Verify the link and source quality.
3. Provide a concise description and relevant category.
4. Include prerequisites for practical labs.
5. Document defensive measures and safety requirements.
6. Follow the repository's contribution guidelines.

Please avoid duplicate entries, unverified security claims, copyrighted
material shared without permission, and credentials or sensitive data.

---

## ⚖️ Responsible Use

This repository is intended for education, authorized security testing,
research, and defensive engineering.

- Test only systems you own or have permission to assess.
- Use isolated environments for vulnerable demonstrations.
- Never publish API keys, passwords, private data, or real secrets.
- Do not deploy intentionally vulnerable demonstrations to production.
- Follow applicable laws, licenses, and responsible disclosure practices.
- Document limitations and potential risks of security tools.

---

## 📜 License

This repository is intended to use an open-source license selected by
the repository maintainer. See the `LICENSE` file for the applicable terms.

Resources linked from third-party projects remain subject to their own
licenses and terms.

---

## ⭐ Support the Project

If this repository helps you learn AI security:

- Star the repository.
- Share useful resources.
- Open issues for corrections and suggestions.
- Contribute labs, research summaries, and defensive improvements.
- Help make AI security education accessible to more people.

**Learn AI Security. Practice Responsibly. Build More Secure AI.**
