# 🎓 Student Project Tracking System

Web‑based system to manage **student projects, teams, milestones, and submissions** with separate views for students, mentors, and admins.

---

## 🎯 Goal

- Replace scattered spreadsheets and emails with one central system.  
- Make it easy for mentors to see:
  - Which teams exist
  - What stage each project is at
  - Which milestones are delayed  

---

## 👥 Roles

- **Student**
  - Register / log in
  - Create project & team
  - Upload milestone work
- **Mentor**
  - Approve/reject project ideas
  - Review submissions
  - Add comments & final approval
- **Admin / HOD**
  - View batch‑wise summary
  - See mentor load
  - Export reports

---

## 🧱 Core Entities

- **User** (role: student, mentor, admin)
- **Project**
  - Title, abstract, technologies, batch
- **Team**
  - Members, roll numbers, allocated mentor
- **Milestone**
  - Name, description, due date, status
- **Submission**
  - File/URL, comments, marks, approved flag

---

## 🔁 Workflow (High‑Level)

1. **Registration & Login**
   - Students and mentors create accounts.
   - Roles decide which dashboard they see.

2. **Project Creation**
   - Student creates a project:
     - Title, description, tech stack
     - Add / invite team members
     - Select preferred mentor (optional)

3. **Mentor Review**
   - Mentor sees pending project requests.
   - Approves or rejects idea.
   - On approval → project becomes “Active”.

4. **Milestone Assignment**
   - Automatic or manual creation of milestones:
     - Topic approval
     - SRS
     - Design
     - Implementation
     - Final report / viva

5. **Submissions & Feedback**
   - For each milestone:
     - Student uploads document(s) or link(s).
     - Mentor reviews, adds comments, updates status:
       - Pending → In Review → Approved / Needs Changes.

6. **Completion & Reports**
   - Once all milestones are approved, project is marked “Completed”.
   - Admin dashboard shows summary per batch / mentor / status.

---

## 🖼️ Example Dashboards

### Student Dashboard

- List of projects (usually 1)
- Milestones with:
  - Due dates
  - Status
  - Upload buttons
- Mentor feedback and remarks

### Mentor Dashboard

- Assigned projects list
- Filters by batch / status
- Quick view:
  - How many milestones are pending review
  - Which teams are delayed

### Admin Dashboard

- Count of:
  - Total projects
  - Active vs completed
  - Projects per mentor
- Export to CSV / PDF (optional extension)

---

## 🔨 Implementation Steps (Conceptual)

1. **Database Design**
   - Create tables/collections for:
     - users, projects, teams, milestones, submissions
   - Decide relationships (e.g. project ↔ mentor: many‑to‑one).

2. **Authentication & Roles**
   - Implement login / logout.
   - Assign role to each user.
   - Use middleware/guards to restrict pages by role.

3. **Project & Team Management**
   - Views to:
     - Create project
     - Add team members
     - Request mentor

4. **Milestone Module**
   - CRUD for milestones (admin/mentor)
   - Attach milestones to projects
   - Generate defaults for each new project

5. **Submissions**
   - File upload or URL attach
   - Store metadata (who submitted, when, which milestone)
   - Add mentor comment & status fields

6. **Dashboards & Filters**
   - Build per‑role dashboards with summary cards
   - Filters for batch, mentor, status

---

## 📊 What Was Learned

- Modeling an academic workflow into a **real system**.  
- Implementing basic **RBAC** (Role‑Based Access Control).  
- Designing dashboards so each role sees what matters to them.  
- Handling file uploads and status transitions cleanly.

---

## 🔮 Next Improvements

- Add **notifications** (email / in‑app) for upcoming deadlines.  
- Add simple **analytics** (on‑time vs late submissions).  
- Provide an **API** so it can integrate with existing college portals.
