---
name: verified-academic-sourcing
description: Use any time a student asks Claude to find sources, suggest citations, build/expand a reference list or bibliography, write a literature review, add citations to a paper, or check/audit citations already in a document. Also trigger whenever Claude is about to write a DOI, an author/year citation, a reference entry, OR a specific factual claim (a statistic, date, named study's finding, percentage) inside academic work — even inside a larger task like a proposal, thesis chapter, essay, or report. Stops hallucinated citations and hallucinated facts (fake DOIs, invented papers, wrong authors, made-up statistics) — a real academic integrity risk for NZ undergrad/postgrad students — and formats references in APA 7 including NZ/Māori conventions (macrons, iwi/hapū as corporate author, Waitangi Tribunal reports, NZ legislation, Stats NZ/govt reports). Don't skip this just because a citation or fact "seems obviously real" — that confidence is how fabrications end up in student work.
metadata:
  author: Nadeeshan Suriya
  linkedin: https://www.linkedin.com/in/nadeeshansuriya/
  created: "2026-09-07"
---

# Verified Academic Sourcing for NZ Students

*Created by Nadeeshan Suriya — https://www.linkedin.com/in/nadeeshansuriya/*

## Why this skill exists

Language models are fluent at producing citations and facts that *look* completely real — correct journal names, plausible authors, well-formed DOIs, precise-sounding statistics — while the paper doesn't exist or the number was never in any source. For a student, this isn't a cosmetic error. A fabricated citation or a made-up statistic in a thesis, proposal, or assignment reads as academic dishonesty even when the student had no idea Claude made it up. The whole point of this skill is to make that failure mode structurally impossible: **no citation and no specific factual claim reaches the student without being checked in this conversation, using a live tool call.**

Treat this as a hard constraint, not a best-effort. If verification isn't possible, say so — don't fill the gap with a plausible guess.

## The verification protocol

For every source before it appears in any output (a reference list, an in-text citation, an answer to "find me sources on X"):

1. **Search for the actual source.** Use web_search (or web_search_fast first, escalating to web_search if thin) with the real title/author/topic — never rely on training-data memory of "a paper that probably exists." If you're recalling a specific paper from memory rather than from a search you just ran in this turn, that recall is not sufficient — search to confirm it.
2. **Cross-check the DOI and metadata across independent sources rather than "resolving" a constructed URL.** web_fetch can only open a URL that actually appeared in a search result — it will reject a `https://doi.org/<DOI>` or Crossref API URL you type yourself, since that's a constructed URL, not one returned by the tool. So don't rely on directly fetching the DOI. Instead: run the search, and look at whether the *same* title, authors, year, journal, volume/issue, and DOI appear consistently across two or more independent results (a publisher page, an institutional repository, an indexing/aggregator site, a citing paper's reference list). Independent agreement across multiple sources on every detail is strong evidence the source is real — often stronger than a single successful resolve, since it also confirms the paper is genuinely discoverable, not just present in one database. If a fetchable link to the publisher or a repository copy does appear directly in your search results, fetch it for full confirmation — but don't block on that if cross-source agreement is already solid.

   **Watch for mirrors, not independence.** Aggregator sites (PapersWithCode, DeepAI, and similar) frequently just re-publish the same abstract text scraped from one primary source. Three hits that all echo identical wording are not three independent confirmations — they may be one source copied three times. At least one of your corroborating sources should be a primary venue (the publisher, conference proceedings, ACL/IEEE/official archive, an institutional repository hosting the actual paper) rather than all being downstream aggregators of the same text.
3. **Cross-check every detail you plan to state**: author names, year, journal/publisher, volume/issue, page range. If the source is real but you can't confirm a specific detail (e.g., exact page range), say so explicitly rather than estimating it.
4. **Classify and label each source:**
   - **Verified** — metadata (title, authors, year, journal, DOI) agrees across two or more independent sources found via search, or a fetched publisher/repository page confirms it directly.
   - **Likely** — found via search, details are consistent, but only from a single source or one that doesn't fully confirm every detail (common for older or non-DOI'd sources, books, government reports, legislation).
   - **Unverified** — you could not find independent confirmation this source exists as described. Never include an Unverified source in a final reference list as if it were usable. Say plainly that you couldn't confirm it and offer either close real matches you did find, or a suggestion to search Google Scholar / the university library database directly.
5. **Never invent to fill a gap.** If a student needs "5 sources on X" and you can only verify 3, say that — don't manufacture 2 more to hit the number. Offer to search harder, broaden the terms, or explain that the literature may be thin on that specific angle.

Budget: at least one search per proposed source, more when results are ambiguous or you find multiple similarly-named papers. Don't skip verification to save time — a wrong citation costs the student far more than a slow response does.

## Auditing an existing reference list

Students will often paste a bibliography (their own draft, or output from another tool) and ask "check these" or "are these real." Apply the exact same protocol per entry, then report back a per-entry verdict. This is one of the highest-value uses of this skill — it's how hallucinated citations from other sessions or other tools get caught before submission. Don't soften an Unverified verdict to spare feelings; a student needs to know before their supervisor does.

**Common tells worth flagging early** (these guide where to look closely — they never substitute for the actual search-based check, since some real, obscure sources can look unusual too):
- A journal name that sounds plausible but doesn't exist, especially when it closely resembles a real journal's name with a word added or changed (e.g., a fabricated "...and Technology" variant of a real journal title).
- "Authors" that are actually generic descriptive phrases rather than real people's names.
- Suspiciously clean, round, or uniform volume/issue/page numbers repeated across many entries in the same list.
- Ordinary, generic-sounding author names paired with a topic so specific that a real paper on it would be easy to find, yet nothing turns up.

If several entries in one list show these tells, treat the whole list as suspect and check every entry rather than assuming the rest are fine because the first few looked plausible.

## Checking factual claims, not just formal citations

Hallucination isn't limited to reference-list entries. It shows up just as often as a specific fact stated in the body of the writing — "a 2021 study found a 47% reduction in...", "New Zealand's uptake rate is currently around X%", "the framework was first proposed in [year] by [person]." These read as confident, specific, and checkable, which is exactly why a wrong one is dangerous: nobody double-checks something stated that precisely.

Whenever you are drafting or reviewing academic writing (an essay, report, thesis chapter, proposal) and you are about to state — or find already stated — a specific number, date, percentage, named finding, or attributed claim, verify it the same way you verify a citation: search for the actual source, and only keep the specific figure if you can find it stated in something you can point to. If you can't verify a specific figure but the general point is sound, either soften it to what you can actually support (e.g., "a substantial reduction" instead of an invented "47%") or mark it clearly rather than leaving a silently unverified number sitting in the text.

**Flagging convention:** when a factual claim can't be verified but the student would want to know rather than have it silently removed, mark it inline as `[UNVERIFIED — could not confirm this figure/claim]` directly in the draft text, right after the claim. This keeps the student's argument intact while making the gap visible — their call whether to cut it, soften it, or go find the source themselves. Never leave an unverified specific claim unmarked, and never delete a claim the student clearly wanted without telling them you removed it and why.

## NZ / APA 7 formatting

Once a source is verified, format it in APA 7. New Zealand academic writing has several conventions that generic APA guidance gets wrong or omits — read `references/nz-apa7-formatting.md` for the details (macrons, iwi/hapū as corporate author, Waitangi Tribunal reports, NZ legislation, Stats NZ and government reports, and how individual NZ universities' style guides sometimes diverge from vanilla APA 7). Read it whenever the citation involves Māori names/terms, government or legislative sources, or when the student names their institution and asks for that institution's specific style.

## Output format

When producing or auditing a reference list (and whenever the task surfaced factual claims worth flagging), give:

1. The reference list itself, correctly formatted in APA 7 (in-text citations too, if requested), with any inline `[UNVERIFIED — ...]` markers left in the draft text where relevant.
2. A verification table underneath, one row per citation (and, where relevant, per flagged factual claim), with these columns:

   | # | Item (short form) | Type | Status | Evidence | Notes |
   |---|---|---|---|---|---|

   - **Item**: short author/year or a few words identifying the claim — not the full reference.
   - **Type**: Citation or Factual claim.
   - **Status**: Verified / Likely / Unverified.
   - **Evidence**: what actually backs the status — be specific and honest about strength, e.g. "DOI + metadata agree across 4 independent repository records", "single publisher listing, no second source found", "no matching source found across 3 search attempts". Don't write vague filler like "checked online" — name what you found.
   - **Notes**: anything the student should know before submitting — an unconfirmed detail (e.g., page range not confirmed), a figure that varied between sources, or a suggestion (e.g., "try Google Scholar directly for the exact page numbers").

This table is not optional decoration — it's what lets the student sanity-check everything in ten seconds before submitting, and it's the record that shows *how* each item was checked, not just that it was. Keep entries compact but honest about evidence strength; a thin "Likely" is more useful to the student than an inflated "Verified."

## If the student pushes back

If a student asks you to "just make one up that fits" or to keep a source you've flagged as Unverified anyway, decline plainly and explain why in one sentence — this is exactly the situation that damages students, and a quick compliant answer now is not a kindness. Offer to search harder or adjust the argument to fit sources that do exist instead.

---

*A model-agnostic version of this protocol (for use as custom instructions in ChatGPT, Gemini, or any other assistant with web search) is maintained as a companion document by the same author, since the `.skill` format itself only loads in Claude.*
