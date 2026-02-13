# Ticket 1: Move to Building to start your project

# Agent Instructions  

• Create the initial project setup based on the project description and specifications provided below.  
• Install the necessary libraries and dependencies and make sure that the app runs smoothly with a base minimum setup.  
• Make sure the target architecture is in place but avoid adding boilerplace that it not needed for a base minimum setup.  
• Make sure the essential product components are represented in line with the specified design preferences.  
• If the bare minimum setup requires data, use dummy data from a single file that can be easily modified and removed later.  
• Do not use any external services and make sure no user actions are required, except for approving coding agent actions.  

---

## Project Description

Bird Dog is a mobile-first field sales application integrated with a CRM backend designed for Mad Matter, Inc., a commercial matting company. It targets sales representatives and administrative staff in the commercial matting industry, enabling users to manage accounts, log activities, and capture data in real-time while on the go. Users can search for accounts, take photos, log calls, set reminders, and submit quote requests, all while benefiting from a unified system that scales from a few users to a larger team across multiple markets.

- Mobile-first responsive design
- GPS/location services for target search
- Photo capture linked to property records
- Integrated VoIP for call logging
- Role-based access control
- Offline capability for data capture
- Anomaly detection for data access patterns
- Campaign/email automation integration
- Performance dashboards for tracking activities

---

## Implementation Instructions

**Core Stack**  

• Frontend framework: React 18+ with Vite  
• Language: TypeScript  
• State management: Redux Toolkit  
• Styling: Tailwind CSS  
• Backend: Supabase  
    • Database: Supabase Postgres  
    • Authentication: Supabase Auth  
    • Storage: Supabase Storage  
    • Edge Functions: Supabase Edge Functions  

**Project and Folder Structure**  

Follow this structure exactly. Do not invent new top•level folders.  

src/  
• assets/       static images, icons, fonts (no code)  
• components/   small, stateless, reusable UI pieces  
    • Button/  
    • Card/  
    • Modal/  
    • ... (one folder per component)  
• modules/      larger, stateful sections of the app (pages + logic)  
    • Dashboard/  
    • Projects/  
    • Settings/  
    • Auth/  
• services/     external service wrappers and configuration  
    • supabase.js  
    • stripe.js  
• store/        Redux store and slices  
    • index.ts    configureStore  
    • slices/  
        • authSlice.ts  
        • globalSlice.ts  
        • ... (one slice per feature)  
• utils/        pure functions, helpers, formatters  
    • date.ts  
    • validators.ts  
    • constants.ts  
• App.tsx  
• main.tsx  

Rules:  
• No files directly in src/ except App.tsx and main.tsx  
• Components are dumb UI with no Redux or side effects  
• Modules are smart pages or features that can use Redux, hooks, services  
• Services contain only configuration and API wrappers with no business logic  

**Naming and Coding Conventions**  

• Files and folders: kebab-case for folders (project-list)  
• Components: PascalCase (ProjectCard.tsx)  
• CSS classes: Tailwind utility classes only  
• Variables: camelCase (projectTitle)  
• Constants: UPPER_SNAKE_CASE (MAX_PROJECTS_FREE)  
• Functions: camelCase (fetchProjects, createTicket)  
• Types and Interfaces: PascalCase (Project, TicketPayload)  
• No default exports – always named exports  
• Prefer named imports over default imports  

**State Management Rules**  

• Global state: Redux Toolkit slices only  
• Local component state: useState or useReducer  
• Never use Context API for global state  
• Slices must be feature•based (auth, projects, ui, etc.)  

**Supabase Rules and Patterns**  

• Use Supabase client v2 (modular)  
• Initialize once in services/supabase.ts  
• Use named exports for auth, database, storage, functions  
• Never expose service role keys in frontend  
• Use Row Level Security – users can only read and write their own data  
• Use Edge Functions for:  
    • Stripe webhooks  
    • Monthly usage resets  
    • Sensitive operations  

**Security and Environment**  

• No API keys in frontend code  
• Use Vite environment variables (VITE_...) for public values  
• Use Edge Functions to proxy private keys and sensitive calls  
• Supabase Auth required for all authenticated routes  
• Row Level Security: lock down tables (users can only access own rows)  

**Build and Deployment**  

• Development: npm run dev – Vite dev server  
• Production build: npm run build – outputs to dist/  
• Hosting: Vercel, Netlify, or Supabase Hosting  
• Ignore files: Add to .gitignore  
    • notes.md  
    • *.md  
    • .env  
    • .env.local  

**Project Goals and Non-Negotiables**  

• Scalable to hundreds of users  
• Secure with no key leakage and proper authentication  
• Maintainable with strict folder structure and separation of concerns  
• Fast user experience with optimistic updates where possible  
• Use TypeScript everywhere with strict mode  
• Write clean, readable code

---

## Design Instructions

DESIGN SYSTEM - BIRD DOG FIELD APP
Visual Language: Glassmorphism, mobile-first. Premium feel, not clunky enterprise CRM. Fast, responsive, most important info visible without scrolling.
Glass Effect: Cards use semi-transparent white backgrounds (rgba 255,255,255 at 15-20% opacity), backdrop blur 12-20px, thin 1px border at rgba white 18% opacity, 16px rounded corners. Cards float over a gradient background running from Mad Matter navy (#1B3A5C) through steel blue (#2E6B9E). Depth through layered translucency, not drop shadows.
Color Palette:

Primary: #1B3A5C (nav, headers)
Secondary: #2E6B9E (gradient mid-tone)
Accent: #E8842C (CTAs, points, active states, from Mad Matter brand)
Success: #2ECC71 (above baseline, completed)
Warning: #F39C12 (approaching baseline, follow-up needed)
Danger: #E74C3C (below baseline, overdue)
Text: white on gradients, #1A2332 on glass cards, secondary text at 70% opacity

Typography: Inter or SF Pro system stack. Semi-bold 600 headings, regular 400 body, bold 700 for metrics/numbers. Thin-line icon set (Lucide or Phosphor), not filled.
Key Components:
Points Circle - Circular progress ring top-right of home screen. Gradient stroke (orange to green). Bold number center, small "/ target" below. Subtle glow when above baseline.
Quick Action Buttons - Glass cards in a horizontal row: Photo (+0.5), Call (+1), Visit (+2.5), Quote (+3), $Sale (+5). Icon above, label below, point value as small text. Light haptic on tap.
Performance Bars - Horizontal bars inside glass card. Gradient fills red-to-green based on baseline percentage. Dashed vertical line at 100% marks target. Each metric row represents increasing value top to bottom (photos through sales). Animate in on scroll.
Location Cards - Glass card with colored pin icon, bold property name, secondary address text. Status pill badge: Pending (gray), Follow Up (orange), Urgent (red), Visited (green). Chevron right. Pulsing indicator if stale 12+ months.
Bottom Nav - Frosted glass bar, 4 tabs: Home, Locations, Activity. Floating + button above the bar in solid accent orange. Active tab gets accent color, inactive white/translucent.
Map View - Full-bleed map, glass card overlay at bottom for selected location. Pins color-coded by status. "Near Me" GPS toggle. Pull-up drawer with sortable list.
Interactions: Swipe right on visit card to complete, swipe left to snooze. Pull to refresh. Long press contact to call/email. Camera opens from Photo action with GPS-based property pre-selection. Toast notifications slide from top.
Screen Hierarchy:

Home: points, quick actions, performance snapshot, upcoming visits
Locations: map + list toggle, search, filters
Property Detail: photos, contacts, mat condition, history, tasks, quotes
Activity: call log, tasks due, reminders, feed
Performance: full bar charts (weekly/monthly/quarterly)
Quick Quote: intake form routed to inside rep
Settings: mileage tracker, notifications