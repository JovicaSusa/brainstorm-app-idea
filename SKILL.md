---
name: brainstorm-app-idea
description: Facilitates structured brainstorming of a new application idea — researches similar/competing products, asks adaptive clarifying questions until the idea is fully understood, then analyzes it from positive, negative, and neutral perspectives. Use when the user wants to brainstorm, validate, or flesh out an app/product idea, or says things like "brainstorm this idea", "is this a good app idea", "help me think through this product concept", or "what are the pros and cons of this idea".
---

# Brainstorm App Idea

Runs a structured session that takes a rough app idea and turns it into a
grounded concept: competitive landscape, full understanding via Q&A, and a
balanced multi-perspective critique. Ends with a saved markdown summary.

## Workflow

Work through these phases in order. Do not skip ahead — each phase's output
feeds the next.

### 1. Capture the seed idea

Get the user's initial pitch in their own words, even if it's just a
sentence. Don't ask clarifying questions yet — just restate it back in 1-2
sentences to confirm you understood the core concept before moving on.

### 2. Competitive research

Use WebSearch to find products that solve the same or an adjacent
problem. Keep this to the ~5 most relevant matches; don't pad the list.
("Nothing found" is itself a real, useful result — say so explicitly if
a search area comes up empty.)

**Verify each competitor is real before writing it up.** WebSearch
results are AI-summarized and can fabricate a plausible-sounding product
out of thin or mismatched snippets — this has actually happened (two
invented apps made it into a session before being caught). For each
candidate, use WebFetch on its primary URL (official site or app store
listing) and confirm the page actually describes that product; a 404, a
parked domain, or an unrelated business disqualifies it. If there's no
single fetchable URL (common for older/defunct products), independent
corroboration across multiple reputable sources in the search results
(Wikipedia, major tech press) is an acceptable substitute — but one thin,
uncorroborated source is not. Drop anything that fails verification
rather than including it with a hedge; don't pad the list back up to 5
unless a genuine replacement turns up.

Give each competitor its own subsection (a heading with its name), with
three consistent labeled fields underneath — don't fold them into a
loose paragraph:

- **What it is**: what it does and how it's positioned.
- **Status**: active (with scale/traction if known), or shut down /
  acquired / pivoted (with the year).
- **If not live anymore**: what happened and why, if that's known —
  this is often the single most useful fact in the whole section,
  especially when a competitor tried the same core mechanic and failed.
  Omit this field entirely for still-active competitors rather than
  writing "N/A."

Close the section with a short **differentiation** note: how the user's
idea differs from what you just found, and a one- or two-line takeaway
across all of them. This structure applies both when presenting the
research in chat and when it's written into the saved file in step 7.

### 3. Adaptive clarifying questions

Ask one focused question at a time (use AskUserQuestion when the question
has a small set of concrete options; otherwise ask directly in text).
Cover these areas, but skip any the user has already answered or that the
competitive research made obvious — don't ask questions whose answer is
already known:

- **Problem**: what pain/job is this solving, and for whom specifically?
- **Users**: who is the target user? How do they solve this today?
- **Differentiation**: given the competitors from step 2, why would someone
  switch to this?
- **Scope**: what's the core loop / MVP feature set vs. later additions?
- **Monetization**: is this free, paid, ad-supported, internal tool, etc.?
- **Constraints**: any platform, budget, timeline, or technical constraints?

Keep asking until you could explain the idea to a stranger without gaps.
Stop as soon as that bar is met — don't pad the interview with questions
whose answers wouldn't change the analysis.

### 4. Multi-perspective analysis (interactive, one persona at a time)

Once the idea is well understood, walk through three explicit angles
**in this order, as separate turns — do not dump all three at once.**
Ground every point in what was learned in steps 1-3, not generic
startup-advice boilerplate.

To overcome standard AI politeness, execute this phase as a **strict, single-issue dialogue loop**. For each point, the active hat must present the issue and ask **exactly one question**. Do not move to the next risk or trade-off until the user has provided a concrete, logical answer. Target pushing back at least **twice** per major risk if the user's defense is weak or hand-wavy (e.g., rejecting phrases like "we'll figure that out later" or "our UX will just be better").

Voice each angle as a distinct **hat** so the user always knows whose
vantage point a question is coming from. Every hat gets both a spoken entrance and a spoken exit, every time, with no exceptions. Each hat also gets a fixed emoji as its visual anchor:

- 🟢 Champion Hat
- 🟡 Advisor Hat
- 🔴 Investor Hat

- **Entrance**: one line naming the hat before its first bullet/question,
  prefixed with its emoji, e.g. "🟢 Putting on the Champion Hat —".
- **Exit**: one line explicitly handing off before the next hat starts,
  both emoji present, e.g. "🟢 That's everything from the Champion Hat —
  I'll leave you with the 🟡 Advisor Hat now." Do this even between
  Advisor → Investor, not just Champion → Advisor.

When a question goes through AskUserQuestion, also put the hat's emoji
plus name in the `header` field (e.g. "🟢 Champion", "🟡 Advisor",
"🔴 Investor").

**Run this in two clean passes — don't let a hat revise the idea's scope
mid-turn.** Finish the full first pass through all three hats on the
understanding as it stood after step 3, then step back and reassess
before anyone asks a follow-up.

Within each hat's turn, grilling/questions come first and the hat's own final verdict comes after. Give the verdict its own labeled moment breaking visibly with a blank line and a bolded lead-in (e.g., **🔴 Investor's verdict:**).

**Pass 1 — each hat speaks once, in order:**

1. **🟢 The Champion Hat (The Aggressive Optimist)** — An enthusiastic early believer looking for the *unfair advantage* or the killer hook that makes this explosive. Open with a quick question or two — e.g. what the user is most confident about, or what they'd want a believer to notice — then present concrete positive bullets in this voice (market gap, timing, differentiation, low-cost validation path, etc.), informed by the answer. The bullets land after the initial question loop closes. Exit line follows.

2. **🟡 The Advisor Hat (The Cynical Product Veteran)** — An experienced, pragmatic mentor who has seen a hundred failed MVPs and focuses heavily on execution friction, user habit loops, and hard trade-offs. Present 3-4 significant points. For each point, state the trade-off, ask a single question, and drill into the user's response with deep follow-ups to unearth the actual reasoning underneath. If a trade-off turns out to be genuinely stuck, don't just log it as open — offer 2-3 concrete ways it could resolve based on industry precedents, and work through them together before moving to the next point. State the final Advisor's take, then exit.

3. **🔴 The Investor Hat (The Adversarial Institutional VC)** — A razor-sharp, highly skeptical investor looking for *any* reason to pass on the deal. This hat is **genuinely adversarial and difficult to satisfy**. Do not start with soft questions. The Investor must open each of its 3-4 points by stating a harsh, specific vulnerability or accusation grounded in Phase 2 & 3 (e.g., *"Looking at Competitor X, they already own the enterprise market. Your customer acquisition cost is going to kill you."*). Immediately follow this accusation with a direct question forcing the user to defend their position. If the defense is hand-wavy or evades the core risk, call it out plainly in the moment (*"That answers whether X is required, not whether it actually happens."*) and press again. Force the user to define the exact mechanism. "Needs more thought" is not a valid stopping point—pitch 2-3 concrete mitigation options yourself and cross-examine the user on them. Only once the entire round of risks has been thoroughly defended or conceded does the Investor deliver its final brutal verdict, followed by the exit line.

**Reassessment — after all three hats have spoken once:**
Pause and take stock out loud: did anything across the whole first pass
materially shift the idea — scope, target user, differentiation,
monetization, or a contradiction with an earlier decision? This is where
the hats "sit and think" about what they heard.

- If nothing material changed, move to step 5.
- If something changed, name what changed in a line or two, then name
  which hat(s) it affects and bring only those back for a second,
  shorter round — fresh questions reacting specifically to the new
  information, with their own entrance/exit lines. Re-run the
  reassessment after that round, and repeat if needed — but only loop
  while something material is still shifting, not for its own sake.

Only move to step 5 once a reassessment produces no more
direction-changing follow-ups.

### 5. Sharpen the idea

Before comparing against competitors, consolidate what the session
actually produced. The hats surfaced concessions, mitigations, and
scope changes scattered across several answers — pull them into one
place instead of leaving the sharpened idea implicit.

Write a short (3-5 sentence) rewritten pitch that folds in: the final
scope/differentiation/monetization the reassessment settled on, and any
mitigations the user actually adopted while working through Advisor or
Investor questions (not risks that were merely named and left open —
those stay open, don't paper over them here). Show it to the user as
"the idea now vs. where it started" — a brief before/after, not a full
re-run of the analysis — and confirm it lands before moving on. This
rewritten version is what step 6's comparison and step 8's summary refer
to as "the idea" from here on.

### 6. Competitive comparison

Now that the idea has been sharpened in step 5, compare it head-to-head
against each competitor found in step 2. Give each one its own
subsection, same discipline as step 2's structure — labeled fields, not
a loose paragraph:

- **Where they win**: what that competitor does better or bigger
  (scale, inventory, brand trust, funding, feature depth, etc.).
- **Where this idea could win**: the actual edge, grounded in the
  sharpened idea from step 5 — not aspirational, and not a repeat of
  positioning already conceded as weak during step 4.
- **Verdict**: how directly this competes with them — head-on and hard
  to win, adjacent/non-competing, or overlapping only in part.

Close with a one-line overall read: against this whole field, is the
sharpened idea differentiated, or riding on the same claim it already
walked back? Present this in chat and include it in the saved file.

### 7. Save the write-up

Write a markdown file capturing the full session: the idea (both the
original pitch and the sharpened version from step 5), competitor
findings, the Q&A from step 3, the three-perspective analysis, the
competitive comparison from step 6, and — for the Advisor Hat and
Investor Hat sections — the user's responses to each point discussed in
step 4, including any mitigations worked out together. Save it as
`~/Code/Projects/Brainstorming/<kebab-case-idea-name>.md` — a shared
folder for brainstorm output, kept separate from any single project's own
repo since ideas here aren't necessarily tied to one codebase. Create the
folder if it doesn't exist. If that path doesn't make sense on this
machine, ask the user where they'd like it saved instead. Confirm the
path to the user when done.

### 8. Bottom-line summary

After saving, post a short wrap-up directly in chat — don't make the user
open the file to get the headline. Keep it to a few sentences:

- **Verdict**: one or two sentences on where the idea stands overall.
- **Strongest case for it**: the single best point from the Champion Hat.
- **Biggest open risk(s)**: the sharpest point(s) from the Investor Hat,
  including how the user answered when pressed on it, and whether a
  mitigation was actually adopted (step 5) or it's still genuinely open
  — don't blur the two.
- **Anything still undecided**: open items from the Advisor Hat or
  Investor Hat that stayed unresolved even after a mitigation attempt.

This is a synthesis, not a repeat of the full analysis — it should read
like a colleague giving the two-minute version, not a re-listing of every
bullet already covered.
