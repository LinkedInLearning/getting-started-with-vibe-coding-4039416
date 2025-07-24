# TurtleRocket Time Twister - Implementation Blueprint

## Project Overview
A React-based calendar optimization tool that imports ICS files, classifies events by cognitive load using keyword matching, and re-optimizes schedules based on user-defined energy levels.

## Development Philosophy
- Test-driven development (TDD)
- Incremental progress with no big complexity jumps
- Each step builds on the previous
- No orphaned code
- Early integration testing

---

## Phase-by-Phase Breakdown

### Phase 1: Foundation Setup
**Goal**: Establish project structure with minimal React app and core utilities

#### Iteration 1.1: Project Initialization
- Create React app structure
- Set up testing framework
- Create basic component hierarchy

#### Iteration 1.2: Core State Structure
- Implement app state management
- Create state types/interfaces
- Add state update utilities

#### Iteration 1.3: Basic Layout
- Create main app container
- Add section placeholders
- Implement responsive layout

### Phase 2: Energy Level Input
**Goal**: Allow users to define their energy levels throughout the day

#### Iteration 2.1: Energy Data Model
- Define energy level types
- Create time slot structure
- Implement energy state management

#### Iteration 2.2: Energy Selector Component
- Build hour block components
- Add click interaction
- Implement visual states

#### Iteration 2.3: Energy Persistence
- Add state persistence
- Implement reset functionality
- Create default patterns

### Phase 3: File Upload & Parsing
**Goal**: Import and parse ICS calendar files

#### Iteration 3.1: File Upload Component
- Create file input UI
- Add file validation
- Implement error handling

#### Iteration 3.2: ICS Parser
- Set up ical.js library
- Create parsing utilities
- Extract event data

#### Iteration 3.3: Event Data Model
- Define event structure
- Map ICS data to internal format
- Handle edge cases

### Phase 4: Event Classification
**Goal**: Classify events by cognitive load using keywords

#### Iteration 4.1: Keyword Configuration
- Define keyword sets
- Create classification rules
- Build matching logic

#### Iteration 4.2: Classification Engine
- Implement classification algorithm
- Add test cases
- Handle ambiguous events

#### Iteration 4.3: Classification UI
- Display event classifications
- Add visual indicators
- Show classification reasoning

### Phase 5: Schedule Optimization
**Goal**: Reorganize events based on energy levels

#### Iteration 5.1: Optimization Algorithm
- Create time slot mapping
- Build event placement logic
- Handle constraints

#### Iteration 5.2: Schedule Generation
- Generate optimized schedule
- Track event movements
- Maintain event integrity

#### Iteration 5.3: Optimization Feedback
- Calculate optimization metrics
- Show improvement indicators
- Add optimization summary

### Phase 6: Schedule Preview
**Goal**: Visualize original vs optimized schedule

#### Iteration 6.1: Schedule Display Component
- Create timeline view
- Add event rendering
- Implement hour grid

#### Iteration 6.2: Comparison View
- Show before/after states
- Highlight changes
- Add movement indicators

#### Iteration 6.3: Visual Polish
- Apply classification colors
- Add animations
- Improve readability

### Phase 7: Export Functionality
**Goal**: Export optimized schedule as ICS file

#### Iteration 7.1: ICS Generation
- Create ICS builder utilities
- Map internal data to ICS
- Validate output format

#### Iteration 7.2: Download Implementation
- Add export button
- Implement file download
- Handle browser compatibility

#### Iteration 7.3: Full Integration
- Wire all components together
- Add end-to-end testing
- Polish user flow

---

## Implementation Prompts

### Prompt 1: Project Foundation

```text
Create a new React project for a calendar optimization tool called "TurtleRocket Time Twister". 

Set up the basic project structure with the following requirements:
1. Use Create React App with TypeScript support
2. Install and configure Jest for testing
3. Add the ical.js library for ICS file parsing
4. Create a basic folder structure: src/components, src/utils, src/types
5. Set up a simple App.tsx that displays "TurtleRocket Time Twister" as a heading
6. Add basic CSS with a centered container (max-width: 800px)
7. Create initial test files for App component

Write tests first, then implement:
- Test that App renders the heading
- Test that the container has proper styling
- Ensure all dependencies are properly installed

Make the UI clean and minimal with a white background and subtle shadows.
```

### Prompt 2: State Management Setup

```text
Building on the React project from Prompt 1, implement the core state management for the calendar optimizer.

Create a TypeScript interface for the app state with these properties:
1. energyLevels: An array of 12 energy levels ('low' | 'medium' | 'high') for hours 8 AM to 8 PM
2. uploadedEvents: Array of parsed calendar events
3. classifiedEvents: Array of events with cognitive load classifications
4. optimizedEvents: Array of rescheduled events
5. isProcessing: Boolean flag for loading states

Requirements:
1. Define all TypeScript types/interfaces in src/types/index.ts
2. Initialize state in App.tsx with default values (all energy levels set to 'medium')
3. Create utility functions for state updates in src/utils/stateHelpers.ts
4. Write comprehensive tests for all state operations

Test cases to implement:
- Initial state has correct default values
- State update functions work correctly
- State immutability is maintained
- Type safety is enforced

Keep the implementation simple and focused on state management only.
```

### Prompt 3: Energy Level Types and Model

```text
Extend the project to define the energy level data model and time slot structure.

Create the following in src/types/energy.ts:
1. EnergyLevel type: 'low' | 'medium' | 'high'
2. TimeSlot interface with hour (8-19) and energy level
3. EnergyEmoji constant mapping levels to emojis (🐢, 😐, 🚀)
4. EnergyColors constant mapping levels to color codes

Create src/utils/energyHelpers.ts with:
1. Function to initialize default energy array
2. Function to update energy level at specific hour
3. Function to get energy level for a given hour
4. Function to reset to default pattern

Write tests for:
- Energy level cycling (low → medium → high → low)
- Boundary checking (hours 8-19 only)
- Default initialization
- Reset functionality

Ensure all functions are pure and easily testable.
```

### Prompt 4: Energy Selector Component

```text
Create an EnergySelector component that allows users to set their energy levels for each hour.

Requirements for src/components/EnergySelector.tsx:
1. Display 12 clickable hour blocks (8 AM to 8 PM)
2. Each block shows the hour, energy emoji, and has appropriate background color
3. Clicking a block cycles through energy levels
4. Include a "Reset to Default" button
5. Pass energy levels and update function as props

Styling requirements:
- Use CSS modules or styled components
- Energy level colors: low (#E3F2FD), medium (#FFF9C4), high (#E8F5E9)
- Hover effects on blocks
- Smooth transitions between states

Write tests for:
- Component renders 12 hour blocks
- Click cycling works correctly
- Visual states update properly
- Reset button functionality
- Accessibility (keyboard navigation)

Integrate the component into App.tsx and ensure state updates work correctly.
```

### Prompt 5: File Upload Component

```text
Create a FileUpload component for importing ICS calendar files.

Requirements for src/components/FileUpload.tsx:
1. Styled file input that only accepts .ics files
2. Display selected filename when file is chosen
3. Show loading state during processing
4. Display error messages for invalid files
5. Clear button to remove selected file

Create src/utils/validation.ts with:
1. Function to validate file type
2. Function to validate file size (max 5MB)
3. Function to check basic ICS format

Props interface:
- onFileSelect: (file: File) => void
- isProcessing: boolean
- error: string | null

Write tests for:
- File type validation
- File size validation  
- Error display
- Loading state display
- Clear functionality
- Accessibility

Style as a nice upload area with drag-and-drop visual cues (implementation optional).
```

### Prompt 6: ICS Parser Implementation

```text
Implement ICS file parsing using the ical.js library.

Create src/utils/icsParser.ts with:
1. parseICSFile function that takes file content and returns event array
2. Event interface with: id, title, startTime, endTime, originalStartTime
3. Error handling for malformed ICS files
4. Support for both date-time and date-only events

Requirements:
1. Extract SUMMARY, DTSTART, DTEND, and UID from events
2. Convert times to JavaScript Date objects
3. Filter out all-day events
4. Only include events within 8 AM - 8 PM range
5. Handle timezone conversions to local time

Write comprehensive tests for:
- Valid ICS file parsing
- Multiple event extraction
- Timezone handling
- All-day event filtering
- Time range filtering
- Error cases (malformed files, missing fields)

Integrate with FileUpload component to trigger parsing on file selection.
```

### Prompt 7: Keyword Configuration

```text
Set up the keyword-based classification system for cognitive load assessment.

Create src/config/keywords.ts with:
1. HEAVY_KEYWORDS array (meeting, review, presentation, etc.)
2. LIGHT_KEYWORDS array (lunch, break, coffee, etc.)
3. Keyword categories for better organization
4. Case-insensitive matching configuration

Create src/types/classification.ts with:
1. CognitiveLoad type: 'heavy' | 'medium' | 'light'
2. ClassifiedEvent interface extending base Event with cognitiveLoad property
3. ClassificationResult interface with matched keywords

Requirements:
1. Keywords should be comprehensive but not overlapping
2. Support partial word matching (e.g., "meetings" matches "meeting")
3. Allow for future keyword customization

Write tests for:
- Keyword list completeness
- No keyword conflicts
- Case sensitivity handling
- Partial matching logic

Document the classification strategy clearly in comments.
```

### Prompt 8: Classification Engine

```text
Implement the event classification algorithm using keyword matching.

Create src/utils/classifier.ts with:
1. classifyEvent function that takes an event and returns cognitive load
2. classifyEvents function for batch processing
3. getMatchedKeywords function to show classification reasoning
4. Support for compound keyword matching

Algorithm requirements:
1. Check title against HEAVY_KEYWORDS first
2. Then check LIGHT_KEYWORDS
3. Default to 'medium' if no matches
4. Handle multiple keyword matches (heavy takes precedence)
5. Case-insensitive and partial word matching

Write extensive tests for:
- Single keyword matching
- Multiple keyword scenarios
- Edge cases (empty titles, special characters)
- Precedence rules
- Batch processing performance
- Classification reasoning accuracy

Integrate with the main app flow to classify events after parsing.
```

### Prompt 9: Time Slot Mapping

```text
Create utilities for mapping time slots to energy levels for optimization.

Create src/utils/timeSlotMapper.ts with:
1. TimeSlotMap type for hour-to-energy mapping
2. createTimeSlotMap function from energy array
3. getAvailableSlots function filtered by energy level
4. isSlotAvailable function for checking conflicts
5. Time utility functions for hour manipulation

Requirements:
1. Support 8 AM - 8 PM time range
2. Handle event duration calculations
3. Account for partial hour events
4. Provide slot availability queries

Write tests for:
- Time slot map creation
- Availability checking
- Duration calculations
- Boundary conditions
- Slot conflict detection

This forms the foundation for the optimization algorithm.
```

### Prompt 10: Basic Optimization Algorithm

```text
Implement the core schedule optimization algorithm.

Create src/utils/optimizer.ts with:
1. optimizeSchedule function taking events and energy levels
2. Sort events by cognitive load (heavy → medium → light)
3. Place events in matching energy slots
4. Maintain original time order when possible
5. Track all schedule changes

Algorithm steps:
1. Create slot availability map
2. Group events by cognitive load
3. For each group, find best matching time slots
4. Assign new times while preserving duration
5. Return optimized events with change tracking

Constraints:
- Keep events within 8 AM - 8 PM
- Preserve event duration
- No double-booking (simple overlap check)
- Minimize total time displacement

Write tests for:
- Basic optimization scenarios
- Edge cases (no suitable slots)
- Duration preservation
- Order preservation within groups
- Change tracking accuracy

Return both optimized events and optimization metrics.
```

### Prompt 11: Schedule Display Component

```text
Create a ScheduleDisplay component to show the daily timeline.

Requirements for src/components/ScheduleDisplay.tsx:
1. Hourly grid from 8 AM to 8 PM
2. Event blocks positioned by time
3. Show event title and duration
4. Color coding by cognitive load
5. Responsive width management

Props interface:
- events: Array of events to display
- showEnergyLevels: boolean
- energyLevels: Array of energy levels (optional)

Visual requirements:
- Hour markers on left side
- Event blocks with rounded corners
- Cognitive load colors as left border
- Proper stacking for overlapping events
- Energy level background when enabled

Write tests for:
- Correct time positioning
- Event rendering
- Energy level display
- Empty state handling
- Accessibility features

Style for clarity and easy scanning of the day's events.
```

### Prompt 12: Schedule Comparison View

```text
Extend ScheduleDisplay to show before/after comparison for optimization.

Create src/components/ScheduleComparison.tsx that:
1. Shows original and optimized schedules side by side
2. Highlights moved events
3. Shows time displacement with arrows
4. Displays optimization summary

Features:
1. Original times with strikethrough if moved
2. New times in bold
3. Movement indicators (↑ moved earlier, ↓ moved later)
4. Time difference labels (e.g., "2 hours earlier")
5. Summary stats (events optimized, average displacement)

Visual design:
- Two-column layout on desktop
- Stacked layout on mobile
- Consistent event styling
- Clear visual hierarchy
- Animation for changes (optional)

Write tests for:
- Correct change detection
- Movement indicator logic
- Responsive layout
- Summary calculations
- Accessibility

Integrate both schedule displays into the main app.
```

### Prompt 13: ICS Export Builder

```text
Implement ICS file generation for the optimized schedule.

Create src/utils/icsBuilder.ts with:
1. buildICSFile function taking optimized events
2. Proper ICS format with headers and footers
3. Event serialization with new times
4. VEVENT generation for each event
5. Proper line folding for long lines

ICS requirements:
1. Valid RFC 5545 format
2. Include PRODID and VERSION
3. Preserve original event UIDs
4. Add X-TURTLEROCKET-OPTIMIZED property
5. Handle timezone declarations

Write comprehensive tests for:
- Valid ICS output format
- Event time updates
- Special character escaping
- Line length compliance
- Multi-event files
- Timezone handling

Validate output can be imported into Google Calendar.
```

### Prompt 14: Export and Download

```text
Create the export functionality to download optimized calendars.

Create src/components/ExportButton.tsx with:
1. Download button with icon
2. Loading state during generation
3. Success feedback
4. Error handling
5. Filename with timestamp

Create src/utils/download.ts with:
1. downloadFile function for browser download
2. Blob creation from ICS string
3. Browser compatibility handling
4. Download progress (if supported)

Integration requirements:
1. Generate ICS from optimized events
2. Trigger download with meaningful filename
3. Show success notification
4. Handle errors gracefully
5. Disable during processing

Write tests for:
- ICS generation integration
- Download trigger
- Error scenarios
- Button states
- Filename generation

Style as a prominent call-to-action button.
```

### Prompt 15: Full Integration and Polish

```text
Complete the integration of all components into a cohesive application.

Final integration tasks:
1. Wire all components in App.tsx with proper data flow
2. Add loading states throughout the process
3. Implement error boundaries
4. Add success notifications
5. Ensure smooth user flow

Polish items:
1. Add transitions between states
2. Implement keyboard shortcuts
3. Add help tooltips
4. Include sample ICS file for testing
5. Add app logo/branding

Create src/App.integration.test.tsx with:
1. End-to-end user flow tests
2. File upload → parse → classify → optimize → export
3. Error handling scenarios
4. State consistency checks
5. Performance benchmarks

Final checklist:
- All components integrated
- No orphaned code
- Consistent styling
- Responsive design
- Accessibility compliance
- Performance optimization

The app should feel polished and production-ready.
```

### Prompt 16: Comprehensive Testing Suite

```text
Create a comprehensive testing suite to ensure reliability.

Add the following test files:
1. src/__tests__/integration.test.tsx - Full user workflows
2. src/__tests__/performance.test.ts - Optimization speed
3. src/__tests__/accessibility.test.tsx - A11y compliance
4. src/__tests__/edge-cases.test.ts - Boundary conditions

Test scenarios to cover:
1. Empty calendar files
2. Calendars with 100+ events
3. Events at day boundaries
4. Overlapping events
5. Various keyword combinations
6. Different energy patterns
7. Mobile responsiveness
8. Browser compatibility

Add test utilities in src/test-utils/:
1. Mock event generators
2. ICS file builders
3. Custom render functions
4. Accessibility helpers

Performance benchmarks:
- Parse 1000 events < 1 second
- Optimization < 500ms
- UI remains responsive
- Memory usage reasonable

Achieve >90% code coverage with meaningful tests.
```

---

## Summary

This blueprint provides a comprehensive, iterative approach to building the TurtleRocket Time Twister application. Each prompt builds upon the previous work, ensuring no orphaned code and continuous integration. The steps are sized to be implementable in focused sessions while maintaining test coverage and best practices throughout.

The progression follows a logical flow:
1. **Foundation** - Set up the project and core infrastructure
2. **Input** - Build energy level configuration
3. **Import** - Handle file upload and parsing
4. **Process** - Classify events by cognitive load
5. **Optimize** - Rearrange schedule based on energy
6. **Visualize** - Show the optimization results
7. **Export** - Allow users to save their optimized calendar
8. **Polish** - Integrate everything and add finishing touches

Each prompt includes specific test requirements to ensure robust, reliable code that can be safely extended and maintained.
