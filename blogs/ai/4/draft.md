# Selecting the Right Software Stack

*The decision you make early that haunts you later—and how AI is changing the calculus*

**TL;DR:** Your software stack choice is one of the most consequential decisions you'll make on a project. Get it wrong and you'll pay in scaling headaches, debugging nightmares, and eventual rewrites. The Python wave in AI is creating a generation of prototypes that will struggle in production. AI coding agents are making it easier to work in unfamiliar stacks, but they can't save you from fundamental architectural mismatches. Think carefully before you start—and especially before you move beyond a prototype.

---

A software stack is the collection of languages, libraries, and services you use to build a solution. For any given problem, there are dozens of reasonable choices. Is there an optimal choice? Surely one stack doesn't fit all problems?

In practice, most developers reach for what they know. The familiar stack. The one where they can be productive on day one. This is rational—familiarity reduces risk and speeds early development. But it's also how you end up maintaining a Python prototype that needed to be a Go service, or a monolithic Rails app that should have been microservices from the start.

I've made this mistake. I've watched others make it. And with the current wave of AI-first development, I'm watching a new generation make it at unprecedented scale.

**The thesis:** Think carefully before starting, and especially before moving beyond a prototype. The choice of the correct stack is key to long-term success. And the Python AI wave will reveal its costs when prototypes need to go into production and scale.

## Why Your Stack Choice Matters

A software stack decision involves multiple interconnected choices:

**Language** — The foundation of your codebase. Some languages have built-in features that make them better suited for certain workloads. Go's goroutines handle concurrency differently than Python's asyncio. Rust's ownership model prevents entire classes of bugs. Java's type system catches errors that Python only discovers at runtime.

**Libraries** — Frameworks, utilities, and dependencies. Historical accidents mean some languages have richer ecosystems for certain domains. Python dominates AI/ML not because it's the best language for the job, but because the research community standardized on it and built numpy, scikit-learn, PyTorch, and TensorFlow there first.

**Services** — Package management, external APIs, databases, cloud infrastructure. How does your stack integrate with the services you need? How painful is deployment?

**Maintenance** — Day 2 operations: keeping software running, upgrading dependencies, managing security patches. Some stacks make this easy; others make it a constant battle.

**Non-functionals** — Performance, security, reliability, maintainability. These matter more as you scale—often revealing problems you didn't anticipate when you started.

## The Current Landscape: Python's AI Dominance

Python has become the default choice for AI solutions. There are good reasons for this:

**The AI/ML ecosystem is unmatched.** PyTorch, TensorFlow, scikit-learn, pandas, numpy, LangChain, LlamaIndex—if you're building AI applications, the libraries you need are in Python first, often Python only. The research community writes Python. The tutorials are in Python. Your team probably knows Python.

**Prototyping speed is excellent.** Python's simplicity and dynamic typing let you move fast. You can go from idea to working demo in hours. For exploratory work, this matters enormously.

**AI coding agents know Python well.** The training data skews heavily toward Python, especially for AI-related code. Your AI assistant will be more helpful with Python than with less common languages.

But there are also good reasons to question Python's dominance:

**Python is slow.** Not 50x slower than C anymore, but still 5-20x slower than compiled languages for CPU-bound work. Instagram and YouTube use Python—but they also have teams dedicated to making Python not suck at scale. You probably don't.

**Concurrency is painful.** The Global Interpreter Lock (GIL) means Python can't efficiently use multiple CPU cores within a single process. You work around this with multiprocessing, but that brings its own complexity and memory overhead.

**Type safety is optional and incomplete.** Type hints help, but they're not enforced at runtime. The tooling has improved, but it still lags behind languages designed with types from the start.

**Large codebases get messy.** Python has no component model as sophisticated as Java Spring. Structuring complex applications quickly becomes painful. The frameworks that exist (Django, FastAPI) are good, but they're not designed for the kind of large-scale systems that enterprises typically need.

**Dependency management is improving but still fragile.** Virtual environments, pip, conda, poetry—the tooling has gotten better, but it's still easier to end up in dependency hell than with npm or cargo.

## Alternative Stacks Worth Considering

### Go (Golang)

**Strengths:** Exceptional concurrency model (goroutines and channels), fast compilation, simple deployment (single binary), strong standard library, designed for networked services. Go excels at building the kind of high-throughput, concurrent services that AI systems often need around the core ML components.

**Weaknesses:** Less expressive than Python, smaller AI/ML library ecosystem, error handling can be verbose.

**Best for:** API servers, microservices, CLI tools, infrastructure components, anything requiring high concurrency.

### Java/Kotlin

**Strengths:** Mature enterprise ecosystem, excellent tooling, proven at massive scale, strong type system, JVM optimizations, huge talent pool. Spring Boot provides a sophisticated component model. The JVM runs much of the world's mission-critical software.

**Weaknesses:** Verbose (Java more than Kotlin), slower iteration than Python, heavyweight frameworks.

**Best for:** Enterprise systems, large team projects, anything requiring long-term maintainability and backward compatibility.

### Rust

**Strengths:** Memory safety without garbage collection, performance comparable to C/C++, excellent package management (cargo), modern type system. Increasingly used for performance-critical AI infrastructure (Qdrant, for example, is written in Rust).

**Weaknesses:** Steep learning curve, slower development speed, smaller ecosystem.

**Best for:** Performance-critical systems, systems programming, infrastructure that needs to be fast and reliable.

### TypeScript/Node.js

**Strengths:** Full-stack unification (same language front and back), huge ecosystem (npm), good for I/O-bound services, familiar to web developers.

**Weaknesses:** Single-threaded event loop isn't ideal for CPU-bound work, npm dependency issues, runtime type checking still limited.

**Best for:** Full-stack web applications, real-time services, teams that want one language everywhere.

## Lessons from Experience

### Twitter's Rails Journey

Twitter famously started with Ruby on Rails and suffered chronic outages as it scaled. The "Twitter can't scale" period became a cautionary tale—though the lesson people drew was often wrong.

The real problem wasn't Ruby or Rails per se. It was that Twitter's data model (a messaging system where each tweet fans out to millions of followers) was fundamentally mismatched with the CMS-style architecture Rails encourages. Any framework would have struggled with that design.

But there's still a lesson here: Rails was great for getting Twitter started quickly. It wasn't great for what Twitter became. The team eventually rewrote critical components in Scala and Java—not because Ruby is bad, but because the problem changed.

**The takeaway:** The stack that gets you to market isn't always the stack that scales. Plan for the transition, or at least be aware it may be necessary.

[PLACEHOLDER: Add your Cloud Foundry experience—what stack decisions worked, what didn't]

[PLACEHOLDER: Add your Knative experience—stack decisions and lessons learned]

### The AI Agent Stack Question

In my current work on AI agents, I've had to make stack choices that will matter for years. The easy path is Python everywhere—LangChain, LlamaIndex, the whole ecosystem. It works. It's what the tutorials show.

But I've found that splitting the stack often makes sense: Python for the AI/ML components where the libraries live, Go or Rust for the performance-critical infrastructure, TypeScript for anything user-facing. The boundaries require careful design, but the result is a system where each part uses the best tool for its job.

[PLACEHOLDER: Add specific examples from your AI agent projects—what you chose and why]

## The AI Coding Agent Factor

AI coding assistants are changing the stack selection calculus in interesting ways:

**The "familiarity tax" is lower.** It's easier than ever to be productive in an unfamiliar language. Claude or Cursor can help you write idiomatic Go even if you've never used it. This doesn't mean you'll be as fast as an expert, but the gap is smaller than it used to be.

**Rapid prototyping speed matters less.** If AI accelerates all development, the relative advantage of a "rapid prototyping" language shrinks. You can prototype in Go almost as fast as Python now.

**Documentation quality becomes more important.** AI assistants work better with well-documented APIs and clear conventions. Languages and frameworks with excellent documentation become more attractive.

**But architecture still requires human judgment.** AI can write code in any language. It can't tell you whether your fundamental architecture is appropriate for your problem. The Twitter-Rails mismatch would still happen today—an AI assistant would happily help you build the wrong thing faster.

**AI agents can mask problems.** When fixing bugs becomes trivially easy, you might not notice that you're fixing the same class of bugs repeatedly. AI makes it easier to patch over architectural problems rather than fix them. The pain that would have forced a rethink gets distributed into a thousand small fixes.

## A Decision Framework

Before starting a new project, ask:

1. **What are the non-negotiable requirements?** Performance? Type safety? Team expertise? Library availability? These constraints often narrow your choices significantly.

2. **What does production look like?** If this succeeds, what will it need to handle? It's fine to prototype in one stack and plan a rewrite, but know that going in.

3. **Who maintains this in 5 years?** Will it be you? A team? A different team entirely? Some stacks are easier to hand off than others.

4. **Where are the libraries?** If you need specific AI/ML capabilities, Python may be non-negotiable for those components. But that doesn't mean everything has to be Python.

5. **What's the deployment story?** A Go binary is trivially deployable. A Python app with a complex conda environment is not. This matters more than people admit.

**Quick heuristics:**

- If it's a prototype that might become production: start with the production stack if possible, or plan the transition explicitly
- If it's AI/ML-heavy: Python for the ML, but consider other languages for the surrounding infrastructure
- If it's a high-concurrency service: Go or Rust deserve serious consideration
- If it's an enterprise system with a long lifespan: Java/Kotlin and their mature tooling may be worth the verbosity
- If the whole team knows one language well: that matters—factor it in

## Conclusion

The Python wave in AI is producing thousands of prototypes. Many will never need to scale. But some will succeed—and their teams will discover, too late, that the stack that got them to demo day isn't the stack that gets them to production.

This isn't Python's fault. It's the natural consequence of optimizing for time-to-first-demo without thinking about time-to-production-scale.

AI coding agents make this both better and worse. Better because switching stacks is easier than ever. Worse because they make it easier to avoid confronting the problem until it's acute.

The advice is boring but true: think before you start. Especially before you move beyond a prototype. The stack you choose will shape what's easy and what's hard for the life of the project. Choose deliberately.

---

*Next post: AI Agents Meetup SF: One Year Retrospective—lessons from nine meetups, 500+ attendees per event, and the evolution of the agent ecosystem.*

*Previous post: [On Vector Search: AI Agents' Knowledge](link-to-post)*

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

### ⏳ Pending

1. [ ] **Cloud Foundry experience:** Add specific anecdotes about stack decisions and lessons learned
2. [ ] **Knative experience:** Stack choices and what you'd do differently
3. [ ] **AI agent project examples:** Specific stack decisions from your current work
4. [ ] **Performance benchmarks:** Consider adding concrete Python vs Go/Rust comparisons for relevant workloads
5. [ ] **Library availability table:** Could add a matrix showing library availability across languages for common AI tasks
6. [ ] **Day 2 operations comparison:** Concrete examples of maintenance burden differences
7. [ ] **Cross-link:** Link to Vector Search post and AI Coding Assistants post once published

---

*Word count: ~2,300 words (target: ~2,000—on target with room for your experience sections)*

