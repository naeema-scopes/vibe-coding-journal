# Vibe Coding Journal

Field notes on working with AI coding tools. What works, what doesn't, and what I've learned the hard way.

This is a living document. I add to it as I build and ship.

---

## Entries

### Always audit generated plans before building

AI agents write ambitious plans that sound great on paper but hide real issues: missing dependencies, contradictory designs, architectural gaps between components. Before implementing anything, have the agent audit its own work  - or better, have a separate agent review it with fresh eyes. I caught 100+ issues across 4 project plans by doing this. Things like async/sync mismatches, missing database models, and security holes that would have cost days to debug later.

### Push back on ideas that aren't actually good

When brainstorming with AI, don't accept the first suggestion. Ask "is this actually useful?" and "does something already do this?" Twice during project planning, I asked the agent whether the idea filled a real gap  - and the research came back showing it genuinely did (and showing what already existed so we didn't reinvent the wheel). Conversely, pushing back on an initial concept ("it's not unique") led to a much stronger project idea.

### Scope ruthlessly  - the agent won't do it for you

AI will happily add features, personalities, modes, and integrations forever. You have to be the one who says "no, one voice, not four" or "keep it limited to what the model was trained on." Every feature the agent suggests sounds reasonable in isolation. Your job is to see the whole picture and cut what doesn't serve it.

### Verify before you trust the output

When the agent says "this will work," ask it to prove it. Does GitPython actually return diffs for untracked files? (No, it doesn't.) Does a rolling average make sense for 3 data points? (No, it doesn't.) The agent is confident about things it's wrong about. Treat its technical claims like a coworker's  - worth hearing, worth verifying.

### Use parallel agents for independent research, not for writing

Spinning up 4 agents to research different things at the same time is great  - results come back fast and each agent goes deep. Spinning up 4 agents to write giant documents at the same time hits token limits and creates more problems than it solves. Research in parallel, write sequentially.

### Let the agent's mistakes teach you the domain

When auditing the WikiMod plan, the agent missed that Jigsaw models have identity term bias (flagging "I am a gay man" as toxic). I only learned this because I asked for a thorough audit and then checked what was missing. The gaps in the agent's knowledge became my learning opportunities.

### Always test locally before pushing

It's tempting to let the agent write code and push it straight to GitHub. Don't. Run it locally first. Make sure tests pass, the app starts, and the thing actually works. The agent can write code that looks correct but breaks in ways you only discover by running it. Build the habit: local verification before every push.

---
