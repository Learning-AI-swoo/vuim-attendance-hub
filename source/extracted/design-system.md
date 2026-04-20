# Design System — Extracted from source HTML files

Reuse across all pages so the hub feels institutionally coherent.

## Palette
- Page background: `bg-slate-100` (or `bg-slate-50` for the supervisor flow)
- Card surface: `bg-white`
- Card border: `border border-slate-200` / `border-slate-300`
- Heading underline: `border-b-2 border-slate-800`
- Body text: `text-slate-900` / `text-slate-800` / `text-slate-700`
- Subtle label text: `text-slate-500` uppercase tracking-wider text-xs
- Info callout (left rule): `bg-slate-50 border-l-4 border-slate-300 text-slate-700`
- Rule/key-callout: `border-2 border-slate-800` card with `bg-slate-800 text-white` header strip

## Status colors
| State | Tone | Tailwind |
|---|---|---|
| Present / OK | emerald | `bg-emerald-50 border-emerald-400 text-emerald-800` |
| Tardy / warning | amber/yellow | `bg-amber-50 / bg-yellow-50 border-amber-400 text-amber-700` |
| Absent / blocked | rose/red | `bg-rose-50 border-rose-300 text-rose-800` (hard-stop: `bg-red-100 border-red-400`) |
| Makeup / informational | blue | `bg-blue-100 border-blue-500 text-blue-800` (LCS blue section emphasis) |
| Escalation alert | red | `bg-red-50 border-l-4 border-red-600 text-red-700` |

## Typography
- Font stack: `-apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif`
- H1: `text-3xl md:text-4xl font-bold text-slate-900 leading-tight`
- Section H2: `text-xl md:text-2xl font-bold text-slate-900` with subtle border underline
- All-caps eyebrow labels: `uppercase tracking-wider font-semibold text-xs text-slate-500`

## Header pattern (every page)
```
<div class="flex items-center gap-2 text-slate-500 font-semibold tracking-wider text-xs uppercase">
  <i data-lucide="building-2"></i> Virginia University of Integrative Medicine • [Subtitle]
</div>
<h1 class="text-3xl md:text-4xl font-bold text-slate-900 leading-tight">[Page Title]</h1>
```
Followed by `border-b-2 border-slate-800` separator.

## Iconography
- Lucide via `https://unpkg.com/lucide@latest`, initialized with `lucide.createIcons()`
- Common icons: `building-2`, `info`, `clock`, `alert-triangle`, `check-circle-2`, `calendar-check`, `pen-line`, `users`, `clipboard-check`, `arrow-left`, `printer`

## Print rules
- `@media print` → white bg, no shadow, no border on container
- `.no-print` hides nav/buttons
- `.print-break-inside-avoid` for callout boxes
- Auto-expand any accordions for print

## CDNs (matches source)
```html
<script src="https://cdn.tailwindcss.com"></script>
<script src="https://unpkg.com/lucide@latest"></script>
```

## Footer (every page)
> Virginia University of Integrative Medicine · Questions: dce@vuim.edu · The VUIM Handbooks remain the formal authority.
