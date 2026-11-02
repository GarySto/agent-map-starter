# Agent Map starter

**A free, single-file 3D map of your AI agents, every hand-off between them, and a clear red line wherever something is broken or left on its own.**

This is the starter version of the [Agent Map on garystow.co.uk](https://garystow.co.uk/agents/map/), where I map the 60+ agents that run my website and my demo trading system. I built it because a busy-looking team of agents can still have a broken link in the middle of it. The full story is in [62 AI Agents and the Broken Links Between Them](https://garystow.co.uk/articles/62-ai-agents-and-the-broken-links-between-them-why-i-built/).

![The example map](https://garystow.co.uk/articles/62-ai-agents-and-the-broken-links-between-them-why-i-built/62-ai-agents-and-the-broken-links-between-them-why-i-built.webp)

## What you get

- Every agent as a glowing light on a slowly spinning sphere, grouped by team, one colour per team.
- Every hand-off as a line, with a small light travelling along it so you can see which way the work flows.
- Broken hand-offs flash red. Any agent marked broken, or with nothing coming in and nothing going out, turns red too.
- Click any light to see its job, what it receives and where it sends its work.
- Large text, high contrast, keyboard-friendly buttons, works on a phone, and respects "reduce motion".
- No libraries, no build step, no tracking. Two files: `index.html` and `agents.json`.

## Use it in three steps

1. **Download** this repository (green **Code** button, then **Download ZIP**) and unzip it.
2. **Edit `agents.json`** with your own agents and hand-offs (the format is below).
3. **Open it through a tiny local web server**, because browsers won't let a page read `agents.json` straight from your disk. In the unzipped folder, run:

   ```
   python -m http.server 8000
   ```

   then open <http://localhost:8000> in your browser. (On Windows, use `py` instead of `python` if that's how Python is installed.)

To share it, put both files on any static host. GitHub Pages works and is free.

## The `agents.json` format

```json
{
  "title": "My AI agent team",
  "checked": "when this data was last checked",
  "teams": [ {"id": "content", "name": "Content team", "colour": "#ffc857"} ],
  "centre": [
    {"id": "goal", "label": "GOAL: grow the business", "desc": "Every chain should end here."},
    {"id": "me", "label": "Me (decides)", "desc": "The human with the final say.", "top": true}
  ],
  "agents": [
    {"id": "writer", "label": "Writer", "team": "content", "desc": "Drafts articles.", "ok": true, "private": false}
  ],
  "handoffs": [
    {"from": "writer", "to": "me", "what": "drafts to approve", "ok": true}
  ]
}
```

- `ok: false` on an agent or hand-off shows it as broken.
- `private: true` adds a PRIVATE tag, so you can keep an agent on the map without describing its job.
- Items in `centre` sit inside the sphere (your goals). Add `"top": true` for the person who decides.

## Make it live, not just a picture

The map is only as good as the data behind it. Mine is written every 30 minutes by a small script that asks three questions of every agent and hand-off: did it run, did it produce something real, and did that reach the next agent? Anything that fails is written as `"ok": false`. Have your own health check write `agents.json` on a schedule and the map stays honest.

## Prefer to build your own from scratch?

Paste this into Claude or ChatGPT, list your agents in the brackets, and you'll get a first version:

```
Build me a single self-contained HTML page that draws my AI agents as an interactive 3D sphere, using a plain HTML canvas and no libraries. Read the agents and hand-offs from a JSON block I can edit. Place each agent as a glowing light grouped by team, one colour per team. Draw each hand-off as a curved line with a small light travelling from sender to receiver. Any hand-off or agent marked "ok": false, or an agent with no working hand-offs, turns red. The sphere spins slowly; drag to turn, scroll or pinch to zoom, and a button turns the spin off. Clicking a light opens a side panel with its job, what it receives and where it sends its work. Large text, high contrast, no sideways scrolling on a phone. My agents: [LIST YOUR AGENTS, WHAT EACH ONE DOES, AND WHO IT SENDS WORK TO].
```

## Licence

MIT. Use it, change it, ship it. A link back to [garystow.co.uk](https://garystow.co.uk/agents/map/) is appreciated, never required.

Built by [Gary Stow](https://garystow.co.uk/). See also [Village Starter](https://github.com/GarySto/village-starter), which shows the same kind of team as a living village.
