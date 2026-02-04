On Vector Search: AI Agents' Knowledge

Target length: ~2000 words

Abstract
* AI Agents need context and access to services to answer esoteric/idiosyncratic questions
* MCP (Model Context Protocol) solved the services context question
* Vector databases are one answer to the unstructured data context question
* VDBs have boomed with the RAG wave of AI
* Many companies focused on VDBs and scaling them (many open source)
* But are vector databases the best solution for Agent knowledge and memory?

Introduction
* VDBs have risen dramatically with RAG (Retrieval Augmented Generation)
* [History of vector databases: from academic research to production systems]
* [Alternatives to VDBs: traditional search, knowledge graphs, hybrid approaches]
* Setting the stage: understanding where VDBs fit in the AI stack

What Are Vector Databases?
* Core concept:
    * Semantic search on unstructured data
    * Many algorithms, but all center on embeddings
    * Create embedding (vector) space, use it for semantic similarity
* Theory fundamentals:
    * Vector space models and dimensionality
    * Cosine similarity and distance metrics
    * Approximate nearest neighbor (ANN) algorithms
    * [HNSW, IVF, and other indexing approaches]
* Embeddings are key:
    * Quality depends on embedding model choice
    * Different models for different domains
    * Trade-offs: size, speed, quality
    * [OpenAI embeddings, Cohere, open source options]
* VDBs are one approach — they have strengths and weaknesses

Good Uses of VDBs
* Flexibility:
    * Works with different data types: text, images, audio
    * Chunking allows large documents to be processed
    * Semantic information from vector embedding
* Performance:
    * Vector search can scale to billions of vectors
    * Sub-millisecond query times with proper indexing
    * Different algorithms for different performance profiles
* Ecosystem:
    * Proven technology with production deployments
    * Many open source options: Qdrant, Milvus, Weaviate, Chroma
    * Hosted cloud versions for easy deployment

Not-So-Good Uses of VDBs
* Chunking challenges:
    * Data must be chunked — can split semantic meaning
    * Chunk size decisions have downstream effects
    * No perfect chunking strategy exists
* Metadata complexity:
    * Need to add metadata and potentially vectorize it
    * Hybrid search (keyword + semantic) often needed
    * LLM can summarize documents, but at cost
* Result processing:
    * Search results are approximate, not precise
    * Often need re-ranking stage
    * Results still need LLM processing to present to users
* Cost considerations:
    * Good embedding models aren't free or open source
    * Vectorization adds latency and cost
    * Storage scales with data size

What VDBs Are Bad At
* Precise search:
    * If you need exact matches, traditional search is better
    * Keyword search has its place
    * Hybrid approaches often necessary
* Structured data:
    * If data can be structured, use relational databases
    * SQL still beats semantic search for structured queries
    * Graph databases for relationship queries
* Small datasets:
    * Overhead not worth it for small collections
    * Simple keyword search might suffice
    * Cost-benefit analysis matters

Choosing a Vector Database
* Open source options:
    * Qdrant: Rust-based, great performance
    * Milvus: Scalable, enterprise features
    * Weaviate: Graph-like queries
    * Chroma: Simple, developer-friendly
* Cloud/Managed options:
    * Pinecone: Fully managed, easy to use
    * Zilliz: Milvus cloud
    * Weaviate Cloud: Managed Weaviate
* Embedded in other databases:
    * PostgreSQL with pgvector
    * Redis with vector search
    * Elasticsearch dense vectors

The Agent Context Story
* How VDBs fit in agent architecture:
    * Long-term memory storage
    * Knowledge base retrieval
    * Context augmentation for queries
* Integration with MCP:
    * MCP for services and tools
    * VDBs for knowledge and memory
    * Complementary, not competing
* weave-cli and the ecosystem:
    * Building tools to work across VDBs
    * Development, testing, production workflows
    * More details coming in future posts

Conclusion
* VDBs are part of the AI Agents context story
* They excel at unstructured data and scale well
* Various options available, including strong OSS choices
* They require processing and upfront decisions
* Flexible but require you to make key choices
* weave-cli, MCP, and Agent frameworks are OSS projects that can help

Recommended Research

Papers:
* "Efficient and Robust Approximate Nearest Neighbor Search" — HNSW paper
* "Dense Passage Retrieval for Open-Domain Question Answering" — Karpukhin et al.
* Original Word2Vec and BERT embedding papers

Books:
* "Introduction to Information Retrieval" — Manning, Raghavan, Schütze
* "Designing Data-Intensive Applications" — Kleppmann (relevant chapters)

Resources:
* Pinecone Learning Center
* Qdrant documentation and blog
* LlamaIndex and LangChain VDB integrations

Comparisons:
* VectorDB benchmarks (ann-benchmarks.com)
* MTEB embedding benchmarks

Bibliography
[To be populated with specific citations]