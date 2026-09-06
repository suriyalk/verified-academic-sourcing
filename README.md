# Verified Academic Sourcing

A citation- and fact-verification protocol built to stop AI-assisted academic writing from producing hallucinated references — fake DOIs, invented papers, wrong authors, made-up statistics — before they end up in a student's essay, proposal, or thesis. Built with a focus on undergraduate and postgraduate students in New Zealand, including APA 7 formatting for NZ- and Māori-specific source types.

**Author:** Nadeeshan Suriya — [linkedin.com/in/nadeeshansuriya](https://www.linkedin.com/in/nadeeshansuriya/)

## Why this exists

Language models are fluent at producing citations that *look* completely real — correct journal names, plausible authors, well-formed DOIs — while the paper doesn't exist or the details are wrong. A fabricated citation in a thesis or assignment reads as academic dishonesty even when the student had no idea the AI made it up. This protocol makes that failure mode structurally harder to hit: no citation or specific factual claim is presented as real unless it's been checked with a live search in that conversation, and anything that can't be confirmed is flagged rather than smoothed over.

## What's in this repo

- **`claude-skill/`** — the native Claude Skill (`SKILL.md` + a Māori/NZ APA 7 reference file). Uses Claude's own search and fetch tools directly. This is the highest-fidelity version, built and tested first.
- **`universal/`** — a model-agnostic instructions document with the same protocol, written for use as custom instructions/a system prompt in ChatGPT, Gemini, or any other assistant with real web search. Includes an explicit check that makes the model admit it if live search isn't available, rather than quietly guessing — since without Claude's native tool integration, that's the main way a portable version could otherwise lose its teeth.

The two versions are kept separately rather than merged into one lowest-common-denominator file, so neither loses quality for the other's sake.

## Installing the Claude Skill

1. Zip the `claude-skill/` folder (or its contents) into a `.skill` file, or upload it as-is wherever your Claude surface accepts skill folders.
2. Once installed, it triggers automatically whenever you ask Claude to find sources, build a reference list, check an existing bibliography, or write academic content that includes specific facts or figures.

## Using the universal version (ChatGPT, Gemini, etc.)

See the "Setup notes by platform" section at the end of `universal/verified-academic-sourcing-instructions.md` for exact steps — it covers Custom GPTs, Gemini Gems, plain ChatGPT sessions, and generic API system prompts.

## What it does

- Verifies every citation via live search before including it, cross-checking metadata across independent sources rather than trusting a single hit or a self-constructed DOI link
- Classifies each source as **Verified**, **Likely**, or **Unverified** — and never presents an Unverified source as usable
- Extends the same check to specific factual claims embedded in writing (a statistic, a date, a named finding), flagging anything unconfirmed inline as `[UNVERIFIED — ...]` instead of silently including or silently dropping it
- Audits pasted-in reference lists for hallucinated entries, using known tells (nonexistent journal names, "authors" that are actually generic phrases, suspiciously uniform volume/page numbers) to guide closer scrutiny
- Applies APA 7 with NZ/Māori-specific conventions: macrons, iwi/hapū as corporate author, Waitangi Tribunal reports, NZ legislation, Stats NZ/government reports
- Outputs a verification table (item, type, status, evidence, notes) alongside every reference list so the result can be sanity-checked in seconds

## Tested against

- A list of 20 real Harvard-style references — correctly verified genuine, well-known papers with specific cross-source evidence rather than a bare "looks fine."
- A list of 20 deliberately fabricated references — caught the fabrication pattern (nonexistent journals, generic-phrase "authors," uniform page numbers) and refused to write the essay citing them as real, offering real alternatives instead.
- A direct head-to-head against the same prompt without the skill: the unguarded version fabricated a citation that wasn't even present in the original reference list it was given.

## License

MIT — see `LICENSE`.
