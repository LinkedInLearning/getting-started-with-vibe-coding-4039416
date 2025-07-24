# TurtleRocket Time Twister - Implementation Checklist

## 🚀 Project Setup

### Initial Setup
- [ ] Create new React app with TypeScript: `npx create-react-app turtlerocket-time-twister --template typescript`
- [ ] Install required dependencies: `npm install ical.js @types/ical.js`
- [ ] Install testing utilities if needed: `npm install --save-dev @testing-library/react @testing-library/user-event`
- [ ] Set up folder structure:
  - [ ] Create `src/components/` directory
  - [ ] Create `src/utils/` directory
  - [ ] Create `src/types/` directory
  - [ ] Create `src/config/` directory
  - [ ] Create `src/__tests__/` directory
  - [ ] Create `src/test-utils/` directory

### Git Setup
- [ ] Initialize git repository
- [ ] Create `.gitignore` if not present
- [ ] Make initial commit
- [ ] Set up remote repository (optional)

---

## 📋 Phase 1: Foundation

### Iteration 1.1: Project Initialization
- [ ] Create basic `App.tsx` with "TurtleRocket Time Twister" heading
- [ ] Set up basic CSS with centered container (max-width: 800px)
- [ ] Add subtle box shadow to container
- [ ] Write test: App renders heading correctly
- [ ] Write test: Container has proper styling
- [ ] Ensure all tests pass
- [ ] Commit: "Add basic app structure and styling"

### Iteration 1.2: Core State Structure
- [ ] Create `src/types/index.ts` with TypeScript interfaces:
  - [ ] Define `EnergyLevel` type
  - [ ] Define `CalendarEvent` interface
  - [ ] Define `ClassifiedEvent` interface
  - [ ] Define `OptimizedEvent` interface
  - [ ] Define `AppState` interface
- [ ] Initialize state in `App.tsx`
- [ ] Create `src/utils/stateHelpers.ts`
- [ ] Write test: Initial state has correct defaults
- [ ] Write test: State update functions work correctly
- [ ] Write test: State immutability is maintained
- [ ] Commit: "Add state management and types"

---

## 🔋 Phase 2: Energy Level Input

### Iteration 2.1: Energy Data Model
- [ ] Create `src/types/energy.ts`:
  - [ ] Define `EnergyLevel` type ('low' | 'medium' | 'high')
  - [ ] Define `TimeSlot` interface
  - [ ] Create `EnergyEmoji` constant object
  - [ ] Create `EnergyColors` constant object
- [ ] Create `src/utils/energyHelpers.ts`:
  - [ ] `initializeDefaultEnergy()` function
  - [ ] `updateEnergyLevel()` function
  - [ ] `getEnergyForHour()` function
  - [ ] `resetToDefault()` function
- [ ] Write test: Energy level cycling works
- [ ] Write test: Boundary checking (8 AM - 8 PM)
- [ ] Write test: Default initialization
- [ ] Commit: "Add energy level data model"

### Iteration 2.2: Energy Selector Component
- [ ] Create `src/components/EnergySelector.tsx`
- [ ] Create `src/components/EnergySelector.module.css` (or styled-components)
- [ ] Implement 12 hour blocks (8 AM to 8 PM)
- [ ] Add click interaction to cycle energy levels
- [ ] Display appropriate emoji and colors
- [ ] Add hover effects
- [ ] Write test: Renders 12 hour blocks
- [ ] Write test: Click cycling works
- [ ] Write test: Visual states update
- [ ] Write test: Keyboard navigation
- [ ] Integrate into `App.tsx`
- [ ] Commit: "Add energy selector component"

### Iteration 2.3: Energy Persistence
- [ ] Add "Reset to Default" button
- [ ] Implement reset functionality
- [ ] Add smooth transitions between states
- [ ] Write test: Reset button works
- [ ] Write test: State persistence between re-renders
- [ ] Add visual feedback for interactions
- [ ] Commit: "Add energy persistence and reset"

---

## 📁 Phase 3: File Upload & Parsing

### Iteration 3.1: File Upload Component
- [ ] Create `src/components/FileUpload.tsx`
- [ ] Create `src/components/FileUpload.module.css`
- [ ] Style file input to look nice
- [ ] Accept only `.ics` files
- [ ] Display selected filename
- [ ] Add clear/remove file button
- [ ] Create `src/utils/validation.ts`:
  - [ ] `validateFileType()` function
  - [ ] `validateFileSize()` function
  - [ ] `checkICSFormat()` function
- [ ] Write test: File type validation
- [ ] Write test: File size validation (max 5MB)
- [ ] Write test: Error display
- [ ] Write test: Clear functionality
- [ ] Commit: "Add file upload component"

### Iteration 3.2: ICS Parser
- [ ] Create `src/utils/icsParser.ts`
- [ ] Implement `parseICSFile()` function
- [ ] Extract event properties:
  - [ ] SUMMARY (title)
  - [ ] DTSTART (start time)
  - [ ] DTEND (end time)
  - [ ] UID (unique identifier)
- [ ] Convert to JavaScript Date objects
- [ ] Handle timezone conversions
- [ ] Write test: Valid ICS parsing
- [ ] Write test: Multiple events extraction
- [ ] Write test: Timezone handling
- [ ] Write test: Error handling for malformed files
- [ ] Commit: "Add ICS parser"

---

## 🏷️ Phase 4: Event Classification

### Iteration 4.1: Keyword Configuration
- [ ] Create `src/config/keywords.ts`
- [ ] Define `HEAVY_KEYWORDS` array:
  - [ ] Work-related: meeting, review, presentation, interview
  - [ ] Planning: strategy, planning, roadmap, brainstorm
  - [ ] Analysis: analysis, report, assessment, evaluation
  - [ ] Decision: decision, approval, priority, budget
- [ ] Define `LIGHT_KEYWORDS` array:
  - [ ] Breaks: lunch, break, coffee, snack
  - [ ] Social: birthday, happy hour, team lunch
  - [ ] Personal: gym, workout, appointment
  - [ ] Optional: optional, tentative, hold
- [ ] Organize keywords by category
- [ ] Write test: No keyword conflicts
- [ ] Write test: Comprehensive coverage
- [ ] Commit: "Add keyword configuration"

### Iteration 4.2: Classification Engine
- [ ] Create `src/utils/classifier.ts`
- [ ] Implement `classifyEvent()` function
- [ ] Implement `classifyEvents()` batch function
- [ ] Add `getMatchedKeywords()` for reasoning
- [ ] Support partial word matching
- [ ] Case-insensitive matching
- [ ] Write test: Single keyword matching
- [ ] Write test: Multiple keyword scenarios
- [ ] Write test: Precedence rules (heavy > light)
- [ ] Write test: Edge cases (empty titles)
- [ ] Write test: Performance with many events
- [ ] Commit: "Add classification engine"

---

## 📊 Phase 5: Schedule Optimization

### Iteration 5.1: Optimization Algorithm
- [ ] Create `src/utils/timeSlotMapper.ts`:
  - [ ] `createTimeSlotMap()` function
  - [ ] `getAvailableSlots()` function
  - [ ] `isSlotAvailable()` function
  - [ ] Time utility functions
- [ ] Create `src/utils/optimizer.ts`
- [ ] Implement core algorithm:
  - [ ] Sort events by cognitive load
  - [ ] Match heavy events to high energy
  - [ ] Match light events to low energy
  - [ ] Preserve order within groups
- [ ] Write test: Basic optimization
- [ ] Write test: No suitable slots scenario
- [ ] Write test: Duration preservation
- [ ] Commit: "Add optimization algorithm"

### Iteration 5.2: Schedule Generation
- [ ] Generate optimized schedule
- [ ] Track all movements
- [ ] Calculate displacement metrics
- [ ] Maintain event integrity
- [ ] Handle conflicts (simple overlap check)
- [ ] Write test: Schedule generation
- [ ] Write test: Movement tracking
- [ ] Write test: Metrics calculation
- [ ] Commit: "Add schedule generation"

### Iteration 5.3: Optimization Feedback
- [ ] Calculate optimization statistics:
  - [ ] Number of events moved
  - [ ] Average time displacement
  - [ ] Optimization score
- [ ] Add optimization summary
- [ ] Show improvement indicators
- [ ] Write test: Statistics calculation
- [ ] Write test: Summary generation
- [ ] Commit: "Add optimization feedback"

---

## 📅 Phase 6: Schedule Preview

### Iteration 6.1: Schedule Display Component
- [ ] Create `src/components/ScheduleDisplay.tsx`
- [ ] Create `src/components/ScheduleDisplay.module.css`
- [ ] Implement hourly grid (8 AM - 8 PM)
- [ ] Add hour markers
- [ ] Position events by time
- [ ] Show event duration
- [ ] Apply cognitive load colors
- [ ] Write test: Correct positioning
- [ ] Write test: Event rendering
- [ ] Write test: Empty state
- [ ] Commit: "Add schedule display"

### Iteration 6.2: Comparison View
- [ ] Create `src/components/ScheduleComparison.tsx`
- [ ] Show original vs optimized side-by-side
- [ ] Add movement indicators:
  - [ ] Strikethrough for old times
  - [ ] Bold for new times
  - [ ] Arrows for direction (↑↓)
  - [ ] Time difference labels
- [ ] Write test: Change detection
- [ ] Write test: Movement indicators
- [ ] Write test: Responsive layout
- [ ] Commit: "Add comparison view"

---

## 💾 Phase 7: Export Functionality

### Iteration 7.1: ICS Generation
- [ ] Create `src/utils/icsBuilder.ts`
- [ ] Implement `buildICSFile()` function
- [ ] Add proper ICS headers:
  - [ ] BEGIN:VCALENDAR
  - [ ] VERSION:2.0
  - [ ] PRODID
  - [ ] CALSCALE:GREGORIAN
- [ ] Generate VEVENT for each event
- [ ] Update event times
- [ ] Add X-TURTLEROCKET-OPTIMIZED property
- [ ] Write test: Valid ICS format
- [ ] Write test: Event serialization
- [ ] Write test: Special character escaping
- [ ] Commit: "Add ICS generation"

### Iteration 7.2: Download Implementation
- [ ] Create `src/components/ExportButton.tsx`
- [ ] Create `src/utils/download.ts`
- [ ] Implement file download:
  - [ ] Create blob from ICS
  - [ ] Trigger browser download
  - [ ] Generate filename with timestamp
- [ ] Add loading state
- [ ] Add success feedback
- [ ] Write test: Download trigger
- [ ] Write test: Filename generation
- [ ] Write test: Error handling
- [ ] Commit: "Add download functionality"

### Iteration 7.3: Full Integration
- [ ] Wire export to optimization results
- [ ] Add download button to UI
- [ ] Style as call-to-action
- [ ] Disable during processing
- [ ] Add error notifications
- [ ] Write test: Full export flow
- [ ] Write test: Button states
- [ ] Test with real calendar apps
- [ ] Commit: "Complete export integration"

---

## 🎨 Phase 8: Integration & Polish

### Main Integration
- [ ] Wire all components in `App.tsx`
- [ ] Implement complete data flow:
  - [ ] Energy selection → State
  - [ ] File upload → Parse → State
  - [ ] Classification → State
  - [ ] Optimization → State
  - [ ] Preview → Export
- [ ] Add loading states between steps
- [ ] Add error boundaries
- [ ] Write integration tests
- [ ] Commit: "Complete app integration"

### User Experience
- [ ] Add smooth transitions
- [ ] Implement keyboard shortcuts:
  - [ ] Tab navigation
  - [ ] Enter to confirm
  - [ ] Escape to cancel
- [ ] Add help tooltips
- [ ] Include instructions/guide
- [ ] Add sample ICS file
- [ ] Write test: Keyboard navigation
- [ ] Write test: User flow
- [ ] Commit: "Enhance user experience"

### Visual Polish
- [ ] Add app logo/branding
- [ ] Consistent spacing
- [ ] Professional typography
- [ ] Loading animations
- [ ] Success animations
- [ ] Error state styling
- [ ] Mobile responsiveness
- [ ] Write test: Responsive design
- [ ] Write test: Animation performance
- [ ] Commit: "Visual polish"

---

## 🧪 Phase 9: Comprehensive Testing

### Integration Tests
- [ ] Create `src/__tests__/integration.test.tsx`
- [ ] Test complete user flow
- [ ] Test error scenarios
- [ ] Test edge cases
- [ ] Test state consistency
- [ ] Achieve >90% coverage

### Performance Tests
- [ ] Create `src/__tests__/performance.test.ts`
- [ ] Test with 100+ events
- [ ] Measure parsing speed (<1s for 1000 events)
- [ ] Measure optimization speed (<500ms)
- [ ] Check memory usage
- [ ] Profile React renders

### Accessibility Tests
- [ ] Create `src/__tests__/accessibility.test.tsx`
- [ ] Test screen reader compatibility
- [ ] Test keyboard navigation
- [ ] Test color contrast
- [ ] Test focus management
- [ ] Run axe accessibility audit

### Edge Case Tests
- [ ] Create `src/__tests__/edge-cases.test.ts`
- [ ] Empty calendar files
- [ ] Calendars with no events in range
- [ ] All events at same time
- [ ] Maximum energy scenarios
- [ ] Minimum energy scenarios

### Test Utilities
- [ ] Create mock event generators
- [ ] Create ICS file builders
- [ ] Create custom render functions
- [ ] Create test data sets
- [ ] Document test patterns


---

## 📝 Notes

- Commit after each completed iteration
- Run tests frequently
- Keep commits atomic and descriptive
- Update this checklist as needed
- Take breaks - this is a lot of work!

**Remember**: Each checkbox represents a discrete, testable piece of work. Don't move on until tests are green!
