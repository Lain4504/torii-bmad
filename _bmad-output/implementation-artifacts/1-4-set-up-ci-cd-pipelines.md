# Story 1.4: Set Up CI/CD Pipelines

Status: ready-for-dev

<!-- Note: Validation is optional. Run validate-create-story for quality check before dev-story. -->

## Story

As a developer,
I want set up CI/CD pipelines for all applications,
so that we can automate linting, testing, and deployment to staging and production.

## Acceptance Criteria

1. GitHub Actions workflows configured for all 4 main applications (Next.js Learner, Vite Admin/Staff, Vite Meet, and NestJS Backend).
2. Automated linting, unit testing, and production build checks triggered on every Pull Request to `develop` and `main` branches.
3. Automatic deployment to the Staging environment upon merging to the `develop` branch.
4. Manual approval gate implemented for Production deployments (triggered by merge to `main`).
5. All environment-specific variables and credentials (secrets) managed securely via GitHub Actions Secrets.
6. Build artifacts (e.g., Docker images for backend, static builds for web) are tagged and stored if applicable.

## Tasks / Subtasks

- [ ] **Infrastructure Setup**
  - [ ] Initialize `.github/workflows` directory
  - [ ] Configure GitHub Secrets (API Keys, Deployment Tokens, DB URLs)
- [ ] **Backend (NestJS) Pipeline**
  - [ ] Step: Linting (ESLint)
  - [ ] Step: Unit Tests (Jest)
  - [ ] Step: Build (Production bundle/Docker image)
  - [ ] Step: Deploy to Staging (Auto)
  - [ ] Step: Deploy to Production (Manual Approval)
- [ ] **Web Learner (Next.js 15) Pipeline**
  - [ ] Step: Linting (Next Lint)
  - [ ] Step: Unit Tests (Vitest/Jest)
  - [ ] Step: Production Build (Next Build)
  - [ ] Step: Deploy to Staging (Auto)
- [ ] **Web Admin/Staff/Meet (Vite) Pipeline**
  - [ ] Step: Linting (ESLint)
  - [ ] Step: Production Build (Vite Build)
  - [ ] Step: Deploy to Staging (Auto)
- [ ] **Mobile (Flutter) Pipeline**
  - [ ] Step: Flutter Lint (Analyze)
  - [ ] Step: Flutter Tests
  - [ ] Step: Build APK/IPA (Build check)
- [ ] **Quality Gates**
  - [ ] Configure branch protection rules in GitHub (require PR checks to pass)

## Dev Notes

- **CI Platform:** GitHub Actions is the selected platform (per Architecture Doc).
- **Environments:** Development (local), Staging (cloud), Production (cloud).
- **Backend Deployment:** Likely Docker-based. Ensure `DOCKER_IMAGE_TAG` leverages commit SHA.
- **Web Deployment:** Vercel (for Next.js) and static hosting (S3/CloudFront or Netlify) for Vite apps.
- **Flutter Deployment:** Focus on build verification (IPA/APK generation) for now; continuous delivery to stores will be handled in later epics.
- **Performance:** Use caching for `node_modules` and `flutter` dependencies to speed up runs.

### Project Structure Notes

- Workflows should be modular if possible, but separate files for each app/service is standard for monorepos.
- Ensure `.github/workflows/backend.yml`, `.github/workflows/web-learner.yml`, etc.
- Alignment with `architecture.md` (NFR34: Unit test coverage > 60%).

### References

- [Source: _bmad-output/planning-artifacts/architecture.md#Infrastructure & Deployment]
- [Source: _bmad-output/planning-artifacts/epics-stories-summary.md#Story 1.4]
- [Source: _bmad-output/planning-artifacts/prd.md#Success Criteria]

## Dev Agent Record

### Agent Model Used

Antigravity (Gemini 2.0 Flash)

### Debug Log References

### Completion Notes List

### File List
