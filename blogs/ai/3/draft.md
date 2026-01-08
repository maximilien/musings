# AI Agents Meetup SF: One Year Retrospective

*Nine events, 4,000+ registrations, and what we learned building a community around AI agents*

**TL;DR:** In January 2025, Dave Nielsen and I asked: does the Bay Area need another AI meetup? The answer was yes—because 2025 was to be the year of AI agents, and there was no dedicated forum. We launched AI Agents Meetup SF and ran 9 events in our first year. This post reflects on what we learned, who spoke, and what's next for 2026.

---

The Bay Area is THE place for AI. Like it or not.

The critical mass is undeniable: OpenAI, Anthropic, and Google's AI labs. Stanford and Berkeley feeding talent and research into the ecosystem. Thousands of startups building on top of foundation models. If you want to be at the center of what's happening in AI, you're probably within a 50-mile radius of San Francisco right now.

I've been deeply connected to this tech community for decades. I've watched waves come and go—cloud computing, mobile, blockchain, and now AI. And in late 2024, it became clear that 2025 was going to be different. The AI agents wave was building, but there was no dedicated community forum for it.

So Dave Nielsen and I decided to create one.

## The Team

I've known Dave for over 20 years. I watched him lead various Bay Area tech communities—Cloud Foundry, ServerlessDays, and countless others. He was also leading IBM's AI Alliance involvement, which gave us a key connection to the broader open-source AI ecosystem. When I pitched the idea, he was in immediately.

We recruited Alexy Khrabrov to round out the team. Alexy has a long history leading tech conferences—he founded AI by the Bay, runs Bay Area AI (the longest-running AI meetup in the world), and recently helped establish AI Agent meetups in Berlin and Amsterdam. His deep community connections and conference experience were exactly what we needed.

Together: the right mix of experience, connections, and passion for building community.

## Meetup #1 — Launch (January 2025)

**"You are invited to our very first event!"**

The inaugural meetup had no theme—we just wanted to introduce the community and establish the format. Would anyone show up? Would people care about agents specifically, or was this just another AI buzzword?

**Speakers:**
- João Moura, CEO at crewAI — scheduled to present on crewAI, but was a no-show
- Sandi Besen (Neudesic/IBM) & Ismael Faro (IBM Research) — "BeeAI"
- Patrick McFadin, DataStax — "LangFlow"

**The result:** 646 registrations and over 200 attendees. Overwhelming response.

The demand was real. People wanted a place to discuss agents specifically—not just LLMs, not just "AI," but the autonomous systems that could actually *do things* in the world. We had validated the thesis. Now we needed to build on it.

## Meetup #2 — Building Momentum (February 2025)

Sponsored by BeeAI and Prometheus Swarm, our second event was an AI Alliance event that built on the first.

**Speakers:**
- Kai of Swarms.ai (Lightning Talk)
- Al Morris — "Prometheus Swarm"
- Dave Nielsen presenting AllyCat project (for Sujee Maniyam of Node51)
- Filip Szymański — "What goes into building a voice agent?"

**The result:** 665 registrations and over 200 attendees—even stronger than the first.

Voice agents emerged as a hot topic. The community was forming around regular attendance. People started recognizing each other. The networking was as valuable as the talks.

## Meetup #3 — Agent Protocols (March 2025)

Our first *themed* meetup. MCP had launched a few months earlier and was gaining serious attention. Google had announced A2A. The protocol landscape was suddenly crowded and confusing.

Sponsored by BeeAI, Neo4j, and Convex.

**Speakers:**
- Ian Macartney, Convex — "Building AI Agents and Workflows for full-stack applications"
- Sarmad Qadri, LastMile — "MCP-Agent"
- Michael Hunger, Neo4j — "MCP for LLM Agents, APIs & Graphs"
- Sandi Besen, BeeAI/IBM — "The AI Protocol Landscape: ACP, MCP & A2A"
- Ivan Nardini, Google — "A2A Overview"
- Panel: Agent Protocols (moderated by Dave and Alexy)

**Key takeaways:**
- MCP was standardizing context for LLM agents—and it was winning
- Multiple protocols were emerging (MCP, A2A, ACP), but integration was the key
- The panel format worked well for topics with multiple perspectives

539 registrations, over 200 attendees. Themed meetups drove focused discussion. We'd found our format.

## Meetup #4 — Agent Evaluations (April 2025)

How do you know if your agent is working? This question kept coming up in conversations, so we made it the theme.

Sponsored by BeeAI.

**Speakers:**
- Ranjan Sinha, IBM Fellow — "Natural Language Interaction Protocol (NLIP)" (Lightning Talk)
- Claire Longo, Comet — "Best Practices for Monitoring Agent Applications in Production"
- Priyan Jindal, Arize — "Prompt Learning: Automatically Optimizing Production Agents"
- Ofer Mendelevitch, Vectara — "Open RAG Eval"

**Key takeaways:**
- Agent observability requires new approaches—traditional monitoring isn't enough
- The TextPRO framework from Arize offered a path to continuous agent improvement
- RAG evaluation is crucial and complex—Vectara's open approach was refreshing

648 registrations. The evaluation theme resonated strongly—everyone was building agents, but few knew how to measure if they were actually working.

## Meetup #5 — Agents in Production (May 2025)

Moving from demos to deployments. What does it actually take to run agents in production?

Sponsored by BeeAI.

**Speakers:**
- Marquita Ellis, IBM Research — "From Academic Innovation to Enterprise-Grade Systems"
- Ricardo Marín, Vozy — "Deploying AI Agents in Voice-first Markets"
- James Ilse, Solo.io — "Agent Gateway: A Rust-built dataplane for AI, MCP, and A2A"
- Kai Wu & Nikhil Maddirala, Meta — "Llama Stack in Production"
- Cornelia Davis, Temporal — "OpenAI Agent SDK + Temporal for production-ready agents"

**Lightning Talks:**
- UC Berkeley/Stanford/IBM Research collaboration survey announcement
- Vozy's experience with voice AI in Latin America

**Key takeaways:**
- Production requires fundamentally different thinking than prototypes
- Agent Gateway was addressing real connectivity challenges
- Meta's Llama Stack + AI Alliance collaboration pointed to where open-source agents were heading

353 registrations. The attendance dipped slightly, but the quality of discussion was the highest yet. Production problems are harder than demo problems.

## Meetup #6 — Agents in the Workplace (June 2025)

AI Workers vs AI Agents—what's the difference? Computer-use agents were emerging as a hot topic.

Sponsored by BeeAI and Neo4j.

**Speakers:**
- Nikita Ivanov, Humatron AI — "Software-Defined AI Workforce: AI Workers vs. AI Agents"
- Jamieson Leibovitch, Uber — "Uber's Multi-Agent Platform"
- Ran Xu, Salesforce AI Research — "Build Computer-Use Agent: from Research to Enterprise"

**Key takeaways:**
- The distinction between task automation and autonomous agents matters for enterprise adoption
- Uber's agent platform offered real-world insights at scale
- Computer-use agents (Salesforce's GTA1 and CoAct-1 research) were the next frontier
- Enterprise security considerations for agents with elevated permissions are non-trivial

514 registrations. The enterprise angle brought in a different crowd—people deploying agents in serious production environments.

## Meetup #7 — Coding Agents (July 2025)

The hottest application of AI agents in 2025. We had to cover it.

Sponsored by Neo4j and AI Alliance.

**Speakers:**
- Beyang Liu, Sourcegraph/AmpCode — "Code Review is Dead; Long Live Code Review!"
- Mike Biglan, DevSwarm — "Parallel is the New Fast: High Velocity Engineering"
- Gary Qi, TRAE — "How AI Coding Is Transforming Product Development"
- Tejas Bhakta, Morph — "Small Models as Tools for Coding Agents" (Lightning Talk)

**Key takeaways:**
- Review is the new bottleneck, not writing—Beyang's thesis resonated deeply
- HiVE methodology: parallel, branch-isolated agents changing how teams work
- TRAE's vision for AI-native development was compelling (and I ended up doing a solo hackathon with it afterward)
- Small models have a place in the agent stack

295 registrations, about 100 attendees. Smaller than our peaks, but intensely focused. The developers building with these tools showed up ready to discuss specifics.

[Note: This meetup directly informed my AI Coding Assistants post earlier this month.]

## Meetup #8 — [I Missed It]

I couldn't attend this one. I had a photography show at Leica Store SF—the final show of the year with an opening reception that perfectly conflicted.

Sometimes you have to choose between your passions. The community handled it without me.

[PLACEHOLDER: Add details from Dave/Alexy's notes on what happened]

## Meetup #9 — Past, Present, and Future (December 2025)

Year-end reflection. Looking back at 2025, the state of AI agents, and predictions for 2026.

[PLACEHOLDER: Add details from event—was this recorded? What were the key predictions?]

## Lessons Learned

**What worked:**
- **Themed meetups drive focused discussion.** Once we moved from general "agents" to specific topics (protocols, evaluations, production), the conversations got better.
- **Mix of big company and startup speakers.** IBM, Meta, Salesforce, Uber—plus startups like crewAI, DevSwarm, Morph. The combination gives attendees both scale and innovation perspectives.
- **Consistent format builds community expectations.** Talks, networking, food/drinks. People knew what they were signing up for.
- **Digital Jungle venue.** Great A/V, professional photos, the right vibe. Venue matters more than you'd think.

**What to improve:**
- **Post-event content sharing.** We could do better at getting slides and recordings out quickly.
- **More interactive formats.** Panels worked well; we should do more of them, plus workshops.
- **Live streaming.** Not everyone can make it to SF. We need to reach the broader community.

**Community insights:**
- Demand for agent-focused content remains strong. This isn't a bubble—it's a fundamental shift.
- Practitioners want real-world stories, not just demos. "How we built it" beats "look what it can do."
- Protocols and infrastructure are hot topics. MCP's rise validated our Protocols meetup timing.

## By the Numbers

| Meetup | Theme | Registrations | Attendees |
|--------|-------|---------------|-----------|
| #1 | Launch | 646 | 200+ |
| #2 | Building Momentum | 665 | 200+ |
| #3 | Agent Protocols | 539 | 200+ |
| #4 | Agent Evaluations | 648 | 200+ |
| #5 | Agents in Production | 353 | 150+ |
| #6 | Agents in the Workplace | 514 | 175+ |
| #7 | Coding Agents | 295 | 100+ |
| #8 | [TBD] | [TBD] | [TBD] |
| #9 | Past, Present, Future | [TBD] | [TBD] |

**Total registrations across 2025: 4,000+**

[VERIFY: Get exact numbers for meetups #5-9 from Luma]

## What's Next for 2026

Dave, Alexy, and I are continuing throughout 2026. Planning is already underway.

**Topics we're considering:**
- **Physical agents (robots)** — embodied AI is the next frontier
- **Securing AI agents** — as agents get more capabilities, security becomes critical
- **Paying agents** — economics, transactions, and the business models around agents
- **Revisiting past themes** — protocols, production, and coding agents will all evolve

**Growing the community:**
- Live streaming and recording all events
- Better documentation and content
- Potential expansion to other cities (following Alexy's lead with Berlin and Amsterdam)

## Join Us

2025 was the year of AI Agents. 2026 will be the year they go mainstream.

We're continuing AI Agents Meetup SF with themes covering important aspects of the space. Our goal: getting experts doing interesting work to share with the community.

All events are streamed and recorded from Digital Jungle with bespoke photos. [VERIFY: Is this accurate? Are all events recorded?]

**Want to speak?** Reach out. We're always looking for practitioners with real stories to tell.

**Interested in sponsoring?** Contact us. Our 2025 sponsors—AI Alliance, Neo4j, BeeAI, Convex, and Prometheus Swarm—helped make the events possible.

**Want to attend?** Follow us on [Luma](https://lu.ma/user/DrMaximilien) for upcoming events.

Let's build the agent future together.

---

## Links to All 2025 Meetups

| # | Theme | Link |
|---|-------|------|
| 1 | Launch | [luma.com/cspedjbp](https://luma.com/cspedjbp) |
| 2 | Building Momentum | [luma.com/i499vcak](https://luma.com/i499vcak) |
| 3 | Agent Protocols | [luma.com/o648ixbd](https://luma.com/o648ixbd) |
| 4 | Agent Evaluations | [luma.com/3h56ba2z](https://luma.com/3h56ba2z) |
| 5 | Agents in Production | [luma.com/x16vikh7](https://luma.com/x16vikh7) |
| 6 | Agents in the Workplace | [luma.com/kf9p57ym](https://luma.com/kf9p57ym) |
| 7 | Coding Agents | [luma.com/5ry1w1ak](https://luma.com/5ry1w1ak) |
| 8 | [TBD] | [TBD] |
| 9 | Past, Present, Future | [TBD] |

---

## The Organizers

**Max (Dr. Michael Maximilien)** — Founder/CEO of a stealth AI agents startup. PhD in multiagent systems. 30 years industry experience including Distinguished Engineer at IBM (Cloud Foundry, Knative). Building the agent future.

**Dave Nielsen** — IBM AI Alliance lead. 25+ years leading Bay Area tech communities including Cloud Foundry and ServerlessDays. The community builder's community builder.

**Alexy Khrabrov** — AI Community Architect at Neo4j. Founder of AI by the Bay, Bay Area AI (the longest-running AI meetup in the world), and AI Agent meetups in SF/Berlin/Amsterdam. Deep connections across the global AI community.

---

## 2025 Sponsors

Thank you to our sponsors who made these events possible:
- **AI Alliance** — The open-source AI community
- **Neo4j** — Graph database for AI
- **BeeAI (IBM)** — Open-source agent framework
- **Convex** — Backend for AI applications
- **Prometheus Swarm** — Multi-agent orchestration

---

*Previous post: [On Vector Search: AI Agents' Knowledge](link-to-post)*

*This is the final post in my January 2026 launch series. See [Introducing AI Musings](https://maximilien.substack.com/p/introducing-ai-musings) for what's coming next.*

---

## Items to Verify/Research Before Publishing

1. [ ] **Meetup #8 details:** Get notes from Dave/Alexy on what happened
2. [ ] **Meetup #9 details:** Add speakers, key takeaways, attendance
3. [ ] **Exact attendance numbers:** Verify from Luma for meetups #5-9
4. [ ] **Recording status:** Are all events recorded? Where are they hosted?
5. [ ] **João Moura no-show:** Is it okay to mention this? What happened?
6. [ ] **Photography show:** Add brief context on the Leica Store show
7. [ ] **2026 dates:** Any confirmed dates to announce?
8. [ ] **Sponsor logos:** Consider adding visual elements
9. [ ] **Cross-reference:** Add links to other January posts once published
10. [ ] **Digital Jungle:** Confirm venue details and link

---

*Word count: ~2,100 words (target: ~2,000—on target)*
