# Value of Hackathons: What I Learned from a Dozen+ Hackathons in 2025

*One of the most underrated research methodologies in tech—and a personal playbook for winning*

**TL;DR:** I participated in over a dozen hackathons in 2025 and came away with more than projects and prizes. Hackathons are scoped, time-boxed, and force you to ship—but they're also accidental research labs where you can observe how people actually build, what tools they reach for, and what strategies work under pressure. This post shares what I learned, what worked, what didn't, and why hackathons deserve recognition as one of the most efficient ways to learn, build, and connect—especially in the age of AI.

---

Hackathons are one of the best ways to innovate. Period.

They're scoped. They're time-boxed. They force you to ship something—anything—by a hard deadline. In a world where projects can drag on for weeks in planning purgatory, there's something liberating about having 24 to 48 hours to turn an idea into a working demo.

But after doing over a dozen of them in 2025, I've come to see hackathons as something else entirely: accidental research labs. You don't just build things at hackathons—you learn how other people build things. You see what tools they reach for, what strategies they use, what shortcuts work and what shortcuts break. And if you're paying attention, that observational data is as valuable as anything you code.

This post is everything I learned from that year of hacking. A playbook, a set of lessons, and a case for why hackathons might be one of the most underrated methodologies in tech.

![The author headlining CF Summit 2019 hackathon which he did for five years in late 2010s](images/max-headlining-cf-summit-2018-hackathon.jpg)

## Why Hackathons Still Matter

Hackathons aren't new. The concept traces back to 1999, when OpenBSD held what's considered the first modern hackathon. But the scene has exploded—especially in the Bay Area, where you can find dozens every week covering AI agents, climate tech, fintech, healthcare, and everything in between. Lu.ma is the best way to discover what's happening, and the calendar is relentless.

What *is* new is what you can build in 24 hours. The rise of AI coding assistants—Claude Code, Codex, Cursor, Lovable, Replit Agent—has fundamentally changed the game. Projects that would have taken a team of five engineers weeks to prototype can now be built by one or two people in a weekend. The barrier to shipping something real has never been lower.

I got hooked after my first one. I went in expecting a coding sprint and came out with a working project, various new connections even when I hacked alone, and a completely different mental model for how fast you can move when constraints are tight. So I kept going back. And the thing I did not fully realize before I started is that hackathons aren't just about building—they're about learning how people build. What tools they use, what services are new and useful, what approaches work under real pressure. That's where it gets interesting.

## Hackathons as Accidental Research Labs

The traditional view of hackathons is straightforward: they're competitions. You show up, you code, you network, maybe you win a prize. All true.

But there's an emerging view that I find more compelling: hackathons are controlled environments for studying innovation and tool usage. **Time compression** forces decisions that might take weeks in normal development—you see people's real instincts, not their committee-approved choices. **Diverse participants** with varied skill levels and backgrounds all tackle the same problems, giving you organic comparison data. **Real motivation** from prizes drives authentic engagement. **Low-stakes experimentation** means people try things they'd never risk in production. And **AI assistants** truly change the landscape—everyone can be productive, reducing the need for outside help and enabling all to take advantage of the scoped time.

Researchers like Lilly Irani and Nolte et al. (HICSS 2020) have studied hackathons as sites of collaborative innovation. But you don't need to be an academic to benefit. Anyone paying attention at a hackathon is doing informal research—and even without a formal study design, just watching and reflecting makes you a better builder.

## What Companies Get Out of Hackathons

Sponsors aren't there out of generosity. They're running product research, often more effectively than their internal teams realize.

**Product-market fit testing** is the big one—companies see how developers actually use their tools versus how they're designed to be used. **Developer feedback loops** are real-time and unfiltered. Sponsors regularly discover **unexpected use cases** their product teams never imagined. Hackathons also function as a **recruiting pipeline** and answer a surprisingly hard question: **how quickly do developers learn new tools?**

I've seen this play out in person. At a hackathon in early fall last year focused on Lovable, I ended up using that tool to help bootstrap all of my UI/UX since it's so good at exploring a quick prototype UI for an idea. This experience also informed and confirmed my decision of using TypeScript as my frontend stack with backend services in Golang or Rust—a combination that again and again has proven most efficient for shipping prototypes in 24 or 48 hours. See my post on [choosing the right stack](https://maximilien.substack.com/p/selecting-the-right-software-stack) for details on how to make your own stack decisions.

![Max headlining the Fudan University (https://www.fudan.edu.cn/en/) in Shanghai, China in 2016: Photo 1](images/max-leading-hack-fdu-shanghai-china-2016-2.jpg)
![Photo 2](images/max-leading-hack-fdu-shanghai-china-2016-3.jpg)
![Photo 3](images/max-leading-hack-fdu-shanghai-china-2016.jpg)

## What *I* Get Out of Hackathons

**Focused exploration time**—permission to go deep on one idea without distractions. **Networking that actually sticks**—you bond with people when you're building under pressure, not swapping LinkedIn profiles. **Keeping up with fast-moving tech**—especially in AI, where the landscape shifts seemingly weekly, hackathons are the fastest way to pressure-test what's real. **Inspiration from other builders**—you might be stuck in a local minimum, and someone from a completely different background shakes you loose. **Testing feasibility**—a hackathon gives you a rapid, honest answer on whether an idea actually works.

2025 was the year **AI agents became hackathon-viable**. What used to require a team of five now takes one or two people with the right tools—and that shift itself is a research insight worth paying attention to. Hackathons are also my go-to for **stress-testing dev tools** I'm building or evaluating. If a tool works under hackathon pressure, it'll work anywhere.

One anecdote worth sharing: I won a GitHub Hack Night in early winter by showing Vectras, a multiagent platform I'd been using internally to build and maintain my projects. I hadn't even intended to submit it since it had no UI/UX—I was using it as infrastructure for another hack. But using Lovable I quickly built a complete UI/UX, connected it to my backend agents, and used Weaviate as the common knowledge base. The excitement and feedback gave me the conviction to keep investing in it, which led to a significantly better version. I'll discuss Vectras and its recent incarnation in a future post.

## My Hackathon Strategy Playbook

This is the section I wish someone had given me before my first hackathon. It's evolved through trial, error, and a lot of 3am debugging sessions.

![CF Summit hackathon participants in 2019](images/cf-summit-2019-hackathon-philadelphia.jpg)

### Before the Hackathon

**Come in with ONE idea.** Have a thesis, not a spec. Have some ideas, not dogmas. Have an area of focus, not a religion. Be ready to pivot if you learn something on day one—but don't discard your plans with zero conviction at the first sign of a shinier idea.

**Understand the rules and judging criteria.** What are sponsors looking for? Creativity? Technical depth? Business viability? These emphases vary wildly, and ignoring them is leaving points on the table.

**Talk to sponsors early.** They'll tell you what they actually care about, which is often different from what's written in the official guidelines. This can give you an unfair advantage in framing your project.

**Pre-build your toolkit.** Have your dev environment, templates, and boilerplate ready. Don't waste hackathon hours on setup.

### During the Hackathon

**Visualize the end product immediately.** Work backwards from the presentation, not forward from the code. This is the single most important mindset shift.

**Create your presentation slides early.** Not at 3am the night before. The narrative should flow: problem, insight, solution, demo, impact. Keep it short and sell the vision.

**Build an MVP, not a polished product.** Focus on the "wow" moment, not edge cases. Use AI-assisted tools like Lovable, Bolt, or Replit Agent to move fast.

**Write basic integration tests early.** Run them after every major change so you don't have a broken demo at pitch time. With AI coding assistants, this is now a breeze—I think it's a MUST.

**Include a business case.** Judges love a TAM slide. **Make it personal**—why do you care about this problem?

**Aim for the stars, reach for the sky.** Judges reward ambition paired with a working demo. Not ambition alone.

### At Presentation Time

**Be ready for a live demo.** Record a backup video just in case—Murphy's Law is never more active than during hackathon demos. **Tell a story, don't list features.** Features are forgettable. Stories stick. **Keep it tight.** Going over time is the fastest way to lose judge goodwill.

## Perspectives from the Hackathon Scene

My perspective is one data point. Here are three others from people who've shaped the Bay Area hackathon ecosystem.

### Dave Nielsen — The Community Builder's Community Builder

I've known Dave for over 20 years. As PayPal's first Developer Advocate (2003), he helped pioneer modern developer relations, then went on to produce over 1,000 events—MashupCamp, CloudCamp, ServerlessDays, and more—before "hackathon" was even mainstream vocabulary.

I asked Dave how the culture has evolved and what's different about AI-era hackathons.

> "Around 2006 something changed when Yahoo opened its internal Hack Day to the public. With a festival-like atmosphere and prizes for demos, hundreds of developers showed up. Developers had a good time while learning how to use new APIs. Yahoo learned what developers could do with them. This event had such an impact on Silicon Valley culture that it became the basis of many community events."

> "This latest AI wave has brought hackathons to a whole new level. Developers using AI tools are building applications much faster than before. What used to take a full weekend can now be accomplished in just a few hours. I've seen startup-quality demos emerge from just one 10-hour hackathon at places like AGI House and Cerebral Valley. It is not unheard of for a developer to be offered funding on the spot, after just one session."

### Adam Chan — The Prolific Organizer

Adam runs events through [hackersquad.io](https://hackersquad.io) and has become one of the most prolific AI-focused hackathon organizers in the Bay Area. I asked him what separates a great hackathon from a forgettable one.

> "Every event must produce working demos. 3-minute technical demos showing code, not slides. The measure of success is code written, APIs integrated, and projects shipped—not attendance."

Adam's philosophy on the builder experience is deliberate: sponsors are constrained to brief technical intros—their value comes from putting APIs in builders' hands, not booth visibility. Music during build time signals work mode. The host's primary job is protecting building time from creeping distractions. As Adam puts it: "I don't treat fun and outcomes as a trade-off. Entertainment creates relaxation, relaxation enables creativity, creativity produces outcomes." The forgettable hackathons? "Too much talking. Sponsor talks running over. Measuring by attendance—a vanity metric that incentivizes the wrong behavior."

### Allie Jones — The Hacker's Hacker

Allie is a full-time engineer and multi-hackathon winner in the Bay Area. I asked her how AI coding assistants have changed hacking and how diversity has shaped the scene.

> "I love hackathons because they strip everything away. No GTM strategy, no onboarding forms, no growth plans. Just: what would you build if you knew you couldn't fail? The worst thing that happens is you learn something. That's freeing in a way that regular work rarely is."

> "The thing that changed everything was treating Claude like a coworker instead of a tool. We collaborate. I make it push back on my ideas. I give it context about *why* I'm making decisions, not just what I want built. That back and forth is where the good ideas come from."

On diversity, Allie sees AI as a leveler: "It used to be that you needed years of experience just to keep up. Now all you need is a moment and the willingness to try and fail. I've watched people from nursing, teaching, finance show up and ship something real in seven hours. The entry point moved from 'can you code fast enough' to 'do you care enough to try.'"

## Lessons Learned (The Hard Way)

**Plan ahead, but not too far ahead.** Over-planning kills the creative energy that makes hackathons work. I showed up to one early in 2025 with a detailed technical spec and felt completely boxed in when the actual environment didn't match my assumptions. The winners planned loosely and adapted fast.

**Your first idea is rarely your best execution.** Be willing to simplify ruthlessly. The version that wins is almost always smaller and tighter than what you originally imagined.

**Solo vs. team trade-offs.** AI tools make solo hackathons viable, but you miss the creative collisions that come from someone saying "wait, what if we tried it this way instead?"

**Don't underestimate the social component.** Some of my most valuable professional relationships started at hackathons, not conferences. Building under pressure bonds people.

**Burnout is real.** Doing a dozen in a year taught me to be selective. By the end of 2025, I was choosing hackathons based on specific sponsors, themes, and communities rather than just showing up to everything.

**The tech you learn sticks.** Hackathon learning is hands-on, and it stays with you in a way tutorials never do.

**Hackathon conditions aren't real-world conditions.** What works under time pressure doesn't always translate. There's self-selection bias, a Hawthorne effect from being observed, and fatigue-driven shortcuts. The insights are real, but they need calibration.

![Group shot by the author at Hugging Face Smol agents hackathon in April 2025](images/smol-hackathon-sf-april-2025.jpg)

## Why You Should Try One

Hackathons are a uniquely efficient way to learn, build, connect, and—yes—do informal research on how people actually innovate. They're research platforms that reveal how builders make decisions under constraints.

The Bay Area scene is thriving, and Lu.ma is the best way to discover what's happening near you. But hackathons are everywhere—online and in-person, across every domain and skill level.

My advice: find a hackathon this month and just show up. You don't need a team. You don't need a polished idea. You don't even need to win. You'll learn more in a weekend than in a month of tutorials.

Just show up and start building. Let's go.

---

*Next post: Experience with AI Assistants*

*Previous post: [Selecting the Right Software Stack](https://maximilien.substack.com/p/selecting-the-right-software-stack)*

---

## Recommended Resources

**Academic Research:**
- Irani, L. (2015) — "Hackathons and the Making of Entrepreneurial Citizenship" — on hackathons as cultural rituals
- Nolte, A. et al. (2020) — "What Happens to All These Hackathon Projects?" — collaborative innovation, HICSS
- Huppenkothen, D. et al. (2018) — "Hack Weeks as a Model for Data Science Education and Collaboration" — hackathons for science
- Trainer, E. et al. (2016) — "How to Hackathon" — steering hackathon projects effectively

**Hackathon Discovery:**
- [Lu.ma](https://lu.ma) — Find hackathons near you
- [Devpost](https://devpost.com) — Browse hackathon projects and upcoming events
- [Major League Hacking](https://mlh.io) — Research reports and hackathon statistics

**Further Reading:**
- [hackersquad.io](https://hackersquad.io) — Adam Chan's AI-focused hackathon events
- Fisher, R.A. — *The Design of Experiments* (for research design enthusiasts)
