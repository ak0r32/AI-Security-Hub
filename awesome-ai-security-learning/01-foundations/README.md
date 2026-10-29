
# 🧠 AI Security Foundations

A curated collection of learning resources for understanding Artificial Intelligence, Machine Learning, Deep Learning, Large Language Models, and modern AI architectures from a security perspective.

This section establishes the technical foundation required to identify, understand, and mitigate vulnerabilities in AI-powered applications.

---

## 📚 Table of Contents

- [Learning Objectives](#-learning-objectives)
- [1. Artificial Intelligence Fundamentals](#1-artificial-intelligence-fundamentals)
- [2. Machine Learning Fundamentals](#2-machine-learning-fundamentals)
- [3. Deep Learning and Neural Networks](#3-deep-learning-and-neural-networks)
- [4. Large Language Models](#4-large-language-models-llms)
- [5. Transformers and Attention](#5-transformers-and-attention)
- [6. Tokens, Embeddings, and Context Windows](#6-tokens-embeddings-and-context-windows)
- [7. Retrieval-Augmented Generation](#7-retrieval-augmented-generation-rag)
- [8. AI Agents and Tool Calling](#8-ai-agents-and-tool-calling)
- [9. AI Application Architecture](#9-ai-application-architecture)
- [10. Python and AI Development Tools](#10-python-and-ai-development-tools)
- [11. AI Security Learning Exercises](#11-ai-security-learning-exercises)
- [12. Knowledge Check](#12-knowledge-check)
- [13. Next Steps](#13-next-steps)

---

## 🎯 Learning Objectives

After completing this section, learners should be able to:

- Explain the differences between AI, ML, and Deep Learning.
- Understand how neural networks learn from training data.
- Explain the basic architecture of an LLM.
- Understand tokens, embeddings, and context windows.
- Describe how RAG applications retrieve external information.
- Explain how AI agents interact with tools and external systems.
- Identify trust boundaries and potential attack surfaces in AI applications.
- Understand why traditional application security remains important for AI systems.

---

## 1. Artificial Intelligence Fundamentals

### What Is Artificial Intelligence?

Artificial Intelligence (AI) is a field of computer science focused on developing systems that perform tasks associated with human intelligence, such as reasoning, language processing, prediction, and decision-making.

### Core Concepts

- Artificial Intelligence (AI)
- Machine Learning (ML)
- Deep Learning (DL)
- Generative AI
- Natural Language Processing (NLP)
- Computer Vision
- Reinforcement Learning

### Learning Resources

| Resource | Description | Link |
|---|---|---|
| Elements of AI | Introduction to AI concepts | https://www.elementsofai.com/ |
| Google Machine Learning | Foundational ML learning resources | https://developers.google.com/machine-learning |
| IBM AI Fundamentals | AI concepts and applications | https://www.ibm.com/think/topics/artificial-intelligence |

### Security Perspective

Understand how AI systems depend on data, models, software, and external services.

Security questions:
- What happens when the input data is manipulated?
- How can sensitive information enter a model's context?
- How should an AI application's output be validated?
- What risks arise when an AI system can take actions?

---

## 2. Machine Learning Fundamentals

Machine Learning enables systems to learn patterns from data and use those patterns to make predictions or decisions.

### Core Topics

- Supervised Learning
- Unsupervised Learning
- Reinforcement Learning
- Training, Validation, and Test Data
- Feature Engineering
- Model Evaluation
- Overfitting and Underfitting
- Classification and Regression
- Model Generalization

### Learning Resources

| Resource | Description | Link |
|---|---|---|
| Google ML Crash Course | Practical introduction to ML | https://developers.google.com/machine-learning/crash-course |
| scikit-learn Documentation | ML algorithms and implementation | https://scikit-learn.org/stable/user_guide.html |
| Kaggle Learn | Practical ML exercises | https://www.kaggle.com/learn |

### Security Perspective

Study how manipulated training data, biased datasets, adversarial inputs, and insecure model deployment can affect system reliability and security.

Important concepts:
- Data poisoning
- Adversarial examples
- Model evasion
- Model extraction
- Membership inference
- Training data privacy

---

## 3. Deep Learning and Neural Networks

Deep Learning uses neural networks with multiple layers to learn complex patterns from data.

### Core Topics

- Artificial Neurons
- Activation Functions
- Forward Propagation
- Backpropagation
- Loss Functions
- Gradient Descent
- Training and Optimization
- Convolutional Neural Networks
- Recurrent Neural Networks

### Learning Resources

| Resource | Description | Link |
|---|---|---|
| PyTorch Tutorials | Build and train neural networks | https://pytorch.org/tutorials/ |
| TensorFlow Tutorials | Deep learning implementation | https://www.tensorflow.org/tutorials |
| Dive into Deep Learning | Interactive deep learning textbook | https://d2l.ai/ |

### Security Perspective

Understand how model architecture, training procedures, datasets, model weights, and inference interfaces introduce different security risks.

Explore adversarial robustness, model backdoors, training data integrity, and secure model distribution.

---

## 4. Large Language Models (LLMs)

Large Language Models are trained on large datasets to process and generate text and other supported forms of content.

### Core Topics

- LLM Architecture
- Pretraining and Fine-Tuning
- Instruction Tuning
- Inference
- Temperature and Sampling
- Model Parameters
- System and User Messages
- Context Management
- Function and Tool Calling

### Learning Resources

| Resource | Description | Link |
|---|---|---|
| Hugging Face LLM Course | LLMs, Transformers, and model usage | https://huggingface.co/learn/llm-course |
| Stanford CS336 | Language modeling foundations | https://cs336.stanford.edu/ |
| Hugging Face Transformers | Models and inference documentation | https://huggingface.co/docs/transformers/ |

### Security Perspective

Learn why LLMs should not automatically be treated as trusted decision-makers.

Important risks include:
- Prompt injection
- Jailbreaks
- Sensitive information disclosure
- Insecure output handling
- Untrusted tool instructions
- Model supply chain vulnerabilities

**Key principle:** An LLM's response is generated content, not a security authorization decision.

---

## 5. Transformers and Attention

Transformers are neural network architectures widely used in modern language models.

### Core Topics

- Self-Attention
- Multi-Head Attention
- Positional Information
- Encoder and Decoder Architectures
- Transformer Blocks
- Context Representation
- Next-Token Prediction

### Learning Resources

| Resource | Description | Link |
|---|---|---|
| The Illustrated Transformer | Visual explanation of Transformer architecture | https://jalammar.github.io/illustrated-transformer/ |
| Attention Is All You Need | Original Transformer research paper | https://arxiv.org/abs/1706.03762 |
| Hugging Face NLP Course | Transformer concepts and practice | https://huggingface.co/learn/llm-course |

### Security Perspective

Understand that attention mechanisms and model representations do not inherently enforce access controls, separate trusted instructions from untrusted data, or guarantee factual outputs.

Security must be implemented through the surrounding application architecture and appropriate model safeguards.

---

## 6. Tokens, Embeddings, and Context Windows

These concepts help explain how LLMs process text and how AI applications retrieve and manage information.

### Tokens

Tokens are units of text or other content processed by a model.

Learn:
- Tokenization
- Token limits
- Token counting
- Context-window constraints
- Resource consumption

### Embeddings

Embeddings are numerical representations of content that can be used to measure semantic similarity.

Learn:
- Vector representations
- Semantic similarity
- Embedding models
- Vector search
- Similarity metrics

### Context Windows

A context window limits the amount of information a model can process in a single interaction.

Learn:
- Context construction
- Conversation history
- Retrieved documents
- Context truncation
- Token budgets

### Learning Resources

| Resource | Description | Link |
|---|---|---|
| Hugging Face Tokenizers | Tokenization documentation | https://huggingface.co/docs/tokenizers/ |
| Sentence Transformers | Embeddings and semantic search | https://sbert.net/ |
| OpenAI Tokenizer | Explore tokenization | https://platform.openai.com/tokenizer |

### Security Perspective

Explore:
- Token-based resource exhaustion
- Sensitive information in context
- Untrusted retrieved content
- Embedding-based retrieval manipulation
- Data isolation between users

Remember that semantic similarity does not prove that retrieved content is trustworthy.

---

## 7. Retrieval-Augmented Generation (RAG)

RAG combines information retrieval with language generation. An application retrieves relevant external information and provides it to an LLM as context.

### Typical RAG Workflow

1. Collect documents.
2. Parse and split documents into chunks.
3. Generate embeddings.
4. Store vectors and associated metadata.
5. Retrieve relevant content for a query.
6. Construct the model context.
7. Generate a response.
8. Return the result to the user.

### Core Topics

- Document Ingestion
- Chunking Strategies
- Embedding Models
- Vector Databases
- Similarity Search
- Metadata Filtering
- Retrieval and Reranking
- Context Construction
- Response Evaluation

### Learning Resources

| Resource | Description | Link |
|---|---|---|
| LlamaIndex Documentation | Data ingestion and RAG pipelines | https://docs.llamaindex.ai/ |
| LangChain Documentation | LLM application development | https://python.langchain.com/docs/ |
| FAISS | Vector similarity search library | https://github.com/facebookresearch/faiss |

### Security Perspective

Study:
- Document poisoning
- Indirect prompt injection
- Unauthorized document retrieval
- Cross-user data leakage
- Insecure ingestion pipelines
- Retrieval manipulation

**Key principle:** Access control must be enforced before protected documents are exposed to the model, not merely through instructions in the prompt.

---

## 8. AI Agents and Tool Calling

AI agents use models to determine or coordinate actions, potentially involving tools, APIs, databases, and external services.

### Core Topics

- Agent Architecture
- Tool Calling
- Planning and Execution
- Agent Memory
- Multi-Agent Systems
- API Integration
- Human-in-the-Loop Workflows
- Permissions and Authorization

### Learning Resources

| Resource | Description | Link |
|---|---|---|
| LangGraph Documentation | Stateful agent workflows | https://docs.langchain.com/oss/python/langgraph/overview |
| Model Context Protocol | Connect AI applications to tools and data | https://modelcontextprotocol.io/ |
| Hugging Face Agents Course | Learn agent fundamentals | https://huggingface.co/learn/agents-course |

### Security Perspective

Explore:
- Excessive agent permissions
- Tool misuse
- Indirect prompt injection
- Memory poisoning
- Unsafe execution
- Untrusted tool results
- Missing human approval

**Key principle:** A model suggesting an action must not automatically grant that action permission to execute.

---

## 9. AI Application Architecture

Understand how an AI application connects models, APIs, users, databases, and external services.

### Typical Architecture

```text
User
  |
  v
Frontend / Client
  |
  v
Backend API
  |
  +----> Authentication and Authorization
  |
  +----> Input Validation
  |
  +----> Retrieval / External Data
  |
  v
LLM or AI Model
  |
  v
Output Validation and Policy Checks
  |
  v
Application Response
```

This is a simplified architecture. Real systems may use different component orders and additional controls.

### Security Components

- Authentication
- Authorization
- Input Validation
- Output Encoding
- Secrets Management
- Rate Limiting
- Data Access Controls
- Logging and Monitoring
- Human Approval for Sensitive Actions

### Security Perspective

Map every component, trust boundary, data flow, and external integration.

Use threat modeling to identify where attackers could manipulate inputs, access protected data, abuse model capabilities, or trigger unauthorized actions.

---

## 10. Python and AI Development Tools

Python is widely used for building AI prototypes, experiments, security tests, and automation.

### Recommended Tools

| Tool | Purpose | Link |
|---|---|---|
| Python | Programming language | https://www.python.org/ |
| Jupyter | Interactive experimentation | https://jupyter.org/ |
| NumPy | Numerical computing | https://numpy.org/ |
| Pandas | Data analysis | https://pandas.pydata.org/ |
| PyTorch | Deep learning | https://pytorch.org/ |
| Hugging Face | Models and datasets | https://huggingface.co/ |
| FastAPI | Build Python APIs | https://fastapi.tiangolo.com/ |
| Docker | Containerized environments | https://docs.docker.com/ |

### Recommended Skills

- Python fundamentals
- Working with JSON and APIs
- Data processing
- Virtual environments and dependency management
- Basic model inference
- HTTP and REST APIs
- Unit and integration testing
- Git and GitHub

---

## 11. AI Security Learning Exercises

Use these exercises to connect AI concepts with security practice.

### Exercise 1: Understand an LLM Application

**Task:** Build a simple application that sends a user prompt to a model.

Learn:
- Input processing
- Model inference
- Response handling
- API key protection

**Security objective:** Identify where validation, authentication, and secret management are required.

### Exercise 2: Explore Tokenization

**Task:** Compare how different text inputs are tokenized.

Learn:
- Token counts
- Context limits
- Input length

**Security objective:** Understand resource-consumption risks and why applications need appropriate limits.

### Exercise 3: Build a Mini RAG Pipeline

**Task:** Index a collection of public or synthetic documents and retrieve relevant passages.

Learn:
- Document chunking
- Embeddings
- Similarity search
- Context construction

**Security objective:** Implement document-level authorization and test whether unauthorized content can be retrieved.

### Exercise 4: Design an AI Agent

**Task:** Build a local agent with one harmless, read-only tool.

Learn:
- Tool schemas
- Model-directed actions
- Tool responses
- Workflow execution

**Security objective:** Enforce tool permissions outside the model and reject unauthorized operations.

### Exercise 5: Create an AI Threat Model

**Task:** Draw the architecture of a small AI application.

Identify:
- Assets
- Trust boundaries
- Entry points
- Sensitive data
- External dependencies
- Threats and mitigations

**Security objective:** Produce a threat model that can guide security testing.

---

## 12. Knowledge Check

Test your understanding before moving to the next section.

1. What is the difference between AI, Machine Learning, and Deep Learning?
2. How does an LLM generate text?
3. What is the role of embeddings in semantic search?
4. How does a RAG application retrieve information?
5. Why is retrieved content considered untrusted?
6. What is the difference between authentication and authorization?
7. Why should an AI agent not have unrestricted tool permissions?
8. Why must an application's output be validated?
9. Where should access control be enforced in a RAG system?
10. What is a trust boundary in an AI application?

Try answering these questions in your own words and support your answers with small experiments.

---

## 13. Next Steps

After completing these foundations, continue with the following topics:

1. **LLM Security:** Prompt injection, jailbreaks, information disclosure, and insecure output handling.
2. **RAG Security:** Document poisoning, retrieval manipulation, and access control.
3. **AI Agent Security:** Tool permissions, memory poisoning, and secure execution.
4. **AI Red Teaming:** Authorized adversarial testing and security evaluation.
5. **Defensive Engineering:** Implement mitigations and verify them through automated tests.

### Recommended Official Security References

- OWASP GenAI Security Project: https://genai.owasp.org/
- MITRE ATLAS: https://atlas.mitre.org/
- NIST AI Risk Management Framework: https://www.nist.gov/itl/ai-risk-management-framework

---

**Learning Philosophy:** Understand the technology, identify its trust boundaries, test security assumptions, and validate the defense.

**Next Section:** [LLM Security](../02-llm-security/README.md)
