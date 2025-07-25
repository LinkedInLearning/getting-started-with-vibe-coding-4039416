# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

TurtleRocket Time Twister is a React-based calendar optimization tool that:
- Imports ICS calendar files from Google Calendar
- Classifies events by cognitive load using keyword matching
- Re-optimizes schedules based on user-defined energy levels throughout the day
- Exports optimized ICS files that can be imported back into calendar applications

## Important Project Structure Rule

**CRITICAL**: ALL project files MUST be created within the `/Users/linkedin/Desktop/Energy/turtlerocket-time-twister/` directory. 
- Never create files in `/Users/linkedin/Desktop/Energy/` directly
- Always use the full path starting with `/Users/linkedin/Desktop/Energy/turtlerocket-time-twister/` when creating or modifying files
- This includes src/, components/, tests, and any other project files

## Common Development Commands

### Initial Setup
```bash
# Create the React app with TypeScript
npx create-react-app turtlerocket-time-twister --template typescript

# Install required dependencies
npm install ical.js @types/ical.js

# Install testing utilities
npm install --save-dev @testing-library/react @testing-library/user-event
```

### Development
```bash
# Start development server
npm start

# Run tests
npm test

# Run tests with coverage
npm test -- --coverage

# Build for production
npm run build

# Run a single test file
npm test -- ScheduleDisplay.test.tsx

# Run tests in watch mode
npm test -- --watchAll
```

### Code Quality
```bash
# Type checking (if TypeScript is configured)
npx tsc --noEmit

# Format code (if prettier is installed)
npx prettier --write src/

# Lint code (if ESLint is configured)
npm run lint
```

## High-Level Architecture

### Core Concepts

1. **Energy-Based Scheduling**: Users define their energy levels (low/medium/high) for each hour from 8 AM to 8 PM. The optimizer matches cognitively demanding tasks to high-energy periods.

2. **Keyword Classification**: Events are classified by cognitive load based on keyword matching:
   - Heavy: meeting, review, presentation, interview, strategy, analysis
   - Light: lunch, break, coffee, gym, social, optional
   - Medium: Everything else (default)

3. **Test-Driven Development**: The blueprint emphasizes TDD - write tests first, then implementation.

### Component Architecture

```
src/
   components/
      EnergySelector.tsx      # Hour blocks for setting energy levels
      FileUpload.tsx          # ICS file input component
      ScheduleDisplay.tsx     # Timeline view of events
      ScheduleComparison.tsx  # Before/after optimization view
      ExportButton.tsx        # Download optimized calendar
   utils/
      classifier.ts           # Event classification logic
      optimizer.ts            # Schedule optimization algorithm
      icsParser.ts           # Parse ICS files using ical.js
      icsBuilder.ts          # Generate ICS files
      energyHelpers.ts       # Energy level management
      timeSlotMapper.ts      # Time slot availability logic
      stateHelpers.ts        # State update utilities
   types/
      index.ts               # Core TypeScript interfaces
      energy.ts              # Energy-related types
      classification.ts      # Classification types
   config/
       keywords.ts            # Keyword configuration
```

### State Management

The app uses React's built-in state management with a central state in App.tsx:

```typescript
{
  energyLevels: Array(12),      // 'low' | 'medium' | 'high' for each hour
  uploadedEvents: [],           // Original parsed events
  classifiedEvents: [],         // Events with cognitive load
  optimizedEvents: [],          // Rescheduled events
  isProcessing: boolean         // Loading state
}
```

### Data Flow

1. User sets energy levels � Updates state
2. User uploads ICS file � Parse with ical.js � Store events
3. Auto-classify events � Add cognitive load property
4. Auto-optimize � Generate new schedule based on energy matching
5. Display preview � Show visual comparison
6. User downloads � Export modified ICS file

## Implementation Guidelines

### Phase-by-Phase Development

The project follows an incremental development approach:
1. Foundation (Project setup, state management, layout)
2. Energy Input (Energy selector component)
3. File Upload & Parsing (ICS handling)
4. Event Classification (Keyword matching)
5. Schedule Optimization (Algorithm implementation)
6. Schedule Preview (Visualization)
7. Export Functionality (ICS generation)
8. Integration & Polish

### Testing Strategy

- Write tests before implementation (TDD)
- Each component should have comprehensive tests
- Target >90% code coverage
- Test categories:
  - Unit tests for utilities
  - Component tests for UI
  - Integration tests for workflows
  - Performance tests for optimization
  - Accessibility tests

### Key Constraints

- Events stay within 8 AM - 8 PM window
- All-day events are skipped
- Single day optimization only (no multi-day support)
- No timezone complexity (use local time)
- Simple overlap checking (no complex conflict resolution)

## Development Tips

1. **Start Small**: Each iteration in the blueprint is designed to be completed incrementally
2. **Test First**: Follow TDD - write failing tests, then make them pass
3. **Preserve State**: Ensure state immutability in all updates
4. **Visual Feedback**: Use emojis (="/=/=�) and colors for energy levels
5. **Error Handling**: Validate ICS files and show clear error messages
6. **Performance**: Optimization should handle 1000+ events in <1 second

## Common Patterns

### Energy Level Cycling
```typescript
const cycleEnergy = (current: EnergyLevel): EnergyLevel => {
  const cycle = { low: 'medium', medium: 'high', high: 'low' };
  return cycle[current];
};
```

### Event Classification
```typescript
// Check title against keywords, heavy takes precedence
if (HEAVY_KEYWORDS.some(keyword => title.toLowerCase().includes(keyword))) {
  return 'heavy';
}
if (LIGHT_KEYWORDS.some(keyword => title.toLowerCase().includes(keyword))) {
  return 'light';
}
return 'medium';
```

### Time Slot Matching
```typescript
// Match events to energy levels
// Heavy events � High energy slots
// Light events � Low energy slots
// Medium events � Medium or remaining slots
```

## Known Edge Cases

- Empty ICS files
- Events outside business hours (8 AM - 8 PM)
- All-day events (should be filtered)
- Malformed ICS data
- Files larger than 5MB
- No available slots for optimization
- Overlapping events in source calendar