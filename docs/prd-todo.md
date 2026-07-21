# Product Requirements Document (PRD) - TODO App Upgrade (Due Dates, Priority, and Filters)

## 1. Overview

We are upgrading the current basic TODO app (title + completed) to make task planning more practical while keeping implementation simple and teachable. The MVP focuses on adding due dates, priority levels, and date-based filters using local-only storage with no backend changes. Advanced presentation and ordering behavior are intentionally deferred to Post-MVP to keep first delivery lean.

---

## 2. MVP Scope

- Add an optional due date field to each task.
- Store due date as ISO date format: YYYY-MM-DD.
- Add a priority field with enum values: P1, P2, P3.
- Set default priority to P3 when no priority is selected.
- Add filter tabs/views: All, Today, Overdue.
- Keep data storage local only (no backend changes and no external storage).
- Enforce title as a required field.
- Enforce priority values to one of P1, P2, P3, with default P3.
- Treat dueDate as optional ISO YYYY-MM-DD; ignore invalid dueDate values and treat them as absent.

---

## 3. Post-MVP Scope

- Visually highlight overdue tasks so they stand out.
- Add sorting behavior: overdue tasks first, then priority order P1 to P3, then due date ascending, with undated tasks last.

---

## 4. Out of Scope

- Notifications.
- Recurring tasks.
- Multi-user support.
- Keyboard navigation and special accessibility enhancements beyond baseline behavior.
- External storage and backend persistence.
