
# AI Security Research Papers

A curated collection of research papers, technical reports, and academic resources covering AI security, LLM vulnerabilities, adversarial machine learning, RAG security, AI agent security, privacy, and AI red teaming.

The goal of this directory is to help learners and security researchers understand current threats, evaluate existing defenses, and develop reproducible AI security research projects.

## Table of Contents

- [1. How to Use This Collection](#1-how-to-use-this-collection)
- [2. Research Paper Categories](#2-research-paper-categories)
- [3. Prompt Injection and Jailbreaking](#3-prompt-injection-and-jailbreaking)
- [4. Adversarial Machine Learning](#4-adversarial-machine-learning)
- [5. LLM Security and Red Teaming](#5-llm-security-and-red-teaming)
- [6. RAG Security](#6-rag-security)
- [7. AI Agent Security](#7-ai-agent-security)
- [8. Privacy and Data Leakage](#8-privacy-and-data-leakage)
- [9. Model Alignment and Defenses](#9-model-alignment-and-defenses)
- [10. Research Databases and Benchmarks](#10-research-databases-and-benchmarks)
- [11. How to Read a Research Paper](#11-how-to-read-a-research-paper)
- [12. Reproducing Research Experiments](#12-reproducing-research-experiments)
- [13. Research Project Ideas](#13-research-project-ideas)
- [14. Research Notes Template](#14-research-notes-template)
- [15. Research Ethics](#15-research-ethics)

---

## 1. How to Use This Collection

Use this directory to:

- Discover important AI security research.
- Understand how vulnerabilities work.
- Compare attack methods and defensive approaches.
- Identify limitations in existing research.
- Reproduce experiments in controlled environments.
- Develop research questions for academic projects.
- Build a portfolio of documented AI security experiments.

### Paper status

Research papers may be preprints, peer-reviewed publications, technical reports, or workshop papers.

Before citing a paper in academic work, verify:
- The exact title and author list.
- Publication venue and year.
- Whether the paper has been peer-reviewed.
- The latest version and any corrections.
- Whether the experiments and code are publicly available.

A paper appearing on arXiv does not necessarily mean it has undergone peer review.

## 2. Research Paper Categories

| Category | Main research questions |
|---|---|
| Prompt injection | How can malicious instructions influence model behavior? |
| Jailbreaking | How can safety restrictions be bypassed, and how robust are defenses? |
| Adversarial ML | How can manipulated inputs affect machine-learning models? |
| LLM red teaming | How can AI system weaknesses be systematically evaluated? |
| RAG security | How can retrieved content introduce security and privacy risks? |
| Agent security | How can tool use, memory, and autonomy create vulnerabilities? |
| Privacy | Can models reveal sensitive training or user information? |
| Alignment and defenses | How can unsafe behavior be reduced and evaluated? |
| AI supply chain | How can datasets, models, and dependencies be compromised? |
| Evaluation | How should AI security tests and benchmarks be designed? |

---

## 3. Prompt Injection and Jailbreaking

Prompt injection is a security risk in which untrusted input or retrieved content influences an AI system in unintended ways.

Jailbreaking refers to attempts to make a model bypass its intended safety constraints.

### Foundational reading

**1. Universal and Transferable Adversarial Attacks on Aligned Language Models**

- Authors: Andy Zou and colleagues
- Year: 2023
- Topic: Adversarial suffixes and jailbreak transferability
- Link: https://arxiv.org/abs/2307.15043

**Why read it?**

Study how adversarial inputs can influence aligned language models and why model-level defenses can be difficult to generalize.

**2. Not What You've Signed Up For: Compromising Real-World LLM-Integrated Applications with Indirect Prompt Injection**

- Authors: Kai Greshake and colleagues
- Year: 2023
- Topic: Indirect prompt injection in LLM-integrated applications
- Link: https://arxiv.org/abs/2302.12173

**Why read it?**

Understand how external content processed by an AI application can influence its behavior, particularly when the application connects an LLM to external tools or data.

### Research questions

- Why is indirect prompt injection difficult to eliminate?
- How can a system separate trusted instructions from untrusted content?
- Which application-level controls reduce the impact of prompt injection?
- How should defenses be evaluated against unseen attacks?
- How do retrieval and tool access change the attack surface?

---

## 4. Adversarial Machine Learning

Adversarial machine learning studies how intentionally manipulated inputs, training data, or model interactions can affect machine-learning systems.

### Foundational reading

**3. Explaining and Harnessing Adversarial Examples**

- Authors: Ian J. Goodfellow, Jonathon Shlens, and Christian Szegedy
- Year: 2014; conference publication in 2015
- Topic: Adversarial examples and fast gradient-based methods
- Link: https://arxiv.org/abs/1412.6572

**Why read it?**

Learn foundational concepts behind adversarial examples and the relationship between model behavior and small input perturbations.

**4. Towards Evaluating the Robustness of Neural Networks**

- Authors: Nicholas Carlini and David Wagner
- Year: 2017
- Topic: Evaluating neural-network robustness
- Link: https://arxiv.org/abs/1608.04644

**Why read it?**

Understand why robust evaluation matters and why a defense should be assessed against adaptive attacks.

### Research questions

- How do adversarial examples differ across image, text, and multimodal systems?
- How should robustness be measured?
- What are the limitations of adversarial training?
- How can evaluations avoid overestimating defense effectiveness?
- How can adversarial ML concepts inform LLM security testing?

---

## 5. LLM Security and Red Teaming

LLM security research investigates vulnerabilities in model behavior and the applications built around models.

### Recommended resources

**5. Red Teaming Language Models to Reduce Harms: Methods, Scaling Behaviors, and Lessons Learned**

- Authors: Ethan Perez and colleagues
- Year: 2022
- Topic: Red teaming and language-model risk evaluation
- Link: https://arxiv.org/abs/2209.07858

**Why read it?**

Explore structured methods for identifying undesirable model behaviors and the challenges of scaling red-team evaluations.

**6. Holistic Evaluation of Language Models (HELM)**

- Authors: Percy Liang and colleagues
- Year: 2022
- Topic: Broad evaluation of language models
- Link: https://arxiv.org/abs/2211.09110

**Why read it?**

Learn how to evaluate language models across multiple dimensions instead of relying on a single benchmark.

### Research questions

- Which metrics are appropriate for AI security evaluations?
- How can red-team coverage be measured?
- What makes an evaluation reproducible?
- How should results be compared across models?
- How can researchers distinguish model-level failures from application-level failures?

---

## 6. RAG Security

Retrieval-augmented generation combines language models with external information sources. It can improve factual grounding, but it introduces new risks related to document trust, access control, retrieval, and information disclosure.

### Recommended reading

**7. PoisonedRAG: Knowledge Corruption Attacks to Retrieval-Augmented Generation of Large Language Models**

- Year: 2024
- Topic: Knowledge-base poisoning in RAG systems
- Link: https://arxiv.org/abs/2402.07867

**Why read it?**

Study how manipulated documents can affect the answers produced by a retrieval-augmented system.

**8. RAG Security Research: A Continuing Research Area**

- Topic: Retrieval manipulation, document poisoning, indirect prompt injection, and cross-user data exposure
- Search papers: https://arxiv.org/search/?query=retrieval+augmented+generation+security&searchtype=all

**Why explore this area?**

RAG security spans more than model behavior. It also depends on document ingestion, retrieval permissions, vector database configuration, and the way retrieved content is passed to the model.

### Research questions

- How does malicious document insertion affect retrieval and generation?
- How can document provenance be tracked?
- How should access control be enforced in multi-tenant RAG?
- Can retrieval filters be bypassed through model-generated queries?
- How should RAG systems handle revoked or outdated documents?
- How can the security impact of retrieved instructions be measured?

### Suggested experiment

Build a small RAG application with synthetic documents. Compare its behavior before and after adding a simulated poisoned document. Measure retrieval results, answer correctness, unauthorized access attempts, and the effectiveness of defensive controls.

Do not use private or real customer documents in an experimental dataset.

---

## 7. AI Agent Security

AI agents can plan tasks, call tools, use memory, and execute multi-step workflows. Their security depends on the model as well as application permissions, orchestration, tools, and execution environments.

### Recommended research directions

**9. Indirect Prompt Injection**

- Foundational paper: Greshake and colleagues
- Link: https://arxiv.org/abs/2302.12173
- Focus: External content influencing an AI application's behavior

**10. Excessive Agency and Agentic AI Security**

- Topic: Unnecessary permissions, uncontrolled tool execution, and unsafe autonomy
- Research search: https://arxiv.org/search/?query=LLM+agent+security&searchtype=all

**11. Memory Poisoning and Agent Trust**

- Topic: Persistent memory manipulation and cross-session influence
- Research search: https://arxiv.org/search/?query=LLM+agent+memory+poisoning&searchtype=all

These search pages identify research directions rather than single verified papers. Review individual papers for relevance, publication details, and methodology before citing them.

### Research questions

- How should tool permissions be enforced independently of model output?
- How can an agent be prevented from exceeding its intended role?
- How can persistent memory be protected against manipulation?
- How should multi-agent systems authenticate and validate messages?
- Which actions should require explicit human approval?
- How can security tests detect unauthorized delegation?

### Suggested experiment

Create a mock agent with separate read and write tools. Configure the agent for read-only access, then test whether server-side authorization blocks prohibited write operations even when the model requests them.

---

## 8. Privacy and Data Leakage

Privacy research examines whether machine-learning systems expose information about training data, users, or other confidential inputs.

### Foundational reading

**12. Extracting Training Data from Large Language Models**

- Authors: Nicholas Carlini and colleagues
- Year: 2021
- Topic: Training-data extraction and privacy risks
- Link: https://arxiv.org/abs/2012.07805

**Why read it?**

Understand how language models may reproduce information from their training data and why data protection requires more than prompt-level filtering.

**13. Membership Inference Attacks Against Machine Learning Models**

- Topic: Determining whether particular examples were used to train a model
- Research search: https://arxiv.org/search/?query=membership+inference+machine+learning&searchtype=all

### Research questions

- Under what conditions can training data be extracted?
- What factors affect membership-inference risk?
- How should sensitive information be handled in prompts and logs?
- How can privacy risks be measured before deployment?
- What trade-offs exist between privacy and model utility?

### Defensive considerations

- Minimize sensitive data in model inputs.
- Restrict access to logs and datasets.
- Apply appropriate retention and deletion policies.
- Evaluate privacy risks before deployment.
- Review model-provider data-handling practices.
- Consider differential privacy when appropriate to the training or analysis task.

---

## 9. Model Alignment and Defenses

Alignment and safety research explores methods for reducing harmful behavior and improving adherence to intended objectives.

### Recommended reading

**14. Training Language Models to Follow Instructions with Human Feedback**

- Authors: Long Ouyang and colleagues
- Year: 2022
- Topic: Instruction following and reinforcement learning from human feedback
- Link: https://arxiv.org/abs/2203.02155

**Why read it?**

Understand a foundational approach to instruction following and human-feedback-based model training.

### Related research topics

- Adversarial robustness
- Constitutional AI
- Safety fine-tuning
- Refusal behavior
- Input and output filtering
- Tool-use restrictions
- Human-in-the-loop controls
- Evaluation against adaptive attacks

### Research questions

- Do safety improvements generalize to unseen inputs?
- How should refusal behavior be evaluated?
- Can model-level defenses be combined with application-level enforcement?
- How can security evaluations avoid relying on one attack method?
- What trade-offs exist between usefulness and safety?

**Important:** A model's safety training is not a substitute for authorization, secure execution, and application-level controls.

---

## 10. Research Databases and Benchmarks

Use these resources to discover newer papers, benchmarks, datasets, and security evaluations.

### Academic search

- [arXiv](https://arxiv.org/)
- [Google Scholar](https://scholar.google.com/)
- [Semantic Scholar](https://www.semanticscholar.org/)
- [ACL Anthology](https://aclanthology.org/)
- [IEEE Xplore](https://ieeexplore.ieee.org/)
- [USENIX Security](https://www.usenix.org/conferences)

### Security frameworks and threat intelligence

- [OWASP GenAI Security Project](https://genai.owasp.org/)
- [MITRE ATLAS](https://atlas.mitre.org/)
- [NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework)

### Useful search queries

Try these searches when updating this collection:

- `large language model security`
- `LLM prompt injection defenses`
- `indirect prompt injection evaluation`
- `retrieval augmented generation security`
- `LLM agent tool authorization`
- `AI agent memory poisoning`
- `training data extraction language models`
- `adversarial robustness evaluation`
- `AI red teaming benchmark`
- `LLM privacy membership inference`

For current developments, filter by publication date and verify whether a paper has been superseded by a newer version.

---

## 11. How to Read a Research Paper

Use a structured reading method to understand papers efficiently.

### Step 1: Read the abstract

Identify:
- The problem being investigated
- The proposed method
- The main result
- The stated contribution

### Step 2: Identify the threat model

Ask:
- Who is the attacker?
- What access does the attacker have?
- What capabilities are assumed?
- What is the target asset?
- What counts as a successful attack?

### Step 3: Understand the methodology

Review:
- Dataset and model selection
- Experimental setup
- Baselines
- Evaluation metrics
- Reproducibility information

### Step 4: Analyze the results

Check:
- Whether the evidence supports the claims
- Whether the evaluation covers realistic scenarios
- Whether the authors discuss limitations
- Whether results generalize to other systems

### Step 5: Evaluate the defenses

Ask:
- Does the defense prevent the attack or only reduce its success?
- Was the defense evaluated against adaptive attacks?
- What is the performance or usability cost?
- What assumptions must hold for it to work?

### Step 6: Record your findings

Write a short summary in your own words and list the questions that remain unanswered.

---

## 12. Reproducing Research Experiments

Reproducibility helps determine whether published findings hold under different conditions.

### Suggested workflow

1. Select a paper with a clearly defined research question.
2. Read its methodology and limitations.
3. Check whether code, datasets, and model configurations are available.
4. Create an isolated environment.
5. Use synthetic or authorized data.
6. Reproduce a small baseline experiment.
7. Record model versions, parameters, and dependencies.
8. Compare your findings with the paper.
9. Explain differences and limitations.
10. Publish a concise, reproducible report.

### Example experiment structure

```text
research-project/
├── README.md
├── paper-notes.md
├── requirements.txt
├── src/
├── data/
│   └── README.md
├── experiments/
├── results/
├── reports/
└── limitations.md
```

Avoid committing credentials, private datasets, large model files without permission, or sensitive test results.

### Suggested result metrics

Depending on the experiment, consider:
- Attack success rate
- False-positive rate
- False-negative rate
- Unauthorized action rate
- Retrieval precision and recall
- Response quality
- Runtime and computational cost
- Defense overhead

Define each metric clearly and explain how it is calculated.

---

## 13. Research Project Ideas

These projects are suitable starting points for a student or independent AI security researcher.

### Project 1: Prompt Injection Defense Evaluation

**Objective:** Compare multiple defenses against a controlled set of prompt-injection tests.

Possible work:
- Create synthetic adversarial test cases.
- Establish a baseline.
- Compare model-level and application-level defenses.
- Measure attack success and false positives.
- Document limitations.

### Project 2: RAG Document Poisoning Analysis

**Objective:** Investigate how manipulated documents affect retrieval and answer generation.

Possible work:
- Build a small RAG pipeline.
- Use synthetic documents.
- Vary the number and position of manipulated documents.
- Measure retrieval and answer changes.
- Test provenance and authorization controls.

### Project 3: AI Agent Least-Privilege Evaluation

**Objective:** Determine whether agent tools enforce their intended permissions.

Possible work:
- Implement mock tools with different permission levels.
- Test unauthorized actions.
- Add server-side authorization.
- Compare results before and after mitigation.
- Publish a test matrix.

### Project 4: Cross-User RAG Privacy

**Objective:** Evaluate information boundaries in a multi-tenant RAG application.

Possible work:
- Create synthetic data for separate users.
- Test document filtering.
- Attempt unauthorized retrieval.
- Evaluate tenant isolation.
- Recommend secure data-layer controls.

### Project 5: AI Security Evaluation Framework

**Objective:** Create a repeatable test suite for a specific class of AI application.

Possible work:
- Define a threat model.
- Organize test cases by risk category.
- Automate repeatable checks.
- Generate a results report.
- Evaluate false positives and coverage limitations.

### Project 6: Comparing AI Security Tools

**Objective:** Compare tools on a defined set of test cases.

Possible work:
- Select two or three suitable tools.
- Use the same authorized test environment.
- Compare setup requirements and coverage.
- Record detected issues and missed cases.
- Document reproducibility and limitations.

**Research principle:** A useful project should have a specific research question, a clear methodology, measurable outcomes, and an honest discussion of limitations.

---

## 14. Research Notes Template

Use the following template when reviewing a paper.

```markdown
# Research Paper Notes

## Paper Information
- Title:
- Authors:
- Publication year:
- Venue:
- DOI or URL:

## Research Problem
What problem does the paper investigate?

## Threat Model
- Attacker:
- Target:
- Assumed capabilities:
- Security objective:

## Methodology
How did the authors conduct the experiment?

## Key Findings
What are the most important results?

## Evaluation
- Dataset:
- Model:
- Baselines:
- Metrics:

## Limitations
What assumptions or weaknesses affect the findings?

## My Analysis
What do I agree or disagree with, and why?

## Future Research
What questions remain unanswered?

## Reproducibility
- Code available:
- Dataset available:
- Environment documented:
- Results reproduced:
```

Save individual notes in a dedicated directory if your collection grows.

---

## 15. Research Ethics

AI security research should be conducted responsibly.

- Test only systems you own or have explicit permission to assess.
- Use synthetic or appropriately authorized datasets.
- Avoid publishing credentials, personal information, or confidential logs.
- Follow responsible disclosure practices.
- Respect dataset, model, and software licenses.
- Document research limitations and unsuccessful experiments.
- Do not present a limited experiment as proof of universal security.
- Separate verified findings from hypotheses.
- Cite original research and acknowledge prior work.
- Review institutional and legal requirements before testing real systems.

---

## Contribution Guidelines

Contributions are welcome!

You can contribute by adding:
- Verified research papers
- Recent conference publications
- Reproducible experiments
- Critical reviews and paper summaries
- Research benchmarks and datasets
- Defensive methods and evaluation frameworks

For every new entry, provide the title, authors, year, original link, topic, and a short explanation of its relevance.

Please verify metadata and links before submitting a contribution.
