# Story 3.2: Course Detail Page

Status: ready-for-dev

## Story

As a Learner,
I want to view detailed information about a specific course, including its syllabus and preview,
so that I can decide whether to enroll.

## Acceptance Criteria

1. **Course Info Header**:
   - Display Title, description, instructor bio, JLPT targets.
   - Show "Enroll now" or "Go to Course" (if already enrolled) button (sticky on mobile).
   - Show price and enrollment count.

2. **Syllabus / Curriculum List**:
   - List modules/lessons hierarchy.
   - Indicate video duration for VOD.
   - Indicate schedule for Live Classes.
   - Allow expanding/collapsing sections.

3. **Preview**:
   - Allow playing a preview video (if available) without enrollment.
   - List "Free Preview" lessons.

4. **Reviews/Ratings**:
   - Show aggregate rating and user reviews summary.

5. **Cross-Platform**:
   - Web: Wide layout with side panel for metadata.
   - Mobile: Vertical scroll with bottom action bar for Enrollment.

## Tasks / Subtasks

- [ ] Implement Course Detail API
  - [ ] GET `/api/v1/courses/:id`
  - [ ] GET `/api/v1/courses/:id/curriculum`
- [ ] Build Course Structure UI
  - [ ] Web: `components/courses/course-curriculum.tsx` (Accordion)
  - [ ] Mobile: `lib/features/courses/widgets/course_syllabus.dart` (ExpansionTile)
- [ ] Implement Hero/Header Section
  - [ ] Video player integration for preview (basic html5 video or specialized player).
- [ ] Handle Enrollment State
  - [ ] Check if user owns course -> "Go to Learning"
  - [ ] If not -> "Buy Now" (Links to Payment flow - Story 3-4)

## Dev Notes

### Technical Requirements
- **Web**: `app/courses/[slug]/page.tsx`
- **Mobile**: `CourseDetailScreen` with `SliverAppBar`.
- **Routing**: Support deep links `/courses/:id`.

### Architecture Compliance
- Use `Course` and `Lesson` entities.
- Re-use `VideoPlayer` component (Story 4-1) if available, or simple preview player for now.

### References
- PRD FR1, FR2.
