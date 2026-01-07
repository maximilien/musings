AI Coding Assistants

Target length: ~2000 words

Abstract
* Coding assistants (agents) represent the most lucrative and impactful application of AI today
* The dream of 10x to 100x engineering productivity is becoming reality
* This post shares my experience using multiple tools over the past year
* Two dominant interfaces have emerged: IDE-based and terminal/CLI-based
* All approaches depend on underlying LLM quality and face common challenges
* Understanding the landscape helps developers choose the right tool for their workflow

Introduction
* The dream of dramatically accelerated engineering is real in 2025
* AI agents have become the most exciting use case for AI in production
* Major players: Anthropic (Claude Code), Cursor, TRAE, and many others
* I started with Cursor more than a year ago then quickly ended using many others as I hit the limits of Cursor and wanting to streamline and parallelize work

Cursor
* First mover advantage:
    * First major player in the IDE-focused agent space
    * Established brand recognition and large user base
    * Fast iteration and feature development
* Strengths:
    * Seamless VSCode integration — feels native
    * Excellent background agent capabilities
    * Clear UI for reviewing and approving changes
    * Model flexibility — choose your preferred LLM
* My experience (3 months of extensive use):
    * Especially liked the background agent workflow
    * Good for UI work but lacks browser context
    * Gets stuck when context approaches its session limits
    * Price volatility has been frustrating
* Best for: Developers who prefer GUI workflows, VSCode users, teams wanting visual code review

Claude Code
* Agent-first CLI approach:
    * Anthropic's bet on terminal-native development
    * Process is fast, intuitive, and focused — no GUI overhead
    * Experience has been revelatory
* Strengths:
    * Deep reasoning capabilities from Claude models
    * Speed of CLI interaction
    * Excellent at complex, multi-file operations
    * MCP integration for tool access
* My experience:
    * So compelling that I switched from Cursor GUI to cursor-agent as well
    * Question: is this CLI preference or model superiority?
    * Likely both: better models AND faster interaction paradigm
* Challenges:
    * Less time reviewing agent-generated code (a feature and a bug)
    * UI doesn't make it easy to review long interactions
    * Easy to accept too many suggestions without scrutiny
    * Critical: establish strong testing practices early
* Best for: CLI-native developers, complex refactoring, those who value speed over visual review

TRAE
* Discovery:
    * Stumbled into TRAE during a meetup
    * Did a TRAE Solo hackathon day — immediately convinced the interface was superior to Cursor
    * ByteDance entry showing serious innovation
* Innovations:
    * Agent-focused design from the ground up
    * Built-in browser (huge for UI work)
    * No-interrupt run mode
    * Multiple agents capability
* Trade-offs:
    * Lacks fast CLI interface
    * Depends on external LLM providers (Anthropic, OpenAI)
    * Also integrates Qwen and other models
    * Newer, less mature ecosystem
* Best for: Developers wanting best-of-both-worlds IDE experience, those doing heavy UI work

Other Notable Tools
* Amp (Sourcegraph):
    * Similar to Claude Code approach
    * FREE with advertising model
    * Beyang Liu (CTO) spoke at our meetup #7
* Warp:
    * CLI-focused with multiple tabs capability
    * Great option for terminal lovers
    * Still depends on underlying LLMs
* Codex (OpenAI):
    * OpenAI's entry in the space
    * Similar approach to Claude Code
    * Limited personal experience but competitive
* Jules (Google):
    * Google's version with proprietary LLM
    * Catching up with leaders
    * Gemini model integration
* Kivo (Amazon):
    * Amazon's entry
    * Depends on other LLMs
    * Q integration potential
* Others to watch: Aider, Continue, Cline, Windsurf

The Two Paradigms
* IDE-based (Cursor, TRAE, Windsurf):
    * Visual code review
    * Integrated with existing workflows
    * Better for those who think visually or come from VSCode
    * Trade-off: more overhead, slower interactions — especially when deep into a session
* CLI-based (Claude Code, Amp, Warp):
    * Speed and focus
    * Natural for terminal-native developers
    * Less visual review friction and more git-based terminal review
    * Trade-off: easier to miss issues, less context

Common Challenges
* Context window limitations:
    * All tools struggle with long contexts
    * Frequent summarization and compacting
    * This is the biggest issue across all approaches
* Filesystem interaction:
    * Slow interfacing for security reasons
    * Necessary but creates friction
    * Different tools handle this differently
* LLM dependency:
    * Tool is only as good as underlying model
    * Model choice significantly affects output quality
    * The great equalizer and differentiator

Best Practices Across Tools
* Testing is non-negotiable:
    * Agent makes changes fast — tests catch mistakes
    * Automate testing early in the project
    * Let the agent run tests after changes
    * Use agents to create tests too!
* Context management:
    * Use temporary files: NEXT_STEPS.md, TODOs.md, CHAGELOG.md
    * Increasing context window helps but isn't enough
    * Develop personal conventions for context handoff
    * I ended up having agent create docs/planning/ directory and add plans there
* Review discipline:
    * Speed is addictive but review matters
    * Build review into your workflow
    * Trust but verify

Looking Forward
* Near-term evolution:
    * Context management will improve dramatically
    * Hybrid approaches combining IDE and CLI
    * Better integration with development lifecycle
* The multi-agent future:
    * Describe goals, let agents manage other agents
    * Orchestration becomes the key skill
    * Human as architect and reviewer and final tester

Conclusion
* Two leading paradigms: IDE-integrated and terminal-native
* All depend on LLM quality and face context window challenges
* Choose based on your workflow preference and project needs
* Invest in testing infrastructure early
* Develop context management strategies
* The productivity gains are real — embrace thoughtfully

Recommended Research

Tool Documentation:
* Claude Code: docs.anthropic.com
* Cursor: cursor.com/docs
* TRAE: trae.ai
* Amp: ampcode.com

Analysis:
* Latent Space podcast episodes on coding agents
* SWE-bench comparisons
* r/ClaudeAI and r/cursor discussions

My meetup talks:
* AI Agents SF #7: Coding Agents (link to recording)

Bibliography
[To be populated with specific citations]
