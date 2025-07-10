# Tomorrow's Portfolio Improvement Plan

## Phase 1: Font System Normalization (30-45 minutes)
1. **Update CSS Variables** in `style.css`:
   - Replace scattered font sizes with consistent scale
   - Implement responsive font system using rem units
   - Add new custom properties for typography hierarchy

2. **Apply Consistent Font Scales** across all pages:
   - Update `index.html` font sizes to use new variables
   - Normalize `cv.html` typography
   - Fix `projects.html` and `about.html` font inconsistencies
   - Ensure proper hierarchy: Hero → Large → Medium → Body → Small

## Phase 2: Profile Photo Scaling Fix (15-20 minutes)
1. **Make Profile Photos Responsive**:
   - Replace fixed `border-width: 10px` with `clamp()` values
   - Implement responsive sizing using `max-width` and viewport units
   - Test scaling behavior across different zoom levels

2. **Update Both Profile Photo Variants**:
   - `.profile-photo` (about.html)
   - `.profile-photo-cv` (cv.html)

## Phase 3: General Scaling Improvements (20-30 minutes)
1. **Review Fixed Pixel Values**:
   - Convert remaining fixed widths to responsive units where appropriate
   - Update project card dimensions to scale properly
   - Ensure consistent spacing across all breakpoints

2. **Test Responsive Behavior**:
   - Verify all elements scale together when zooming
   - Check consistency across different viewport sizes
   - Test navigation menu responsiveness

## Phase 4: Quick Wins & Polish (15-20 minutes)
1. **Contact Details Consistency**:
   - Fix HTML structure mismatch between `<ul>` and `<a>` tags in cv.html
   - Ensure hover effects work properly across all contact links

2. **Final Testing**:
   - Quick review of all 4 pages for visual consistency
   - Test zoom behavior on each page
   - Verify font hierarchy is clear and readable

## Expected Outcome
- **Consistent typography** system across all pages
- **Responsive profile photos** that scale with zoom
- **Professional visual hierarchy** with clear content organization
- **Improved user experience** with better scaling behavior

## Files to Modify
- `style.css` (main changes)
- `cv.html` (minor HTML structure fix)
- Quick verification of `index.html`, `projects.html`, `about.html`

**Total estimated time: 1.5-2 hours**
**Priority: High (affects overall site quality and user experience)**