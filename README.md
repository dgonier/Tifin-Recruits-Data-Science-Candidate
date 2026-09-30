# Northwind Wealth Partners: Insight Engine Take-Home

**Time: 2–3 hours.** Please stop at ~3.5 hours even if you're not done. We'll ask what
you'd do next.

## Context

TIFIN builds AI products for wealth management. One of our pilot clients is
**Northwind Wealth Partners** (fictional), a registered investment adviser (RIA):

- ~2,200 client households, ~$4.2B in assets under management (AUM)
- 30 advisors across 5 offices
- Client assets are held at three custodians (Schwab, Fidelity, Pershing); Northwind
  manages them and bills an advisory fee as a % of assets

Northwind sent us three years of raw exports from their custodians and CRM (`data/`,
described in [`data_dictionary.md`](data_dictionary.md)), plus an email thread from their
leadership: [`stakeholder_thread.md`](stakeholder_thread.md). **Read the thread first.**
It's short, and the asks in it conflict on purpose.

It is **Monday, January 5, 2026**. The data runs through December 31, 2025.

## The task

Northwind wants a system that turns their data into **insights that people act on**,
every week.

**Pick one audience**: advisors *or* leadership. Build a small pipeline that runs on the
provided data and produces **the one artifact that audience would receive this Monday**.
For advisors that could be a weekly digest; for leadership, a one-page brief. The format
is up to you.

You decide what counts as an "insight", what makes the cut and what you leave out.
There is no single correct answer.

## Constraints

1. **Attention.** An advisor reads at most **~5 items a week**. Leadership reads **one
   page**. Anything beyond that gets the whole system ignored.
2. **Traceability.** Compliance must be able to trace every statement back to the
   records that support it.
3. **Privacy.** CRM notes and client names may not be sent to a third-party API as-is.
   Using an LLM is optional; if you do, handle this (a stub or mock is fine).
4. **Data is as delivered.** Nobody has checked it.

## Deliverables

1. **Code** (repo or zip) with a `README` giving **one command** to run it end to end.

2. **One useful output**: the artifact your pipeline produced for Monday, Jan 5, 2026.
   It should be something the recipient could act on today, not a demo of the pipeline.

3. **`DESIGN.md` (max 1 page)**, about what you *built*:
   - Who it's for, and the decision it helps them make.
   - How items make the cut and in what order.
   - How you know it's right: what you checked, and what you'd trust least.
   - A few bullets on how you used AI tools, including one place they were wrong or
     misleading.

4. **`ROADMAP.md` (max 2 pages)**, about what you'd build *next*, on a longer horizon.
   You built one artifact for one audience. Tell us what else you'd build and in what order,
   for example:
   - Artifacts for the other stakeholders in the thread, and which of them you'd deliberately
     *not* serve, and why.
   - What you'd need to know whether it works once it's live (feedback loops, metrics,
     experiments).
   - **Scale:** the system runs weekly for ~400 firms (~1.5M households) on a ~$2,000/week
     LLM budget. What changes in the architecture? Include a back-of-envelope estimate.
   - What you'd ask Northwind (or the next firm) for that isn't in this data.
   - Rough sequencing: what would you ship in weeks, months, and a quarter or more?

   Don't build any of this. We want to see how you think about the bigger system and what
   comes first.

A narrow thing that is right and well reasoned beats a broad thing that is merely
plausible. The roadmap is where breadth belongs.

## On using AI

AI use is expected and encouraged, including coding agents. What we evaluate is the part
they can't do for you: framing, trade-offs, knowing when an output is wrong, and building
something you understand well enough to change on the spot.

## After you submit

A 60-minute session:

- **~10 min**: you walk us through what you built and why.
- **~35 min**: we hand you **new data (Q1 2026)** to run through your pipeline and change a
  constraint or two. Expect to modify your own code live, using whatever tools you normally use.
- **~15 min**: your questions for us.

## How we evaluate (high level)

- **Framing and judgment:** who you built for and what you prioritized.
- **Trust:** in the data, and in what your output claims.
- **Usefulness:** would the recipient act on your output on Monday?
- **Roadmap:** sequencing, scale and cost thinking, and how you'd know it works.
- **Ownership:** how well you reason about and change your work in the live session.

If anything is ambiguous, make a reasonable assumption and write it down.
