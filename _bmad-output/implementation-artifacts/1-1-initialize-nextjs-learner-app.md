# Story 1.1: Initialize Next.js Learner App

Status: ready-for-dev

<!-- Note: Validation is optional. Run validate-create-story for quality check before dev-story. -->

## Story

As a developer,
I want to initialize the Next.js 15 learner app with shadcn/ui,
so that we have a production-ready foundation for the learner-facing web application.

## Acceptance Criteria

1. **Next.js 15 Project Created**
   - Next.js 15 installed with App Router enabled
   - TypeScript strict mode configured
   - Tailwind CSS 4 integrated
   - ESLint with Next.js recommended rules
   - Turbopack enabled for development builds
   - src/ directory structure in place

2. **shadcn/ui Configured**
   - shadcn/ui initialized with default configuration
   - Base color: Slate
   - CSS variables enabled for theming
   - Dark mode support configured
   - Initial components added: button, card, input, dialog, table, tabs

3. **Project Structure Established**
   - `src/app/` - App Router pages and layouts
   - `src/components/` - Reusable React components
   - `src/lib/` - Utility functions and helpers
   - `public/` - Static assets
   - Component aliases configured (@/components, @/lib/utils)

4. **Development Environment Working**
   - `npm run dev` starts development server successfully
   - Hot Module Replacement (HMR) working with Turbopack
   - TypeScript IntelliSense functioning
   - ESLint running without errors
   - Build command (`npm run build`) completes successfully

5. **Environment Configuration**
   - `.env.local` template created for local development
   - `.env.example` documented with required variables
   - Environment variable types defined in TypeScript

6. **Documentation**
   - README.md updated with project setup instructions
   - Development workflow documented
   - Available scripts documented

## Tasks / Subtasks

- [ ] **Task 1: Initialize Next.js 15 Project** (AC: #1)
  - [ ] Run `npx create-next-app@latest` with recommended options
  - [ ] Configure TypeScript with strict mode
  - [ ] Verify Tailwind CSS integration
  - [ ] Enable Turbopack for development
  - [ ] Set up import aliases (@/*)

- [ ] **Task 2: Install and Configure shadcn/ui** (AC: #2)
  - [ ] Run `npx shadcn@latest init`
  - [ ] Configure shadcn/ui with Slate base color
  - [ ] Enable CSS variables for theming
  - [ ] Set up dark mode support
  - [ ] Add initial components (button, card, input, dialog, table, tabs)

- [ ] **Task 3: Establish Project Structure** (AC: #3)
  - [ ] Create src/app/ directory structure
  - [ ] Create src/components/ for reusable components
  - [ ] Create src/lib/ for utilities
  - [ ] Set up component aliases in tsconfig.json
  - [ ] Create public/ directory for static assets

- [ ] **Task 4: Configure Development Environment** (AC: #4)
  - [ ] Test development server startup
  - [ ] Verify HMR with Turbopack
  - [ ] Configure ESLint rules
  - [ ] Test production build
  - [ ] Verify TypeScript compilation

- [ ] **Task 5: Set Up Environment Configuration** (AC: #5)
  - [ ] Create .env.local template
  - [ ] Create .env.example with documentation
  - [ ] Define environment variable types
  - [ ] Add .env* to .gitignore

- [ ] **Task 6: Documentation** (AC: #6)
  - [ ] Update README.md with setup instructions
  - [ ] Document development workflow
  - [ ] Document available npm scripts
  - [ ] Add architecture notes

## Dev Notes

### Architecture Context

**Project:** torii-nihongo - Japanese Language Learning Platform (EdTech)  
**Epic:** Foundation & Project Initialization  
**Application Type:** Server-Side Rendered Web Application (Learner-Facing)

**Technology Stack (from Architecture Document):**
- **Framework:** Next.js 15 with App Router
- **Language:** TypeScript (strict mode)
- **Styling:** Tailwind CSS 4 + shadcn/ui components
- **Build Tool:** Turbopack (development), Webpack (production)
- **State Management:** Zustand (lightweight, SSR-friendly) - to be added in future stories
- **Server State:** TanStack Query - to be added in future stories
- **HTTP Client:** Axios with interceptors - to be added in future stories

**Why Next.js 15 for Learner App:**
- **SEO-Friendly:** Server-side rendering for course catalog and discovery pages
- **Performance:** Turbopack provides 700x faster builds than Webpack for development
- **Type Safety:** Full TypeScript integration with Next.js and shadcn/ui
- **Modern Tooling:** App Router with Server Components by default
- **Scalability:** Supports complex routing patterns needed for multi-role UI

[Source: _bmad-output/planning-artifacts/architecture.md#Starter Template Evaluation]

### Technical Requirements

**Initialization Command (from Architecture):**
```bash
npx create-next-app@latest torii-web-learner \
  --typescript \
  --tailwind \
  --eslint \
  --app \
  --src-dir \
  --turbopack \
  --import-alias "@/*"
```

**shadcn/ui Configuration:**
```bash
npx shadcn@latest init

# Configuration options:
# - TypeScript: Yes
# - Style: Default (or New York based on preference)
# - Base color: Slate
# - Global CSS: src/app/globals.css
# - CSS variables: Yes
# - Tailwind config: tailwind.config.ts
# - Components alias: @/components
# - Utils alias: @/lib/utils

# Add initial components
npx shadcn@latest add button card input dialog table tabs
```

[Source: _bmad-output/planning-artifacts/architecture.md#Selected Starter: Next.js 15 + shadcn/ui]

### Project Structure Requirements

**Directory Organization:**
```
torii-web-learner/
├── src/
│   ├── app/              # App Router pages and layouts
│   │   ├── layout.tsx    # Root layout
│   │   ├── page.tsx      # Home page
│   │   └── globals.css   # Global styles
│   ├── components/       # Reusable React components
│   │   └── ui/           # shadcn/ui components
│   ├── lib/              # Utility functions and helpers
│   │   └── utils.ts      # shadcn/ui utility functions
│   └── types/            # TypeScript type definitions (future)
├── public/               # Static assets
├── .env.local            # Local environment variables
├── .env.example          # Environment variable template
├── next.config.js        # Next.js configuration
├── tailwind.config.ts    # Tailwind CSS configuration
├── tsconfig.json         # TypeScript configuration
├── package.json          # Dependencies and scripts
└── README.md             # Project documentation
```

[Source: _bmad-output/planning-artifacts/architecture.md#Code Organization]

### Environment Variables

**Required Environment Variables (Initial Setup):**
```env
# API Configuration (to be used in future stories)
NEXT_PUBLIC_API_URL=http://localhost:3000/api
NEXT_PUBLIC_API_GATEWAY_URL=http://localhost:4000

# Environment
NODE_ENV=development
```

**Note:** More environment variables will be added in future stories for:
- Authentication (JWT tokens)
- VNPay payment integration
- LiveKit WebRTC
- NATS real-time communication
- MinIO/S3 storage

[Source: _bmad-output/planning-artifacts/architecture.md#Environment Configuration]

### Performance Targets

**Page Load Performance (from NFRs):**
- Initial page load: <2s (web)
- Time to Interactive (TTI): <3s
- First Contentful Paint (FCP): <1s
- Largest Contentful Paint (LCP): <2.5s

**Build Performance:**
- Development server startup: <1s (with Turbopack)
- Hot Module Replacement: <50ms
- Production build: <2 minutes

[Source: _bmad-output/planning-artifacts/architecture.md#Performance Optimization]

### Design System Integration

**shadcn/ui Components:**
- Built on Radix UI primitives for accessibility (WCAG 2.1 AA compliance)
- Copy-paste components (not npm dependency) for full ownership
- CSS variables for theming (supports dark mode)
- Tailwind CSS utility classes for styling

**Initial Components to Add:**
1. **button** - Primary UI interaction
2. **card** - Course cards, content containers
3. **input** - Form inputs (search, login, etc.)
4. **dialog** - Modals for enrollment, confirmations
5. **table** - Data display (course lists, progress)
6. **tabs** - Navigation (course sections, profile tabs)

**Future Components (in subsequent stories):**
- dropdown-menu, select, checkbox, radio-group (forms)
- badge, avatar, progress (UI elements)
- toast, alert (notifications)
- calendar, date-picker (scheduling)

[Source: _bmad-output/planning-artifacts/architecture.md#Component Architecture]

### Testing Standards

**Testing Requirements (from NFRs):**
- Unit test coverage: >60% (graduation requirement)
- Integration tests for critical flows
- E2E tests for user journeys

**Testing Setup (Future Stories):**
- **Unit Tests:** Jest + React Testing Library
- **E2E Tests:** Playwright or Cypress
- **Component Tests:** Storybook (optional)

**Note:** Testing infrastructure will be set up in Story 1.4 (Set Up CI/CD Pipelines)

[Source: _bmad-output/planning-artifacts/architecture.md#Testing Strategy]

### Accessibility Requirements

**WCAG 2.1 AA Compliance:**
- Keyboard navigation for all interactive elements
- Screen reader support (ARIA labels, semantic HTML)
- Color contrast ratios meeting AA standards
- Focus indicators visible
- Skip-to-content links

**shadcn/ui Accessibility:**
- Radix UI primitives ensure baseline accessibility
- All components have proper ARIA attributes
- Keyboard navigation built-in

[Source: _bmad-output/planning-artifacts/architecture.md#Accessibility & Internationalization]

### Cross-Platform Consistency

**Design Token Synchronization:**
- Tailwind config will define shared design tokens (colors, typography, spacing)
- These tokens must match Flutter mobile app theme
- Document design tokens for future reference

**Component Naming Conventions:**
- Use consistent naming across web and mobile
- Example: `CourseCard` (web) ↔ `CourseCard` (Flutter)

[Source: _bmad-output/planning-artifacts/architecture.md#Cross-Platform Consistency Strategy]

### Security Considerations

**Initial Security Setup:**
- TypeScript strict mode for type safety
- ESLint security rules enabled
- No sensitive data in client-side code
- Environment variables properly scoped (NEXT_PUBLIC_ prefix for client-side)

**Future Security Enhancements (in Auth stories):**
- Content Security Policy (CSP) headers
- CSRF protection
- XSS prevention
- Rate limiting

[Source: _bmad-output/planning-artifacts/architecture.md#API Security]

### References

**Primary Source Documents:**
1. [Architecture Document: _bmad-output/planning-artifacts/architecture.md]
   - Section: "Starter Template Evaluation"
   - Section: "Selected Starter: Next.js 15 + shadcn/ui (Learner App)"
   - Section: "Frontend Architecture"
   - Section: "Infrastructure & Deployment"

2. [PRD: _bmad-output/planning-artifacts/prd.md]
   - Section: "Learner Experience (Web & Mobile)"
   - Section: "Non-Functional Requirements"

3. [Epics & Stories: _bmad-output/planning-artifacts/epics.md]
   - Epic 1: Foundation & Project Initialization
   - Story 1.1: Initialize Next.js Learner App

### Implementation Notes

**Critical Success Factors:**
1. ✅ Use exact initialization commands from architecture document
2. ✅ Enable Turbopack for fast development builds
3. ✅ Configure TypeScript strict mode from the start
4. ✅ Set up shadcn/ui with CSS variables for theming
5. ✅ Verify all scripts work (dev, build, lint)
6. ✅ Document setup process for team members

**Common Pitfalls to Avoid:**
- ❌ Don't skip TypeScript strict mode (causes issues later)
- ❌ Don't forget to add .env* to .gitignore
- ❌ Don't install shadcn/ui components via npm (use copy-paste approach)
- ❌ Don't skip ESLint configuration (code quality issues)
- ❌ Don't forget to test production build

**Verification Checklist:**
- [ ] Development server starts without errors
- [ ] TypeScript compilation succeeds
- [ ] ESLint runs without errors
- [ ] Production build completes successfully
- [ ] shadcn/ui components render correctly
- [ ] Dark mode toggle works
- [ ] HMR updates instantly

### Next Steps After Completion

**Immediate Next Stories:**
1. **Story 1.2:** Initialize Vite Admin/Staff/Meet Apps
2. **Story 1.3:** Initialize Flutter Mobile App
3. **Story 1.4:** Set Up CI/CD Pipelines
4. **Story 1.5:** Configure Monitoring & Logging
5. **Story 1.6:** Set Up Environment Configuration

**Dependencies for Future Stories:**
- **Epic 2 (Authentication):** Will add Axios, TanStack Query, Zustand
- **Epic 3 (Course Discovery):** Will build on this foundation
- **Epic 7 (Live Classes):** Will integrate WebRTC and NATS

## Dev Agent Record

### Agent Model Used

_To be filled by Dev Agent_

### Debug Log References

_To be filled by Dev Agent_

### Completion Notes List

_To be filled by Dev Agent_

### File List

_To be filled by Dev Agent_
