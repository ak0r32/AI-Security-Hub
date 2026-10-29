
# 🛡️ RAG Security

A practical learning hub for understanding, testing, and securing Retrieval-Augmented Generation (RAG) systems.

RAG enables Large Language Models (LLMs) to retrieve information from external knowledge sources before generating responses. While this improves the relevance of responses, it introduces additional security risks involving documents, embeddings, retrieval pipelines, permissions, and model context.

This section covers RAG architecture, vulnerabilities, security testing, defensive engineering, tools, research, and hands-on labs.

---

## 📚 Table of Contents

- [Learning Objectives](#-learning-objectives)
- [1. RAG Fundamentals](#1-rag-fundamentals)
- [2. RAG Architecture](#2-rag-architecture)
- [3. RAG Attack Surface](#3-rag-attack-surface)
- [4. Core RAG Vulnerabilities](#4-core-rag-vulnerabilities)
- [5. Vector Database Security](#5-vector-database-security)
- [6. RAG Security Tools](#6-rag-security-tools)
- [7. Hands-On Labs](#7-hands-on-labs)
- [8. Secure RAG Engineering](#8-secure-rag-engineering)
- [9. Research Papers and Resources](#9-research-papers-and-resources)
- [10. RAG Security Checklist](#10-rag-security-checklist)
- [11. Knowledge Check](#11-knowledge-check)
- [12. Next Steps](#12-next-steps)

---

## 🎯 Learning Objectives

After completing this section, learners should be able to:

- Explain how RAG systems retrieve and use external knowledge.
- Understand document ingestion, chunking, embeddings, and vector search.
- Identify security risks throughout the RAG pipeline.
- Understand direct and indirect prompt injection in retrieval systems.
- Explain document poisoning and retrieval manipulation.
- Implement document-level authorization and tenant isolation.
- Test for unauthorized information disclosure.
- Secure document ingestion and vector database access.
- Evaluate retrieval quality and security controls.
- Build a RAG application with practical security tests.

---

## 1. RAG Fundamentals

### What Is Retrieval-Augmented Generation?

Retrieval-Augmented Generation combines information retrieval with text generation.

Instead of relying only on information encoded during model training, a RAG application retrieves relevant information from an external knowledge source and supplies it to the model as context.

### Core Components

- Document Sources
- Document Parsing
- Text Chunking
- Embedding Models
- Vector Databases
- Similarity Search
- Metadata Filtering
- Context Construction
- LLM Generation
- Response Evaluation

### Learning Resources

| Resource | Description | Link |
|---|---|---|
| LlamaIndex | Data ingestion and retrieval pipelines | https://docs.llamaindex.ai/ |
| LangChain | RAG application development | https://python.langchain.com/docs/ |
| Sentence Transformers | Embeddings and semantic search | https://sbert.net/ |
| FAISS | Vector similarity search | https://github.com/facebookresearch/faiss |

### Security Perspective

Every component can introduce security risks.

For example, an unauthorized document might enter the index, a retrieval query might return another user's information, or a malicious document might influence the model through its retrieved context.

---

## 2. RAG Architecture

### Typical RAG Pipeline

```text
             DOCUMENT INGESTION
                     |
                     v
             Document Validation
                     |
                     v
              Text Extraction
                     |
                     v
               Text Chunking
                     |
                     v
              Embedding Model
                     |
                     v
               Vector Database
                     |
                     |
USER QUERY ----------+
                     |
                     v
             Query Processing
                     |
                     v
             Secure Retrieval
                     |
                     v
            Retrieved Documents
                     |
                     v
             Context Construction
                     |
                     v
                LLM Inference
                     |
                     v
          Output Validation and Checks
                     |
                     v
               Final Response
```

This is a simplified architecture. Real systems may use rerankers, keyword search, hybrid retrieval, caching, multiple data stores, and additional validation stages.

### Security Boundaries

Identify the following trust boundaries:

1. External document sources to the ingestion pipeline.
2. Document processors to the vector database.
3. User requests to the retrieval service.
4. Retrieval results to the LLM context.
5. The LLM to downstream tools and applications.
6. The application to its users.

### Practical Exercise

Draw a RAG architecture and mark:

- Sensitive data stores
- Authentication boundaries
- Authorization checks
- External dependencies
- Untrusted documents
- Model input and output
- Logging and monitoring points

---

## 3. RAG Attack Surface

A RAG application has a larger attack surface than a standalone chatbot because it depends on external data and retrieval components.

### Main Attack Surfaces

| Component | Potential Security Concern |
|---|---|
| Document ingestion | Malicious or unauthorized documents |
| File parsing | Unsafe or malformed files |
| Chunking | Loss of security-relevant context |
| Embedding generation | Untrusted or sensitive content entering the index |
| Vector database | Unauthorized access or data exposure |
| Retrieval queries | Missing access-control filters |
| Metadata | Forged or incorrectly assigned ownership |
| Prompt construction | Indirect prompt injection |
| LLM response | Disclosure or misuse of retrieved content |
| Caching | Cross-user information leakage |
| Monitoring | Sensitive information in logs |

### Threat Modeling Questions

- Who can upload or modify documents?
- How is document ownership established?
- Can users retrieve information from other tenants?
- Are authorization checks applied before content reaches the model?
- Can an external source influence model behavior?
- Can cached responses expose private information?
- What happens when a document is deleted or its permissions change?

---

## 4. Core RAG Vulnerabilities

### 4.1 Document Poisoning

Document poisoning occurs when malicious or misleading content is inserted into a knowledge base to influence retrieval or downstream model responses.

Potential sources include:
- Untrusted file uploads
- Compromised data sources
- Malicious external documents
- Unauthorized changes to indexed content

**Defensive measures:**
- Authenticate document sources.
- Validate document ownership and provenance.
- Restrict who can modify indexed data.
- Maintain version history and audit logs.
- Re-index or remove documents when necessary.
- Evaluate retrieval results for suspicious content.

**Practice:** Use synthetic documents in a local RAG application and compare how trusted and untrusted documents affect retrieval results.

### 4.2 Indirect Prompt Injection

Indirect prompt injection occurs when instructions embedded in retrieved content influence an LLM.

For example, a retrieved document might contain text that attempts to override the application's intended behavior or encourage an unauthorized action.

**Defensive measures:**
- Treat retrieved documents as untrusted data.
- Separate instructions from retrieved content where possible.
- Limit the tools available to the model.
- Enforce permissions in application code.
- Require approval for sensitive actions.
- Test the complete retrieval-to-response workflow.

**Practice:** Add a harmless test document containing conflicting instructions to a local knowledge base. Verify that the application does not allow the retrieved text to bypass authorization or trigger restricted actions.

### 4.3 Cross-User Data Leakage

Cross-user data leakage occurs when a user receives information belonging to another user or tenant.

Possible causes:
- Missing authorization filters
- Incorrect document ownership metadata
- Shared indexes without adequate isolation
- Insecure caching
- Application-level access-control mistakes

**Defensive measures:**
- Derive tenant identity from authenticated server-side context.
- Enforce document-level authorization before retrieval results are exposed.
- Validate ownership metadata.
- Isolate tenant-specific caches and indexes where appropriate.
- Test with multiple synthetic users.

**Practice:** Create two test users with different document permissions. Verify that each user can retrieve only authorized documents.

### 4.4 Retrieval Manipulation

Retrieval manipulation attempts to influence which documents are returned for a query.

Potential causes:
- Maliciously crafted content
- Poor retrieval configuration
- Incorrect metadata filters
- Misleading or irrelevant documents
- Weak ranking and relevance checks

**Defensive measures:**
- Validate source quality.
- Enforce access control independently of relevance scores.
- Evaluate retrieval precision and recall.
- Monitor unexpected retrieval patterns.
- Test with adversarial and benign query sets.

**Practice:** Build a small evaluation dataset and compare retrieval results before and after introducing controlled misleading documents.

### 4.5 Embedding Security Risks

Embeddings represent text or other data as numerical vectors. They are useful for semantic search but do not provide authorization or confidentiality by themselves.

Potential concerns:
- Sensitive content entering an index
- Unauthorized access to vector records
- Retrieval of semantically similar but inappropriate content
- Exposure through vector database backups or logs

**Defensive measures:**
- Minimize sensitive information in indexed content.
- Restrict vector database access.
- Apply authorization and metadata filtering.
- Protect backups and stored records.
- Evaluate the privacy implications of embeddings.

### 4.6 Insecure Document Ingestion

A RAG system may process PDFs, HTML, office documents, or other uploaded content.

Risks include:
- Untrusted document content
- Incorrect document classification
- Unsafe file parsing
- Excessive file sizes
- Malformed metadata
- Unauthorized indexing

**Defensive measures:**
- Validate file types and sizes.
- Use isolated document-processing environments.
- Apply appropriate parser security controls.
- Verify source ownership and permissions.
- Record document provenance.
- Reject unsupported or malformed files.

---

## 5. Vector Database Security

Vector databases store embeddings and often associated text, metadata, or references to source documents.

### Security Topics

- Authentication and Authorization
- Network Isolation
- Tenant Isolation
- Metadata Filtering
- Document-Level Permissions
- Encryption and Secret Management
- Backup Security
- Retention and Deletion
- Audit Logging
- Secure Configuration

### Technologies to Explore

| Technology | Learning Resource |
|---|---|
| FAISS | https://github.com/facebookresearch/faiss |
| Chroma | https://docs.trychroma.com/ |
| Qdrant | https://qdrant.tech/documentation/ |
| Milvus | https://milvus.io/docs |
| Weaviate | https://docs.weaviate.io/ |

These technologies have different deployment and security characteristics. Review each product's official documentation before selecting one.

### Security Exercise

Build a local vector index with synthetic documents belonging to two tenants.

Implement a retrieval function that:

1. Accepts an authenticated tenant identity from trusted application context.
2. Applies the required authorization constraints.
3. Retrieves relevant documents.
4. Verifies document ownership before exposing results.
5. Records security-relevant events without logging unnecessary sensitive content.

---

## 6. RAG Security Tools

Use the following resources to explore RAG evaluation and AI security testing.

| Tool or Framework | Purpose | Link |
|---|---|---|
| Ragas | RAG evaluation metrics and testing | https://github.com/vibrantlabsai/ragas |
| DeepEval | LLM and RAG evaluation | https://github.com/confident-ai/deepeval |
| garak | LLM vulnerability probing | https://github.com/NVIDIA/garak |
| Promptfoo | LLM evaluation and red teaming | https://github.com/promptfoo/promptfoo |
| PyRIT | Generative AI red teaming | https://github.com/Azure/PyRIT |

### What to Evaluate

- Retrieval relevance
- Context precision and recall
- Answer correctness
- Source attribution
- Unauthorized data retrieval
- Prompt injection resistance
- Security regression tests

**Important:** Evaluation metrics are not proof of security. Combine automated evaluation with explicit authorization tests, architecture review, and manual verification.

---

## 7. Hands-On Labs

All exercises should use synthetic data, isolated environments, and applications you own or have permission to test.

### Beginner Labs

#### Lab 01: Build a Mini RAG Application
Create a local application that retrieves passages from a small collection of public or synthetic documents.

Learn:
- Chunking
- Embeddings
- Vector search
- Context construction

#### Lab 02: Inspect Retrieval Results
Create several documents with overlapping topics and examine which passages are returned.

Learn:
- Similarity search
- Retrieval ranking
- Relevance evaluation

### Intermediate Labs

#### Lab 03: Document Poisoning Simulation
Introduce controlled misleading content into a test knowledge base.

Learn:
- Source validation
- Content provenance
- Retrieval evaluation
- Data integrity controls

#### Lab 04: Cross-Tenant Access-Control Testing
Create two synthetic users with separate document permissions.

Learn:
- Tenant isolation
- Authorization filtering
- Negative security tests

#### Lab 05: Indirect Prompt Injection Evaluation
Use a harmless test document containing conflicting instructions.

Learn:
- Untrusted context handling
- Tool authorization
- Security evaluation

### Advanced Labs

#### Lab 06: Secure RAG Pipeline
Build a RAG application with document authorization, secure ingestion, and automated regression tests.

#### Lab 07: RAG Security Evaluation Suite
Create a repeatable suite that evaluates retrieval quality, access control, and prompt-injection handling.

### Recommended Lab Structure

```text
lab-name/
├── README.md
├── app/
├── data/
│   └── synthetic-documents/
├── tests/
├── solutions/
├── requirements.txt
└── SECURITY-NOTES.md
```

Each lab should explain its objective, setup, expected results, vulnerabilities, mitigations, and validation tests.

---

## 8. Secure RAG Engineering

### Recommended Security Controls

#### Document Ingestion
- Verify the origin and ownership of documents.
- Validate uploaded files.
- Record provenance and version history.
- Restrict indexing privileges.

#### Retrieval
- Enforce authorization before retrieved content is exposed.
- Apply tenant isolation.
- Validate metadata used for access decisions.
- Test access-control filters independently of similarity scores.

#### Model Context
- Treat retrieved content as untrusted.
- Minimize unnecessary sensitive information.
- Avoid relying on prompt instructions as the sole defense.
- Restrict downstream tool access.

#### Application
- Validate model outputs.
- Protect API keys and database credentials.
- Apply rate limits and timeouts.
- Prevent cross-user caching errors.
- Monitor security-relevant events.

#### Testing
- Use negative authorization tests.
- Include malicious and benign documents in test datasets.
- Verify that defenses work after code changes.
- Re-test document deletion and permission updates.

### Secure RAG Design Principle

**Retrieval relevance and access authorization are separate concerns.**

A document may be highly relevant to a query but still be unauthorized for the requesting user.

---

## 9. Research Papers and Resources

Use these resources to discover research on retrieval systems, prompt injection, and AI security.

| Resource | Focus | Link |
|---|---|---|
| OWASP GenAI Security Project | AI application security | https://genai.owasp.org/ |
| arXiv | Research papers | https://arxiv.org/ |
| USENIX Security | Security research | https://www.usenix.org/conferences |
| IEEE Xplore | AI and cybersecurity research | https://ieeexplore.ieee.org/ |
| NIST AI Risk Management Framework | AI risk management | https://www.nist.gov/itl/ai-risk-management-framework |

### Research Topics

- Security of Retrieval-Augmented Generation
- Indirect Prompt Injection
- Knowledge-Base Poisoning
- Vector Database Privacy
- Retrieval-Time Authorization
- RAG Evaluation and Robustness
- Secure Enterprise Knowledge Assistants

When adding papers, record the title, authors, publication year, main findings, limitations, and official publication link.

---

## 10. RAG Security Checklist

Use this checklist when assessing a RAG application.

### Data Ingestion
- [ ] Document sources are verified.
- [ ] File types and sizes are validated.
- [ ] Document ownership and provenance are recorded.
- [ ] Unauthorized document changes are restricted.

### Vector Database
- [ ] Database access is authenticated.
- [ ] Tenant isolation is enforced.
- [ ] Sensitive data and backups are protected.
- [ ] Metadata cannot independently grant unauthorized access.

### Retrieval
- [ ] Authorization is enforced before content is exposed.
- [ ] Retrieval filters are tested.
- [ ] Cross-user data leakage tests are included.
- [ ] Deleted or newly restricted documents are handled correctly.

### LLM Integration
- [ ] Retrieved documents are treated as untrusted.
- [ ] Prompt injection scenarios are evaluated.
- [ ] Tool permissions are enforced outside the model.
- [ ] Model outputs are validated.

### Operations
- [ ] Secrets are stored securely.
- [ ] Rate limits and resource controls are applied.
- [ ] Security events are monitored.
- [ ] Regression tests are maintained.

---

## 11. Knowledge Check

1. What is the difference between an LLM and a RAG application?
2. What are the major stages of a RAG pipeline?
3. How can document poisoning affect retrieval results?
4. What is indirect prompt injection?
5. Why are embeddings not an access-control mechanism?
6. How can cross-tenant data leakage occur?
7. Why must authorization be enforced outside the model?
8. What is the difference between retrieval relevance and document authorization?
9. How can document provenance improve security?
10. How would you test a RAG system that contains confidential documents?

Try answering each question with a practical example and a mitigation strategy.

---

## 12. Next Steps

Continue your learning with:

- [AI Security Foundations](../01-foundations/README.md)
- [LLM Security](../02-llm-security/README.md)
- [AI Agent Security](../04-ai-agent-security/README.md)
- [AI Security Tools](../05-ai-security-tools/README.md)
- [Research Papers](../06-research-papers/README.md)
- [Hands-On Labs](../07-hands-on-labs/README.md)

### Core References

- OWASP GenAI Security Project: https://genai.owasp.org/
- MITRE ATLAS: https://atlas.mitre.org/
- NIST AI Risk Management Framework: https://www.nist.gov/itl/ai-risk-management-framework

---

**Learning Philosophy:** Understand the data pipeline, identify trust boundaries, enforce authorization, test adversarial scenarios, and verify every security control.
