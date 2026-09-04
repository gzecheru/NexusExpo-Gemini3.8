# NexusEXPO — Product Requirements Document (PRD) & Solution Architecture

> **Note**: This file is maintained in tandem with [`NexusEXPO-prd.md`](./NexusEXPO-prd.md). For the complete enterprise solution architecture, technical stack recommendations, and Keysight production roadmap, see [`NexusEXPO-prd.md`](./NexusEXPO-prd.md).

---

## Section 1: Vision, Requirements & Solution Architecture

### 1.1 Product Vision & Overview
**NexusEXPO (Keysight EventOps)** is an enterprise-grade event and marketing budget operations hub designed for marketing budget owners, product managers, industry solutions teams (IST), and finance leads at Keysight Technologies.

The platform unifies the intake, multi-tier taxonomy alignment (#initiatives and product hierarchies), approval state machines, booth logistics, staffing conflict detection, creative/messaging approvals, and fiscal treasury optimization into a cohesive, high-performance platform.

### 1.2 User Personas & Scale
- **Core Power Users (25 Users)**: Product Management (PM), Industry Solutions Teams (IST), Marketing Budget Managers, and Finance.
- **Extended Field Users (50–100 Sales Users)**: Occasional interaction to submit event sponsorship requests, monitor approval status, receive automated notifications as event and payment deadlines approach, and update payment statuses.

### 1.3 Recommended Technical Stack (Production)
- **Frontend**: Next.js 15 (App Router, React 19) + TypeScript + Tailwind CSS + Shadcn UI / Radix + TanStack Table v8 & Query.
- **Backend & API**: NestJS / Fastify Node.js API with OpenAPI specs.
- **Authentication**: Enterprise SAML 2.0 / OIDC integrated with Keysight Corporate SSO (Okta / Azure AD) + RBAC.
- **Database**: PostgreSQL 16 (AWS RDS / Azure) with Prisma ORM and JSONB structures for timelines/tech specs.
- **Workflows & Queues**: BullMQ + Redis 7 for approval routing, reminder escalations, and staff conflict checks.
- **Integrations**: Salesforce API (`Campaign_ID` lead sync), Oracle Cloud Procurement (PO & vendor checks), SendGrid & Microsoft Teams Webhook Bots.

### 1.4 Filter UI/UX Optimization Blueprint
Instead of stacking multiple horizontal rows of dropdowns and pill buttons on the main screen, the production architecture specifies:
1. **Unified Command Bar**: A sleek top bar featuring full-text search with natural language hashtag indexing, primary quick selectors for Period and Upcoming/Past toggle, and a prominent **"Filters (N)"** button with active badge count.
2. **Faceted Filter Drawer (Slide-Over)**: A collapsible right-hand drawer organizing filters into logical accordions:
   - *Cadence & Treasury*: Fiscal Year/Quarter, Calendar Year/Month, Custom Date Range.
   - *Location Hierarchy*: Region (*Americas, Europe, META, APAC*), Country, City.
   - *Strategic Taxonomies*: Initiatives (#CyberSecurity, #AI, etc.) & Product Hierarchies.
   - *Staffing & Governance*: Event Lead, Supporting Staff, Approval Status, Priority Tier.
   - *Treasury & Readiness*: Payment Status, Vendor Onboarding, Quick-Pull Ready toggle.
3. **Floating Active Chips Strip**: Clean tags beneath the search bar with 1-click dismissal and global clear.

---

## Section 2: Features, Microtasks & Implementation Checklist

### Feature 1: Core Dashboard Shell & Layout
- [x] Responsive dark-mode dashboard with branding, search bar, and user profile <!-- Implemented in index.html:L116-L175 -->
- [x] Ambient glowing backdrop lighting effects and glassmorphic styling <!-- Implemented in index.html:L109-L114 -->
- [x] Executive KPI summary counter (Visible Expos, Total Reach, Regions, Staff Deployed) <!-- Implemented in index.html:L200-L225, index.html:L955-L970 -->
- [x] Global keyboard shortcuts (`⌘K` / `Ctrl+K` for search, `Escape` to close modals) <!-- Implemented in index.html:L1490-L1505 -->
- [ ] *[Production]* Next.js 15 App Router migration with SSR and dynamic route caching

### Feature 2: 3x3 Card Grid View
- [x] High-resolution photographic backdrops with multi-stop gradient overlay <!-- Implemented in index.html:L73-L86, index.html:L1065-L1070 -->
- [x] Animated shimmer glassmorphic category badges with Lucide icons <!-- Implemented in index.html:L67-L71, index.html:L87-L100, index.html:L1075-L1085 -->
- [x] Micro-interactions: Card lift, image zoom (`scale-110`), and glowing hover borders <!-- Implemented in index.html:L1060-L1140 -->
- [x] Region, Priority Tier, and Fiscal Cadence badge overlays (`FY26 Q4`, `Americas`, `Tier 1 Flagship`) <!-- Implemented in index.html:L1140-L1155 -->
- [x] Staffing assignment capsule preview on cards (Event Lead + Supporting Staff members) <!-- Implemented in index.html:L1170-L1190 -->
- [x] Strategic initiatives and product tags preview capsules with overflow indicator (`+2`) <!-- Implemented in index.html:L1192-L1210 -->
- [ ] *[Production]* Secure S3 banner image upload with automated thumbnail generation

### Feature 3: Spreadsheet / Table View Format
- [x] View switcher toggle (Card Grid vs. Table View) <!-- Implemented in index.html:L355-L368, index.html:L1285-L1300 -->
- [x] Dense glassmorphic table layout with hover highlight states <!-- Implemented in index.html:L395-L415, index.html:L1145-L1200 -->
- [x] Dedicated table columns: Event & Category, Region/Country/Venue, Timeline & Cadence, Team (Lead & Staff), Initiatives & Products, Status & Tier, and Actions <!-- Implemented in index.html:L1145-L1200 -->
- [x] Row action triggers: Details Modal, Quick Edit, Watchlist/Bookmark toggle, Delete <!-- Implemented in index.html:L1180-L1200 -->
- [ ] *[Production]* Virtualized table rendering via TanStack Table v8 with multi-column sorting and CSV/Excel export

### Feature 4: Fiscal & Dual-Calendar Cadence Engine
- [x] Keysight Fiscal Year calculation engine (Nov 1 Start: Q1 Nov–Jan, Q2 Feb–Apr, Q3 May–Jul, Q4 Aug–Oct) <!-- Implemented in index.html:L875-L925 -->
- [x] Fast period filters: Current Fiscal Year, Current Fiscal Quarter, Current Calendar Year, Current Calendar Quarter, Current Calendar Month, Next Fiscal Year <!-- Implemented in index.html:L235-L250, index.html:L930-L950 -->
- [x] Past vs. Future timeline toggle relative to reference date (`2026-09-03`) <!-- Implemented in index.html:L252-L265, index.html:L950-L960 -->
- [x] Custom Date Interval filter (From Date – To Date) with instant clear <!-- Implemented in index.html:L268-L280, index.html:L935-L950 -->
- [x] Fiscal configuration settings modal allowing user to customize Fiscal Year start date and reference timestamp <!-- Implemented in index.html:L385-L425, index.html:L1230-L1260 -->
- [ ] *[Production]* Store `Original Target Fiscal Quarter` vs. `Actual Paid Fiscal Quarter` for "Pull-Forward" variance reporting

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
