# AI Coding Assistants

*The tools that are changing how we build software—and the ones that aren't*

**TL;DR:** AI coding assistants represent the most impactful application of AI today, with 85% of developers now using them regularly. After a year of extensive testing across Cursor, Claude Code, TRAE, and others, I've found that two paradigms dominate: IDE-integrated and terminal-native. Each has strengths, and all face the same fundamental challenge: context window limitations. The productivity gains are real—but so is the need for discipline around testing and review.

---

The dream of dramatically accelerated software engineering is no longer a dream.

In 2025, 41% of all code is AI-generated or AI-assisted. According to Stack Overflow's Developer Survey, 84% of developers are using or planning to use AI tools in their development process—up from 76% just a year prior. JetBrains reports that 85% of developers regularly use AI tools for coding, with nearly nine out of ten saving at least an hour every week.

These aren't incremental improvements. They're a fundamental shift in how software gets built.

I've been living in this shift for over a year now. I started with Cursor more than a year ago, then quickly found myself testing many others as I hit Cursor's limits and wanted to streamline and parallelize my work. What follows is what I've learned—not from reading about these tools, but from building with them daily.

## The Landscape in Early 2026

The AI coding assistant space has exploded. Major players include Anthropic (Claude Code), Cursor, ByteDance (TRAE), Sourcegraph (Amp), GitHub Copilot, OpenAI (Codex), Google (Jules), and many others. New entrants appear monthly.

But beneath all the product names, two fundamental paradigms have emerged:

**IDE-integrated tools** like Cursor, TRAE, and Windsurf embed AI directly into a Visual Studio Code-like environment. You get visual diffs, inline suggestions, and a familiar editing experience.

**Terminal-native tools** like Claude Code, Amp, and Warp operate from the command line. You describe what you want, and the agent goes and does it—navigating files, making changes, running tests.

Both approaches have passionate advocates. Both have real limitations. Let me walk through what I've learned about each.

## Cursor: The First Mover

Cursor was the first major player in the IDE-focused agent space, and it shows. The brand recognition is enormous, the user base is large, and the iteration speed has been impressive.

**What works well:**

The VSCode integration feels native because it essentially *is* native—Cursor is a fork of VSCode. If you're coming from that ecosystem, there's almost no learning curve. Your extensions work. Your keybindings work. It just feels like VSCode with superpowers.

The background agent capabilities are particularly compelling. You can spin up tasks and let them run while you focus on something else. The UI for reviewing and approving changes is clear and well-designed. And model flexibility means you can choose your preferred LLM—Claude, GPT-4, or others.

**My experience (three months of extensive use):**

I especially liked the background agent workflow for parallelizing work. For UI-heavy projects, Cursor worked well, though I often found myself needing to provide browser context manually--copying browser's JavaScript console and pasting it to the agent. Where it struggled was with long sessions—context approaching its limits would cause the agent to slow down significantly and "forget" earlier decisions or make suggestions that conflicted with code it had written minutes before.

[VERIFY: Current context window limits—search results suggest 200K advertised but 70K-120K effective in practice]

The pricing volatility has also been frustrating. Cursor has raised significant funding and is growing rapidly, but the plan changes and usage limits have been inconsistent. [VERIFY: Check current pricing tiers—reports suggest $20-$200/month depending on tier]

**Best for:** Developers who prefer GUI workflows, VSCode users, teams wanting visual code review.

## Claude Code: The Terminal-Native Revelation

Claude Code is Anthropic's bet on terminal-native development, and for me, it's been revelatory.

The philosophy is fundamentally different from Cursor. Instead of embedding AI into an existing IDE, Claude Code operates as an autonomous agent that lives in your terminal (and now also has a VS Code extension). You describe what you want, it goes and does it—cloning repos, grepping for answers, editing files, running tests, staging commits.

**What works well:**

The deep reasoning capabilities from Claude models are immediately apparent. Multi-file operations that would require careful orchestration in an IDE-based tool happen naturally here. The MCP (Model Context Protocol) integration opens up powerful tool access. And the speed of CLI interaction removes the overhead of waiting for visual updates.

The 200K context window actually delivers what it promises. When you're working on a large codebase and need the AI to understand how your authentication system connects to your API routes connects to your database schema—that context matters. Reports suggest Claude Code uses 5.5x fewer tokens than Cursor for equivalent tasks while finishing faster with fewer errors.

**My experience:**

So compelling that I switched from Cursor's GUI to using cursor-agent as well (the CLI interface for Cursor). At first, I questioned whether my preference was about the CLI interaction or Anthropic's model superiority. The answer is likely both—better models AND a faster interaction paradigm.

The challenge is review discipline. Speed is addictive. The terminal-based workflow makes it easy to accept suggestions without the same scrutiny you'd apply when visually reviewing diffs. I've found myself accepting too many changes without sufficient review—a feature and a bug of the approach.

**Critical learning:** Establish strong testing practices early. Let the agent run tests after changes. Use agents to create tests too! Without this discipline, the speed advantage becomes a liability.

**Best for:** CLI-native developers, complex refactoring, multi-file operations, those who value speed over visual review.

## TRAE: The ByteDance Wildcard

I stumbled into TRAE during a meetup and decided to do a solo hackathon day with it. Within hours, I was convinced the interface was superior to Cursor for certain workflows.

TRAE (The Real AI Engineer) launched in early 2025 and has grown remarkably fast—over 6 million registered users and 1.6 million monthly active users as of late 2025. The approach is agent-focused from the ground up.

**What sets it apart:**

The built-in browser is huge for UI work. No more switching between your IDE and a browser to see what you're building—it's integrated directly. The no-interrupt run mode lets you kick off complex tasks without constant prompting. And the multiple agents capability means you can parallelize work within the IDE itself.

TRAE's "SOLO mode" takes this further—full-process automated development from requirements input to deployment. It's ambitious, has an agent-focused interface, and early reports suggest it's genuinely useful for rapid prototyping.

The price is also hard to argue with: it's half the price of Cursor (at the time of this writing), with access to many models including GPT-4o models--seems like Claude model was removed.

**The trade-offs:**

TRAE lacks the fast CLI interface that makes Claude Code so compelling. For developers who think in terminal commands, this is a significant gap. The ecosystem is also newer and less mature than Cursor's.

And then there's the elephant in the room: ByteDance ownership. Security researchers have documented extensive telemetry in TRAE, including persistent connections to multiple ByteDance servers even during idle periods. For some developers and organizations, this is a dealbreaker. Others accept it as the cost of reduced costs, powerful tooling.

**Best for:** Developers wanting an agent-focused IDE experience, those doing heavy UI work, cost-conscious developers willing to accept ByteDance's data practices.

## Other Notable Tools

The landscape is crowded. Here's a quick rundown of other tools worth knowing:

**Amp (Sourcegraph):** Similar to Claude Code in its CLI-focused approach, with a free tier supported by advertising. Beyang Liu, the co-founder and CTO, spoke at our AI Agents Meetup SF #7 on Coding Agents. His thesis: "Code review is dead; long live code review!"—the bottleneck has shifted from writing to reviewing. [LINK: Add link to meetup recording]

**Warp:** CLI-focused with multiple tabs capability. Great for terminal lovers who want AI assistance without leaving their shell. Still depends on underlying LLMs. My friend Allie Jones introduced me to this tool and swears by it.

**Codex (OpenAI):** OpenAI's entry has re-emerged as a serious agent-first tool. Limited personal experience, but reports suggest it's competitive, particularly for deterministic multi-step tasks.

**Jules (Google):** Google's version with Gemini model integration. Catching up with leaders but not yet a daily driver for most developers.

**Kivo (Amazon):** Amazon's entry, integrating with Q. Early days, but worth watching given AWS's enterprise footprint.

**Others to watch:** Aider (open source, git-focused), Continue (open source IDE extension), Cline (Claude-focused), Windsurf (Codeium's IDE).

## The Two Paradigms

After a year of testing, I've concluded that the IDE vs CLI distinction is more fundamental than the specific tool you choose.

**IDE-based (Cursor, TRAE, Windsurf):**

- Visual view of your code base
- Visual code review is built into the workflow 
- Integrated with existing development patterns
- Better for those who think visually or come from VSCode
- Trade-off: more overhead, slower interactions—especially deep into a session

**CLI-based (Claude Code, Amp, Warp):**

- Speed and focus without GUI overhead
- Natural for terminal-native developers
- Excellent for parallelization--I typically am working on two or three repos at once using iTerm's tabs
- Review happens via git and terminal tools rather than visual diffs
- Trade-off: easier to miss issues, requires more discipline (testing, diff reviews)

Neither is objectively better. The right choice depends on how you think about code.

## Common Challenges

All these tools share fundamental limitations:

**Context window is the biggest issue.** Every tool struggles with long contexts. Frequent summarization and compacting means the AI "forgets" earlier decisions. This is improving—Claude Code's 200K window is genuinely better than what we had a year ago—but it remains the primary constraint.

**Filesystem interaction creates friction.** For security reasons, tools interact with the filesystem slowly and carefully. This is necessary but creates noticeable latency, especially for operations touching many files.

**LLM dependency is the great equalizer.** The tool is only as good as its underlying model. This is why Claude Code feels different from Cursor even when both use Claude models—the integration, prompting, and workflow matter, but the model quality is the foundation.

**The productivity paradox is real.** A recent METR study found that experienced open-source developers actually took 19% *longer* with AI tools than without in certain contexts. Meanwhile, DX's Q4 2025 report shows 91% adoption and real time savings. The difference? Context matters. AI helps more with unfamiliar codebases and routine tasks; it can slow you down on deeply familiar code where your intuition is faster than explaining to an agent.

[RESEARCH: Cite METR study and DX Q4 2025 report properly]

## Best Practices Across Tools

Whatever tool you choose, these practices make a difference:

**Testing is non-negotiable.** Agents make changes fast—tests catch mistakes and regressions. Automate testing early in the project. Let the agent run tests after changes. Use agents to create tests too! This is the single most important discipline for AI-assisted development.

**Context management matters.** I've developed personal conventions: NEXT_STEPS.md, TODOs.md, CHANGELOG.md files that persist context across sessions. A docs/planning/ directory for the agent to reference and create detail plans of features. Explicit handoff notes when context is getting long. These feel manual, but they dramatically improve agent performance.

**Review discipline is essential.** Speed is addictive. Build review into your workflow deliberately. Trust but verify. The 30% code acceptance rate for GitHub Copilot suggestions isn't a bug—it's appropriate skepticism.

**Multiple tools in parallel is normal.** 59% of developers now run three or more AI coding tools simultaneously. This isn't indecision—it's pragmatism. Different tools excel at different tasks. I often use different tools or models to write tests vs code or to plan before writing code.

## Looking Forward

The space is evolving fast. Here's where I see it heading:

**Near-term:** Context management will improve dramatically. Hybrid approaches combining IDE and CLI will become common. Better integration with the full development lifecycle—not just coding, but testing, deployment, and monitoring.

**Medium-term:** The multi-agent future is coming. You'll describe goals and let agents manage other agents. Orchestration becomes the key skill. Human developers become architects and reviewers rather than primary code writers.

**Longer-term:** The 41% of code that's AI-generated today will grow. The question isn't whether AI will change software development—it's how we adapt our practices, our teams, and our careers to the new reality.

## Conclusion

Two leading paradigms: IDE-integrated and terminal-native. All depend on LLM quality and face context window challenges. Choose based on your workflow preference and project needs.

The productivity gains are real—developers report 30-75% time savings on coding, testing, and documentation. For me it's easily in the 50% to 80%. But so are the challenges: context limits, review discipline, and the need to maintain your own coding skills even as you delegate more to agents.

Invest in testing infrastructure early--locally and in CI/CD. Develop context management strategies. Embrace the tools thoughtfully, not uncritically.

The dream of dramatically accelerated engineering isn't just a dream anymore. But realizing it requires more than downloading the latest AI IDE. It requires adapting how we work.

---

*Next post: Vector Search for AI Agents—how vector databases provide the knowledge layer that makes AI agents actually useful.*

*Previous post: [Introducing AI Musings](https://maximilien.substack.com/p/introducing-ai-musings)*

---

## Recommended Resources

**Tool Documentation:**
- Claude Code: [docs.anthropic.com](https://docs.anthropic.com)
- Cursor: [cursor.com/docs](https://cursor.com/docs)
- TRAE: [trae.ai](https://www.trae.ai)
- Amp: [ampcode.com](https://ampcode.com)

**Analysis & Research:**
- [Latent Space podcast](https://www.latent.space/) — Episodes on coding agents
- [SWE-bench](https://www.swebench.com/) — Benchmark comparisons
- [r/ClaudeAI](https://reddit.com/r/ClaudeAI) and [r/cursor](https://reddit.com/r/cursor) — Community discussions
- [2025 Stack Overflow Developer Survey](https://survey.stackoverflow.co/2025/) — AI section
- [JetBrains State of Developer Ecosystem 2025](https://www.jetbrains.com/lp/devecosystem-2025/)
- [METR Study on AI Developer Productivity](https://metr.org/blog/2025-07-10-early-2025-ai-experienced-os-dev-study/)

**From AI Agents Meetup SF:**
- [#7: Coding Agents](https://luma.com/5ry1w1ak) — Talks from Sourcegraph, DevSwarm, TRAE, and Morph.

---

## Items to Verify/Research Before Publishing

1. [x] **Cursor context window:** Reports suggest 200K advertised but 70K-120K effective. Verify current state.

Cursor's context window varies, with standard use around 10k-20k tokens for edits/chat and a powerful 200k token default for larger projects via Max Mode, which can access even larger model contexts (like 1M tokens for some models) for deeper analysis, balancing speed and capability. You can monitor usage in real-time and use features like rules to manage larger context effectively across chats. 


2. [x] **Cursor pricing:** Confirm current tiers ($20-$200/month range reported)

In 2026, Cursor uses a hybrid pricing model that combines flat monthly fees with usage-based credit pools. As of January 2026, the primary tiers are: 

Individual Plans

Hobby (Free): Includes 2,000 Tab completions and 50 slow requests per month.

Pro ($20/mo): The standard tier for solo developers. It provides unlimited Tab completions, unlimited usage of the "Auto" model, and a $20 monthly credit pool for advanced/premium models (like Claude 3.5 Sonnet or GPT-4o).

Pro+ ($60/mo): A mid-tier for frequent users, offering the same features as Pro but with a larger $60 (3x) credit pool for premium model usage.

Ultra ($200/mo): Designed for power users, providing a $400 (20x) credit pool and priority access to new features. 

3. [x] **TRAE model availability:** Reports suggest Claude support may have changed recently

Reports that Trae has discontinued Claude support are accurate. As of early November 2025, ByteDance-owned Trae officially removed all Claude models from its platform. 

Reason for Change

The removal was driven by Anthropic's updated policy restricting services for Chinese-controlled entities globally. Because Trae is a ByteDance product, it lost access to the Claude series models (including the popular 3.5 Sonnet and 3.7 Sonnet) due to these geopolitical and service interruptions. 

Current Model Availability (2026)

Trae has shifted to other frontier and specialized models to replace Claude:
Frontier Models: GPT-5 and Gemini 2.5 Pro.

Specialized Models: Kimi-K2-0905 and DeepSeek V3.1-Terminus.
Custom Optimizations: Trae states that these new models are optimized for "reasoning quality" and "execution chain" to maintain performance levels similar to when Claude was available. 

Impact on Users
Pro Member Compensation: To address the loss of Claude, Trae is giving Pro members a 50% increase in "Fast Queue" requests (an extra 300 requests per month) through January 31, 2026.

Third-Party Alternatives: Many users are using tools such as Cursor or Windsurf, which maintain full access to the Claude series models.

Trae CLI: The open-source Trae-CLI core agent still supports bring-your-own-key functionality. This allows users with their own Anthropic API keys to continue using Claude outside of the primary IDE interface. 

While Claude is not available, the fact that new OSS models like Mimi and DeepSeek are is a boom since IMO variety of models is important for better results overall. Since I use Claude primarily, TRAE is a good counterbalance to see results from other models or counterbalance when testing, reviewing, etc.

4. [x] **TRAE privacy concerns:** Consider how deeply to address ByteDance data collection

In 2026, Trae (developed by ByteDance) presents a complex privacy profile characterized by aggressive telemetry and unique regional storage policies. While ByteDance has introduced features like Privacy Mode to address backlash, significant concerns remain regarding data persistence and legal obligations. 

Core Privacy Concerns

Extensive Telemetry: Independent research in 2025 revealed that Trae can generate up to 500 network calls (roughly 26MB of data) in under 10 minutes of active use. This data includes persistent identifiers like machine ID and hardware fingerprints (CPU, RAM, motherboard) that can follow users across different projects and reinstalls.
Persistent Data Collection: Even with "Privacy Mode" enabled, some telemetry data collection may continue via Trae tools not covered by the standard IDE toggle. While codebase files are stored locally, they are temporarily uploaded to ByteDance servers for embedding/indexing.

Chat Retention: Any information or code snippets manually pasted into the AI chatbot are historically collected and retained, even if the original plaintext codebase is deleted after indexing.

Regional Data Sovereignty: Trae stores information on secure servers located in the United States, Singapore, and Malaysia. However, as a ByteDance product, it remains subject to Chinese data security laws that can compel companies to provide access to user data for national security purposes. 

Available Privacy Controls (2026)

Privacy Mode: A toggle in Account Settings that, when active, prevents Trae from using chat interactions and code snippets for model training or product improvement.
Local-First Indexing: Trae follows a "local-first" principle where the primary codebase stays on your machine, only leaving for the generation of numerical embeddings.

Ignore Files: Users can use .traeignore or similar "ignore" functions to prevent specific sensitive files from ever being indexed or uploaded. 
Comparison for Developers

Feature 	Trae (ByteDance)	Cursor
Data Training	Opt-out via Privacy Mode	Opt-out available (Privacy Mode)
Telemetry	High (Deep hardware fingerprinting)	Standard usage analytics
Storage Location	US, Singapore, Malaysia	Primarily US-based
Trust Model	Subject to PRC data laws	Subject to US data laws

For developers working on proprietary or sensitive government-related code, the deep telemetry and jurisdictional concerns of ByteDance-owned tools typically necessitate a more cautious approach compared to Western-based alternatives like Cursor or Windsurf. 

For more details, you can review the Trae Privacy Policy.

These legal and technical analyses address the privacy risks associated with Trae, focusing on ByteDance's data collection, international storage, and regulatory landscape:

https://studentbriefs.law.gwu.edu/ilpb/2023/10/30/china-bytedance-and-data-privacy-how-the-federal-trade-commission-could-regulate-tiktoks-collection-and-usage-of-american-users-data-at-home-and-abroad/#:~:text=Since%20its%20meteoric%20rise%20in,shares%20with%20its%20governmental%20partner.

5. [ ] **METR study citation:** Get proper citation for the 19% slowdown finding
6. [ ] **DX Q4 2025 report:** Cite properly (91% adoption, 3.6 hours saved weekly)

7. [x] **Add personal anecdotes:** Specific examples of wins/failures with each tool

The need to cut and paste JavaScript console errors and logs to Cursor has made it hard to use for developing Web-based front end. In summer and fall of last year I could see that the Cursor agent would try different approaches of testing Web UI, including creating test pages etc. However you still need to cut and paste JS console logs. 

TRAE solves this with built-in Web browser. Guessing Cursor and others will follow suit. I have seen TRAE solo and Cursor UI slowdown to a crawl if you issue multiple request as agent is working. Better to have few requests at once.

Claude Code has been most stable and reliable for all coding tasks. Even Web UI but suffers from JavaScript console issue as well.

All agents seem to work better if you plan better and divide work into features you can execute steps by step. The agent typically can help create plan so that's been my modus operandi.

Finally, I've had great results when I use many agents to address issues, testing, plan, debug -- different than one generating code. So while one is generating code I might use other Claude Code instance or Cursor or TRAE to test and or plan. And feed result to Claude Code to fix or implement new feature.

8. [x] **Meetup recording link:** Add link to AI Agents SF #7 recording

AI Alliance LinkedIn live stream: https://www.linkedin.com/posts/the-ai-alliance_ai-agent-meetup-7-in-san-francisco-https-activity-7384387097518018560-UaOQ?utm_source=share&utm_medium=member_desktop&rcm=ACoAAACwFN8BoX7uhT4LLNqDmA6ESIpzaQN2DJA

9. [ ] **Screenshot/visuals:** Consider adding UI screenshots of each tool

10. [x] **Amp details:** Verify current features and pricing model

In 2026, Amp (often referred to as AmpCode), an agentic coding tool developed by Sourcegraph, follows an innovative "Free Frontier" pricing model. Unlike traditional seat-based subscriptions, Amp focuses on a daily-replenishing credit system supported by high-tier frontier models. 

Current Pricing Model (2026)

Amp Free ($0/mo): Provides $10 worth of credits per day (approximately $300/mo in value).

Credits replenish hourly.

Includes access to all modes and frontier models (e.g., Opus 4.5).

Privacy Note: While early versions required data sharing for training, the 2026 free version is supported by unobtrusive ads within the IDE and does not require sharing code for training.

Pay-as-you-go: Individual users can purchase additional credits beyond the daily free limit with no markup on underlying API costs.

Enterprise: Tailored for large teams with features like centralized billing, SSO, and shared context. 

Key Features

Agentic Operation: Unlike standard autocomplete, Amp functions as an autonomous agent that can plan multi-step workflows, manage its own context, and execute coordinated changes across dozens of files simultaneously.

Multi-Model Intelligence:

Smart Mode: Currently driven by Opus 4.5 for high-reasoning tasks.

Rush Mode: Optimized for speed and lower cost, powered by Haiku 4.5.

Sub-Agents: Utilizes specialized sub-agents like the "Oracle" and "Librarian" for deep codebase search and analysis.

Editor Flexibility: Not a standalone IDE, but a "layer" that integrates as a VS Code extension, CLI tool, or even as an extension within other AI editors like Cursor and Windsurf.

Efficient Context (MCP): Uses Model Context Protocol (MCP) to load tools and context only when needed, preventing "context bloat" during long sessions.

Agentic Review: A specialized agent for reviewing code generated by other AI agents to ensure production-readiness.

Visual Integration: Supports "Clickable Diagrams" where Mermaid charts generated by the AI link directly back to the relevant code blocks. 

For the most current usage limits, you can check your status in the Amp Dashboard or via the /settings command in the CLI. 

---

*Word count: ~2,400 words (target: ~2,000—consider trimming "Other Notable Tools" section)*
