---
name: launch-video-script
description: Write a ~30-second demo or launch video script (70–85 spoken words) from a product's website URL or README, with every line time-coded and cited to the exact source page or section it came from. Use when someone asks for a launch video script, demo video VO, product teaser script, or a 30-second explainer built from a site or repo.
---

# Launch video script

Turn a product's own website or README into a roughly 30-second launch or demo video script. Every spoken line is traceable to a quoted snippet on a page you actually read. If a line can't be traced, it doesn't ship.

## Inputs

- **Required:** one starting point, either a website URL (e.g. `https://example.com`) or a README (a repo URL, a raw README URL, or a local `README.md` file).
- **Optional:** target length (default 30s), audience (default: someone who has never heard of the product), tone (default: plain and confident), a CTA the user wants (default: whatever the source's primary CTA is).

If the user gives nothing but a product name, ask for a URL or README. Don't guess the domain.

## Process

### 1. Collect sources

Read the starting point first, then follow at most 3–5 more first-party pages that are likely to hold facts:

- **Marketing site:** home page, then (if linked) features/product, pricing, docs intro or quickstart, about. Skip blog posts unless the home page is thin.
- **README-only repo:** the README, then docs it links to in the same repo (`docs/`, `examples/`, `CONTRIBUTING` only if relevant), the repo description, and the package registry page if the README links to one.

Use whatever fetch tool you have (a web fetch tool, `curl`, a browser). For each page record: the exact URL, the date you fetched it, and whether the fetch succeeded. Never cite a page you didn't fetch in this session. Don't cite search-result snippets, your memory, or third-party coverage as sources. Product claims come from the product's own pages.

If a page fails (404, blocked, empty JS shell), note it and try one fallback: a different fetcher, the raw HTML, or the page's docs/README equivalent. If it still fails, list it under "Sources not reachable" and move on.

### 2. Pull out facts

Make a fact sheet before writing anything. One row per fact:

| # | Fact (in the source's words) | Source URL | Section / heading | Exact quote |

Capture:
- what the product is (the source's own one-line description);
- who it's for;
- the problem it names;
- 3–6 concrete things it does, or that a user sees it do;
- how you get started (install, sign-up, time-to-first-value only if the source states it);
- the primary CTA wording and destination;
- pricing or "free" language **only if stated**;
- the product's own terms: product name casing, feature names, nouns ("workspace", "handoff", "session").

Mark anything that looks like a mockup, placeholder, demo data or UI illustration (e.g. a counter in a screenshot) as **not a claim**. Don't quote it as a stat.

If two sources disagree (e.g. "5 minutes" on one page, "10 minutes" on another), keep both with their context and use the more specific one, or neither.

### 3. Pick the beats

Choose from the fact sheet only:

1. **Hook (0–3s):** the sharpest line on the site, usually the H1 or the problem in one breath.
2. **Problem (3–8s):** the pain in the source's words.
3. **Turn (≈8–11s):** what changes with the product, named by its real name.
4. **Demo beats (≈11–26s):** 2–3 concrete things the viewer could see happen on screen. Prefer actions over adjectives.
5. **CTA (last 3–4s):** the source's own CTA wording plus the domain.

Leave out anything you can't show or source, even if it sounds good.

### 4. Write

- Target **70–85 spoken words** for 30 seconds (about 2.3–2.8 words per second). Scale proportionally for other lengths.
- Allocate words per beat by its duration: roughly `seconds × 2.5` words. A 3-second hook is 6–8 words.
- Stay close to source wording. Light trimming and joining is fine; changing meaning isn't.
- Use the product's own terminology and name casing. Don't rename features.
- One idea per line. Short sentences. Write for the ear: no parentheses, no URLs read aloud except the final domain.
- On-screen / B-roll suggestions should show the thing the line describes (a UI moment, a command, a terminal, a diagram). Describe them from what the sources show or say; don't invent UI that isn't described.

### 5. Self-check (do this before returning)

Go through each item and fix anything that fails:

- [ ] Every VO line has a source URL **and** a quoted snippet copied from that page.
- [ ] Each quote actually appears on the cited page (re-check it against the fetched text; whitespace and curly-vs-straight quotes aside).
- [ ] No line claims more than its quote supports. No invented stats, customer names, logos, integrations, pricing, awards, or timelines.
- [ ] Unsupported lines are listed under "Dropped lines" with the reason, and are not in the script.
- [ ] Word count is in range: count the VO words and report the total.
- [ ] Time codes are continuous (each beat starts where the last ended), start at 0s, and end at the target length (±1s).
- [ ] Each beat's word count fits its duration (≤ ~3 words/second; flag any beat above that).
- [ ] Product name and terms match the source exactly.
- [ ] Fetch dates are listed for every source.

If the script fails the word count or pacing check, cut adjectives first, then whole demo beats. Never pad with unsourced claims to hit the minimum. A shorter honest script is better; say it's short and why.

## Output format

Return Markdown in this order:

```markdown
# <Product> — 30s launch video script

**Sources fetched:** <list of URLs, each with fetch date (YYYY-MM-DD) and status>
**Sources not reachable:** <list, or "none">
**VO word count:** <n> words · **Runtime:** <n>s · **Avg pace:** <n> words/s

| Time | Beat | VO line | On-screen / B-roll | Source |
|------|------|---------|--------------------|--------|
| 0–3s | Hook | "…" | … | <URL> (section): "exact quote" |
| 3–8s | Problem | "…" | … | <URL> (section): "exact quote" |
| … | … | … | … | … |
| 26–30s | CTA | "…" | … | <URL> (section): "exact quote" |

## VO only (read-through)
<the spoken lines as one paragraph, for timing a read-aloud>

## Dropped lines
- "<line>": <why: no source / mockup data / contradicts another page / too long>

## Self-check
- Citations: <n>/<n> lines cited, all quotes verified against fetched text
- Timing: <beats sum to Xs>, <word count>, <any beat over pace>
- Notes: <conflicts between sources, thin sources, assumptions>
```

A list of beats is fine instead of a table if the output surface renders tables badly, but each beat still needs all five fields: time, VO, on-screen, source URL, quote.

## Rules

- **Only sourced claims.** Every VO line maps to a quote on a page you fetched. If you can't cite it, drop it and list it under "Dropped lines".
- **No invented facts.** No made-up stats, user counts, customer names, testimonials, pricing, benchmarks, or "trusted by" lines. Numbers in UI mockups or sample data aren't stats.
- **Pricing only verbatim.** Say "free" or a price only if the source says it, and keep its qualifier ("free to start" isn't "free").
- **Backers, logos, awards** only if stated on a first-party page, and only if they earn their seconds.
- **Keep their words.** Product name, feature names and casing as the source writes them.
- **No outcome promises** the source doesn't make (rankings, revenue, "10x", guaranteed results).
- **Be explicit about gaps.** If something the user asked for isn't in the sources, say so rather than filling it in.

## Thin, missing or tricky sources

- **README-only repo:** the hook usually comes from the repo description or the README's first line; demo beats come from the quickstart/usage section (install command, a code snippet, the output). Good B-roll: the install command, the snippet running, the result. The CTA is usually "star / install / read the docs" plus the repo or package URL, whichever the README itself points to. Cite README sections by heading, e.g. `README.md#quickstart`.
- **Marketing site:** hook from the H1/hero, problem from the sub-headline or the first section, demo beats from feature sections, CTA from the primary button. Prefer the docs intro over the hero for precise technical claims.
- **JS-only or blocked page:** try raw HTML (`curl -L`), which often still contains the hero text and structured data, or a docs subdomain. Structured data (JSON-LD) is first-party but cite it as such.
- **Thin sources (fewer than ~5 usable facts):** write a shorter script (e.g. 15–20s) or fewer demo beats, and say why. Don't stretch.
- **No sources reachable:** don't write a script. Report what you tried and ask for a README, a different URL, or pasted copy.
- **User-pasted copy:** you can use it as a source; cite it as "user-provided text" with the quote.
- **Conflicting sources:** prefer the more specific and more recent page, and note the conflict in the self-check.
