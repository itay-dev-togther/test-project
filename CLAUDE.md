# Project Context for AI

## Overview
This is a weather dashboard application built for learning purposes. Contributors work on tickets to build features incrementally.

## Architecture

### Directory Structure (planned)
```
src/
├── components/     # React components
│   ├── ui/        # Reusable UI components (Button, Card, etc.)
│   └── features/  # Feature-specific components
├── services/      # API calls and external integrations
├── hooks/         # Custom React hooks
├── types/         # TypeScript type definitions
└── utils/         # Helper functions
```

### Tech Stack
- **Framework:** React 18 with TypeScript
- **Styling:** Tailwind CSS
- **State:** React hooks (useState, useContext)
- **API:** Fetch with async/await

## Coding Conventions

### TypeScript
- Use strict mode
- Define interfaces for all props and data types
- Prefer `interface` over `type` for object shapes
- Use explicit return types on functions

### React Components
- Use functional components with hooks
- Props interface named `{ComponentName}Props`
- One component per file
- Co-locate styles and tests with components

### Naming
- Components: PascalCase (`TemperatureDisplay.tsx`)
- Functions: camelCase (`formatTemperature`)
- Constants: UPPER_SNAKE_CASE (`API_BASE_URL`)
- Files: Match component name or kebab-case for utils

### Styling
- Use Tailwind utility classes
- Keep class lists readable (one per line for long lists)
- Use `cn()` helper for conditional classes

## Example Component

```tsx
interface TemperatureDisplayProps {
  celsius: number;
  showFahrenheit?: boolean;
}

export function TemperatureDisplay({ 
  celsius, 
  showFahrenheit = true 
}: TemperatureDisplayProps): JSX.Element {
  const fahrenheit = (celsius * 9/5) + 32;
  
  return (
    <div className="flex flex-col items-center p-4">
      <span className="text-2xl font-bold">
        {celsius.toFixed(1)}°C
      </span>
      {showFahrenheit && (
        <span className="text-lg text-gray-500">
          {fahrenheit.toFixed(1)}°F
        </span>
      )}
    </div>
  );
}
```

## API Patterns

```tsx
// services/weather.ts
const API_BASE_URL = 'https://api.weather.example.com';

export async function fetchWeather(city: string): Promise<WeatherData> {
  const response = await fetch(`${API_BASE_URL}/weather?city=${city}`);
  if (!response.ok) {
    throw new Error(`Weather API error: ${response.status}`);
  }
  return response.json();
}
```

## Review Priorities

When reviewing PRs, focus on:
1. **Does it work?** - Meets acceptance criteria
2. **Is it typed?** - Proper TypeScript usage
3. **Is it readable?** - Clear naming, comments where needed
4. **Does it fit?** - Follows existing patterns
