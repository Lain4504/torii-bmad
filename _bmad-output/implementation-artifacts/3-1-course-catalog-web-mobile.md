# Story 3.1: Course Catalog (Web & Mobile)

Status: ready-for-dev

## Story

As a Learner,
I want to browse and search for courses (VOD and Live) on both web and mobile,
so that I can discover content relevant to my JLPT level and interests.

## Acceptance Criteria

1. **Course Listing**:
   - Display courses in a responsive grid (Web) or list/grid (Mobile).
   - Each course card must show: Thumbnail, Title, Instructor Name, JLPT Level (N5-N1), Type (VOD/Live), Price (or "Free"), and Rating (stars).
   - [Web] Use `shadcn/ui` Card component.
   - [Mobile] Use Material 3 Card widget.

2. **Filtering & Searching**:
   - Filter by JLPT Level (N5, N4, N3, N2, N1).
   - Filter by Course Type (VOD, Live Class).
   - Search bar functionality (search by course title or instructor).
   - Server-side filtering (API query parameters).

3. **Pagination / Infinite Scroll**:
   - [Web] Implement pagination (or infinite scroll if preferred by design).
   - [Mobile] Implement infinite scroll (lazy loading).

4. **Performance**:
   - Initial load < 2s.
   - Images optimized (Next.js Image / Flutter cached network image).

5. **Responsiveness**:
   - Web: Desktop (4 cols), Tablet (2-3 cols), Mobile (1 col).

## Tasks / Subtasks

- [ ] Implement Course Listing API Integration
  - [ ] Define `Course` interface/model (shared DTO).
  - [ ] Implement `useCourses` query (TanStack Query) on Web.
  - [ ] Implement `courseRepository` (Riverpod) on Mobile.
- [ ] Build Course Card Component
  - [ ] Web: `components/courses/course-card.tsx`
  - [ ] Mobile: `lib/features/courses/widgets/course_card.dart`
- [ ] Build Catalog Page
  - [ ] Web: `app/courses/page.tsx` with sidebar filters.
  - [ ] Mobile: `lib/features/courses/views/course_catalog_screen.dart` with filter bottom sheet.
- [ ] Implement Search & Filter Logic
  - [ ] Update URL query params on Web.
  - [ ] Manage filter state on Mobile.

## Dev Notes

### Technical Requirements
- **Web**: Next.js 15 (App Router), Server Components for initial fetch if possible.
- **Mobile**: Flutter, Riverpod for state.
- **API**: GET `/api/v1/courses?page=1&limit=12&level=N5&type=vod&q=...`
- **Images**: Use placeholder if thumbnail missing.

### Architecture Compliance
- **Web**: `src/features/courses` (if feature-based) or `src/components/courses`.
- **Mobile**: `lib/features/courses/`.
- **State**:
  - Web: URL as source of truth for filters.
  - Mobile: `CourseFilterProvider`.

### Complexity
- Image aspect ratios must be consistent.
- Handle "Live Class" specific UI (e.g., "Starting soon" badge).

### References
- PRD FR1
- UX Design Spec: Course Catalog wireframes
