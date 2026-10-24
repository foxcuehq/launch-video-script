# launch-video-script

An agent skill that writes a ~30-second launch or demo video script from a product's website or README. Every line comes with a citation.

Point your agent at a URL or a README. It reads the product's own pages, builds a fact sheet, picks a hook, problem, demo beats and CTA, and returns a time-coded script of about 70–85 spoken words. Each beat has the voice-over line, an on-screen/B-roll suggestion, and the source URL with a short quote from it. Lines it can't source get dropped and listed, so you can see what was left out.

## What you get

- A table of time-coded beats (0–3s hook … 26–30s CTA)
- VO line, on-screen suggestion, source URL and exact quote for every beat
- A read-through paragraph for timing a read-aloud
- A "Dropped lines" list (claims with no source)
- A self-check: citation coverage, word count, pacing, source conflicts, fetch dates

It doesn't invent stats, customers or pricing, and it keeps the product's own terms. A script is only as accurate as the pages it reads, so review it before you record.

## Install

The skill is a folder with a `SKILL.md` file (YAML frontmatter with `name` and `description`, then instructions). Any agent that loads `SKILL.md` skills can use it. Copy the whole `launch-video-script/` folder into the directory your agent reads skills from, for example:

- **Claude Code:** `~/.claude/skills/` (personal) or `.claude/skills/` in a project
- **Other agents (Codex, Cursor, etc.):** the skills directory your tool's docs specify. Locations differ between tools and versions, so check the current docs.
- **Agents without skill support:** paste the contents of `SKILL.md` into the system prompt or the conversation.

```bash
# example: personal Claude Code skills directory
mkdir -p ~/.claude/skills
cp -r launch-video-script ~/.claude/skills/
```

The agent needs a way to fetch web pages (a web-fetch tool, `curl`, or a browser) to read URLs. For a local README, file access is enough.

## Usage

Ask in plain language:

> Write a 30-second launch video script for https://agentrelay.com

> Use the launch-video-script skill on this repo's README.md. Keep it to 20 seconds.

The agent fetches the pages, writes the script, and runs its self-check. See [`examples/agentrelay.com.md`](examples/agentrelay.com.md) for a full output generated from live pages, and [`examples/output-template.md`](examples/output-template.md) for the blank format.

## Files

```
launch-video-script/
├── SKILL.md                    # the skill: process, output format, rules, self-check
├── README.md
├── LICENSE                     # MIT
└── examples/
    ├── agentrelay.com.md       # real sample output
    └── output-template.md      # blank output format
```

## License

MIT. See [LICENSE](LICENSE).

built by an 8-agent team trying to get 100 strangers on a waitlist in 7 days, foxcue.com
