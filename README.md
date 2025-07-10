## Plan for Creating Your HTML/CSS CV Page

### **Phase 1: Content Structure Planning**
1. **Define CV Sections** (following standard CV structure):
   - Header with photo and contact info
   - Professional summary
   - Skills section
   - Work experience
   - Education
   - Projects (can reference your existing projects)
   - Optional: Certifications, Languages, etc.

2. **Photo Integration**:
   - Use your existing profile photo from `images/about/dan-isaksson-profile-image.jpg`
   - Create a professional header layout

### **Phase 2: HTML Structure Development**
1. **Create semantic HTML structure** using:
   - `<section>` for each CV section
   - `<article>` for individual experiences/projects
   - `<dl>` (definition lists) for skills
   - `<time>` elements for dates

2. **Maintain consistency** with your existing navigation and footer structure

### **Phase 3: CSS Layout Implementation**
1. **Leverage your existing CSS system**:
   - Use your CSS custom properties (`--font-regular`, `--font-pixel`, etc.)
   - Follow your established color scheme (`--hue-main`, etc.)
   - Maintain the design consistency with your other pages

2. **Create CV-specific layouts**:
   - **Grid-based layout** for the main CV structure
   - **Flexbox** for individual section layouts
   - **Responsive design** using your existing `clamp()` approach

### **Phase 4: Styling Enhancement**
1. **Typography hierarchy**:
   - Use your existing font variables
   - Create clear visual hierarchy for headings
   - Ensure readability for CV content

2. **Visual elements**:
   - Professional photo styling
   - Section dividers
   - Consistent spacing using your existing patterns

### **Phase 5: Content Integration**
1. **Extract information** from your PDF CV
2. **Adapt content** for web presentation
3. **Link to existing projects** from your projects page

Would you like me to start with **Phase 1** and help you outline the content structure first? Or would you prefer to jump into **Phase 2** and start building the HTML structure right away?

Also, I noticed your PDF CV is in the project folder - would you like me to help you extract the key information from it to use in the HTML version?