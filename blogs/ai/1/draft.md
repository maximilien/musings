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

The background agent capabilities are particularly compelling. You can spin up tasks, in containers, and let them run while you focus on something else. The UI for reviewing and approving changes is clear and well-designed. And model flexibility means you can choose your preferred LLM—Claude, GPT-5, or others.

**My experience (three months of extensive use):**

I especially liked the background agent workflow for parallelizing work. For UI-heavy projects, Cursor worked well, though I often found myself needing to provide browser context manually—copying the browser's JavaScript console output and pasting it to the agent. Where it struggled was with long sessions—context approaching its limits would cause the agent to slow down significantly and "forget" earlier decisions or make suggestions that conflicted with code it had written minutes before. the UI would also slow down and even hang.

Context windows in Cursor vary: standard use runs around 10K-20K tokens for edits and chat, while "Max Mode" provides 200K tokens for larger projects and can access even larger model contexts (up to 1M tokens for some models) for deeper analysis. You can monitor usage in real-time and use features like rules to manage larger context effectively across chats.

**Pricing (as of January 2026):**

Cursor uses a hybrid model combining flat monthly fees with usage-based credit pools:
- **Hobby (Free):** 2,000 Tab completions and 50 slow requests per month
- **Pro ($20/mo):** Unlimited Tab completions, unlimited "Auto" model, $20 credit pool for premium models
- **Pro+ ($60/mo):** Same as Pro with 3x credit pool ($60)
- **Ultra ($200/mo):** 20x credit pool ($400) and priority access to new features

The pricing volatility has been frustrating—plan changes and usage limits have shifted as Cursor has grown rapidly.

**Best for:** Developers who prefer GUI workflows, VSCode users, teams wanting visual code review.

## Claude Code: The Terminal-Native Revelation

Claude Code is Anthropic's bet on terminal-native development, and for me, it's been revelatory.

The philosophy is fundamentally different from Cursor. Instead of embedding AI into an existing IDE, Claude Code operates as an autonomous agent that lives in your terminal (and now also has a VS Code extension). You describe what you want, it goes and does it—cloning repos, grepping for answers, editing files, running tests, staging commits.

**What works well:**

The deep reasoning capabilities from Claude models are immediately apparent. Multi-file operations that would require careful orchestration in an IDE-based tool happen naturally here. The MCP (Model Context Protocol) integration opens up powerful tool access. And the speed of CLI interaction removes the overhead of waiting for visual updates.

The 200K context window actually delivers what it promises. Reports suggest Claude Code uses 5.5x fewer tokens than Cursor for equivalent tasks while finishing faster with fewer errors.

**My experience:**

Claude Code has been the most stable and reliable tool for all my coding tasks. So compelling that I switched from Cursor's GUI to using cursor-agent as well (the CLI interface for Cursor). At first, I questioned whether my preference was about the CLI interaction or Anthropic's model superiority. The answer is likely both—better models AND a faster interaction paradigm.

Even for Web UI work, Claude Code excels—though it suffers from the same JavaScript console limitation as Cursor. You still need to manually copy and paste browser console output to provide context about runtime errors.

The challenge is review discipline. Speed is addictive. The terminal-based workflow makes it easy to accept suggestions without the same scrutiny you'd apply when visually reviewing diffs. I've found myself accepting too many changes without sufficient review—a feature and a bug of the approach.

**Critical learning:** Establish strong testing practices early. Let the agent run tests after changes. Use agents to create tests too! Without this discipline, the speed advantage becomes a liability.

**Best for:** CLI-native developers, complex refactoring, multi-file operations, those who value speed over visual review.

## TRAE: The ByteDance Wildcard

I stumbled into TRAE during a meetup and decided to do a solo hackathon day with it. Within hours, I was convinced the interface was superior to Cursor for certain workflows.

TRAE (The Real AI Engineer) launched in early 2025 and has grown remarkably fast—over 6 million registered users and 1.6 million monthly active users as of late 2025. The approach is agent-focused from the ground up.

**What sets it apart:**

The built-in browser is huge for UI work. Less switching between your IDE and a browser to see what you're building—it's integrated directly. No more copying JavaScript console errors and pasting them to the agent. This alone solves a major friction point that Cursor and Claude Code still have. (I expect others will follow suit.)

The no-interrupt run mode lets you kick off complex tasks without constant prompting. And the multiple agents capability means you can parallelize work within the IDE itself.

TRAE's "SOLO mode" takes this further—full-process automated development from requirements input to deployment. It's ambitious, has an agent-focused interface, and early reports suggest it's genuinely useful for rapid prototyping.

**Pricing and models:**

TRAE is roughly half the price of Cursor (at the time of this writing). However, there's a significant caveat: as of early November 2025, ByteDance removed all Claude models from TRAE due to Anthropic's updated policy restricting services for Chinese-controlled entities globally.

Current model availability includes GPT-5, Gemini 2.5 Pro, Kimi-K2-0905, and DeepSeek V3.1-Terminus. TRAE states these models are optimized for "reasoning quality" and "execution chain" to maintain performance levels similar to when Claude was available. The open-source Trae-CLI still supports bring-your-own-key functionality if you want to use your own Anthropic API key.

For me, this is actually a feature: since I use Claude Code as my primary tool, TRAE provides a useful counterbalance with different models for testing, reviewing, and getting alternative perspectives, at times, on specific code.

**The trade-offs:**

TRAE lacks the fast CLI interface that makes Claude Code so compelling. For developers who think in terminal commands, this is a significant gap. The ecosystem is also newer and less mature than Cursor's. I've also seen TRAE SOLO (and Cursor) slow to a crawl if you issue multiple requests while the agent is working—better to queue up requests one at a time or wait for agent to be done and waiting for input.

**Privacy concerns:**

And then there's the elephant in the room: ByteDance ownership. Independent research in 2025 revealed that TRAE can generate up to 500 network calls (roughly 26MB of data) in under 10 minutes of active use. This includes persistent identifiers like machine ID and hardware fingerprints that can follow users across different projects and reinstalls.

TRAE offers a "Privacy Mode" toggle that prevents chat interactions and code snippets from being used for model training. The primary codebase stays on your machine, with only numerical embeddings uploaded for indexing. But as a ByteDance product, TRAE remains subject to Chinese data security laws that can compel companies to provide access to user data. For developers working on proprietary or government-related code, this typically necessitates a more cautious approach compared to Western-based alternatives.

**Best for:** Developers wanting an agent-focused IDE experience, those doing heavy UI work, cost-conscious developers willing to accept ByteDance's data practices.

## Other Notable Tools

The landscape is crowded. Here's a quick rundown of other tools worth knowing:

**Amp (Sourcegraph):** An agentic coding tool following an innovative "Free Frontier" pricing model. The free tier provides $10 worth of credits per day (approximately $300/month in value), replenishing hourly, with access to all modes and frontier models including Opus 4.5. Unlike standard autocomplete, Amp functions as an autonomous agent that can plan multi-step workflows and execute coordinated changes across dozens of files. It uses MCP to load tools and context only when needed, preventing "context bloat" during long sessions. Beyang Liu, the co-founder and CTO, spoke at our [AI Agents Meetup SF #7 on Coding Agents](https://www.linkedin.com/posts/the-ai-alliance_ai-agent-meetup-7-in-san-francisco-https-activity-7384387097518018560-UaOQ). His thesis: "Code review is dead; long live code review!"—the bottleneck has shifted from writing to reviewing.

**Warp:** CLI-focused with multiple tabs capability. Great for terminal lovers who want AI assistance without leaving their shell. Still depends on underlying LLMs. My friend [Allie Jones](https://www.linkedin.com/in/allierays/) introduced me to this tool and swears by it--at least in late fall 2025.

**Codex (OpenAI):** OpenAI's entry has re-emerged as a serious agent-first tool. Limited personal experience, but reports suggest it's competitive, particularly for deterministic multi-step tasks.

**Jules (Google):** Google's version with Gemini model integration. Catching up with leaders but not yet a daily driver for most developers.

**Kivo (Amazon):** Amazon's entry, integrating with Q. Early days, but worth watching given AWS's enterprise footprint.

**Others to watch:** Aider (open source, git-focused), Continue (open source IDE extension), Cline (Claude-focused), Windsurf (Codeium's IDE).

## The Two Paradigms

After a year of testing, I've concluded, at this point, that the IDE vs CLI distinction is more fundamental than the specific tool you choose.

**IDE-based (Cursor, TRAE, Windsurf):**

- Visual view of your code base
- Visual code review is built into the workflow
- Integrated with existing development patterns
- Better for those who think visually or come from VSCode
- Trade-off: more overhead, slower interactions—especially deep into a session

**CLI-based (Claude Code, Amp, Warp):**

- Speed and focus without GUI overhead
- Natural for terminal-native developers
- Excellent for parallelization—I typically work on two or three repos at once using iTerm's tabs
- Review happens via git and terminal tools rather than visual diffs
- Trade-off: easier to miss issues, requires more discipline (testing, diff reviews)

Neither is objectively better. The right choice depends on how you think about code.

## Common Challenges

All these tools share fundamental limitations:

**Context window is the biggest issue.** Every tool struggles with long contexts. Frequent summarization and compacting means the AI "forgets" earlier decisions. This is improving—Claude Code's 200K window is genuinely better than what we had a year ago—but it remains the primary constraint.

**Filesystem interaction creates friction.** For security reasons, tools interact with the filesystem slowly and carefully. This is necessary but creates noticeable latency, especially for operations touching many files.

**LLM dependency is the great equalizer.** The tool is only as good as its underlying model. This is why Claude Code feels different from Cursor even when both use Claude models—the integration, prompting, and workflow matter, but the model quality is the foundation.

**The productivity paradox is real.** A recent METR study found that experienced open-source developers actually took 19% *longer* with AI tools than without in certain contexts. Meanwhile, DX's Q4 2025 report shows 91% adoption and real time savings. The difference? Context matters. AI helps more with unfamiliar codebases and routine tasks; it can slow you down on deeply familiar code where your intuition is faster than explaining to an agent.

[CITE: METR study (metr.org/blog/2025-07-10-early-2025-ai-experienced-os-dev-study) and DX Q4 2025 report (getdx.com)]

## Best Practices Across Tools

Whatever tool you choose, these practices make a difference:

**Testing is non-negotiable.** Agents make changes fast—tests catch mistakes and regressions. Automate testing early in the project. Let the agent run tests after changes. Use agents to create tests too! This is the single most important discipline for AI-assisted development.

For instance, all my repos include a `lint.sh`, `build.sh`, and `test.sh` that I use to ensure quality and avoid regressions. I use AI to create these and update them but for each new project I point the AI to previous versions so that the scripts are similar keeping my flow: `./lint.sh && ./build.sh && ./test.sh` a command I use before and after every change. Then when ready I move this to CI/CD ensuring every push re-runs these as well as longer integration tests.

**Context management matters.** I've developed personal conventions: NEXT_STEPS.md, TODOs.md, and the classic CHANGELOG.md files that persist context across sessions. A docs/planning/ directory for the agent to reference and create detailed plans of features. Explicit handoff notes when context is getting long. These feel manual, but they dramatically improve agent performance. And again the agent can update and clean these easily with one prompt.

**Planning before coding pays off.** All agents seem to work better if you plan better and divide work into features you can execute step by step. The agent can help create the plan—so that's become my modus operandi. Describe the goal, have the agent break it down, save a plan with TODOs, then execute incrementally.

**Review discipline is essential.** Speed is addictive. Build review into your workflow deliberately. Trust but verify. The 30% code acceptance rate for GitHub Copilot suggestions isn't a bug—it's appropriate skepticism.

**Multiple tools in parallel is normal.** 59% of developers now run three or more AI coding tools simultaneously. This isn't indecision—it's pragmatism. Different tools excel at different tasks. I often use different tools or models to write tests vs code, or to plan before writing code. While one agent is generating code, I might use another Claude Code instance or Cursor or TRAE to test and plan—then feed results back to fix or implement new features.

## Looking Forward

The space is evolving fast. Here's where I see it heading:

**Near-term:** Context management will improve dramatically. Hybrid approaches combining IDE and CLI will become common. Better integration with the full development lifecycle—not just coding, but testing, deployment, and monitoring. And built-in browsers will become standard (TRAE is ahead here).

**Medium-term:** The multi-agent future is coming. You'll describe goals and let agents manage other agents. Orchestration becomes the key skill. Human developers become project managers, architects, and reviewers rather than primary code writers.

**Longer-term:** The 41% of code that's AI-generated today will grow. The question isn't whether AI will change software development—it's how we adapt our practices, our teams, and our careers to the new reality.

## Conclusion

Two leading paradigms: IDE-integrated and terminal-native. All depend on LLM quality and face context window challenges. Choose based on your workflow preference and project needs.

The productivity gains are real—developers report 30-75% time savings on coding, testing, and documentation. For me it's easily in the 50% to 80% range. But so are the challenges: context limits, review and testing discipline, and the need to maintain your own coding skills even as you delegate more to agents.

Invest in testing infrastructure early—locally and in CI/CD. Develop context management strategies. Embrace the tools thoughtfully, not uncritically.

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
- [DX Q4 2025 AI Impact Report](https://getdx.com/blog/ai-assisted-engineering-q4-impact-report-2025/)

**From AI Agents Meetup SF:**
- [#7: Coding Agents](https://luma.com/5ry1w1ak) — Talks from Sourcegraph, DevSwarm, TRAE, and Morph
- [AI Alliance LinkedIn Live Stream](https://www.linkedin.com/posts/the-ai-alliance_ai-agent-meetup-7-in-san-francisco-https-activity-7384387097518018560-UaOQ) — Full recording

---

## Items to Verify/Research Before Publishing

### ✅ Completed

1. **Cursor context window:** 10K-20K standard, 200K in Max Mode, up to 1M for some models
2. **Cursor pricing:** Hobby (Free), Pro ($20), Pro+ ($60), Ultra ($200) with credit pool system
3. **TRAE model availability:** Claude removed Nov 2025; now GPT-5, Gemini 2.5 Pro, Kimi-K2, DeepSeek V3.1
4. **TRAE privacy concerns:** 500 network calls/10 min, hardware fingerprinting, Privacy Mode available, subject to PRC data laws
5. **Personal anecdotes:** JS console friction, TRAE browser advantage, multi-agent workflow, planning approach
6. **Meetup recording link:** AI Alliance LinkedIn live stream added
7. **Amp details:** Free Frontier model ($10/day credits), MCP integration, Opus 4.5 access

### ⏳ Pending

1. **METR study citation:** Add formal citation (currently linked in Resources)
2. **DX Q4 2025 report citation:** Add formal citation (currently linked in Resources)  
3. **Screenshots/visuals:** Add UI screenshots of Cursor, Claude Code, TRAE, Amp

---

## Assessment: DRAFT 2

**Strengths:**
- Strong personal voice with authentic experience
- Good balance of technical detail and practical advice
- Pricing and feature info is current and detailed
- Privacy section on TRAE is thorough without being alarmist
- Best practices section is genuinely useful
- Multi-agent workflow insight is distinctive

**Ready for publication with:**
- Adding 2-3 screenshots to break up text
- Optional: formal academic citations for METR/DX (the links are sufficient for a blog)

**Word count:** ~2,800 words (over target, but content is substantive—consider whether to trim "Other Notable Tools" or keep the depth)

**Recommendation:** This is ready for final polish. The additional detail from your research makes it genuinely useful rather than just another overview. The personal anecdotes differentiate it from the dozens of "Cursor vs Claude Code" posts out there.
