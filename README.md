# VUIM Clinic Attendance & Makeup Resource Hub

A static, role-based hub that consolidates VUIM's clinic attendance and makeup-shift procedures (Spring 2026) into a single performance-support site for **students, supervisors, and reception staff**. Each role page opens with the quick-reference needed on the floor and continues into the full operational guide with deep-linkable anchors so announcement emails can point at specific rules.

## File structure

```
vuim-attendance-hub/
├── index.html                              role-selector landing
├── student/index.html                      checklist + full guide + scenario FAQ
├── supervisor/index.html                   decision flow + full guide
├── staff/index.html                        at-a-glance card + full SOP
├── assets/
│   └── site.css                            shared styles + print rules + anchor highlight
├── source/                                 original 5 reference docs (PDF + HTML)
│   └── extracted/                          working markdown extractions used to build pages
└── README.md
```

## How it's built
- **Vanilla HTML.** No framework, no build step.
- **Tailwind via CDN** (`https://cdn.tailwindcss.com`) and **Lucide icons via CDN** (`https://unpkg.com/lucide@latest`) — same as the source reference pages.
- Anchored sections + sticky TOC on desktop. The `:target` CSS rule highlights the linked rule in pale yellow when arriving via an external link.
- Print-optimized: `@media print` hides nav, expands all `<details>` accordions, removes shadows and backgrounds, and forces handout-friendly type. Use the **Print** button (top-right of any role page) or browser print.
- Student FAQ uses native `<details>` elements and auto-opens the targeted question on hash arrival.

## Deep-link examples (use in announcement emails)
- Student "I'm 50 minutes late" scenario → `student/#faq-50-late`
- Student first-absence rule → `student/#first-absence-rule`
- Supervisor escalation rule → `supervisor/#escalation`
- Supervisor common errors → `supervisor/#errors`
- Staff late-patient 15-min rule → `staff/#late-15-min`

Every section, sub-rule, and FAQ has a unique ID; see the role pages or `source/extracted/*.md` for the full anchor list.

## Preview locally
From the project directory:
```bash
python3 -m http.server 8000
```
Then open <http://localhost:8000/>.

## Deploy

### Vercel (recommended — drag and drop)
1. Sign in to <https://vercel.com>, click **Add New → Project**.
2. Drag the `vuim-attendance-hub/` folder onto the upload zone (no framework preset; treat as static).
3. Production URL is published instantly. Subsequent updates: drag the folder again, or use `vercel deploy --prod` from the project root.

### GitHub Pages (alternative)
1. Push the repo to GitHub.
2. **Settings → Pages →** source: `Deploy from a branch`, branch: `main`, folder: `/ (root)`.
3. Site goes live at `https://<your-org>.github.io/<repo-name>/` within a minute or two.

### Netlify (alternative)
Drag the folder onto <https://app.netlify.com/drop>.

## Updating content
Each role page is a single self-contained HTML file. To revise a rule:
1. Edit the relevant section inside `student/`, `supervisor/`, or `staff/index.html`.
2. Keep existing `id` attributes on sections, list items, and FAQ `<details>` so previously-shared deep links don't break.
3. If a rule is added or removed, update the corresponding extraction in `source/extracted/*.md` so it stays in sync.

## Update date
- **Effective:** Spring 2026
- **Source-doc revision marker:** 04.18.26

## Authority
The **VUIM Student Clinic Handbook** and **Supervisor Handbook** remain the formal authority on all institutional policies. This hub is a performance-support layer — in any conflict between this hub and the Handbooks (as updated by official University memos), the Handbooks govern.

Questions: **dce@vuim.edu**
