# Product Requirements Document (PRD) - Todo App Upgrade: Due Dates, Priorities, and Filters

## 1. Overview

We are upgrading the basic Todo app (currently supporting only `title` and `completed`) to add due dates, priorities, and simple filters so users can better understand what is urgent and focus on the right tasks. The goal is a simple, teachable MVP with no backend changes, relying solely on local storage while keeping the UI lean and easy to demonstrate.

---

## 2. MVP Scope

- **Data model**
  - Each task has:
    - `title` (string): required.
    - `completed` (boolean): existing field, unchanged.
    - `priority` (string enum): `"P1" | "P2" | "P3"`, default `"P3"` when not specified.
    - `dueDate` (string | null): optional ISO `YYYY-MM-DD` value.
  - `dueDate` validation:
    - If the value is not a valid ISO `YYYY-MM-DD` date, it is ignored and treated as absent.

- **Task creation and editing**
  - Users can create a new task by providing at minimum a `title`.
  - Users can optionally set a `dueDate` using a date input constrained to `YYYY-MM-DD`.
  - Users can choose a `priority` level (`P1`, `P2`, `P3`), with new tasks defaulting to `P3` if no priority is selected.
  - Users can mark tasks as completed or incomplete (existing behavior preserved).

- **Priority display**
  - Each task visually displays its priority as a simple badge.
  - Recommended color semantics:
    - `P1`: red badge (highest priority).
    - `P2`: orange badge (medium priority).
    - `P3`: gray badge (lowest/default priority).

- **Filters and views**
  - Provide three primary views, accessible via simple tabs or buttons:
    - **All**
      - Shows all tasks, both completed and incomplete.
    - **Today**
      - Shows only **incomplete** tasks whose `dueDate` is today (based on the user’s local date).
      - Tasks without a `dueDate` are not included in Today.
    - **Overdue**
      - Shows only **incomplete** tasks where `dueDate` is earlier than today.
      - Tasks without a `dueDate` are not included in Overdue.
  - Switching between views should be instantaneous and purely client-side (no page reloads).

- **Storage and architecture**
  - All task data is stored locally (e.g., in-memory plus browser local storage or equivalent) with **no backend changes**.
  - No external or cloud storage is introduced for MVP.

- **UX and constraints**
  - UI remains simple and easy to explain in a teaching environment.
  - No special keyboard navigation or advanced accessibility work is required beyond default browser behavior.

---

## 3. Post-MVP Scope

- **Overdue visual highlighting**
  - Overdue tasks are visually highlighted (e.g., red text, red border, or background) so they stand out clearly from non-overdue tasks.

- **Sorting behavior**
  - Apply a consistent sort order to task lists (especially in All, Today, and Overdue views):
    - Overdue tasks first.
    - Within the same overdue/non-overdue group, sort by priority: `P1` → `P2` → `P3`.
    - Within the same priority, sort by `dueDate` ascending (earlier dates first).
    - Tasks without a `dueDate` appear last.

---

## 4. Out of Scope

- **Notifications and reminders**
  - No push notifications, email alerts, or reminder systems.

- **Recurring tasks**
  - No support for repeating tasks or automated recurrence rules.

- **Multi-user functionality**
  - No user accounts, authentication, or shared/collaborative task lists.

- **Keyboard navigation and advanced accessibility**
  - No custom keyboard shortcuts, focus management systems, or additional accessibility features beyond default HTML and browser behavior.

- **External storage and backend services**
  - No integration with external or cloud storage providers.
  - No new backend services or APIs; the application remains local-only for this upgrade.