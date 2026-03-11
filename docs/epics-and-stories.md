- Epic: Task Data Model Enhancements
  - Story: Add priority field to tasks
    - Acceptance Criteria:
      - Each task record includes a priority field with allowed values "P1", "P2", or "P3".
      - When a new task is created without explicitly selecting a priority, it is saved with priority "P3".
      - Existing tasks created before this change are assigned priority "P3" without losing their existing title or completed status.

  - Story: Add optional due date field to tasks
    - Acceptance Criteria:
      - Each task record can store an optional dueDate field that may be empty.
      - A task can be created or updated without specifying any dueDate.
      - When a valid due date is provided, it is stored with the task and persists across browser refreshes.

  - Story: Validate due date format as ISO YYYY-MM-DD
    - Acceptance Criteria:
      - When the user enters a date in the ISO format YYYY-MM-DD, the value is accepted and stored as the task's dueDate.
      - When the user enters an invalid date or a non-ISO format, the value is not saved to dueDate and the application continues to function without errors.
      - Tasks with invalid date input behave as if they have no dueDate in all filters and views.

- Epic: Task Creation and Editing
  - Story: Create tasks with title, priority, and due date
    - Acceptance Criteria:
      - A user can create a task by entering a non-empty title.
      - The creation form allows selecting a priority and an optional due date in YYYY-MM-DD format.
      - If no priority is selected, the task is created with priority "P3".
      - If no dueDate is selected, the task is created without a dueDate.
      - After creation, the new task appears in the All view and, if incomplete with a qualifying dueDate, in the Today or Overdue views.

  - Story: Edit existing task details
    - Acceptance Criteria:
      - A user can open an existing task and change its title, priority, and dueDate.
      - Saving edits updates the task immediately in all views where it appears.
      - Updating a task's dueDate causes it to appear or disappear from the Today and Overdue views according to the defined rules.

  - Story: Toggle task completion status
    - Acceptance Criteria:
      - Each task has a control to mark it as completed or incomplete.
      - Toggling completion updates the task's completed state without navigating away from the current view.
      - Completed tasks remain visible in the All view.
      - Completed tasks do not appear in the Today or Overdue views, even if their dueDate is today or in the past.

- Epic: Priority Display UI
  - Story: Show priority badges on tasks
    - Acceptance Criteria:
      - Every task in the list shows its current priority as a visible badge next to the title or main text.
      - When a task's priority changes, the badge updates immediately without a page reload.

  - Story: Apply color scheme for P1, P2, and P3 badges
    - Acceptance Criteria:
      - P1 tasks display a red priority badge.
      - P2 tasks display an orange priority badge.
      - P3 tasks display a gray priority badge.
      - The badge colors are consistent across All, Today, and Overdue views.

- Epic: Task Filters and Views
  - Story: Add All tasks view
    - Acceptance Criteria:
      - An All view is available via a tab or button.
      - In the All view, both completed and incomplete tasks are displayed.
      - The All view includes tasks regardless of whether they have a dueDate.

  - Story: Add Today tasks view
    - Acceptance Criteria:
      - A Today view is available via a tab or button.
      - The Today view shows only incomplete tasks whose dueDate is equal to the user's current local date.
      - Tasks without a dueDate never appear in the Today view.

  - Story: Add Overdue tasks view
    - Acceptance Criteria:
      - An Overdue view is available via a tab or button.
      - The Overdue view shows only incomplete tasks whose dueDate is earlier than the user's current local date.
      - Tasks without a dueDate never appear in the Overdue view.

  - Story: Exclude completed tasks from Today and Overdue views
    - Acceptance Criteria:
      - Completed tasks do not appear in the Today or Overdue views.
      - Marking a task as completed removes it from the Today and Overdue views while leaving it visible in the All view.
      - Marking a completed task as incomplete causes it to reappear in Today or Overdue if its dueDate qualifies.

  - Story: Provide tab-based navigation between task views
    - Acceptance Criteria:
      - Users can switch between All, Today, and Overdue views using clearly labeled tabs or buttons.
      - The active view is visually indicated.
      - Switching between views does not cause a full page reload and preserves the current task data in memory.

- Epic: Local Storage Persistence
  - Story: Persist tasks locally without backend services
    - Acceptance Criteria:
      - Task data is stored using a browser-local mechanism (such as localStorage) with no network requests to a backend.
      - Creating, editing, or completing tasks updates the stored data.
      - The application continues to function correctly if the network is disabled.

  - Story: Load tasks from local storage on app start
    - Acceptance Criteria:
      - When the app loads, it reads any previously stored tasks and displays them in the appropriate views.
      - If no stored data exists, the app starts with an empty task list without errors.
      - Changes made during a session remain after a full browser refresh.

- Epic: Teaching-Friendly UX
  - Story: Review task list layout for simplicity
    - Acceptance Criteria:
      - The main task screen shows only essential elements: task list, completion controls, and view filters.
      - No advanced configuration panels or extra features beyond the PRD are introduced in MVP.
      - The layout is readable on a standard laptop resolution without horizontal scrolling.

  - Story: Streamline task form for classroom demonstrations
    - Acceptance Criteria:
      - The task creation/edit form includes fields only for title, priority, and due date.
      - Form labels for title, priority, and due date are clear and concise.
      - Creating or updating a task requires at most filling the fields and clicking a single button to save.

- Epic: Overdue Task Highlighting
  - Story: Visually highlight overdue tasks
    - Acceptance Criteria:
      - Overdue tasks (incomplete tasks with a dueDate earlier than today) have a distinct visual style, such as red text, border, or background.
      - Non-overdue tasks do not use the overdue visual style.
      - Changing a task's completion state or dueDate immediately adds or removes the overdue highlighting as appropriate.

  - Story: Differentiate overdue tasks from upcoming tasks
    - Acceptance Criteria:
      - Users can visually distinguish overdue tasks from tasks due today or in the future without reading the dates.
      - Tasks due today do not use the same styling as overdue tasks.
      - Adjusting a dueDate so it is no longer overdue removes the overdue styling.

- Epic: Task Sorting Rules
  - Story: Sort tasks with overdue items first
    - Acceptance Criteria:
      - In the All view, overdue tasks are listed before non-overdue tasks.
      - Updating a task's dueDate or completion status immediately updates its position relative to overdue and non-overdue groups.

  - Story: Sort tasks by priority within groups
    - Acceptance Criteria:
      - Within the overdue group and within the non-overdue group, tasks are ordered by priority: P1 first, then P2, then P3.
      - Changing a task's priority reorders it correctly within its group.

  - Story: Sort tasks by due date within priority
    - Acceptance Criteria:
      - For tasks with the same overdue status and priority, tasks with earlier dueDate appear before tasks with later dueDate.
      - Editing a task's dueDate repositions it according to this rule.

  - Story: Place tasks without due dates at the end of lists
    - Acceptance Criteria:
      - Tasks without a dueDate always appear after tasks with any valid dueDate within the same view.
      - Adding a dueDate to an undated task moves it into the dated section according to the other sorting rules.
      - Removing a dueDate from a task moves it to the end of the list within its priority and overdue/non-overdue group.
