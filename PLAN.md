# PLAN.md — EduTrack (Training Institute Management System)

## 1. Goal

Build an admin panel for a training institute, in the same style as the other
class projects:

**Training Institute Management System : Dashboard, Courses, Batches, Students,
Enrollments, Fee Invoices, Certificates**

It is different from every project already assigned in class (hostel, car
service, food cart, hotel, appointment booking, shipping), and when it is
finished it can be used for a real institute.

## 2. Phases

| Phase | What | Tech | Folder | Status |
|---|---|---|---|---|
| 1 | Static frontend of the admin panel | HTML, CSS, Bootstrap, Bootstrap Icons | `frontend/` | Now |
| 2 | Backend with database | Laravel, MySQL, XAMPP | `backend/` | When class reaches it |
| 3 | Student portal | React / Next.js | Decide when class reaches it | Later |

Frontend and backend live in separate folders from day one. In Phase 2 the
finished HTML pages are copied into Laravel as Blade views, so clean,
well-commented pages now save work later.

## 3. Modules

| Module | What it manages | Pages |
|---|---|---|
| Login | Admin sign in | `index.html` |
| Dashboard | Totals, recent activity, pending fees | `dashboard.html` |
| Courses | Course title, duration, fee, status | `courses.html`, `course-add.html`, `course-view.html` |
| Batches | A course run with dates, timing, instructor, seats | `batches.html`, `batch-add.html`, `batch-view.html` |
| Students | Student profile and contact details | `students.html`, `student-add.html`, `student-view.html` |
| Enrollments | Which student is in which batch | `enrollments.html`, `enrollment-add.html` |
| Fee Invoices | Fee amount, due date, paid / pending / overdue | `invoices.html`, `invoice-add.html`, `invoice-view.html` |
| Certificates | Certificates issued to students who completed | `certificates.html`, `certificate-view.html` |

Total: 18 pages. Every module follows the same pattern, so after the first
module the rest are mostly copy and adjust.

## 4. Page details

### Shared layout (every page after login)

- Top navbar: brand with icon on the left, admin name and Logout on the right.
- Left sidebar (`col-lg-2`): one link per module, each with its icon, current
  page marked `active`. Stacks on top of the content on mobile.
- Content area (`col-lg-10`): page title, breadcrumb, then the page content.

### Login (`index.html`)

- Two columns: illustration from unDraw on the left, login card on the right.
- Email, password, "Remember me" checkbox, Login button.
- Form `action="dashboard.html"`.

### Dashboard (`dashboard.html`)

- Four stat cards with icons: Total Students, Active Batches, Fees Collected
  This Month, Pending Invoices.
- "Recent Enrollments" table (5 rows).
- "Upcoming Batches" list group.
- "Pending Fees" table with status badges.

### List pages (`courses.html`, `students.html`, ...)

- Header row: page title, search box, "Add New" button.
- Table: `table table-hover align-middle` inside a card, wrapped in
  `table-responsive`.
- Columns end with Status (badge) and Actions (view, edit, delete icon buttons).
- Static pagination at the bottom.

### Add / edit form pages (`course-add.html`, ...)

- A card with a two-column form (`row` + `col-md-6`).
- Labels on every input, `required` on mandatory fields.
- Save and Cancel buttons. Form `action` goes back to the list page.

### View pages (`student-view.html`, `batch-view.html`, ...)

- Profile or summary card on the left, related records table on the right.
  Example: a student's page shows their enrollments and invoices.

### Invoice (`invoice-view.html`)

- Looks like a real fee invoice: institute name and logo icon, invoice number,
  student and batch details, fee table, total, status badge.
- Prints cleanly with Ctrl+P (navbar, sidebar and buttons use `d-print-none`).

### Certificate (`certificate-view.html`)

- The showpiece page: bordered certificate with student name, course name,
  completion date, certificate number and signature lines.
- Styled in `css/style.css`. Prints cleanly with Ctrl+P.

## 5. Schedule

Assignment 01 and 02 dates have already passed, so they come first.

| Day | Work | Class assignment |
|---|---|---|
| Wed 7 Oct | Project setup, git init, shared layout, login, dashboard, project details image | 01 (details image) |
| Thu 8 Oct | Courses, Batches, Students (list, add, view) | 02 (frontend) |
| Fri 9 Oct | Enrollments, Fee Invoices, Certificates. Install XAMPP and post screenshot | 02 (frontend), 03 (XAMPP, due 9 Oct) |
| Sat 10 Oct | Polish: mobile check, consistent icons and badges, write README | |
| Sun 11 Oct | Push to GitHub and post the link in the group | 04 (GitHub, due 11 Oct) |

If time is short, finish these first: login, dashboard, all six list pages,
one add form, `invoice-view.html`. Then add the remaining pages.

## 6. Phase 2 preview: database plan

Not built yet. This is here so the frontend forms use the right field names.

| Table | Main fields |
|---|---|
| `users` | id, name, email, password, role |
| `courses` | id, title, duration_weeks, fee, description, status |
| `batches` | id, course_id, name, start_date, end_date, timing, instructor, seats, status |
| `students` | id, name, email, phone, address, photo, status |
| `enrollments` | id, student_id, batch_id, enrolled_on, status |
| `invoices` | id, enrollment_id, invoice_no, amount, due_date, paid_on, status |
| `certificates` | id, enrollment_id, certificate_no, issued_on |

Relationships:

- A course has many batches.
- A batch has many enrollments.
- A student has many enrollments.
- An enrollment has many invoices and one certificate.

Use the form field `name` attributes from this table in Phase 1
(for example `name="duration_weeks"`), so the forms connect to Laravel
without renaming.

## 7. Phase 3 preview: student portal

Follows the class "Client Portal" pattern: student login, dashboard,
My Courses, My Invoices, My Certificates, Profile. Planned in detail when the
class reaches React / Next.js.

## 8. Checklist

### Setup
- [ ] Create `edutrack/` with `frontend/` and `backend/` folders
- [ ] Copy the class `bootstrap/` folder into `frontend/`
- [ ] Create `frontend/css/style.css` and `frontend/images/`
- [ ] Add `backend/README.md` placeholder
- [ ] `git init`, add `.gitignore`, first commit

### Assignment 01
- [ ] Project details image (`project-details.png`), same style as the class `bookly.png`

### Assignment 02: frontend
- [ ] Shared layout (navbar + sidebar) finalised
- [ ] `index.html` (login)
- [ ] `dashboard.html`
- [ ] Courses: list, add, view
- [ ] Batches: list, add, view
- [ ] Students: list, add, view
- [ ] Enrollments: list, add
- [ ] Fee Invoices: list, add, view (printable)
- [ ] Certificates: list, view (printable)
- [ ] Mobile check on every page
- [ ] Same icons and badge colours on every page

### Assignment 03
- [ ] Install XAMPP, post screenshot in the group

### Assignment 04
- [ ] Write `README.md` (what the project is, modules, screenshots, how to open)
- [ ] Push to GitHub, post the link in the group
