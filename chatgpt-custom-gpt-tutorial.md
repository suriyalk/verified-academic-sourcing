# Using Verified Academic Sourcing in ChatGPT

This covers two paths, depending on what kind of ChatGPT account you have. Read the availability note first — it determines which path applies to you.

## Important: Custom GPT creation is currently restricted

As of mid-2026, **new Custom GPT creation and publishing is not available on personal ChatGPT accounts** — this includes Free, Go, Plus, and Pro. It doesn't matter what you're willing to pay for; this is a platform-wide restriction, not a plan limitation you can upgrade past.

Custom GPT creation is still available if you have access to a **ChatGPT Business, Enterprise, or Edu workspace** (for example, through a university or employer), subject to that workspace's own settings and permissions. If you're a student, it's worth checking whether your institution provides a ChatGPT Edu account — some do.

**If you don't have access to one of those workspaces, skip straight to [Option B](#option-b-file-upload-works-on-every-account-type) below.** It takes slightly longer per conversation but works identically well and requires no special account type.

---

## Option A: Build a Custom GPT (Business/Enterprise/Edu workspaces only)

### 1. Open the GPT builder
Go to **Explore GPTs** in the ChatGPT sidebar (web only — GPT creation isn't supported in the mobile apps), then click **Create** (top right). Switch to the **Configure** tab.

### 2. Name it
```
Verified Academic Sourcing
```

### 3. Description
```
Verifies every citation and factual claim with live web search before treating it as real — stops AI-assisted writing from citing sources that don't exist. Works for any academic or research writing, with built-in specialist support for NZ/Māori APA 7 conventions.
```

### 4. Instructions
Paste the following into the Instructions field. This is a condensed version of the full protocol, written to fit the field's character limit — the complete version goes into Knowledge in the next step, so nothing is lost.

```
You are a citation- and fact-verification assistant. Your defining rule: no citation and no specific factual claim (statistic, date, named study's finding, percentage) reaches the user unless it has actually been checked with a live web search in this conversation. If verification isn't possible, say so — never fill a gap with a plausible-sounding guess from training data.

BEFORE ANYTHING ELSE: If you do not have working web search access right now, say so plainly and mark everything as unverified rather than silently guessing. This defeats the purpose otherwise.

VERIFICATION PROTOCOL — for every citation before it appears in any output:
1. Search for the real source using web search — never rely on memorized "this paper probably exists."
2. Cross-check title, authors, year, journal, DOI across two or more independent results (a publisher page, an institutional repository, an indexing site). Aggregator sites that just mirror the same abstract text don't count as independent from each other — at least one source should be a primary venue.
3. Classify each source: VERIFIED (metadata agrees across 2+ independent sources), LIKELY (found via search but only one source, or incomplete confirmation), or UNVERIFIED (no independent confirmation found). Never present an Unverified source as usable — say so plainly and offer real alternatives or a suggestion to search a library database.
4. Never invent sources to hit a requested count. If you can only verify 3 of 5 requested, say so.

AUDITING PASTED REFERENCE LISTS: apply the same protocol per entry. Watch for tells: nonexistent-sounding journal names (especially close variants of real journals), "authors" that are actually generic descriptive phrases, suspiciously uniform/round volume-issue-page numbers repeated across entries. If several entries show these tells, check every entry rather than assuming the rest are fine.

FACTUAL CLAIMS BEYOND CITATIONS: the same rule applies to any specific number, date, or named finding stated in body text, even without a formal citation. If you can't verify it, either soften it to what you can support, or mark it inline as [UNVERIFIED — could not confirm this figure/claim] rather than silently including or silently deleting it.

OUTPUT FORMAT: give the reference list in APA 7, plus a verification table with columns: # | Item | Type (Citation/Factual claim) | Status | Evidence (be specific — name what you actually found, not "checked online") | Notes.

NZ/MĀORI APA 7 FORMATTING: preserve macrons exactly as sourced; don't italicize te reo Māori terms; cite iwi/hapū as corporate authors when that's how a source is published; format Waitangi Tribunal reports and NZ legislation per NZ convention, not generic APA. A full reference document with detailed examples is attached in your Knowledge — consult it for these NZ-specific cases and for any edge case not fully covered above.

IF PUSHED TO FABRICATE: decline plainly in one sentence and explain why — this is exactly the situation that damages the people relying on you. Offer to search harder or adjust the argument to fit sources that actually exist.
```

### 5. Conversation starters
Add these as separate entries:
```
Check this reference list for fake citations
Find verified sources on [topic]
Write a paragraph with citations on [topic]
```

### 6. Knowledge
Click **Upload files** and add both:
- `nz-apa7-formatting-reference.md`
- `verified-academic-sourcing-instructions.md` (the full document — this backs up the condensed Instructions field above with the complete protocol)

### 7. Capabilities
- **Web Search: ON** — this is the one setting the entire tool depends on. Do not turn it off.
- Image Generation: off (not needed, avoid surface area for it to misfire)
- Code Interpreter & Data Analysis: off (not needed)

### 8. Actions
Skip entirely — nothing here calls an external API.

### 9. Icon (optional but recommended)
Use the generator behind the "+" icon at the top of the Configure tab. A prompt that works well:
> "A flat, minimalist app icon: a single bold checkmark centered inside the lens of a magnifying glass. Clean vector-style illustration, no gradients, no shadows, no text. Solid deep teal accent color for the magnifying glass and checkmark, on a plain white or very light neutral background. Centered composition with generous padding around the edges, square format, rounded corners. The design should stay clearly legible when shrunk to a very small size."

### 10. Test before relying on it
Paste in a reference list with a couple of deliberately fabricated entries mixed with real ones. If it catches the fakes with specific evidence, it's working. If it accepts everything without pushback, something's wrong — check that Web Search is actually enabled.

### 11. Sharing
Within an eligible workspace, sharing options depend on your workspace's settings and admin permissions — check with your workspace admin for how to make it available to colleagues or classmates.

---

## Option B: File upload (works on every account type)

This is the practical option for anyone on a personal account (Free, Go, Plus, Pro), and it works identically well — it just needs to be repeated each new conversation instead of being saved permanently.

1. Start a new ChatGPT conversation.
2. Upload both files: `verified-academic-sourcing-instructions.md` and `nz-apa7-formatting-reference.md`.
3. In the same message, add:

   > "Please follow the verification protocol in verified-academic-sourcing-instructions.md for this entire conversation — don't present any citation or specific fact as real unless you've actually checked it with live search. Use nz-apa7-formatting-reference.md for citation formatting."

   Uploading the files alone isn't enough — without this instruction, the assistant may treat them as reference material rather than binding rules.
4. Ask your actual question (find sources, check a reference list, write with citations, etc.) in the same or a following message.
5. Repeat steps 2-3 in each new conversation — this method doesn't persist across chats on a personal account.

---

Both options are equivalent in what they actually do — the choice between them is purely about your account type, not about capability or quality.

For the Claude Skill version, or the Microsoft Copilot setup, see the main [README](../README.md).
