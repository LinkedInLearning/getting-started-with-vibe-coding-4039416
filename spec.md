# TurtleRocket Time Twister (Minimal Version) - Technical Specification

## 1. Project Overview
A single-page React application that imports Google Calendar ICS files, classifies events by cognitive load using keyword matching, and re-optimizes the schedule based on user-defined energy levels throughout the day. The app exports an optimized ICS file that can be imported back into Google Calendar.

## 2. Core Features (30-Minute Build)

### 2.1 Energy Curve Input (10 minutes to implement)
#### Simple Click-Based Interface
- **Time Range**: Fixed 8 AM - 8 PM (12 hours)
- **Interaction**: Click on hour blocks to cycle through energy levels
- **Visual States**:
  - Low Energy: 🐢 with light blue background
  - Medium Energy: 😐 with light yellow background  
  - High Energy: 🚀 with light green background
- **Default**: All hours start at Medium energy
- **Storage**: Simple array of 12 values: `['medium', 'medium', 'high', ...]`

### 2.2 ICS File Upload (5 minutes to implement)
#### Minimal Upload Interface
- **Component**: Basic file input with styled button
- **Accepted Type**: `.ics` files only
- **Processing**: Use browser FileReader API
- **Library**: `ical.js` (lightweight, works in browser)
- **Extract Only**:
  - Event title (SUMMARY)
  - Start time (DTSTART)
  - End time (DTEND)
  - UID (for tracking)

### 2.3 Keyword-Based Classification (5 minutes to implement)
#### Classification Rules
```javascript
const HEAVY_KEYWORDS = [
  'meeting', 'review', 'presentation', 'interview', 'planning',
  'strategy', 'analysis', 'report', 'budget', 'decision',
  'brainstorm', 'workshop', 'training', 'evaluation'
];

const LIGHT_KEYWORDS = [
  'lunch', 'break', 'coffee', 'walk', 'gym', 'social',
  'birthday', 'chat', 'casual', 'optional', 'tentative'
];
```

**Logic**:
1. Check event title for heavy keywords → classify as "heavy"
2. Check for light keywords → classify as "light"
3. Default to "medium" if no keywords match
4. Case-insensitive matching

### 2.4 Simple Optimization Algorithm (5 minutes to implement)
#### Placement Strategy
1. **Sort events** by cognitive load (heavy → medium → light)
2. **Place heavy events** in high-energy time slots first
3. **Place medium events** in medium or remaining high slots
4. **Place light events** in low-energy slots or any remaining
5. **Maintain original order** when possible within same category

#### Constraints
- Events stay within 8 AM - 8 PM window
- No overlap checking (simplified)
- Round start times to nearest hour
- Preserve event duration

### 2.5 Visual Schedule Preview (3 minutes to implement)
#### Simple Day View
- **Layout**: Single column with hourly rows (8 AM - 8 PM)
- **Event Display**:
  - Colored blocks showing event title
  - Original time crossed out if moved
  - New time in bold
  - Energy emoji indicator
- **Interaction**: None (static preview)

### 2.6 ICS Export (2 minutes to implement)
#### Download Optimized Calendar
- **Button**: "Download Optimized Calendar"
- **Filename**: `optimized-calendar.ics`
- **Method**: Create blob and trigger download
- **Content**: Basic ICS with updated times

## 3. Technical Implementation

### 3.1 Dependencies (Minimal)
```json
{
  "dependencies": {
    "react": "^18.0.0",
    "ical.js": "^1.5.0"
  }
}
```

### 3.2 Component Structure (Simplified)
```
src/
├── App.jsx                    # Main app component
├── components/
│   ├── EnergySelector.jsx    # Click-to-set energy levels
│   ├── FileUpload.jsx        # ICS file input
│   ├── SchedulePreview.jsx   # Before/after view
│   └── ExportButton.jsx      # Download ICS
└── utils/
    ├── classifier.js         # Keyword matching logic
    ├── optimizer.js          # Simple scheduling algorithm
    └── icsHelpers.js         # Parse and generate ICS
```

### 3.3 State Structure
```javascript
const [appState, setAppState] = useState({
  energyLevels: Array(12).fill('medium'), // 8 AM to 8 PM
  uploadedEvents: [],                      // Original events
  classifiedEvents: [],                    // Events with load levels
  optimizedEvents: [],                     // Rescheduled events
  isProcessing: false
});
```

## 4. Implementation Steps (30 minutes)

### Step 1: Energy Selector (5 min)
- Create grid of 12 hour blocks
- onClick cycles through low → medium → high
- Display emoji and background color
- Store in state array

### Step 2: File Upload (5 min)
- Styled file input button
- FileReader to get text content
- Parse with ical.js
- Extract basic event properties
- Store in state

### Step 3: Event Classification (5 min)
- Loop through events
- Check title against keyword arrays
- Assign cognitive load level
- Add classification to event objects

### Step 4: Schedule Optimization (5 min)
- Create time slot availability map from energy levels
- Sort events by cognitive load
- Place events in matching energy slots
- Maintain list of changes

### Step 5: Preview Display (5 min)
- Show hourly grid 8 AM - 8 PM
- Display events as colored blocks
- Show original vs new times
- Use strikethrough for moved events

### Step 6: Export Function (5 min)
- Generate ICS string with new times
- Create blob from string
- Trigger browser download
- Use simple ICS template

## 5. Styling Guidelines (Minimal CSS)

### 5.1 Layout
- Single centered column (max-width: 800px)
- White background with subtle shadows
- Clear section separation

### 5.2 Energy Level Colors
```css
.energy-low { background: #E3F2FD; }    /* Light blue */
.energy-medium { background: #FFF9C4; }  /* Light yellow */
.energy-high { background: #E8F5E9; }    /* Light green */
```

### 5.3 Event Classification Colors
```css
.event-heavy { border-left: 4px solid #F44336; }   /* Red */
.event-medium { border-left: 4px solid #FF9800; }  /* Orange */
.event-light { border-left: 4px solid #4CAF50; }   /* Green */
```

## 6. Data Flow

1. **User sets energy levels** → Updates state array
2. **User uploads ICS** → Parse and store events
3. **Auto-classify events** → Add cognitive load property
4. **Auto-optimize** → Generate new schedule
5. **Display preview** → Show changes visually
6. **User downloads** → Export modified ICS

## 7. Edge Cases to Handle

### 7.1 Required Handling
- Empty ICS file → Show error message
- Events outside 8 AM - 8 PM → Keep at original time
- All-day events → Skip optimization
- Invalid file type → Show error on upload

### 7.2 Simplified Assumptions
- Single day optimization only
- No recurring events support
- No timezone handling (use local time)
- No conflict resolution
- No manual adjustments

## 8. Sample Classification Keywords

### Heavy Cognitive Load
- Work: meeting, presentation, review, interview
- Planning: strategy, planning, roadmap, brainstorm
- Analysis: analysis, report, assessment, evaluation
- Decision: decision, approval, priority, budget

### Light Cognitive Load  
- Breaks: lunch, break, coffee, snack
- Social: birthday, happy hour, team lunch, coffee chat
- Personal: gym, workout, appointment, errand
- Optional: optional, tentative, hold, buffer

## 9. Quick Testing Checklist

1. ✓ Energy selector cycles through all three states
2. ✓ File upload accepts only .ics files
3. ✓ Events display with correct classification
4. ✓ Heavy events move to high-energy times
5. ✓ Light events move to low-energy times
6. ✓ Download produces valid .ics file

## 10. Extensions (If Time Permits)

### 10.1 Quick Wins (5 minutes each)
- Add "Reset to Defaults" button for energy levels
- Show count of optimized events
- Add loading spinner during processing
- Include time shift amount (e.g., "Moved 2 hours earlier")

### 10.2 Nice-to-Haves (10 minutes each)
- Drag-and-drop file upload
- Multiple day support
- Custom keyword configuration
- Undo/redo functionality

---

This minimal specification focuses on building a functional calendar optimizer in 30 minutes, using keyword-based classification instead of AI, and keeping everything client-side for simplicity.
