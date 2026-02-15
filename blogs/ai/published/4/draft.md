# Selecting the Right Software Stack

*The decision you make early that haunts you later—and how AI is changing the calculus*

**TL;DR:** Your software stack choice is one of the most consequential decisions you'll make on a project. Get it wrong and you'll pay in scaling headaches, debugging nightmares, and eventual rewrites. From experience, most web services solutions follow predictable patterns, defaulting to Python (in previous years Ruby) for a rewrite. AI coding agents are making it easier to work in unfamiliar stacks—but they can also mask fundamental architectural mismatches, delaying the inevitable. Think carefully before you start, and especially before you move beyond a prototype.

---

## Introduction

### What is a Software Stack?

A software stack is the collection of languages, libraries, and services you use to build a solution. For any given problem, there are dozens of reasonable choices. Is there an optimal choice? Surely one stack doesn't fit all problems?

### The Default Stack Problem

In practice, most developers reach for what they know. The familiar stack. The one where they can be productive on day one. This is rational—familiarity reduces risk and speeds early development. But it's also how you end up maintaining a Python prototype that needed to be a Go service, or a monolithic Rails app that should have been microservices from the start.

Here's an underappreciated wrinkle: AI coding agents might actually delay the inevitability by hiding the issue. When fixing bugs and patching over problems becomes trivially easy, you might not notice that you're compensating for a fundamental stack mismatch. The ease of fixing masks the complexity of the underlying problem. But the underlying stack choice still matters—the debt compounds.

I've made this mistake. I've watched others make it. And with the current wave of AI-first development, I'm watching a new generation make it at unprecedented scale.

### The Current Landscape

Python stacks have become the default choice for AI solutions. There are good reasons for this, which I'll explore below. But other stacks are possible and sometimes preferable.

**The thesis:** The choice of the correct stack is key to long-term success. Think carefully before starting, and especially before moving beyond a prototype. AI agents make exploring unfamiliar stacks easier than ever before—but they can't save you from choosing the wrong one. And the Python AI wave will reveal its costs when prototypes need to go into production and scale.

## Why Your Software Stack Matters

### Components of a Stack

A typical stack decision involves multiple interconnected choices:

**Language** — The foundation of your codebase. Some languages have built-in features that make them better suited for certain workloads. Go's goroutines handle concurrency differently than Python's asyncio. Rust's ownership model prevents entire classes of bugs. Java's type system catches errors that Python only discovers at runtime.

**Libraries** — Frameworks, utilities, and dependencies. Historical accidents mean some languages have richer ecosystems for certain domains. Python dominates AI/ML not because it's the best language for the job, but because the research community standardized on it and built numpy, scikit-learn, PyTorch, and TensorFlow there first.

**Services** — Package management, external APIs, databases, cloud infrastructure. How does your stack integrate with the services you need? How painful is deployment?

**Maintenance** — Day 2 operations: keeping software running, upgrading dependencies, managing security patches. Some stacks make this easy; others make it a constant battle. This is often the most underestimated component—it's invisible until it isn't.

**Non-functionals** — Performance, security, reliability, maintainability. These matter more as you scale—often revealing problems you didn't anticipate when you started. A stack that feels frictionless at prototype scale can become a bottleneck at production scale.

### AI Stack Choices

#### The Python Ecosystem

Python has become the default choice for AI solutions. There are good reasons:

**The AI/ML ecosystem is unmatched.** PyTorch, TensorFlow, scikit-learn, pandas, numpy, LangChain, LlamaIndex—if you're building AI applications, the libraries you need are in Python first, often Python only. The research community writes Python. The tutorials are in Python. Your team probably knows Python.

**Prototyping speed is excellent.** Python's simplicity and dynamic typing let you move fast. You can go from idea to working demo in hours. For exploratory work, this matters enormously.

**AI coding agents know Python well.** The training data skews heavily toward Python, especially for AI-related code. Your AI assistant will be more helpful with Python than with less common languages.

But there are also good reasons to question Python's dominance:

**Python is slow.** Not 50x slower than C anymore, but still 5-20x slower than compiled languages for CPU-bound work. Instagram and YouTube use Python—but they also have teams dedicated to making Python not suck at scale. You probably don't.

**Concurrency is painful.** The Global Interpreter Lock (GIL) means Python can't efficiently use multiple CPU cores within a single process. You work around this with multiprocessing, but that brings its own complexity and memory overhead.

**Type safety is optional and incomplete.** Type hints help, but they're not enforced at runtime. The tooling has improved, but it still lags behind languages designed with types from the start.

**Large codebases get messy.** Python has no component model as sophisticated as Java Spring. Structuring complex applications quickly becomes painful. The frameworks that exist (Django, FastAPI) are good, but they're not designed for the kind of large-scale systems that enterprises typically need.

**Dependency management is improving but still fragile.** Virtual environments, uv, pip, conda, poetry—the tooling has gotten better, but it's still easier to end up in dependency hell than with npm or cargo.

#### Alternative Stacks

**Go (Golang)** — Exceptional concurrency model (goroutines and channels), fast compilation, simple deployment (single binary), strong standard library. Go excels at building the kind of high-throughput, concurrent services that AI systems often need around the core ML components. Less expressive than Python and a smaller AI/ML library ecosystem, but best for API servers, microservices, CLI tools, and infrastructure components.

**Rust** — Memory safety without garbage collection, performance comparable to C/C++, excellent package management (cargo), modern type system. Increasingly used for performance-critical AI infrastructure (Qdrant, for example, is written in Rust). Steep learning curve and slower development speed, but best for systems that need to be fast and reliable.

**Java/Kotlin** — Mature enterprise ecosystem, excellent tooling, proven at massive scale, strong type system, JVM optimizations, huge talent pool. Spring Boot provides a sophisticated component model. Verbose (Java more than Kotlin) and slower iteration than Python, but best for enterprise systems, large team projects, and anything requiring long-term maintainability.

**TypeScript/Node.js** — Full-stack unification (same language front and back), huge ecosystem (npm), good for I/O-bound services. Single-threaded event loop isn't ideal for CPU-bound work, but best for full-stack web applications and teams that want one language everywhere.

### Stack Comparison at a Glance

| Criteria | Python | Go | Rust | Java/Kotlin | TypeScript |
|---|---|---|---|---|---|
| **AI/ML Libraries** | ★★★★★ | ★★ | ★★ | ★★★ | ★★ |
| **Prototyping Speed** | ★★★★★ | ★★★★ | ★★★ | ★★★ | ★★★★ |
| **Execution Speed** | ★★ | ★★★★★ | ★★★★★ | ★★★★ | ★★★ |
| **Concurrency** | ★★ | ★★★★★ | ★★★★★ | ★★★★ | ★★★ |
| **Type Safety** | ★★ | ★★★★ | ★★★★★ | ★★★★★ | ★★★★ |
| **Dependency Mgmt** | ★★ | ★★★★ | ★★★★★ | ★★★★ | ★★★ |
| **Deploy Simplicity** | ★★ | ★★★★★ | ★★★★ | ★★★ | ★★★ |
| **Community/Ecosystem** | ★★★★★ | ★★★★ | ★★★ | ★★★★★ | ★★★★★ |
| **AI Agent Support** | ★★★★★ | ★★★★ | ★★★ | ★★★★ | ★★★★ |
| **Day 2 Maintenance** | ★★★ | ★★★★★ | ★★★★ | ★★★★ | ★★★ |

## Evaluating Stacks: Advantages & Disadvantages

Beyond the specifics of each language, here's a framework of evaluation criteria to apply to any stack decision:

### Development Experience

- **Ease of development** — Developer productivity and learning curve. How fast can your team be productive?
- **Rapid prototyping** — Speed to first demo. Note: this advantage is shrinking as AI coding agents accelerate development in all languages.
- **Availability of libraries** — Ecosystem richness for your specific problem domain.
- **Open source & communities** — Quality of support, documentation, examples, and the pace of ecosystem evolution.

### Runtime Performance

- **Execution speed** — Raw performance for your workload type (CPU-bound vs I/O-bound).
- **Concurrency** — How naturally the language handles parallel workloads. Go's goroutines vs Python's GIL can be a night-and-day difference.
- **Memory usage** — Footprint and resource efficiency, especially at scale.
- **Resource usage on deployment** — Cloud costs and scaling behavior. A Go binary uses a fraction of the memory of a Python process with its interpreter and dependencies.

### Architecture & Maintenance

- **Type safety** — Compile-time error catching and refactoring confidence. This matters more as codebases grow.
- **Dependency management** — How easily you avoid dependency hell. Cargo (Rust) and Go modules handle this well; pip historically has not.
- **Distribution model** — Binary vs. library vs. container. A single Go binary is trivially deployable. A Python app with a complex conda environment is not.
- **Ease of upgrading** — Migration paths and breaking changes. How painful are major version bumps?
- **Security** — Vulnerability surface and patching cadence.

### DevOps & Tooling

- **Package management** — Access to libraries, update workflows, and reproducible builds.
- **CI/CD support** — Build pipeline integration, testing framework maturity.
- **Containerization** — Docker compatibility, image sizes. A Go container image can be 10MB; a Python ML image can be 2GB+.
- **Observability** — Logging, monitoring, debugging, and profiling tools.

## The AI Coding Agent Factor

AI coding assistants are changing the stack selection calculus in interesting ways:

**The "familiarity tax" is lower.** It's easier than ever to be productive in an unfamiliar language. Claude or Cursor can help you write idiomatic Go even if you've never used it. This doesn't mean you'll be as fast as an expert, but the gap is smaller than it used to be.

**Rapid prototyping speed matters less.** If AI accelerates all development, the relative advantage of a "rapid prototyping" language shrinks. You can prototype in Go or Rust almost as fast as Python now.

**Documentation quality becomes more important.** AI assistants work better with well-documented APIs and clear conventions. Languages and frameworks with excellent documentation become more attractive.

**But architecture still requires human judgment.** AI can write code in any language. It can't tell you whether your fundamental architecture is appropriate for your problem. The Twitter-Rails mismatch would still happen today—an AI assistant would happily help you build the wrong thing faster.

**AI agents can mask problems.** When fixing bugs becomes trivially easy, you might not notice that you're fixing the same class of bugs repeatedly. AI makes it easier to patch over architectural problems rather than fix them. The pain that would have forced a rethink gets distributed into a thousand small fixes.

## Lessons from Experience

### Twitter's Rails Journey

Twitter famously started with Ruby on Rails and suffered chronic outages as it scaled. The "Twitter can't scale" period became a cautionary tale—though the lesson people drew was often wrong.

The real problem wasn't Ruby or Rails per se. It was that Twitter's data model (a messaging system where each tweet fans out to millions of followers) was fundamentally mismatched with the CMS-style architecture Rails encourages. Any framework would have struggled with that design.

But there's still a lesson here: Rails was great for getting Twitter started quickly. It wasn't great for what Twitter became. The team eventually rewrote critical components in Scala and Java—not because Ruby is bad, but because the problem changed.

**The takeaway:** The stack that gets you to market isn't always the stack that scales. Plan for the transition, or at least be aware it may be necessary.

### Cloud Foundry

Cloud Foundry (CF) also started as a Ruby on Rails platform. And like Twitter, it suffered significantly from that choice. Building a Platform-as-a-Service designed to run applications in any stack ironically showed the CF team that Rails was the wrong choice for the core of CF. I was there and witnessed the long hours debugging.

![PLACEHOLDER: CF pair programming photo — insert your photo of the CF pair programming experience here]

To their credit, Pivotal—the steward of CF—took great care to enforce TDD and pair programming for all CF code. The quality of code was there, but no amount of engineering discipline could solve the original sin of the wrong stack choice.

This is why the CF team gradually replaced most of CF with Golang. It started with the CLI, which was the core entry point for anyone using CF and was executed countless times during development and by users. The Go CLI proved so successful and pleasing to users that the rest of CF explored a rewrite in Golang.

Some components remained in Ruby and Rails, but most new development had switched to Golang. This was not only the choice of CF engineers but also validated by competing PaaS platforms—Docker and especially Kubernetes—which were implemented almost entirely in Golang.

### Recent AI Agent Projects

In my current work on AI agents, I've had to make stack choices that will matter for years. The easy path is Python everywhere—LangChain, LlamaIndex, the whole ecosystem. It works. It's what the tutorials show.

But I've found that splitting the stack often makes sense: Python for the AI/ML components where the libraries live, Go or Rust for the performance-critical infrastructure, TypeScript for anything user-facing. The boundaries require careful design, but the result is a system where each part uses the best tool for its job.

One specific example is the data layer and tooling for vector databases. While it's easy to have Python scripts integrated into pipelines for these tasks, I often find that the need to execute these frequently and the need to parallelize (many documents) make languages with fast startup, low memory usage, and better parallelization a much better choice—areas where languages like Golang and Rust shine.

## Conclusion

The Python wave in AI is producing thousands of prototypes. Many will never need to scale. But some will succeed—and their teams will discover, too late, that the stack that got them to demo day isn't the stack that gets them to production.

This isn't Python's fault. It's the natural consequence of optimizing for time-to-first-demo without thinking about time-to-production-scale.

AI coding agents make this both better and worse. Better because switching stacks is easier than ever. Worse because they make it easier to avoid confronting the problem until it's acute.

The best AI practitioners don't just default—they choose deliberately. Before starting a new project, ask: What are the non-negotiable requirements? What does production look like? Who maintains this in 5 years? Where are the libraries? What's the deployment story?

![Stack Selection Decision Flowchart](images/stack-decision-flowchart.svg)

The advice is boring but true: think before you start. Especially before you move beyond a prototype. The stack you choose will shape what's easy and what's hard for the life of the project. Choose deliberately.

---

*Next post: Hackathons as research platform.*

*Previous post: [AI Agents Meetup SF](https://maximilien.substack.com/p/ai-agents-meetup-sf-one-year-retrospective?r=4pz80): One Year Retrospective—lessons from nine meetups, 500+ attendees per event, and the evolution of the agent ecosystem*

---

## Recommended Resources

**On Python's Scaling Challenges:**
- Rod Johnson's "Production-Ready Gen AI: Beyond the Python Prototype" (Medium)
- Darryl Taft's "Your Enterprise AI Strategy Must Start With Java, Not Python" (The New Stack)
- "Why Do They Say Rails Doesn't Scale?" (codefol.io) — still relevant lessons

**On Stack Selection:**
- *Designing Data-Intensive Applications* — Kleppmann (the best book on thinking about systems)
- "The Twelve-Factor App" (12factor.net) — deployment considerations

**Language-Specific Resources:**
- Go: "Learn Go with Tests" (quii.gitbook.io)
- Rust: "The Rust Programming Language" (doc.rust-lang.org)
- Kotlin: "Kotlin in Action" — Jemerov & Isakova

---

## Items to Verify/Research Before Publishing

1. [x] **Cloud Foundry experience:** Added — Ruby to Go migration story
2. [x] **Knative experience:** Removed — similar Ruby vs Go narrative, avoids repetition
3. [x] **AI agent project examples:** Added — vector DB tooling example
4. [ ] **Performance benchmarks:** Consider adding concrete Python vs Go/Rust comparisons for relevant workloads
5. [ ] **Library availability table:** Stack comparison table added above — review star ratings for accuracy
6. [ ] **Day 2 operations comparison:** Covered in evaluation framework; consider adding a concrete anecdote
7. [x] **Cross-link:** Previous post linked
8. [x] **weave-cli connection:** Deferred to dedicated future post
9. [x] **Diagram/visual:** Stack comparison table and decision flowchart added
10. [ ] **CF pair programming photo:** Placeholder added — insert your photo before publishing
11. [ ] **Final proofread:** One more pass before publishing

---

*Word count: ~2,600 words (target: ~2,000 — consider trimming the evaluation framework section or the alternative stacks descriptions to hit target)*
