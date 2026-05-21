Here is the **Stage 4: UI/UX Prototyping & User Journey Mapping** document. 

Since we cannot build actual clickable Figma files here, this document acts as the exact brief you will hand to your UI/UX Designer. It details the step-by-step user flow, the visual layout of the core screens, the design system guidelines, and the testing strategy.

---

# **Stage 4 UI/UX & User Journey Document: CivicVoice**

## **1. The Core User Journey Flow (The "Happy Path")**
This maps the exact step-by-step path a user takes to report a new issue (e.g., reporting the Dunnes Stores noise hazard). The design must prioritize **progressive disclosure**—only showing the user one simple question or task at a time to prevent cognitive overload.

*   **Step 1: Landing & Intake**
    *   User clicks "Report an Issue."
    *   *Prompt:* "What type of issue are you reporting?" (Grid of icons: 📢 Noise, 🏢 Workplace Hazard, 🏠 Tenancy, 🌳 Environment).
*   **Step 2: Geolocation & Targeting**
    *   *Prompt:* "Where is this happening?" (User inputs Eircode or drops a pin on a map).
    *   *Prompt:* "Who is responsible?" (User types "Dunnes Stores" or selects "Private Landlord").
*   **Step 3: The Evidence Vault (Upload)**
    *   User is prompted to upload photos, videos, or CSV files.
    *   *System Action:* Progress bar shows upload status. A secure link (e.g., `civicvoice.io/vault/case-1234`) is instantly generated.
*   **Step 4: The Action Center**
    *   *System Action:* Based on Steps 1 & 2, the system identifies the target (e.g., HSA & Dublin City Council).
    *   User views the auto-generated email, selects a "Tone" (Firm vs. Friendly), and views their "In-Person Script."
*   **Step 5: Dispatch & Tracking**
    *   User copies the generated email and clicks a link that automatically opens their default email app (Gmail/Apple Mail) with the recipient and subject line pre-filled.
    *   User clicks "Mark as Sent," and the system routes them to the Case Management Dashboard.

---

## **2. Core Screen Wireframe Descriptions**
These are the layout instructions for the UI designer to build the wireframes.

### **Screen 1: The User Dashboard (Mobile & Desktop View)**
*   **Header:** "Welcome back, [Name]." Quick "New Case" Floating Action Button (FAB) prominently displayed.
*   **Active Cases Kanban Board:** 
    *   Cards representing ongoing issues. 
    *   *Example Card:* "Commercial Noise Hazard - Dunnes Stores (Tier 2 Escalation)".
    *   Color-coded Status Tags: 🟠 *Awaiting Reply* | 🔴 *Action Required* | 🟢 *Resolved*.
*   **Alerts Section:** "You have 1 case ready for Tier 3 escalation to the HSA. Click here to send the statutory notice."

### **Screen 2: The Issue Builder (The Wizard)**
*   **Layout:** A distraction-free, full-screen wizard. A progress bar sits at the top (e.g., "Step 2 of 4").
*   **Interaction:** Large, easily tappable cards for selecting issue types.
*   **Contextual Help:** Small "i" info icons next to complex terms. If a user selects "Noise Hazard," a tooltip explains: *"Include specific details like the time of day, frequency (e.g., high-pitch whine), and how it affects you."*

### **Screen 3: The Evidence Vault**
*   **Top Section:** "Upload Evidence." A large drag-and-drop zone (desktop) or a "Select from Camera Roll / Files" button (mobile).
*   **List View:** Uploaded files appear in a list with thumbnail previews and file sizes. 
*   **External Link Option:** A simple text input field: *"Files too large? Paste your Google Drive or Dropbox link here."*
*   **The Output:** A highly visible, copyable URL link field: `Your Secure Evidence Link: civicvoice.io/vault/case-abc`. (Includes a "Copy to Clipboard" button).

### **Screen 4: The Action Center (Letters & Scripts)**
*   **Tabbed Interface:** The user can toggle between two main tabs: ✉️ **Written Complaint** and 🗣️ **Speaking Script**.
*   **Written Complaint Tab:**
    *   A dropdown menu for "Select Recipient" (e.g., Store Manager, Head Office, HSA).
    *   A "Tone Selector" slider (Friendly <---> Formal Legal).
    *   A text box displaying the generated email. Variable data (e.g., the statutory law) is highlighted in a subtle background color so the user knows the AI/system added it.
    *   "Copy Email" and "Open in Email App" buttons.
*   **Speaking Script Tab:**
    *   Displayed like a teleprompter or flashcards. 
    *   Clear headings: "How to open the conversation," "What to say if they are dismissive," "Your legal rights in this conversation."

---

## **3. Design System & Accessibility Guidelines**
Because this platform will be used by frustrated, stressed, and potentially vulnerable people, the UI must invoke calm, trust, and extreme clarity.

### **A. Color Palette**
*   **Primary (Trust & Authority):** Deep Navy Blue (#1E3A8A). Used for headers and primary buttons.
*   **Secondary (Action & Calm):** Soft Teal or Sage Green (#0F766E). Used for success states and "Next Step" buttons.
*   **Backgrounds (Focus):** Off-white or Light Gray (#F9FAFB) to reduce eye strain. Pure white (#FFFFFF) for content cards.
*   **Alerts (Urgency, not panic):** Muted Orange (#EA580C) rather than aggressive bright red. 

### **B. Typography**
*   **Font Family:** A highly legible sans-serif font like *Inter*, *Roboto*, or *Public Sans* (designed for government/civic interfaces).
*   **Hierarchy:** Large headers for instructions (24px+). Body text must be a minimum of 16px to ensure readability on mobile devices.

### **C. Accessibility (WCAG 2.1 AA Standards)**
*   **Contrast Ratios:** All text must have a minimum contrast ratio of 4.5:1 against its background.
*   **Touch Targets:** All buttons and interactive elements on the mobile view must be at least 44x44 pixels to prevent "fat-finger" errors.
*   **Screen Readers:** All uploaded images must have hidden alt-text tags. Form fields must have explicit labels (not just placeholder text that disappears when typing).

---

## **4. Prototyping & User Testing Strategy**
Before writing backend code, the UI Designer will build a clickable prototype in **Figma** and test it with real people to catch usability flaws.

### **A. The Prototype Build**
*   Create a high-fidelity prototype connecting Screens 1 through 4.
*   Simulate the "Issue Builder" so the user can click through the exact flow of reporting a retail noise complaint.

### **B. The User Testing Script**
Recruit 5 unassociated individuals (friends, community members) and conduct a "Think-Aloud" test. Give them the following scenario:

> **Scenario:** *"You are standing outside a Dunnes Stores. There is a deafening, high-pitched mechanical noise coming from an extraction fan. You have recorded a video on your phone. Using this app prototype, I want you to log the issue, upload your video, and find the email you need to send to the Health and Safety Authority."*

### **C. Metrics to Watch During Testing**
*   **Time on Task:** How long does it take them to get from the home screen to the generated letter? (Goal: Under 3 minutes).
*   **Friction Points:** Do they understand what "Tier 3 Escalation" means, or do we need to rename it to "Report to Government Regulator"?
*   **Upload Confusion:** Do they intuitively know how to paste a Google Drive link if the video file is too large?

---

### **Next Steps for the Dev/Design Team based on Stage 4:**
1.  **Design Action:** The UI/UX designer begins building the wireframes in Figma based on these descriptions.
2.  **Copywriting Action:** Finalize the "Plain English" micro-copy (the text on buttons, tooltips, and empty states). 
3.  **Tech Handoff:** Once the Figma prototype is approved via user testing, hand it over to the CTO/Lead Developer to begin Stage 5 (Technical System Design), where they will map out the React components and API routes needed to bring the UI to life.
