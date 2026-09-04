# Product Requirements Document (PRD) — NexusEvents Dashboard

## Section 1: Vision & Requirements

### 1.1 Product Vision & Overview
**NexusEvents (NexusExpo)** is an enterprise-grade, high-performance web dashboard engineered for event directors, trade show organizers, and corporate attendees to discover, manage, and monitor premier global trade shows and conferences in real time. 

The application combines striking visual aesthetics (frosted glassmorphism, dynamic photographic backdrops, fluid hover micro-interactions) with rich operational capabilities (live search, multi-tier category filtering, strategic initiative & product tagging, multi-criteria sorting, card grid & spreadsheet table view modes, modal deep dives, bookmarking, and complete event management workflows).

### 1.2 Target Users
- **Conference Directors & Event Organizers**: Manage conference portfolios, track booth logistics, sponsor tiers, budgets, and lead targets.
- **Product Marketing & Business Development**: Align strategic corporate initiatives (#ai, #cybersecurity, #sovereign cloud, #tsn, #carriers) and showcase flagship products (#BreakingPoint, #CyberRange, #AresONE-1600GE, #KAI-IB).
- **Corporate Sponsors & Exhibitors**: Track venue logistics, stand locations, and engagement goals.
- **Attendees & Keynote Speakers**: Discover high-impact trade shows, search by technology tracks, and bookmark upcoming conferences.

### 1.3 Core Requirements
1. **Responsive Modern UI/UX**:
   - Dark-mode first aesthetic built with Tailwind CSS, custom blur filters, and Google Fonts (`Plus Jakarta Sans` & `Inter`).
   - Clean, adaptive layouts supporting Mobile, Tablet, and Desktop viewport resolutions.
2. **Dynamic 9+ Conference Cards**:
   - High-resolution photographic backgrounds with gradient overlay legibility masks.
   - Distinctive frosted glassmorphic category badges with animated shimmer and category-specific Lucide iconography.
   - Comprehensive event metadata: Event Title, Full Venue / City, Timeline / Dates, Registration Status pills, Booth Stand #, Priority Tier, and Key Metrics.
3. **Multi-Format Viewports (Cards vs. Table)**:
   - 3x3 Card Grid view with hover zoom (`scale-110`), initiatives/products chips, and action drawers.
   - Compact / Spreadsheet Table view displaying structured columns for fast multi-row scanning.
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
- [x] Executive KPI summary counter (Active Expos, Total Reach, Initiatives, Products) with dynamic calculations <!-- Implemented in index.html:L200-L225, index.html:L840-L855 -->
- [x] Ambient glowing backdrop lighting effects <!-- Implemented in index.html:L109-L114 -->
- [x] Global keyboard shortcuts (`⌘K` / `Ctrl+K` for search, `Escape` to close modals) <!-- Implemented in index.html:L1140-L1150 -->

### Feature 2: 9 Conference Cards with Photographic Backgrounds
- [x] Global AI & Robotics Summit 2026 card (San Francisco, CA) <!-- Implemented in index.html:L644-L670, index.html:L950-L1050 -->
- [x] FinTech Disrupt World Congress card (London, UK) <!-- Implemented in index.html:L671-L695, index.html:L950-L1050 -->
- [x] BioHealth & MedTech International card (Boston, MA) <!-- Implemented in index.html:L696-L720, index.html:L950-L1050 -->
- [x] NextGen Auto & Electric Mobility Expo card (Munich, Germany) <!-- Implemented in index.html:L721-L745, index.html:L950-L1050 -->
- [x] CleanEnergy & Climate Solutions Expo card (Copenhagen, Denmark) <!-- Implemented in index.html:L746-L770, index.html:L950-L1050 -->
- [x] CloudScale & DevOps Architecture Expo card (Seattle, WA) <!-- Implemented in index.html:L771-L795, index.html:L950-L1050 -->
- [x] CyberShield Global Defense Forum card (Singapore) <!-- Implemented in index.html:L796-L820, index.html:L950-L1050 -->
- [x] DesignOps & Creative Frontiers Summit card (Amsterdam, NL) <!-- Implemented in index.html:L821-L845, index.html:L950-L1050 -->
- [x] SpaceTech & Commercial Aerospace Expo card (Houston, TX) <!-- Implemented in index.html:L846-L870, index.html:L950-L1050 -->
- [x] Multi-stop dark gradient overlay for text legibility over background photography <!-- Implemented in index.html:L73-L86, index.html:L965-L970 -->
- [x] Glassmorphism category badges with icon and shimmer effect <!-- Implemented in index.html:L67-L71, index.html:L87-L100, index.html:L975-L985 -->

### Feature 3: Live Search, Category Filtering & Sorting
- [x] Instant full-text search across titles, locations, venues, initiatives, and products <!-- Implemented in index.html:L139-L146, index.html:L920-L945 -->
- [x] Dynamic category filter buttons with auto-computed item counts <!-- Implemented in index.html:L230-L235, index.html:L856-L885 -->
- [x] Multi-option sorting (Upcoming date, Furthest date, Attendees count, Alphabetical) <!-- Implemented in index.html:L240-L250, index.html:L935-L945 -->
- [x] Empty state screen with one-click filter reset <!-- Implemented in index.html:L330-L340, index.html:L1110-L1120 -->

### Feature 4: Table / Spreadsheet View Format
- [x] View switcher toggle (Cards Grid vs. Table View) <!-- Implemented in index.html:L252-L265, index.html:L1122-L1135 -->
- [x] Responsive glassmorphic table structure with hover row highlight <!-- Implemented in index.html:L305-L325, index.html:L1050-L1105 -->
- [x] Table columns for Event & Category, Location & Stand, Timeline, Initiatives & Products, Status & Tier, Metrics, and Row Actions <!-- Implemented in index.html:L1050-L1105 -->
- [x] Direct modal trigger, edit modal launch, bookmarking, and deletion controls from table rows <!-- Implemented in index.html:L1090-L1105 -->

### Feature 5: Event Creation & Modal Management
- [x] "Add Conference" modal with form validation <!-- Implemented in index.html:L345-L530 -->
- [x] Curated high-res photographic background presets <!-- Implemented in index.html:L490-L510 -->
- [x] Dynamic KPI recalculation and real-time state insertion on submission <!-- Implemented in index.html:L840-L855, index.html:L1060-L1095 -->
- [x] Conference detail deep-dive modal (description, logistics breakdown, initiatives, products) <!-- Implemented in index.html:L535-L630, index.html:L960-L1015 -->
- [x] Toast feedback notification system <!-- Implemented in index.html:L632-L640, index.html:L1136-L1145 -->

### Feature 6: Git & GitHub Repository Check-in
- [x] Initialize git repository and configure `.gitignore` <!-- Implemented in .gitignore & local git init -->
- [x] Authenticate GitHub account and verify target profile <!-- Authenticated via gzecheru -->
- [x] Create remote GitHub repository `NexusExpo-Gemini3.8` <!-- Created at https://github.com/gzecheru/NexusExpo-Gemini3.8 -->
- [x] Commit initial codebase (`index.html`, `prd.md`, assets) and push to `main` branch <!-- Pushed to origin/main -->

### Feature 7: Event Management Metadata, Featured Initiatives & Products
- [x] Capture Featured Initiatives (`#cybersecurity`, `#ai`, `#carriers`, `#sovereign cloud`, `#industrial`, `#aerospace&defense`, `#tsn`) in event data model <!-- Implemented in index.html:L650-L870 -->
- [x] Capture Featured Products (`#BreakingPoint`, `#CyberRange`, `#CyPerf`, `#APS-100/400G`, `#AresONE-1600GE`, `#INPT-1600GE`, `#KAI-IB`, `#KAI-DCB`) in event data model <!-- Implemented in index.html:L650-L870 -->
- [x] Comprehensive event management metadata: Booth/Stand #, Priority Tier, Lead Manager, Budget/Investment, and Target Leads <!-- Implemented in index.html:L650-L870 -->
- [x] Strategic Initiatives filter toolbar with active pill highlights <!-- Implemented in index.html:L270-L280, index.html:L886-L905 -->
- [x] Featured Products filter toolbar with active pill highlights <!-- Implemented in index.html:L285-L295, index.html:L906-L925 -->
- [x] Active filter criteria bar displaying applied filters with 1-click clearing <!-- Implemented in index.html:L298-L305, index.html:L926-L945 -->
- [x] Card View initiative & product tag capsules with overflow indicator <!-- Implemented in index.html:L1015-L1035 -->
- [x] Table View initiative & product tag capsules <!-- Implemented in index.html:L1070-L1085 -->
- [x] Detail Modal "Event Management & Logistics" analytics grid (Stand, Budget, Leads, Priority Tier) <!-- Implemented in index.html:L575-L605, index.html:L980-L1000 -->
- [x] "Edit Conference Logistics" workflow enabling real-time edits for any event's metadata, initiatives, and products <!-- Implemented in index.html:L1010-L1050 -->
- [x] Quick-toggle interactive preset buttons for Initiatives and Products inside the Add/Edit form <!-- Implemented in index.html:L420-L480, index.html:L1030-L1060 -->
