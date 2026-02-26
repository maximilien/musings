# Value of Hackathons: What I Learned from a Dozen+ Hackathons in 2025

*Target: ~2,500–3,000 words | Tone: Casual, first-person, story-driven | Substack: AI Musings*
*Lead with personal experience; weave in research-platform angle as the "deeper why"*

---

## Hook / Abstract
- Hackathons are one of the best ways to innovate — they're scoped, time-boxed, and force you to ship
- But they're also something else: accidental research labs
- I participated in over a dozen hackathons in 2025, and I came away with both a personal playbook and a different way of thinking about what hackathons actually are
- This post: what I learned, what worked, what didn't, and why hackathons might be the most underrated research methodology in tech

---

## 1. Introduction — Why Hackathons Still Matter

- Not a new concept — hackathons trace back to 1999 (OpenBSD), but the modern scene has exploded
- The Bay Area alone has dozens every week: AI agents, climate tech, fintech, healthcare, you name it
- The rise of AI tools has changed the game — you can now build real products in 24–48 hours that would have taken weeks before
- Personal angle: what drew me in, how I got hooked after the first one, why I kept going back
- The thing nobody told me: hackathons aren't just about building — they're about learning how people build, what tools they used, what services are new and useful, and that's where it gets interesting

---

## 2. Hackathons as Accidental Research Labs

*(Bridge from personal experience to the bigger idea — the "research platform" thesis)*

- Traditional view: hackathons are competitions, networking, fun coding
- Emerging view: they're controlled environments for studying innovation and tool usage
- Why hackathons create uniquely useful research conditions:
  - **Time compression** — 24–48 hours forces decisions that might take weeks in normal development; you see people's real instincts
  - **Diverse participants** — varied skill levels, backgrounds, and approaches all tackling the same problems
  - **Observable behavior** — teams work in concentrated settings, easy to watch and learn from
  - **Real motivation** — prizes and competition drive authentic engagement, not lab-study compliance
  - **Low-stakes experimentation** — participants try things they'd never risk in production
  - **Natural A/B testing** — different teams solve the same problem differently, giving you organic comparison data
- Researchers are catching on — cite Irani's "Hackathons as Co-optation Ritual" (2015) and Nolte et al.'s work on collaborative innovation (HICSS 2020) as examples of academics studying this space
- Universities are using hackathons for CS education research too — studying how students learn under pressure and comparing teaching methodologies through hackathon outcomes (Huppenkothen et al. 2018)
- But you don't need to be an academic to benefit — anyone paying attention at a hackathon is doing informal research
- If you *wanted* to be systematic about it: pre-hackathon surveys to baseline skills, observation protocols during the event, post-hackathon interviews and code analysis, even control groups comparing teams with different toolsets
  - The ethical piece matters too — informed consent, not letting data collection distort the competition, respecting privacy
  - Longitudinal angle: tracking hackathon participants over time to see what sticks (do projects become products? do skills transfer?)
- But even without a formal study design, just watching and reflecting makes you a better builder

---

## 3. What Companies Get Out of Hackathons

*(How sponsors use hackathons as product research — seen through my eyes)*

- **Product market fit testing** — companies sponsor hackathons to see how developers actually use their tools vs. how they're designed to be used
- **Developer feedback loops** — real-time, unfiltered feedback that's more honest than surveys or focus groups
- **Discovering unexpected use cases** — builders often find applications the company never imagined
- **Recruiting pipeline** — hackathons double as talent scouting, though companies rarely say this out loud
- **How quickly do devs learn new tools?** — hackathons answer this in 48 hours instead of months of onboarding studies
- **Corporate internal hackathons** — some companies run internal hackathons specifically to test new tools and measure adoption; the data they get post-hackathon is gold for product teams
- Brief anecdote from a hackathon where I saw a company visibly surprised by how people used (or ignored) their product
- Example: Anthropic and OpenAI hackathons — watching LLM adoption patterns in real time; what prompting strategies emerge organically, what features get used vs. ignored under pressure

TODO: add anecdocte and example(s) here from interviews or myself.

---

## 4. What *I* Get Out of Hackathons

*(Personal "why bother" before the "how to win")*

- **Focused exploration time** — permission to go deep on one idea without distractions
- **Networking that actually sticks** — you bond with people when you're building together under pressure, not just swapping LinkedIn profiles
- **Keeping up with fast-moving tech** — especially AI, where the landscape shifts monthly; hackathons are the fastest way to pressure-test what's real
- **Inspiration from other builders** — you might be caught in a local minima and other builders (from different background) might bring perspective and half-baked ideas that inspire you (and vice versa) for your next hack and maybe winning idea
- **Testing feasibility** — can this idea actually work? A hackathon gives you a rapid, honest answer
- **The AI agent moment** — 2025 was the year AI agents became hackathon-viable and accessible to all; what used to require a team of 5 now takes 1-2 people with the right tools (and that itself is a research insight worth paying attention to)
- **Testing tools like weave-cli** — hackathons are my go-to environment for stress-testing dev tools I'm building or evaluating; if it works under hackathon pressure, it'll work anywhere
- Anecdote: I won Github Hack Night showing Vectras (multiagent platform) that I used internally to build and maintain my projects. This was a surprise win since I did not intend to submit it but the excitement and feedback help me keep the focus which has led to better version. I will discuss Vectras and it's recent incarnation in a future post.

---

## 5. My Hackathon Strategy Playbook ⭐

*(Main section — this is what readers came for)*

### Before the Hackathon

- **Come in with ONE idea** — don't show up blank, but don't overcommit to a rigid plan either
  - Have a thesis, not a spec. Have some ideas, not dogmas. Have an area of focus, not a religion.
  - Be ready to pivot if you learn something on day one but also don't discard your ideas and plans with zero conviction.
- **Understand the rules and judging criteria** — read them carefully, tailor your project accordingly
  - What are sponsors looking for? Creativity? Technical depth? Business viability?
- **Talk to sponsors early** — before or at the start of the event
  - They'll tell you what they actually care about (often different from what's written)
  - This gives you an unfair advantage in framing your project
- **Pre-build your toolkit** — have your dev environment, templates, and boilerplate ready
  - Know which AI tools you'll lean on (Claude, Codex, Cursor, Lovable, Replit, etc.)
  - Don't waste hackathon hours on setup

### During the Hackathon

- **Visualize the end product immediately** — what does the demo look like?
  - Work backwards from the presentation, not forward from the code
- **Create your presentation slides early** — not at 3am the night before
  - Even a rough deck forces you to clarify your story
  - Slides should tell the narrative: problem → insight → solution → demo → impact
- **Build an MVP, not a polished product** — just enough to demo convincingly
  - Use AI-assisted tools like Lovable, Bolt, or Replit Agent to move fast
  - Focus on the "wow" moment, not edge cases
  - Do have a working system but it does not need to solve all the use cases
- **Write basic integration tests early** — just enough to catch breaking changes
  - Run them after every major change so you don't have a broken demo at pitch time
  - Having good tests (integtration) is now a breeze with AI coding assistants so I think this is a MUST now
- **Include a business case** — judges love a TAM (Total Addressable Market) slide
  - Even a rough market sizing shows you're thinking beyond the code
  - Give some indication of your background in the space or why you care (make it personal rather than about money)
- **Aim for the stars, reach for the sky** — be ambitious in vision, pragmatic in execution
  - Judges reward ambition paired with a working demo

### At Presentation Time

- **Be ready for a live demo** — practice it, have a backup plan, know your failure modes
  - Record a backup video just in case
- **Tell a story, don't list features** — what problem did you solve and for whom?
- **Keep it tight** — respect the time limit, leave room for questions

---

## 6. Perspectives from the Hackathon Scene in Bay Area

*(Voices beyond my own — adds credibility and texture)*

### Dave Nielsen
- One of the oldest community managers in the Bay Area
- Background: Mashup Camps, Cloud Camps — pioneered the unconference/hackathon format before it was mainstream
- Dave's perspective on how hackathons have gone global and how the culture has evolved
- What Dave sees differently about the AI-era hackathon scene

### Adam Chan
- Prolific hackathon organizer, AI-focused
- Runs events through hackdev.io
- Adam's take on what makes a great hackathon vs. a forgettable one
- How Adam's think about the balance between entertainment and generating useful outcomes

### Allie Jones
- Hacker and multi-hackathon winner in Bay Area
- Full time engineer but hacking inside company and in the wild
- Allie's perspective on how AI Coding assistants have changed hacking? Her process and tips?
- Allie's views on how to encourage diversity in hackathons and how diverse (age, gender, etc) have changed hackathons?

---

## 7. Lessons Learned (The Hard Way)

*(Honest reflection — complements the strategy section)*

- **Plan ahead, but not too far ahead** — over-planning kills the creative energy of a hackathon
  - TODO: Anecdote: a time I over-planned and felt boxed in
- **Your first idea is rarely your best execution** — be willing to simplify ruthlessly
- **Solo vs. team trade-offs** — AI tools make solo hackathons viable, but you miss the team dynamic and diverse perspectives
  - TODO: Anecdote: what I missed working alone vs. what I gained in speed
- **Don't underestimate the social component** — some of my best professional connections came from hackathons, not conferences
- **Burnout is real** — doing a dozen in a year taught me to be selective; quality > quantity
- **The tech you learn sticks** — hackathon learning is hands-on and stays with you in a way tutorials don't
- **Hackathon conditions aren't real-world conditions** — what works under time pressure doesn't always translate; be honest about that gap
  - Self-selection bias in who participates, Hawthorne effect of being observed, fatigue-driven shortcuts
- Specific "I wish I'd known" anecdote

---

## 8. Conclusion — Why You Should Try One

- Hackathons are a uniquely efficient way to research, learn, build, and connect
- They also deserve recognition as something more than competitions — they're informal research platforms that reveal how people actually innovate
- The Bay Area scene is thriving, and Lu.ma is the best way to discover what's happening near you
- In the age of AI, the barrier to building something real in 24 hours has never been lower
- For tool builders: hackathons reveal real UX issues faster than any focus group
- For developers: there's no better forcing function for staying sharp
- Call to action: find a hackathon this month and just show up — you'll learn more in a weekend than in a month of tutorials

---

## Notes for Drafting

- **Anecdotes needed:** Flag 3-4 specific hackathon stories to weave throughout (a win, a failure, a surprising connection, a research insight)
    DONE: include inline
- **Interviews:** Schedule or draft Q&A with Dave Nielsen and Adam Chan; even 3-4 pull quotes each would add a lot
    DONE: contacted Dave and Adam and Allie Jones. Will include responses to the two questions to each as I get reply.
- **weave-cli:** Decide how much detail to include — could be a brief mention or a mini case study of testing it at a hackathon
    DONE: it's in one of anecdote
- **References to weave in naturally:**
  - Papers: Irani 2015 (co-optation ritual), Trainer et al. 2016 (steering hackathon projects), Huppenkothen et al. 2018 (hackathons for science), Nolte et al. 2020 (collaborative innovation), arXiv 2022 (hackathon projects becoming products). Drop these casually — e.g., "researchers like Lilly Irani have argued that..." or "a 2020 study found that..."
  - Blogs/reports: Major League Hacking research reports, Devpost hackathon statistics and trends, Anthropic and OpenAI hackathon retrospectives — good for linking as "further reading" at the end
  - Books (optional depth): Fisher's "The Design of Experiments" for research design nerds, Boellstorff's "Ethnography and Virtual Worlds" for methodology — probably too deep for this post but worth mentioning if the research angle resonates with readers
- **Potential visuals:** Photo from a hackathon, screenshot of a project, simple infographic of the strategy playbook
    TODO: I have many need to select. Let's have three and spread accross so add placeholder
- **Substack formatting:** Use pull quotes for key takeaways, keep paragraphs short, consider a TL;DR at the top
    TODO: and make sure to keep the same voice of previous post as much as possible
