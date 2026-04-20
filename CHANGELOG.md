# Changelog

All notable changes to the VUIM Clinic Attendance & Makeup Resource Hub.

## [1.0.0] — 2026-04-19

### Initial release
- Role-based landing page with Student / Supervisor / Staff entry points
- Three full role guides with deep-linkable anchors (129 total across site)
  - Student: 13-section guide + 17-question scenario FAQ (61 anchors)
  - Supervisor: 15-section operations guide (41 anchors)
  - Staff: 10-section SOP with at-a-glance quick reference (27 anchors)
- Sticky TOC with scrollspy highlighting active section
- Hero-level quick references on each role page (checklist / decision flow / at-a-glance card)
- Print-optimized CSS: TOC hidden, accordions expanded, clean handout output
- Collapsible scenario FAQ that auto-expands when arrived at via deep link
- Anchor target highlight flash on direct navigation

### Fixed
- Scrollspy off-by-one bug: previous implementation used a scrollY threshold smaller than the clicked-anchor landing position due to stacked scroll-padding-top and scroll-mt-24. Replaced with IntersectionObserver using rootMargin "-12% 0px -80% 0px", explicit setActive on TOC click, and syncFromHash that walks from any sub-anchor up to the nearest tracked section ancestor.
