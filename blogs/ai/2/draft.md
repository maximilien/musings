# On Vector Search: AI Agents' Knowledge

*Understanding where vector databases fit—and where they don't—in the AI agent stack*

**TL;DR:** AI agents need context to answer questions beyond their training data. MCP solved the services and tools problem; vector databases are one answer to the unstructured data problem. VDBs have exploded with the RAG wave, with the market valued at $2.2B in 2024 and projected to reach $7-10B by 2030-2032. But they're not always the right choice. Understanding when to use them—and when not to—is essential for building effective agent systems.

---

AI agents need context.

Without it, even the most sophisticated model is trapped behind its training cutoff, unable to answer questions about your company's policies, last quarter's sales, or that document you uploaded five minutes ago. The agent might be brilliant at reasoning, but brilliance without knowledge is just eloquent guessing.

Two complementary solutions have emerged. The Model Context Protocol (MCP), which Anthropic introduced in November 2024 and donated to the Linux Foundation's Agentic AI Foundation in December 2025, provides a universal standard for connecting AI systems to external services and tools. MCP has seen remarkable adoption—over 97 million monthly SDK downloads across Python and TypeScript, with over 10,000 active servers and first-class client support across ChatGPT, Claude, Cursor, Gemini, Microsoft Copilot, and Visual Studio Code. The Agentic AI Foundation was co-founded by Anthropic, Block, and OpenAI, with support from Google, Microsoft, AWS, Cloudflare, and Bloomberg.

But MCP solves the *services* context problem. What about *knowledge*? What about the unstructured documents, the institutional memory, the domain expertise that lives in PDFs and wikis and Slack threads?

This is where vector databases enter the picture. And this is where things get interesting—because vector databases are powerful, but they're not always the right answer.

## What Are Vector Databases?

The core concept is deceptively simple: semantic search on unstructured data.

Traditional databases store data in rows and columns. You query them with exact matches: "Find all customers in California" or "Show me orders from last month." This works beautifully for structured data with known schemas.

But what if you want to ask: "Find documents similar to this one"? Or "What do we know about customer onboarding challenges"? Traditional databases can't answer these questions because they don't understand *meaning*—only exact matches.

Vector databases solve this by storing *embeddings*: numerical representations of content that capture semantic meaning. When you embed a document, you convert its meaning into a point in high-dimensional space. Similar documents cluster together. Different documents are far apart.

**The theory fundamentals:**

Embeddings typically have hundreds or thousands of dimensions (OpenAI's text-embedding-3-large uses 3,072; Cohere's embed-v4 uses 1,024). At query time, you embed your question and find the nearest neighbors in vector space using distance metrics like cosine similarity or Euclidean distance.

Finding exact nearest neighbors in high-dimensional space is computationally expensive at scale. So vector databases use Approximate Nearest Neighbor (ANN) algorithms—most commonly HNSW (Hierarchical Navigable Small World)—that trade perfect accuracy for dramatic speed improvements. A system running at 99% recall misses 1 in 100 relevant documents; at 95% recall, it misses 1 in 20. That difference matters for production systems.

**Embeddings are key:**

The quality of your vector search depends heavily on your embedding model. Different models excel at different tasks—some are optimized for code, others for legal text, others for multilingual content. The choice of embedding model often matters more than the choice of vector database.

**Top embedding models (as of late 2025, per MTEB benchmarks):**

| Model | Dimensions | MTEB Score | Price/1M tokens | Best For |
|-------|------------|------------|-----------------|----------|
| Cohere embed-v4 | 1,024 | 65.2 | $0.10 | Multilingual, search, multimodal |
| OpenAI text-embedding-3-large | 3,072 (configurable) | 64.6 | $0.13 | General purpose, high accuracy |
| Voyage AI voyage-3-large | 1,536 | 63.8 | $0.12 | Domain tuning |
| BGE-M3 (open source) | 1,024 | 63.0 | Free | Self-hosted, multilingual |
| E5-Mistral-7B-Instruct | 4,096 | 61.8 | Free | Open-source |
| OpenAI text-embedding-3-small | 1,536 | 55.8 | $0.02 | Cost-effective |

For most use cases, start with OpenAI's text-embedding-3-small for prototyping (cheap and good enough), then evaluate Cohere embed-v4 or text-embedding-3-large for production. If you need to self-host or have budget constraints, BGE-M3 is the strongest open-source option with support for 100+ languages and hybrid dense/sparse retrieval.

## Good Uses of Vector Databases

Vector databases shine in several scenarios:

**Flexibility across modalities:**

VDBs work with any data that can be embedded: text, images, audio, video, code. You can build systems that search across modalities—finding images similar to a text description, or documents related to a diagram. This flexibility is genuinely powerful for building rich knowledge systems.

**Scale:**

Modern vector databases handle billions of vectors with sub-100ms query times. Milvus, Qdrant, Pinecone, and others have proven this at production scale. If you need to search across millions of documents, vector search is the proven path.

**Semantic understanding:**

Unlike keyword search, vector search understands meaning. "How do I reset my password?" and "I forgot my login credentials" might share no keywords, but vector search recognizes they're asking the same question. This semantic understanding is what makes RAG systems feel intelligent rather than merely indexed.

**Ecosystem maturity:**

The tooling has matured rapidly. Strong open-source options exist: Qdrant (Rust-based, excellent performance), Milvus (battle-tested at scale), Weaviate (strong hybrid search), Chroma (developer-friendly for prototyping). Cloud options like Pinecone provide managed simplicity. Integration with frameworks like LangChain and LlamaIndex is straightforward.

## Not-So-Good Uses of Vector Databases

Here's where honest assessment matters:

**Chunking is an unsolved problem:**

To embed documents, you must chunk them—split them into pieces that fit within embedding model context windows. But chunking can split semantic meaning. A question might be answered by information spanning two chunks that never appear together in search results.

There's no perfect chunking strategy. Fixed-size chunks are simple but semantically arbitrary. Semantic chunking is smarter but computationally expensive. Overlapping chunks help but increase storage and cost. Every choice has tradeoffs, and those tradeoffs propagate through your entire system.

**Metadata complexity:**

Raw vector search is often insufficient. You typically need to combine semantic search with metadata filtering (by date, document type, permissions) and sometimes keyword search for precise terms. This "hybrid search" is more complex to implement and tune than pure vector search.

**Approximate results require processing:**

Vector search returns *approximate* matches ranked by similarity scores. The top results aren't guaranteed to contain the answer—they're guaranteed to be *similar* to the question, which isn't the same thing. Production systems often need re-ranking stages (using cross-encoders or LLMs) to improve precision before presenting results to users.

**Cost accumulates:**

Good embedding models aren't free. Vectorizing millions of documents takes time and money. Storage scales with data size and dimensionality. For small datasets, this overhead may not be worth it.

## What Vector Databases Are Bad At

Sometimes vector databases are simply the wrong tool:

**Precise search:**

If you need exact matches—specific product SKUs, legal citations, error codes—traditional search is better. Vector search optimizes for semantic similarity, which actively works against precision for these use cases.

**Structured data:**

If your data can be structured with known schemas, use a relational database. SQL beats semantic search for structured queries, every time. "Show me all orders over $1,000 from Q4" doesn't need embeddings.

**Small datasets:**

For collections under 10,000 chunks, the overhead of vector databases often isn't worth it. Simple keyword search with BM25 might suffice. Chroma is popular for prototyping precisely because it minimizes this overhead—but teams regularly migrate to more robust solutions as they scale.

**Relationship-heavy data:**

If your questions involve traversing relationships ("What vendors does this customer's subsidiary use?"), knowledge graphs may serve you better than vector search. Graph databases excel at relationship queries; vector databases excel at similarity queries.

## Alternatives and Complements

The RAG landscape is evolving beyond pure vector search:

**Hybrid search** combines vector similarity with keyword matching (BM25) and metadata filtering. Weaviate, Qdrant, and Pinecone all support this natively. For most production systems, hybrid search outperforms pure vector search.

**Knowledge graphs and GraphRAG** structure information as entities and relationships. Microsoft's GraphRAG creates a knowledge graph from an input corpus, using community summaries and graph machine learning outputs to augment prompts at query time. GraphRAG excels at reasoning across documents and answering "corpus-wide" questions that require connecting multiple pieces of information—questions like "What are the five key themes across this entire document set?" However, it comes with higher indexing costs and complexity. For many specific, fact-retrieval questions, traditional ("naive") RAG actually outperforms GraphRAG.

**LightRAG** offers a simpler, faster, and more cost-efficient alternative to full GraphRAG, combining knowledge graphs with embedding-based retrieval without the heavy community-hierarchy overhead. Good choice for teams that want graph-aware retrieval without the complexity.

**LLM-driven retrieval** uses the language model itself to iteratively retrieve and refine results, rather than relying on a single vector search query.

**Prompt-based retrieval** skips embeddings entirely for some use cases, using the LLM's own understanding to select relevant context—particularly viable now that context windows have grown to 100K+ tokens.

## Choosing a Vector Database

If you've determined a vector database is right for your use case, here's how to choose:

**For prototyping and small scale:**
- **Chroma**: Developer-friendly, simple API, free. Excellent for getting started. Outgrow it and migrate when you hit scale.
- **pgvector**: If you're already on PostgreSQL, adding vector search is straightforward. Not as fast as dedicated solutions, but eliminates operational complexity.

**For production scale (open source):**
- **Qdrant**: Rust-based, excellent performance, strong filtering, cost-effective. My current recommendation for teams that want control without excessive operational burden.
- **Milvus**: Battle-tested at billion-vector scale. More operational complexity, but proven. Zilliz provides managed hosting.
- **Weaviate**: Strong hybrid search, good documentation, GraphQL API. Solid middle ground. Also provides managed hosting.

**For managed simplicity:**
- **Pinecone**: Fully managed, easy to use, reliable. Higher cost, but minimal operational overhead. Good default for teams that don't want to manage infrastructure.

**Decision framework:**

1. If you need it yesterday and don't want to manage anything: Pinecone, Weaviate Cloud, Zilliz Cloud
2. If you have ops capacity and want cost efficiency at scale: Qdrant or Milvus
3. If hybrid search is critical: Weaviate or Qdrant
4. If you're prototyping: Chroma
5. If you're already on Postgres and scale is moderate: pgvector (Supabase)

## The Agent Context Story

How do vector databases fit into the broader agent architecture?

**MCP for services, VDBs for knowledge:**

MCP provides the protocol for agents to connect to external tools and services—databases, APIs, file systems, communication platforms. Vector databases provide the knowledge layer—the long-term memory and domain expertise that agents retrieve when answering questions.

These are complementary, not competing. An agent might use MCP to connect to your company's Slack, then use vector search to find relevant documentation based on the conversation context.

**Long-term memory:**

Vector databases can store not just documents but conversation history, user preferences, and learned context. This enables agents to "remember" across sessions—a capability that feels magical when it works well.

**Integration with frameworks:**

LangChain, LlamaIndex, and similar frameworks provide abstractions for working with vector databases. These make it easier to experiment with different databases and retrieval strategies without rewriting your entire system.

**weave-cli and the ecosystem:**

[PLACEHOLDER: Add details about weave-cli—your tool for working across VDBs. What problem does it solve? Development/testing/production workflows? What makes it different from existing tools?]

This is an area I'm actively working on and will cover in more detail in a future post.

## Conclusion

Vector databases are a powerful part of the AI agent context story. They excel at unstructured data and scale well. A strong ecosystem of open-source and managed options exists.

But they're not magic. They require upfront decisions about chunking, embedding models, and retrieval strategies. They work best as part of hybrid systems that combine semantic search with other approaches. And they're not the right choice for every knowledge retrieval problem.

The key insight: vector databases are one tool in the agent knowledge toolkit, not the entire toolkit. Use them where they shine—semantic search over unstructured data at scale—and use other tools where they don't.

The dream of AI agents with comprehensive knowledge access is becoming real. MCP solved services. Vector databases are one answer to knowledge. The pieces are coming together—and understanding how they fit is essential for building agents that actually work.

---

*Next post: AI Agents Meetup SF: One Year Retrospective—lessons from nine meetups, 500+ attendees per event, and the evolution of the agent ecosystem.*

*Previous post: [AI Coding Assistants](link-to-post)*

---

## Recommended Resources

**Papers:**
- "Efficient and Robust Approximate Nearest Neighbor Search Using Hierarchical Navigable Small World Graphs" — the HNSW paper
- "Dense Passage Retrieval for Open-Domain Question Answering" — Karpukhin et al.
- "From Local to Global: A Graph RAG Approach to Query-Focused Summarization" — Microsoft Research (GraphRAG)
- Original Word2Vec and BERT embedding papers

**Books:**
- *Introduction to Information Retrieval* — Manning, Raghavan, Schütze (free online)
- *Designing Data-Intensive Applications* — Kleppmann (relevant chapters on search)

**Documentation & Learning:**
- [Pinecone Learning Center](https://www.pinecone.io/learn/)
- [Qdrant Documentation](https://qdrant.tech/documentation/)
- [Weaviate Documentation](https://weaviate.io/developers/weaviate)
- [Microsoft GraphRAG Documentation](https://microsoft.github.io/graphrag/)
- LlamaIndex and LangChain VDB integrations

**Benchmarks:**
- [ann-benchmarks.com](http://ann-benchmarks.com) — ANN algorithm comparisons
- [MTEB Leaderboard](https://huggingface.co/spaces/mteb/leaderboard) — Embedding model benchmarks
- [VectorDBBench](https://github.com/zilliztech/VectorDBBench) — Vector database benchmarks

**MCP Resources:**
- [Model Context Protocol](https://modelcontextprotocol.io/) — Official documentation
- [MCP Blog](https://blog.modelcontextprotocol.io/) — Updates and technical posts
- [Agentic AI Foundation Announcement](https://www.anthropic.com/news/donating-the-model-context-protocol-and-establishing-of-the-agentic-ai-foundation)

---

## Items to Verify/Research Before Publishing

### ✅ Completed

1. **Market size stats:** Updated to $2.2B in 2024, projected $7-10B by 2030-2032 (sources: GMInsights, MarketsandMarkets, SNS Insider—various estimates, used range)
2. **MCP stats:** Confirmed 97M+ monthly SDK downloads, 10,000+ active servers, support across major platforms (source: MCP Blog, Anthropic announcement)
3. **Embedding model recommendations:** Added table with specific models, dimensions, MTEB scores, and pricing (source: MTEB leaderboard, provider docs)
4. **GraphRAG/alternatives:** Added detail on Microsoft GraphRAG, LightRAG, and when each excels (source: Microsoft Research, GraphRAG docs)

### ⏳ Pending

5. [ ] **VDB pricing:** Current tiers for Pinecone, Qdrant Cloud, Weaviate Cloud, Zilliz (prices change frequently—verify before publish)
6. [ ] **weave-cli details:** Add specifics about your tool—what it does, how it helps
7. [ ] **Chunking strategies:** Consider adding more practical guidance (or save for future post)
8. [ ] **Personal experience:** Add anecdotes from your own VDB usage
9. [ ] **Recall/precision tradeoffs:** Consider adding concrete examples
10. [ ] **Cross-link:** Link to AI Coding Assistants post once published

---

*Word count: ~2,400 words (target: ~2,000—slightly over but covers the topic comprehensively)*
