# Development Notes

Working notes for the VUIM Clinic Attendance & Makeup Resource Hub. Raw material for a future case study.

## Context

**Client**: Dr. Yaron Cohen, Director of Clinical Education at VUIM.
**Request**: "Use our design resources to create the HTMLs into visually accessible resources that students and supervisors can reference."
**Assumption in the request**: that the CTLE would do HTML conversion. CTLE (one director + one recent hire) doesn't do web production. Reframed as an ID/LXD opportunity.
**Timeline**: Spring quarter already in progress; Yaron wanted to send out announcement reminders soon.

## Source material

Five files, handed over as a package:

1. Student Attendance & Makeup Guide (PDF, 7 pages)
2. Supervisor Attendance & Makeup Operations Guide (PDF, 6 pages)
3. Staff Makeup Scheduling SOP (PDF, 5 pages)
4. Student Absence-to-Makeup Checklist (HTML, quick-reference)
5. Supervisor Attendance & Makeup Decision Flow (HTML, quick-reference)

Content was thorough. Structure was fragmented across roles and formats.

## Problem analysis

The source material had three design problems, regardless of how polished each individual file was:

1. **Role-overlap without differentiation.** Students, supervisors, and staff each needed different slices of the same policy. In PDFs they had to read through someone else's content to find their own.
2. **No deep-link surface.** Yaron's stated use case was early-quarter announcement emails. PDFs and bare HTMLs can't deep-link to a specific rule, so every reminder had to restate the rule in full.
3. **Performance-support vs textbook mismatch.** Someone opening this mid-clinic shift needs "what do I do right now." PDFs present everything with equal weight.

Yaron's "Common Mistakes" section in the Student Guide was effectively free user-research data. Every mistake listed there was a failure to find the relevant rule at the moment of decision.

## Design decisions

**Role-first IA.** Three separate entry points (Student / Supervisor / Staff) instead of one combined site. Audiences don't overlap operationally; mixing them creates noise.

**Three-layer pattern per role page.**
- Layer 1 (hero): Yaron's existing quick-reference visuals, preserved. These are the "what do I do" layer.
- Layer 2 (full guide): Complete policy content from the corresponding PDF, rendered as semantic HTML with a sticky TOC.
- Layer 3 (scenario FAQ, student only): Yaron's "Common Mistakes" reframed as searchable scenarios.

**Anchor-per-rule.** Every section, sub-rule, and FAQ item got a unique anchor ID (129 total across the site). This turns the site into an announcement-email toolkit — reminders can link directly to a specific rule instead of restating it.

**Print-optimized.** Each role page has a print button that hides nav/TOC, expands all accordions, and outputs a clean handout. Staff may want to pin a card to the clinic wall.

**Preserve operational detail verbatim.** Minute thresholds, escalation paths, sanction specifics, form names (LCS, Populi, Clinical Diary, DCE Office) — none of these were paraphrased. When the agent I was working with suggested 4 items in one section where the source had 3, I caught that and forced it to match the source.

## Workflow

- Agentic build via Claude Code running locally, phased: content extraction → verification pass → page build → deploy.
- Required an explicit audit pass after Phase 1 extraction before letting the agent build pages. This caught several details that would have gone missing.
- Scrollspy off-by-one bug discovered in user testing (TOC highlight landed on the previous section). Root cause: scroll threshold didn't account for stacked scroll-padding-top. Fixed with IntersectionObserver using rootMargin + explicit setActive on click + hash walk-up for deep-linked sub-anchors.
- Deploy blocked in-agent by Claude Code sandbox (api.vercel.com POST not in egress allowlist). Finished deploy via CLI from my own terminal.

## Stack

- Vanilla HTML, Tailwind via CDN (matches source HTML files, no build step).
- Lucide icons via CDN.
- GitHub → Vercel auto-deploy pipeline.
- Source files kept in repo under /source/; internal extraction notes excluded from production via .vercelignore.

## What I'd add in v2

- Analytics (Plausible or Umami) to see which sections get hit, which deep links land most. Data for a next iteration.
- Tardy/Absence calculator: input arrival time → automatic Tardy / Absence-may-remain / Absence-must-leave verdict. Converts a reference lookup into a decision tool.
- "I missed a shift" interactive decision tree for students, mirroring the supervisor flow.
- Feedback form so supervisors and students can flag unclear sections.
- A second-quarter check-in with Yaron: did "Common Mistakes" frequency drop? That's the real measure.

## Things I want to remember

- The client didn't ask for ID work. The request was framed as "convert the HTMLs visually." Reframing it as role-based IA + deep-link infrastructure is what made it ID work. Worth practicing — recognizing when a conversion request is actually a design opportunity.
- The scrollspy bug was the kind of thing that only shows up in use, not in spec. Testing at the content level isn't enough; need to test at the interaction level.
- Keeping source PDFs accessible at public URLs (not buried) turned out to be a judgment call worth making explicitly — audience here is internal, policy is already distributed to them, so exposure is fine. Different project, different call.
