Here is the **Stage 6: Project Planning & Sprint 0** document. 

This document represents the bridge between planning and active coding. It outlines how the development team will organize their work, set up their technical environments, and break down the previously defined User Stories into actionable, trackable coding tasks (Sprints).

---

# **Stage 6 Project Planning & Sprint 0: CivicVoice**

## **1. Sprint 0: Environment & Infrastructure Checklist**
Before developers can build user-facing features, the core foundation (Sprint 0) must be established. This ensures that when coding starts, the team is working in a secure, uniform, and automated environment.

### **A. Version Control & Repositories**
*   [ ] **Create GitHub/GitLab Repository:** Initialize the main codebase repository.
*   [ ] **Set Branch Protection Rules:** Lock the `main` (Production) and `develop` (Staging) branches. Require at least one code review (Pull Request approval) before any code is merged.
*   [ ] **Monorepo or Polyrepo setup:** Set up a monorepo structure (e.g., using Turborepo) if frontend and backend will be housed together.

### **B. Cloud & DevOps Provisioning**
*   [ ] **AWS Setup:** Provision the AWS accounts. Set up the VPC, create the primary PostgreSQL RDS instance, and create the two S3 buckets (`civicvoice-quarantine-bucket` and `civicvoice-vault-bucket`).
*   [ ] **Vercel Setup:** Connect Vercel to the GitHub repository for automated Next.js frontend deployments.
*   [ ] **CI/CD Pipelines:** Write GitHub Actions scripts to automatically run code linters and unit tests every time a developer pushes code.

### **C. Local Development Environment**
*   [ ] **Docker Compose:** Create a `docker-compose.yml` file so developers can spin up a local PostgreSQL database and Redis cache with a single command.
*   [ ] **Environment Variables (`.env`):** Distribute a secure `.env.example` file containing dummy API keys so devs know exactly what keys they need (e.g., SendGrid, AWS, Google Maps/Autoaddress).
*   [ ] **Prisma Initialization:** Initialize the Prisma ORM and execute the first database migration to create the tables defined in Stage 5.

---

## **2. Agile / Scrum Cadence**
The project will be managed using Agile methodology, broken down into 2-week coding cycles called **Sprints**. 

*   **Sprint Length:** 2 Weeks.
*   **Sprint Planning (Day 1):** The team meets to drag tickets from the Backlog into the active Sprint, estimating how many hours/points each will take.
*   **Daily Standup (Days 2-10):** A 15-minute daily sync: *What did you do yesterday? What are you doing today? Are you blocked?*
*   **Sprint Review (Day 14):** Developers demo the working software to stakeholders (e.g., showing the new Evidence Vault uploading an HQ video).
*   **Definition of Done (DoD):** A ticket is not "Done" until it is coded, peer-reviewed, tested, and successfully deployed to the Staging environment.

---

## **3. The Backlog Breakdown (First 4 Sprints)**
This maps the User Stories from Stage 1 into the first two months of development.

### **Sprint 1: Authentication & Core UI Skeleton**
*Focus: Allowing users to securely sign up, log in, and navigate the app.*
*   **Ticket 1.1:** Configure Next.js, Tailwind CSS, and global UI components (Buttons, Navbars, Modals based on Figma).
*   **Ticket 1.2:** Set up NextAuth.js for Email/Password login and JWT session handling.
*   **Ticket 1.3:** Build the `Users` database table using Prisma.
*   **Ticket 1.4:** Create the generic "User Dashboard" view (empty state).

### **Sprint 2: The Issue Builder & Authority DB**
*Focus: The intake questionnaire and mapping logic.*
*   **Ticket 2.1:** Populate the `Authorities` database table with the master spreadsheet of Irish Councils/Agencies.
*   **Ticket 2.2:** Build the step-by-step UI Wizard (Issue Selection -> Geolocation/Eircode).
*   **Ticket 2.3:** Write the mapping logic (e.g., If Eircode starts with "D01" + "Noise", return "Dublin City Council ID").
*   **Ticket 2.4:** Build the `Cases` database table to save the user's drafted issue.

### **Sprint 3: The Evidence Vault (AWS Integration)**
*Focus: Handling media uploads securely.*
*   **Ticket 3.1:** Build the UI Drag-and-Drop component with progress bars.
*   **Ticket 3.2:** Write the backend endpoint to request an AWS S3 "Pre-Signed URL" for secure, direct-to-cloud uploading.
*   **Ticket 3.3:** Build the `Evidence_Files` database table to map the S3 URL back to the specific Case ID.
*   **Ticket 3.4:** Create the secure, read-only public URL viewer (e.g., `civicvoice.io/vault/[uuid]`).

### **Sprint 4: Communication Engine & Case Management**
*Focus: Generating the letters and tracking the status.*
*   **Ticket 4.1:** Build the dynamic text parser that injects database variables (Name, DB level, Law) into the JSON templates.
*   **Ticket 4.2:** Build the Action Center UI (Tabs for "Email" and "Phone Script").
*   **Ticket 4.3:** Implement the "Mailto:" deep link so clicking "Send Complaint" opens the user's Gmail/Apple Mail with the text pre-filled.
*   **Ticket 4.4:** Build the Kanban Case Tracker UI (Draft -> Sent -> Escalated) on the main dashboard.

---

## **4. Developer Ticket Standard (Example)**
To ensure developers build exactly what was planned, every Jira/Linear ticket must follow a strict format. Here is an example of what **Ticket 3.2** looks like inside the project management software:

> **Title:** Implement S3 Pre-Signed URL Generation for Evidence Uploads
> **Epic:** The Evidence Vault
> **Assignee:** Backend Developer | **Story Points:** 5
> 
> **User Story Context:** 
> *As a user, I want to securely upload heavy video files directly to the cloud so my browser doesn't crash.*
> 
> **Technical Requirements:**
> 1. Create a secure POST endpoint at `/api/vault/generate-upload-url`.
> 2. Endpoint must accept `fileName`, `fileType`, and `fileSize`.
> 3. Verify the user has an active session via NextAuth.
> 4. Reject requests if `fileSize` > 50MB.
> 5. Connect to AWS S3 SDK and return a pre-signed PUT URL valid for exactly 15 minutes.
> 
> **Acceptance Criteria:**
> *   [ ] User cannot access the endpoint without an active auth token (401 Unauthorized).
> *   [ ] Uploads larger than 50MB return a 400 Bad Request error.
> *   [ ] The file successfully lands in the `civicvoice-quarantine-bucket` in AWS.
> *   [ ] The S3 object key is saved to the `Evidence_Files` table in PostgreSQL.

---

### **Project Transition Complete**
With Stage 6 approved, the **Planning Phase** is officially over. 

The Project Manager will now load these Sprints into Jira/Linear, assign the Sprint 0 and Sprint 1 tickets to the engineering team, and **Day 1 of Development begins.**
