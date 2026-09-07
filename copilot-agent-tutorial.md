# Using Verified Academic Sourcing as a Microsoft Copilot Agent

This covers building the protocol as a custom agent in Microsoft 365 Copilot's Agent Builder, so it's available on demand without re-uploading files each conversation.

## Before you start

Agent creation requires a Microsoft 365 Copilot license through a work or school account — this isn't available on personal/consumer Copilot. If you're a student, check whether your institution provides a Copilot Edu license; many do.

## 1. Open Agent Builder

In Microsoft 365 Copilot Chat, go to **Agents** in the left pane and choose **New agent**. Skip the natural-language description step and go to manual configuration (**Configure** tab) if you already know what you want in each field.

## 2. Name and describe it

**Name:**
```
Verified Academic Sourcing
```

**Description:**
```
Verifies every citation and factual claim with live web search before treating it as real — stops AI-assisted writing from citing sources that don't exist. Works for any academic or research writing, with built-in specialist support for NZ/Māori APA 7 conventions.
```

## 3. Paste the instructions

Use the same condensed instructions block used for the ChatGPT Custom GPT (see `chatgpt-custom-gpt-tutorial.md` in this repo for the full text) — it's already proven to fit a constrained instructions field.

## 4. Set up Knowledge and Web search

This is the step most likely to trip people up, so a few notes from real testing:

- **Turn the Web search toggle ON.** This is the setting the entire protocol depends on.
- Under **Add knowledge**, adding a link (e.g., `https://github.com/suriyalk/verified-academic-sourcing`) alongside Web search worked correctly in testing — the agent still searched broadly across the open web (Crossref, Google Scholar, Scopus, publisher pages, etc.) rather than being restricted to just that one link. Microsoft's own documentation describes website links as narrowing search scope, which raised a concern during setup — but real testing against a large reference list showed genuine broad verification still happening, so this combination is confirmed working in practice.
- **SharePoint/OneDrive personal sharing links are unreliable here** — they often fail with a "URL path is too deep" error due to long encoded paths and query strings. If you hit that, use a public GitHub raw URL instead (e.g., `https://raw.githubusercontent.com/suriyalk/verified-academic-sourcing/main/universal/verified-academic-sourcing-instructions.md`), which has neither issue.
- If a direct file-upload option is available on your Configure tab (separate from the "Enter a link" flow), that's also a valid way to add the two `.md` files from `universal/` as knowledge sources.

## 5. Test before trusting it

Don't skip this. Paste in a real reference list — ideally a large one (20+ entries) mixing genuine and fabricated sources — and check that:
- It gives specific evidence per source (which databases it checked, not just "looks fine")
- It correctly refuses to treat Unverified sources as real
- It won't write an essay citing unverified sources as fact, even when asked directly, but offers to write around the general topic instead or help find real sources

This exact test (a 20-reference list with several fabricated entries) was run successfully — the agent correctly flagged multiple unverifiable references with specific per-source evidence, identified the common warning signs of fabricated reference lists (plausible-but-unverifiable journal names, unusually uniform volume/issue/page formatting, generic descriptive titles), and declined to write the requested essay treating them as real sources — offering to either audit the full list or replace them with real, verifiable sources instead.

## 6. Publish and share

Share according to your workspace's permissions — typically through the Agents panel, either with specific colleagues, a team, or your wider organization if your admin allows it.

---

For the Claude Skill version or the ChatGPT Custom GPT, see the main [README](README.md) and [chatgpt-custom-gpt-tutorial.md](chatgpt-custom-gpt-tutorial.md).
