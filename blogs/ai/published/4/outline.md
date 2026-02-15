# Selecting the Right Software Stack

Target: AI Musings Substack

---

## Abstract

Selecting the wrong stack can cause significant pain later. Scaling, debugging, and integration are all impacted by your stack choice — and the more code you have, the harder it becomes to change. AI coding agents now make it easier to work with unfamiliar stacks, but from experience, most web solutions still follow predictable patterns, defaulting to Python for a rewrite. Thesis: think carefully before starting, and especially before moving beyond a prototype.

## Introduction

### What is a Software Stack?

- A software stack is the collection of libraries & services used to build a solution
- For any given problem, there are many possible choices
- Is there an optimal choice for each problem?
- Surely one stack does not fit all solutions to all problems?

### The Default Stack Problem

- People tend to use their default/familiar stack — is this the right approach?
- Are some stacks better suited for certain problems than others?
- AI agents might delay the inevitability by hiding the issue — ease of fixing and masking complex problems
- But the underlying stack choice still matters

### The Current Landscape

- Python stacks have become the default choice for AI solutions
- But other stacks are possible and sometimes preferable
- Core argument: the choice of the correct stack is key to long-term success
- AI agents make exploring unfamiliar stacks easier than ever before

## Why Software Stack Matters

### Components of a Stack

A typical stack decision involves:

- **Language** — The foundation; some languages have built-in features that make them better suited for certain workloads
- **Libraries** — Frameworks, utilities, and dependencies; for historical reasons some languages have richer ecosystems in certain domains
- **Services** — Package management, external APIs, databases, cloud infrastructure
- **Maintenance** — How easy is it to keep your software running and up to date (day 2 operations)
- **Non-functional** — Performance, security, reliability, and maintainability

### AI Stack Choices

#### Python Ecosystem

- Web frameworks: Django, Flask, FastAPI
- AI/ML libraries: scikit-learn, PyTorch, TensorFlow, LangChain
- Data processing: pandas, NumPy
- [Add discussion of why Python dominates AI]

#### Alternative Stacks

- **Go (Golang)** — Performance, concurrency, deployment simplicity
    - [Elaborate key features]
- **Rust** — Memory safety, performance
    - [Elaborate key features]
- **Java/Kotlin** — Enterprise ecosystem, mature tooling
    - [Elaborate key features]
- **TypeScript/Node.js** — Full-stack unification
    - [Elaborate key features]
- [Add more as relevant]

## Advantages & Disadvantages

*Evaluation criteria for stack selection:*

### Development Experience

- **Ease of development** — Developer productivity, learning curve
- **Rapid prototyping** — Note: less important now due to AI coding agents
- **Availability of libraries** — Ecosystem richness
- **Open source & communities** — Support, documentation, examples

### Runtime Performance

- **Execution speed** — Raw performance benchmarks
- **Concurrency** — Handling parallel workloads
- **Memory usage** — Footprint and resource efficiency
- **Resource usage on deployment** — Cloud costs, scaling behavior

### Architecture & Maintenance

- **Type safety** — Compile-time error catching, refactoring confidence
- **Dependency management** — Avoiding dependency hell
- **Distribution model** — Binary vs. library vs. container
- **Ease of upgrading** — Migration paths, breaking changes
- **Security** — Vulnerability surface, patching cadence

### DevOps & Tooling

- **Package management** — Access to libraries, updates
- **CI/CD support** — Build pipelines, testing frameworks
- **Containerization** — Docker compatibility, image sizes
- **Observability** — Logging, monitoring, debugging tools

## The AI Coding Agent Factor

*How AI changes the stack selection calculus:*

- AI agents reduce the "familiarity tax" — easier to work in unfamiliar languages
- Rapid prototyping speed matters less when agents accelerate all development
- Documentation quality becomes more important (AI needs good docs)
- Still need human expertise for architecture decisions
- AI makes exploring unfamiliar stacks easier than ever, but can also mask poor stack choices
- [Add your practitioner perspective on this shift]

## Experience & Examples

### Cloud Foundry

- [Stack decisions and lessons learned]
- [What worked, what didn't, what you'd do differently]

### Twitter (now X)

- [Ruby/Rails issues and stack evolution]

### Knative

- [Relevant stack experience]

### Recent AI Agent Projects

- [Recent experiences with AI agent stack choices]
- [Contrast Python vs. alternatives you've evaluated]

## Conclusion

- Summarize key decision framework
- Reiterate thesis: think before starting, and before moving beyond a prototype
- Predict that the Python AI wave will reveal issues when prototypes need to go to production and scale
- The best AI practitioners don't just default — they choose deliberately
- [Call to action or reflection for readers]
- Consider adding a decision matrix or flowchart

---

## Notes

Consistent elements to include:

- Personal anecdotes and experiences where relevant
- Connections to weave-cli and other projects where natural
- Clear calls to action
- Links to relevant previous AI Musings posts
