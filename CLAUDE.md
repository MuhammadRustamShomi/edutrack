# CLAUDE.md — EduTrack (Training Institute Management System)

Instructions for Claude Code when working in this repository.

## What this project is

EduTrack is my course assignment: an admin panel for a training institute.
It manages courses, batches, students, enrollments, fee invoices and certificates.

"EduTrack" is a working name. If I rename the project, update it everywhere.

The course teaches in this order, and the project follows the same order:

1. **Phase 1 (now):** static frontend with HTML, CSS and Bootstrap only.
2. **Phase 2 (later):** backend with Laravel and MySQL on XAMPP.
3. **Phase 3 (later):** student portal with React / Next.js.

Only work on the current phase. Do not write Laravel or React code until I say
the class has reached that phase.

Read `PLAN.md` before starting any work. It has the page list, the database
plan and the schedule.

Class reference repo (instructor's example project):
https://github.com/asadmukhtarr/bookly

## Folder structure

Frontend and backend stay in separate folders. Never mix them.

```
edutrack/
├── CLAUDE.md
├── PLAN.md
├── README.md
├── .gitignore
├── project-details.png      # Assignment 01 image
├── frontend/                # Phase 1: static HTML + Bootstrap
│   ├── index.html           # login page
│   ├── dashboard.html
│   ├── courses.html, course-add.html, course-view.html
│   ├── ...                  # other module pages, see PLAN.md
│   ├── bootstrap/           # local Bootstrap files copied from class (css/ and js/)
│   ├── css/
│   │   └── style.css        # the only custom stylesheet
│   └── images/
└── backend/                 # Phase 2: Laravel app goes here
    └── README.md            # placeholder until Phase 2 starts
```

- All HTML pages sit flat inside `frontend/` (no sub-folders for pages), so
  every link and asset path is a simple relative path.
- `backend/` stays empty except for its README until Phase 2.

## Phase 1 rules (frontend)

### No custom JavaScript

- Do not write any JavaScript: no `.js` files of our own, no `<script>` blocks
  with code, no inline handlers such as `onclick`.
- The only script allowed is the class Bootstrap bundle
  (`bootstrap/js/bootstrap.bundle.js`), exactly as the instructor uses it.
  Use its components only through `data-bs-*` attributes
  (navbar toggler, dropdown, modal).
- Check the version comment at the top of `bootstrap/css/bootstrap.min.css`
  before using a component, and only use components that version supports.

### Bootstrap first

- Build layouts with the Bootstrap grid (`container`, `row`, `col-lg-*`,
  `col-md-*`, `col-sm-*`) and Bootstrap utility classes.
- Put custom CSS only in `css/style.css`. Keep it small: brand colour, sidebar
  look, certificate design. No inline `style=""` attributes.
- No npm, no build tools, no CSS preprocessors, no other CSS frameworks.

### Page template

Every page uses the same `<head>` and the same script line at the end of `<body>`:

```html
<link href="bootstrap/css/bootstrap.min.css" rel="stylesheet">
<link href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.13.1/font/bootstrap-icons.min.css" rel="stylesheet">
<link href="css/style.css" rel="stylesheet">
...
<script src="bootstrap/js/bootstrap.bundle.js"></script>
```

Every page after login shares one layout: top navbar, left sidebar
(`col-lg-2`, stacks on top on mobile) and a content area (`col-lg-10`).
Copy the sidebar and navbar exactly between pages and mark the current
module's link with `active`.

### Icons and free assets

Use only free resources. Do not use anything paid.

| Need | Source | Notes |
|---|---|---|
| Icons (main) | Bootstrap Icons — https://icons.getbootstrap.com | Free, open source. Use as `<i class="bi bi-people"></i>` |
| Icons (alternative) | Font Awesome Free — https://fontawesome.com | Class uses 4.7. Do not mix two icon sets on one page |
| Illustrations | unDraw — https://undraw.co | For the login page and empty states. Save SVG/PNG into `images/` |
| Photos | Unsplash / Pexels | Only if a page really needs a photo |
| Font | Google Fonts — https://fonts.google.com | One font only (Poppins), loaded with a `<link>` |

Icon per module (keep these the same on every page):

| Module | Icon class |
|---|---|
| Brand / logo | `bi-mortarboard-fill` |
| Dashboard | `bi-speedometer2` |
| Courses | `bi-journal-bookmark` |
| Batches | `bi-calendar3` |
| Students | `bi-people` |
| Enrollments | `bi-person-check` |
| Fee Invoices | `bi-receipt` |
| Certificates | `bi-award` |
| Logout | `bi-box-arrow-right` |

Action buttons: add `bi-plus-lg`, view `bi-eye`, edit `bi-pencil-square`,
delete `bi-trash`, print `bi-printer`, search `bi-search`.

### Making static pages feel real without JS

- Login form: `action="dashboard.html"`.
- Add/edit forms: `action` points back to that module's list page.
- Search boxes and filters are visual only in Phase 1.
- Invoice and certificate pages print with the browser's Ctrl+P. Hide the
  navbar, sidebar and buttons on paper with Bootstrap's `d-print-none`.
- Use realistic sample data (5 to 8 rows per table), amounts in PKR.

### Status badge colours

Use the same colours everywhere:

- `bg-success`: Paid, Active, Issued
- `bg-warning text-dark`: Pending, Upcoming
- `bg-danger`: Overdue, Dropped
- `bg-secondary`: Completed, Closed

## Code style

- I reuse my code as teaching material, so clarity beats cleverness.
- Add an HTML comment above each major section, for example
  `<!-- Sidebar -->`, `<!-- Stats cards -->`, `<!-- Students table -->`.
- Indent with 4 spaces. Use lowercase file names with hyphens (`course-add.html`).
- Give every `<img>` an `alt` and every form input a `<label>`.
- Do not remove my existing comments or notes when editing a file.
- Do not over-engineer. Get a simple working version first, then improve it.

## Workflow

- Tell me briefly what you are going to do before making large changes.
- Build one module at a time and let me check it in the browser before moving on.
- I am on Windows. Give commands that work in PowerShell, or give both variants.
- Git: commit after each finished module with a short imperative message,
  for example `Add students list and form pages`.
- `.gitignore` must cover OS/editor files now, and `backend/vendor/`,
  `backend/.env` and `node_modules/` for the later phases.
- If something is unclear on a big decision, ask me one question. For small
  decisions, pick a sensible default and tell me what you picked.
- Tick off finished items in the checklist in `PLAN.md`.
