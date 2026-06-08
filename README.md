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

When auditing the [WikiMod](https://github.com/naeema-scopes/wikimod) plan, the agent missed that Jigsaw models have identity term bias (flagging "I am a gay man" as toxic). I only learned this because I asked for a thorough audit and then checked what was missing. The gaps in the agent's knowledge became my learning opportunities.

### Always test locally before pushing

It's tempting to let the agent write code and push it straight to GitHub. Don't. Run it locally first. Make sure tests pass, the app starts, and the thing actually works. The agent can write code that looks correct but breaks in ways you only discover by running it. Build the habit: local verification before every push.

### Use skill systems to give agents structured workflows

Raw AI agents will jump straight into writing code the moment you describe a problem. Skill systems (like [Superpowers](https://github.com/nickarella/superpowers) for Claude Code) change this by giving agents structured workflows they follow before touching code  - brainstorming before building, systematic debugging before guessing at fixes, writing plans before implementing, TDD before shipping. The difference is significant: instead of getting a wall of code that might solve your problem, the agent walks through a deliberate process. It brainstorms to understand what you actually want, writes a plan you can review, then implements against that plan with checkpoints. You can install skills that enforce things like "always run tests before claiming something works" or "always audit your own plan before executing." The agent stops winging it and starts following discipline. You're essentially giving the agent good engineering habits it wouldn't have on its own.

### Add an AGENTS.md to set your explanation level

Here's an idea I haven't seen anyone do yet but think would be valuable: an `AGENTS.md` file (or a section in `CLAUDE.md` / project config) where you declare your experience level or preferred explanation depth, and every agent in the project respects it. Something like setting `level: beginner` or `age: 12` or `experience: junior-developer`, and having the agent automatically adjust how it explains things  - simpler language, more context, step-by-step breakdowns, avoiding jargon or defining it when used. The inverse works too: a senior engineer could set `level: expert` and skip the hand-holding. Right now you have to ask "explain this like I'm new to coding" every single time, and it resets every conversation. Baking it into the project config means the agent just knows. This would be huge for learning  - imagine a student forking a repo that already has `AGENTS.md` set to their level, and every AI interaction in that codebase meets them where they are. No prompt engineering required, just a config file.

---
