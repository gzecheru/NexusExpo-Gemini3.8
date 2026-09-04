# NexusEXPO — Product Requirements Document (PRD) & Solution Architecture

**Product Name:** NexusEXPO (Enterprise Event & Marketing Budget Operations Hub)  
**Target Organization:** Keysight Technologies  
**Version:** 3.0 (Production Roadmap & Architecture Baseline)  
**Author / Solution Architect:** AI Solution Architect & Product Management  

---

## Section 1: Product Vision, Requirements & Solution Architecture

### 1.1 Executive Summary & Problem Statement
Marketing budget owners and event managers across Keysight coordinate dozens of multi-stakeholder trade shows, global conferences, and operational investments annually across disparate divisions (Product Management [PM], Industry Solutions Teams [IST], Marketing, Business Development, Sales, Engineering, and Finance).

Today, this process suffers from:
1. **Fragmented Intake & Governance**: Spreadsheets and email chains conceal who approved spend, whether technical demo hardware is secured, and whether staff are double-booked.
2. **End-of-Quarter Budget Scrambles**: Marketing budget managers lack visibility into "Pull-Forward" readiness (which approved events have active quotes and approved vendors ready for immediate budget execution before fiscal deadlines).
3. **Dual-Calendar Friction**: Disconnect between the **Keysight Fiscal Calendar** (starts November 1st: Q1 Nov–Jan, Q2 Feb–Apr, Q3 May–Jul, Q4 Aug–Oct) and standard **Calendar Quarters/Months**.
4. **Disjointed Field Sales Participation**: Field sales teams (50–100 users) lack a unified interface to submit sponsorship requests, check approval progress, or receive notifications for impending deadlines and payment statuses.

**NexusEXPO** unifies intake, multi-tier taxonomy alignment (#initiatives and product hierarchies), approval state machines, booth logistics, staffing conflict detection, creative/messaging approvals, and fiscal treasury optimization into a cohesive, high-performance platform.

---

### 1.2 User Personas & Audience Scale

| Persona Group | User Count | Primary Needs & Responsibilities |
| :--- | :---: | :--- |
| **Marketing Budget & Event Ops Leads** | 5–8 Users | Oversee entire corporate event envelope, execute end-of-quarter budget sweeps, manage vendor onboarding, track PO/credit card locks. |
| **Product Managers (PM) & IST Leads** | 10–12 Users | Define strategic initiatives, mandate product hierarchies (KAI, APS, INPT), configure technical demo requirements (power, bandwidth, hardware). |
| **Field Marketing & Regional Directors** | 5–8 Users | Manage regional portfolios across **Americas**, **Europe**, **META**, and **APAC**; assign Event Leads and booth staffing rosters. |
| **Finance & Procurement Partners** | 3–5 Users | Audit dual-calendar fiscal attribution, verify quotes/invoices, approve treasury sweeps and Oracle POs. |
| **Field Sales & Business Development** *(Occasional)* | 50–100 Users | Submit event sponsorship requests; view approval state; receive automated notifications for contract deadlines, upcoming dates, and payment confirmations. |

---

### 1.3 Recommended Technical Stack & System Architecture

Given the user base (25 daily power users + 50–100 occasional sales users, low peak concurrency ~50 active sessions, high relational data density, workflow state machines, and file attachments), the optimal technical architecture is a modern, modular cloud stack:

```
+---------------------------------------------------------------------------------------+
|                                    NEXUS-EXPO CLIENT                                  |
|   Next.js 15 (React 19) + TypeScript + Tailwind CSS + Shadcn UI + TanStack Table/Query |
+---------------------------------------------------------------------------------------+
                                           |  HTTPS / REST & OpenAPI
                                           v
+---------------------------------------------------------------------------------------+
|                                 APPLICATION & API TIER                                |
|   Node.js (Fastify / NestJS) or Next.js Route Handlers                                |
|   - Authentication: Keysight Okta SSO / SAML 2.0 & OIDC + RBAC                        |
|   - Workflow Engine: XState / BullMQ (Approval Routing, Quorum, State Machines)       |
|   - Conflict Engine: Date overlap validator for booth staffing directory              |
+---------------------------------------------------------------------------------------+
        |                                   |                                   |
        v                                   v                                   v
+------------------+             +--------------------+             +-------------------+
|  PRIMARY DATABASE|             |   CACHE & QUEUES   |             |   OBJECT STORAGE  |
|  PostgreSQL 16   |             |   Redis 7.x        |             |   AWS S3 / Azure  |
|  (Prisma ORM /   |             |   - BullMQ Jobs    |             |   - Banner Proofs |
|   JSONB schemas) |             |   - Session Cache  |             |   - Quotes & POs  |
+------------------+             +--------------------+             +-------------------+
        |                                                                       |
        +-------------------------+---------------------------------------------+
                                  |
                                  v
+---------------------------------------------------------------------------------------+
|                              ENTERPRISE INTEGRATIONS                                  |
|  - Salesforce (SFDC) API: Automated Campaign_ID sync and lead conversion tracking     |
|  - Oracle Cloud Procurement API: Vendor verification, PO creation & status sync      |
|  - Communication Gateway: SendGrid (Email) & Microsoft Teams Webhook Bots             |
+---------------------------------------------------------------------------------------+
```

#### Detailed Stack Selection:
1. **Frontend**:
   - **Framework**: Next.js 15 (App Router, Server Components) + TypeScript.
   - **Styling**: Tailwind CSS + custom glassmorphic tokens (retaining our dark-mode visual identity).
   - **Component Library**: Shadcn UI (Radix Primitives) for accessible modals, popovers, and accordions.
   - **Data Grids**: TanStack Table v8 for virtualized, dense spreadsheet views with column filtering and sorting.
   - **State & Data Fetching**: TanStack Query (React Query) for optimistic updates and real-time cache invalidation.
2. **Backend & Application Services**:
   - **API Framework**: NestJS (TypeScript) or Fastify for structured enterprise microservices.
   - **Authentication & RBAC**: SAML 2.0 / OpenID Connect integrated with Keysight Corporate SSO (Okta / Azure AD). Role-Based Access Control (Admin, Event Lead, Finance, Staff, Sales Submitter).
   - **Workflow & Background Tasks**: BullMQ backed by Redis for escalation triggers, deadline reminders, and notification queues.
3. **Database & Data Tier**:
   - **Database**: PostgreSQL 16 (hosted on AWS RDS or Azure Database for PostgreSQL).
   - **ORM**: Prisma ORM or Drizzle for type-safe relational queries.
   - **Attachments**: Secure S3-compatible bucket with pre-signed URLs for creative proofs and quotes.
4. **Integrations**:
   - **Salesforce**: Bi-directional sync of `Campaign_ID` (format: `NT_2026_FQ4_RSA_SanFrancisco_March_2026`).
   - **Microsoft Teams & Outlook**: Interactive approval cards (Actionable Messages) for single-click approvals.
   - **Oracle Cloud ERP (Phase 2)**: Vendor active check and PO number sync.

---

### 1.4 Filter UI/UX Redesign Blueprint

#### The Optimization Problem:
In our initial PoC, multiple stacked horizontal rows (Categories, Initiatives, Products, Fiscal Periods, Locations, Staff) occupied significant vertical real estate above the card grid.

#### The Production UI/UX Solution: **Unified Command Bar + Faceted Filter Drawer**

```
+------------------------------------------------------------------------------------------------------+
| [Search events, #initiatives, #products, cities... ⌘K]  [All Time ▾] [Upcoming ▾]  [⚙ Filters (3)]  |
+------------------------------------------------------------------------------------------------------+
| Active Chips: [Region: Europe ✕] [Initiative: #AI ✕] [FY26 Q4 ✕]                    [Clear All]     |
+------------------------------------------------------------------------------------------------------+
```

1. **Top Command Strip (Clean & Compact)**:
   - **Search Input**: Full-text search with natural language hashtag recognition (`#ai`, `#CyberRange`).
   - **Primary Quick Selectors**: Quick dropdowns for **Cadence Period** (*FY26*, *CY2026*, etc.) and **Timeline** (*Upcoming* vs *Past*).
   - **Faceted Drawer Trigger**: A prominent `Filters` button displaying active filter count badges (e.g., `Filters (3)`).
2. **Slide-Over Faceted Filter Drawer (Right Side / Collapsible)**:
   - **Section 1: Cadence & Treasury**: Fiscal Year, Fiscal Quarter, Calendar Year/Month, Date Interval Range.
   - **Section 2: Location Hierarchy**: Region selector (*Americas, Europe, META, APAC*), cascading Country and City.
   - **Section 3: Strategic Taxonomy**: Initiatives manager (#CyberSecurity, #AI, etc.) & Product Hierarchies (KAI, APS, INPT).
   - **Section 4: Staffing & Governance**: Event Lead selector, Supporting Staff multi-select, Priority Tier (*Tier 1 Flagship*, *Tier 2 Strategic*, *Tier 3 Regional*).
   - **Section 5: Treasury & Readiness**: Payment Status (*PO*, *CC*), Vendor Status (*Active* vs *Setup Needed*), and "Quick-Pull Ready" toggle.
3. **Floating Active Criteria Strip**:
   - Chips displayed under the search bar for every active filter with 1-click removal (`✕`) and `Clear All`.

---

### 1.5 Master Data Schema & Taxonomy Alignment

#### Strategic Taxonomy Mapping:
- **Initiatives / Themes**: `#CyberSecurity`, `#Artificial Intelligence`, `#Carriers`, `#Sovereign Cloud`, `#Industrial`, `#Aerospace & Defense`, `#TSN`, `#SupplyChain/SBOM`.
- **Product Hierarchy (Parent $\rightarrow$ Child)**:
  - `Keysight KAI` $\rightarrow$ `KAI-IB` (Inference Builder), `KAI-DCB` (Datacenter Builder).
  - `Keysight APS-100/400` $\rightarrow$ `APS-M8400`, `APS-ONE-400`, `APS-M1010`.
  - `Keysight Network Security` $\rightarrow$ `BreakingPoint`, `CyberRange`, `CyPerf`.
  - `Keysight High-Speed Ethernet` $\rightarrow$ `AresONE-1600GE`, `INPT-1600GE`.

#### Treasury & End-of-Quarter Budget Sweep:
$$\text{Readiness Score} = \text{Vendor Setup (Active)} + \text{Quote Attached} + \text{Payment Method Selected}$$
Events flagged as `Quick_Pull_Ready = true` can be executed within 48 hours to capture end-of-quarter budget surpluses.

---

## Section 2: Features, Microtasks & Implementation Checklist

### Feature 1: Executive Dashboard & Modern Viewport Architecture
- [x] Responsive dark-mode dashboard with branding, search, and user profile <!-- Implemented in index.html:L116-L175 -->
- [x] Ambient glowing backdrop lighting effects and frosted glassmorphic styling <!-- Implemented in index.html:L109-L114 -->
- [x] Executive KPI summary counter (Visible Expos, Total Reach, Regions, Staff Deployed) <!-- Implemented in index.html:L200-L225, index.html:L955-L970 -->
- [x] Global keyboard shortcuts (`⌘K` / `Ctrl+K` for search, `Escape` to close modals) <!-- Implemented in index.html:L1490-L1505 -->
- [ ] *[Production]* Migrate frontend shell to Next.js 15 App Router with SSR and dynamic caching

### Feature 2: Visual 3x3 Card Grid & Density Displays
- [x] High-resolution photographic backdrops with multi-stop gradient overlay for legibility <!-- Implemented in index.html:L73-L86, index.html:L1065-L1070 -->
- [x] Animated shimmer glassmorphic category badges with Lucide icons <!-- Implemented in index.html:L67-L71, index.html:L87-L100, index.html:L1075-L1085 -->
- [x] Micro-interactions: Card lift, image zoom (`scale-110`), and glowing hover borders <!-- Implemented in index.html:L1060-L1140 -->
- [x] Region, Priority Tier, and Fiscal Cadence badge overlays (`FY26 Q4`, `Americas`, `Tier 1 Flagship`) <!-- Implemented in index.html:L1140-L1155 -->
- [x] Staffing assignment capsule preview on cards (Event Lead + Supporting Staff members) <!-- Implemented in index.html:L1170-L1190 -->
- [x] Strategic initiatives and product tags preview capsules with overflow indicator (`+2`) <!-- Implemented in index.html:L1192-L1210 -->
- [ ] *[Production]* Custom banner image upload to S3/Azure Blob Storage with automated thumbnail generation

### Feature 3: Spreadsheet / Table View Format
- [x] View switcher toggle (Card Grid vs. Table View) <!-- Implemented in index.html:L355-L368, index.html:L1285-L1300 -->
- [x] Dense glassmorphic table layout with hover highlight states <!-- Implemented in index.html:L395-L415, index.html:L1145-L1200 -->
- [x] Dedicated table columns: Event & Category, Region/Country/Venue, Timeline & Cadence, Team (Lead & Staff), Initiatives & Products, Status & Tier, and Actions <!-- Implemented in index.html:L1145-L1200 -->
- [x] Row action triggers: Details Modal, Quick Edit, Watchlist/Bookmark toggle, Delete <!-- Implemented in index.html:L1180-L1200 -->
- [ ] *[Production]* Virtualized table rendering via TanStack Table v8 supporting multi-column sorting and CSV/Excel export

### Feature 4: Fiscal & Dual-Calendar Cadence Engine
- [x] Keysight Fiscal Year calculation engine (Nov 1 Start: Q1 Nov–Jan, Q2 Feb–Apr, Q3 May–Jul, Q4 Aug–Oct) <!-- Implemented in index.html:L875-L925 -->
- [x] Fast period filters: Current Fiscal Year, Current Fiscal Quarter, Current Calendar Year, Current Calendar Quarter, Current Calendar Month, Next Fiscal Year <!-- Implemented in index.html:L235-L250, index.html:L930-L950 -->
- [x] Past vs. Future timeline toggle relative to reference date (`2026-09-03`) <!-- Implemented in index.html:L252-L265, index.html:L950-L960 -->
- [x] Custom Date Interval filter (From Date – To Date) with instant clear <!-- Implemented in index.html:L268-L280, index.html:L935-L950 -->
- [x] Fiscal configuration settings modal allowing user to customize Fiscal Year start date and reference timestamp <!-- Implemented in index.html:L385-L425, index.html:L1230-L1260 -->
- [ ] *[Production]* Store `Original Target Fiscal Quarter` vs. `Actual Paid Fiscal Quarter` to generate quarterly "Pull-Forward" variance reports

### Feature 5: Geographic Location Hierarchy
- [x] 4 Global Operating Theaters / Regions: `Americas`, `Europe`, `META`, `APAC` <!-- Implemented in index.html:L685-L1035 -->
- [x] Cascading Location Hierarchy: Region $\rightarrow$ Country $\rightarrow$ City dropdowns <!-- Implemented in index.html:L285-L330, index.html:L950-L990 -->
- [x] Region badge indicator on cards, table rows, and modal headers <!-- Implemented in index.html:L1140-L1155, index.html:L1230-L1250 -->
- [x] Full venue, street address, and booth/stand tracking <!-- Implemented in index.html:L1120, index.html:L1170 -->
- [ ] *[Production]* AI/Web look-up integration: Auto-populate venue address and official event links when entering Event Name and City

### Feature 6: Strategic Taxonomies (Initiatives & Product Hierarchies)
- [x] Strategic Initiatives support (#CyberSecurity, #AI, #Carriers, #Sovereign Cloud, #Industrial, #Aerospace&Defense, #TSN) <!-- Implemented in index.html:L695-L1035 -->
- [x] Featured Products support (#BreakingPoint, #CyberRange, #CyPerf, #APS-100/400G, #AresONE-1600GE, #INPT-1600GE, #KAI-IB, #KAI-DCB) <!-- Implemented in index.html:L695-L1035 -->
- [x] Dual interactive filter pill bars for Initiatives and Products <!-- Implemented in index.html:L370-L395, index.html:L1000-L1035 -->
- [x] Quick-toggle interactive preset buttons inside Add & Edit Event modals <!-- Implemented in index.html:L495-L555, index.html:L1260-L1290 -->
- [ ] *[Production]* Relational taxonomy database mapping Parent Product Family $\rightarrow$ Child Product Name / NPI

### Feature 7: Staffing Roster, Roles & Conflict Engine
- [x] Event Lead Manager assignment and filtering <!-- Implemented in index.html:L330-L340, index.html:L950-L990 -->
- [x] Supporting Staff deployment tracking and filtering <!-- Implemented in index.html:L342-L355, index.html:L950-L990 -->
- [x] Dedicated "Assigned Event Staff & Field Team" showcase inside conference detail modal <!-- Implemented in index.html:L680-L705, index.html:L1340-L1365 -->
- [x] Quick-add staff pills inside Add/Edit modal (`+ Alex Rivera`, `+ Jordan Lee`, etc.) <!-- Implemented in index.html:L580-L610 -->
- [ ] *[Production]* Role assignment per staff member (`Demo Lead`, `Booth Manager`, `Speaker`, `Setup/Teardown Support`)
- [ ] *[Production]* Embedded T&E attribution: per-employee travel/hotel estimates rolled up into total event budget
- [ ] *[Production]* Automated Staff Conflict Engine: Active cross-check alerting if an employee is assigned to concurrent events with overlapping travel dates

### Feature 8: Filter UI/UX Modernization & Redesign
- [x] Multi-tier active filter criteria tags bar with 1-click dismissal and global reset <!-- Implemented in index.html:L398-L415, index.html:L1035-L1050 -->
- [ ] *[Production]* Implement slide-over / collapsible Faceted Filter Drawer grouping filters into clean collapsible accordions
- [ ] *[Production]* Unified top command bar with active filter badge indicator (e.g. `Filters (4)`)

### Feature 9: Governance, Multi-Approver Matrix & Sales Portal
- [ ] *[Production]* Simplified submission form for 50–100 Occasional Sales Users to request event sponsorships
- [ ] *[Production]* Multi-approver engine supporting single, sequential, or unanimous sign-offs
- [ ] *[Production]* Budget envelope protection: Automatic routing of over-budget submissions to `For Consideration` queue with non-blocking warning badge
- [ ] *[Production]* Automated email and Microsoft Teams notifications when approval deadlines approach, event dates near, or payment updates are required
- [ ] *[Production]* Sales feedback portal: Allow sales leads to confirm payment status, input post-event lead metrics, and upload final receipts

### Feature 10: Treasury, End-of-Quarter Budget Sweep & CRM Integration
- [ ] *[Production]* End-of-Quarter "Budget Sweep" Optimizer dashboard ranking ready-to-execute events by Readiness Score
- [ ] *[Production]* Payment pipeline tracking: `Vendor Setup Active` vs `Vendor Setup Required`, PO vs. Corporate Credit Card
- [ ] *[Production]* Standardized `Campaign_ID` generation (e.g., `NT_2026_FQ4_RSA_SanFrancisco_March_2026`) formatted for Salesforce export
- [ ] *[Production]* Oracle Procurement Cloud integration: PO synchronization and invoice payment confirmation
