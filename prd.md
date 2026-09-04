# Product Requirements Document (PRD) — NexusEvents Dashboard

## Section 1: Vision & Requirements

### 1.1 Product Vision & Overview
**NexusEvents (NexusExpo)** is an enterprise-grade, high-performance web dashboard engineered for event directors, trade show organizers, and corporate attendees to discover, manage, and monitor premier global trade shows and conferences in real time. 

The application combines striking visual aesthetics (frosted glassmorphism, dynamic photographic backdrops, fluid hover micro-interactions) with rich operational capabilities (live search, category filtering, multi-criteria sorting, card grid & spreadsheet table view modes, modal deep dives, bookmarking, and conference publishing workflows).

### 1.2 Target Users
- **Conference Directors & Event Organizers**: Manage conference portfolios, monitor attendee registrations, keynote schedules, and exhibitor booths.
- **Corporate Sponsors & Exhibitors**: Track venue logistics, booth availability, dates, and sector convergence.
- **Attendees & Keynote Speakers**: Discover high-impact trade shows, search by technology tracks, and bookmark upcoming conferences.

### 1.3 Core Requirements
1. **Responsive Modern UI/UX**:
   - Dark-mode first aesthetic built with Tailwind CSS, custom blur filters, and Google Fonts (`Plus Jakarta Sans` & `Inter`).
   - Clean, adaptive layouts supporting Mobile, Tablet, and Desktop viewport resolutions.
2. **Dynamic 9+ Conference Cards**:
   - High-resolution photographic backgrounds with gradient overlay legibility masks.
   - Distinctive frosted glassmorphic category badges with animated shimmer and category-specific Lucide iconography.
   - Comprehensive event metadata: Event Title, Full Venue / City, Timeline / Dates, Registration Status pills, and Key Metrics (Attendees, Speakers, Booths).
3. **Multi-Format Viewports (Cards vs. Table)**:
   - 3x3 Card Grid view with hover zoom (`scale-110`) and action drawers.
   - Compact / Spreadsheet Table view displaying structured columns for fast multi-row scanning.
4. **Live Data Management & CRUD Operations**:
   - Real-time client-side search across conference titles, venues, and topic tracks with `⌘K` keyboard shortcut.
   - Dynamic category filter tabs recalculating counts on the fly.
   - Add New Conference Modal with instant validation, photo presets, metric recalculation, and automatic sorting.
   - Event deletion with confirmation prompts and toast notifications.
   - Interactive Detail Modal with complete topic agendas, venue details, and registration links.

---

## Section 2: Features & Microtasks

### Feature 1: Core Dashboard Layout & Navigation
- [x] Responsive navigation bar with branding, search bar, and user profile avatar <!-- Implemented in index.html:L116-L175 -->
- [x] Executive KPI summary counter (Active Expos, Total Reach, Hubs) with dynamic calculations <!-- Implemented in index.html:L200-L219, index.html:L847-L855 -->
- [x] Ambient glowing backdrop lighting effects <!-- Implemented in index.html:L109-L114 -->
- [x] Global keyboard shortcuts (`⌘K` / `Ctrl+K` for search, `Escape` to close modals) <!-- Implemented in index.html:L1000-L1010 -->

### Feature 2: 9 Conference Cards with Photographic Backgrounds
- [x] Global AI & Robotics Summit 2026 card (San Francisco, CA) <!-- Implemented in index.html:L644-L663, index.html:L734-L814 -->
- [x] FinTech Disrupt World Congress card (London, UK) <!-- Implemented in index.html:L664-L683, index.html:L734-L814 -->
- [x] BioHealth & MedTech International card (Boston, MA) <!-- Implemented in index.html:L684-L703, index.html:L734-L814 -->
- [x] NextGen Auto & Electric Mobility Expo card (Munich, Germany) <!-- Implemented in index.html:L704-L723, index.html:L734-L814 -->
- [x] CleanEnergy & Climate Solutions Expo card (Copenhagen, Denmark) <!-- Implemented in index.html:L724-L743, index.html:L734-L814 -->
- [x] CloudScale & DevOps Architecture Expo card (Seattle, WA) <!-- Implemented in index.html:L744-L763, index.html:L734-L814 -->
- [x] CyberShield Global Defense Forum card (Singapore) <!-- Implemented in index.html:L764-L783, index.html:L734-L814 -->
- [x] DesignOps & Creative Frontiers Summit card (Amsterdam, NL) <!-- Implemented in index.html:L784-L803, index.html:L734-L814 -->
- [x] SpaceTech & Commercial Aerospace Expo card (Houston, TX) <!-- Implemented in index.html:L804-L823, index.html:L734-L814 -->
- [x] Multi-stop dark gradient overlay for text legibility over background photography <!-- Implemented in index.html:L73-L86, index.html:L749-L751 -->
- [x] Glassmorphism category badges with icon and shimmer effect <!-- Implemented in index.html:L67-L71, index.html:L87-L100, index.html:L753-L758 -->

### Feature 3: Live Search, Category Filtering & Sorting
- [x] Instant full-text search across titles, locations, venues, and categories <!-- Implemented in index.html:L139-L146, index.html:L884-L895, index.html:L907-L910 -->
- [x] Dynamic category filter buttons with auto-computed item counts <!-- Implemented in index.html:L226-L229, index.html:L857-L882 -->
- [x] Multi-option sorting (Upcoming date, Furthest date, Attendees count, Alphabetical) <!-- Implemented in index.html:L233-L243, index.html:L896-L903 -->
- [x] Empty state screen with one-click filter reset <!-- Implemented in index.html:L285-L295, index.html:L930-L936 -->

### Feature 4: Table / Spreadsheet View Format
- [x] View switcher toggle (Cards Grid vs. Table View) <!-- Implemented in index.html:L245-L256, index.html:L917-L928 -->
- [x] Responsive glassmorphic table structure with hover row highlight <!-- Implemented in index.html:L263-L283, index.html:L817-L898 -->
- [x] Table columns for Event Thumbnail, Category, Location, Dates, Status, Metrics, and Row Actions <!-- Implemented in index.html:L818-L897 -->
- [x] Direct modal trigger, bookmarking, and deletion controls from table rows <!-- Implemented in index.html:L869-L893 -->

### Feature 5: Event Creation & Modal Management
- [x] "Add Conference" modal with form validation <!-- Implemented in index.html:L298-L460 -->
- [x] Curated high-res photographic background presets <!-- Implemented in index.html:L406-L425, index.html:L967-L969 -->
- [x] Dynamic KPI recalculation and real-time state insertion on submission <!-- Implemented in index.html:L971-L1022 -->
- [x] Conference detail deep-dive modal (description, agenda topics, speakers, booths) <!-- Implemented in index.html:L463-L545, index.html:L1024-L1066 -->
- [x] Toast feedback notification system <!-- Implemented in index.html:L548-L557, index.html:L1084-L1095 -->

### Feature 6: Git & GitHub Repository Check-in
- [ ] Initialize git repository and configure `.gitignore`
- [ ] Authenticate GitHub account and verify target profile
- [ ] Create remote GitHub repository `NexusExpo-Gemini3.8`
- [ ] Commit initial codebase (`index.html`, `prd.md`, assets) and push to `main` branch
