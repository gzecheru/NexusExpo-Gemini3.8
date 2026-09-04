# Product Requirements Document (PRD) — NexusEvents Dashboard

## Section 1: Vision & Requirements

### 1.1 Product Vision & Overview
**NexusEvents (NexusExpo)** is an enterprise-grade, high-performance web dashboard engineered for event directors, trade show organizers, and corporate attendees to discover, manage, and monitor premier global trade shows and conferences in real time. 

The application combines striking visual aesthetics (frosted glassmorphism, dynamic photographic backdrops, fluid hover micro-interactions) with rich operational capabilities (live search, multi-tier category filtering, strategic initiative & product tagging, fiscal & temporal filtering, multi-criteria sorting, card grid & spreadsheet table view modes, modal deep dives, bookmarking, and complete event management workflows).

### 1.2 Target Users
- **Conference Directors & Event Organizers**: Manage conference portfolios, track booth logistics, sponsor tiers, budgets, and lead targets across fiscal years and quarters.
- **Product Marketing & Business Development**: Align strategic corporate initiatives (#ai, #cybersecurity, #sovereign cloud, #tsn, #carriers) and showcase flagship products (#BreakingPoint, #CyberRange, #AresONE-1600GE, #KAI-IB).
- **Executive Leadership & Finance**: Review event investments and ROI across corporate fiscal cadences (Current Fiscal Year, Fiscal Quarter, Calendar Year, Calendar Quarter, and Calendar Month).
- **Corporate Sponsors & Exhibitors**: Track venue logistics, stand locations, and engagement goals.
- **Attendees & Keynote Speakers**: Discover high-impact trade shows, search by technology tracks, and bookmark upcoming conferences.

### 1.3 Core Requirements
1. **Responsive Modern UI/UX**:
   - Dark-mode first aesthetic built with Tailwind CSS, custom blur filters, and Google Fonts (`Plus Jakarta Sans` & `Inter`).
   - Clean, adaptive layouts supporting Mobile, Tablet, and Desktop viewport resolutions.
2. **Dynamic Conference Cards & Spreadsheet Views**:
   - High-resolution photographic backgrounds with gradient overlay legibility masks.
   - Distinctive frosted glassmorphic category badges with animated shimmer and category-specific Lucide iconography.
   - Comprehensive event metadata: Event Title, Full Venue / City, Timeline / Dates, Fiscal Cadence Tag (`FY26 Q4`), Registration Status pills, Booth Stand #, Priority Tier, and Key Metrics.
3. **Temporal & Fiscal Cadence Filters**:
   - Configurable Fiscal Year start (defaults to **November 1st, 2025**; FY26 spans Nov 1, 2025 – Oct 31, 2026).
   - Fast period presets: *Current Fiscal Year*, *Current Fiscal Quarter*, *Current Calendar Year*, *Current Calendar Quarter*, *Current Calendar Month*, *Next Fiscal Year*, and *All Time*.
   - Timeline toggle: *All Events*, *Upcoming / Future*, and *Past Events* relative to reference date (`2026-09-03`).
   - Custom Date Interval range picker (From Date – To Date).
4. **Live Data Management & CRUD Operations**:
   - Real-time client-side search across conference titles, venues, topic tracks, #initiatives, and #products with `⌘K` shortcut.
   - Multi-tier filtering: Categories, Strategic Initiatives, and Featured Products.
   - Add & Edit Event Modals with validation, quick-toggle tag pills, photo presets, and instant recalculations.
   - Event deletion with confirmation prompts and toast notifications.
   - Interactive Detail Modal with complete topic agendas, venue details, logistics breakdown, and registration links.

---

## Section 2: Features & Microtasks

### Feature 1: Core Dashboard Layout & Navigation
- [x] Responsive navigation bar with branding, search bar, and user profile avatar <!-- Implemented in index.html:L116-L175 -->
- [x] Executive KPI summary counter (Active Expos, Total Reach, Initiatives, Products) with dynamic calculations <!-- Implemented in index.html:L200-L225, index.html:L955-L970 -->
- [x] Ambient glowing backdrop lighting effects <!-- Implemented in index.html:L109-L114 -->
- [x] Global keyboard shortcuts (`⌘K` / `Ctrl+K` for search, `Escape` to close modals) <!-- Implemented in index.html:L1300-L1315 -->

### Feature 2: Conference Cards with Photographic Backgrounds
- [x] Global AI & Robotics Summit 2026 card (San Francisco, CA) <!-- Implemented in index.html:L735-L755, index.html:L1050-L1140 -->
- [x] FinTech Disrupt World Congress card (London, UK) <!-- Implemented in index.html:L756-L775, index.html:L1050-L1140 -->
- [x] BioHealth & MedTech International card (Boston, MA) <!-- Implemented in index.html:L776-L795, index.html:L1050-L1140 -->
- [x] NextGen Auto & Electric Mobility Expo card (Munich, Germany) <!-- Implemented in index.html:L796-L815, index.html:L1050-L1140 -->
- [x] CleanEnergy & Climate Solutions Expo card (Copenhagen, Denmark) <!-- Implemented in index.html:L816-L835, index.html:L1050-L1140 -->
- [x] CloudScale & DevOps Architecture Expo card (Seattle, WA) <!-- Implemented in index.html:L836-L855, index.html:L1050-L1140 -->
- [x] CyberShield Global Defense Forum card (Singapore) <!-- Implemented in index.html:L856-L875, index.html:L1050-L1140 -->
- [x] DesignOps & Creative Frontiers Summit card (Amsterdam, NL) <!-- Implemented in index.html:L876-L895, index.html:L1050-L1140 -->
- [x] SpaceTech & Commercial Aerospace Expo card (Houston, TX) <!-- Implemented in index.html:L896-L915, index.html:L1050-L1140 -->
- [x] MWC Global Mobile & Carrier Congress 2026 card (Barcelona, Spain - Past event FY26 Q2) <!-- Implemented in index.html:L695-L715 -->
- [x] Black Hat Security USA 2026 card (Las Vegas, NV - Past event FY26 Q4) <!-- Implemented in index.html:L716-L734 -->
- [x] AI Hardware & Edge Silicon Summit 2026 card (Santa Clara, CA - Current Month Sep 2026) <!-- Implemented in index.html:L735-L754 -->
- [x] Multi-stop dark gradient overlay for text legibility over background photography <!-- Implemented in index.html:L73-L86, index.html:L1065-L1070 -->
- [x] Glassmorphism category badges with icon and shimmer effect <!-- Implemented in index.html:L67-L71, index.html:L87-L100, index.html:L1075-L1085 -->

### Feature 3: Live Search, Category Filtering & Sorting
- [x] Instant full-text search across titles, locations, venues, initiatives, and products <!-- Implemented in index.html:L139-L146, index.html:L1025-L1045 -->
- [x] Dynamic category filter buttons with auto-computed item counts <!-- Implemented in index.html:L270-L275, index.html:L975-L1000 -->
- [x] Multi-option sorting (Upcoming date, Furthest date, Attendees count, Alphabetical) <!-- Implemented in index.html:L280-L290, index.html:L1040-L1050 -->
- [x] Empty state screen with one-click filter reset <!-- Implemented in index.html:L370-L380, index.html:L1270-L1285 -->

### Feature 4: Table / Spreadsheet View Format
- [x] View switcher toggle (Cards Grid vs. Table View) <!-- Implemented in index.html:L292-L305, index.html:L1285-L1300 -->
- [x] Responsive glassmorphic table structure with hover row highlight <!-- Implemented in index.html:L345-L365, index.html:L1145-L1200 -->
- [x] Table columns for Event & Category, Location & Stand, Timeline & Cadence, Initiatives & Products, Status & Tier, Metrics, and Row Actions <!-- Implemented in index.html:L1145-L1200 -->
- [x] Direct modal trigger, edit modal launch, bookmarking, and deletion controls from table rows <!-- Implemented in index.html:L1180-L1200 -->

### Feature 5: Event Creation & Modal Management
- [x] "Add Conference" modal with form validation <!-- Implemented in index.html:L425-L600 -->
- [x] Curated high-res photographic background presets <!-- Implemented in index.html:L560-L580 -->
- [x] Dynamic KPI recalculation and real-time state insertion on submission <!-- Implemented in index.html:L955-L970, index.html:L1215-L1250 -->
- [x] Conference detail deep-dive modal (description, logistics breakdown, initiatives, products) <!-- Implemented in index.html:L605-L700, index.html:L1205-L1250 -->
- [x] Toast feedback notification system <!-- Implemented in index.html:L702-L710, index.html:L1300-L1310 -->

### Feature 6: Git & GitHub Repository Check-in
- [x] Initialize git repository and configure `.gitignore` <!-- Implemented in .gitignore & local git init -->
- [x] Authenticate GitHub account and verify target profile <!-- Authenticated via gzecheru -->
- [x] Create remote GitHub repository `NexusExpo-Gemini3.8` <!-- Created at https://github.com/gzecheru/NexusExpo-Gemini3.8 -->
- [x] Commit initial codebase (`index.html`, `prd.md`, assets) and push to `main` branch <!-- Pushed to origin/main -->

### Feature 7: Event Management Metadata, Featured Initiatives & Products
- [x] Capture Featured Initiatives (`#cybersecurity`, `#ai`, `#carriers`, `#sovereign cloud`, `#industrial`, `#aerospace&defense`, `#tsn`) in event data model <!-- Implemented in index.html:L695-L915 -->
- [x] Capture Featured Products (`#BreakingPoint`, `#CyberRange`, `#CyPerf`, `#APS-100/400G`, `#AresONE-1600GE`, `#INPT-1600GE`, `#KAI-IB`, `#KAI-DCB`) in event data model <!-- Implemented in index.html:L695-L915 -->
- [x] Comprehensive event management metadata: Booth/Stand #, Priority Tier, Lead Manager, Budget/Investment, and Target Leads <!-- Implemented in index.html:L695-L915 -->
- [x] Strategic Initiatives filter toolbar with active pill highlights <!-- Implemented in index.html:L310-L320, index.html:L1000-L1020 -->
- [x] Featured Products filter toolbar with active pill highlights <!-- Implemented in index.html:L325-L335, index.html:L1020-L1035 -->
- [x] Active filter criteria bar displaying applied filters with 1-click clearing <!-- Implemented in index.html:L338-L345, index.html:L1035-L1050 -->
- [x] Card View initiative & product tag capsules with overflow indicator <!-- Implemented in index.html:L1110-L1130 -->
- [x] Table View initiative & product tag capsules <!-- Implemented in index.html:L1160-L1175 -->
- [x] Detail Modal "Event Management & Logistics" analytics grid (Stand, Budget, Leads, Priority Tier) <!-- Implemented in index.html:L640-L670, index.html:L1220-L1240 -->
- [x] "Edit Conference Logistics" workflow enabling real-time edits for any event's metadata, initiatives, and products <!-- Implemented in index.html:L1240-L1280 -->
- [x] Quick-toggle interactive preset buttons for Initiatives and Products inside the Add/Edit form <!-- Implemented in index.html:L495-L555, index.html:L1260-L1290 -->

### Feature 8: Fiscal & Temporal Filtering, Past vs. Future, and Custom Date Interval
- [x] Fiscal Year calculation logic with Nov 1st start date definition <!-- Implemented in index.html:L875-L925 -->
- [x] Filter by Current Fiscal Year (FY26: Nov 1, 2025 - Oct 31, 2026) <!-- Implemented in index.html:L235-L250, index.html:L930-L950 -->
- [x] Filter by Current Fiscal Quarter (FY26 Q4: Aug 1, 2026 - Oct 31, 2026) <!-- Implemented in index.html:L235-L250, index.html:L930-L950 -->
- [x] Filter by Current Calendar Year (CY 2026: Jan 1 - Dec 31, 2026) <!-- Implemented in index.html:L235-L250, index.html:L930-L950 -->
- [x] Filter by Current Calendar Quarter (CY Q3 2026: Jul 1 - Sep 30, 2026) <!-- Implemented in index.html:L235-L250, index.html:L930-L950 -->
- [x] Filter by Current Calendar Month (September 2026) <!-- Implemented in index.html:L235-L250, index.html:L930-L950 -->
- [x] Filter by Past vs. Future events relative to reference date <!-- Implemented in index.html:L252-L265, index.html:L950-L960 -->
- [x] Custom Date Interval filtering (From Date - To Date) with instant clear <!-- Implemented in index.html:L268-L280, index.html:L935-L950, index.html:L1250-L1270 -->
- [x] Fiscal Cadence tag generation on cards, table rows, and modals (`FY26 Q4`, `FY27 Q1`) <!-- Implemented in index.html:L920-L935, index.html:L1085, index.html:L1160 -->
- [x] Fiscal Configuration settings modal allowing user to adjust Fiscal Year Start date and Reference Date with immediate recalculation <!-- Implemented in index.html:L385-L425, index.html:L1230-L1260 -->
- [ ] *[Future Phase]* Persist user-configured fiscal definitions and custom multi-entity fiscal periods to remote backend database / user profile API
