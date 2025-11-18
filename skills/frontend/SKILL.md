---
name: react-javascript-mastery
description: Master React, modern JavaScript (ES6+), TypeScript, and popular frontend frameworks. Learn state management, hooks, and component design patterns for building scalable user interfaces.
---

# React & Modern JavaScript Mastery

## Quick Start

Learn React fundamentals with hooks and modern patterns:

```javascript
import React, { useState, useEffect } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = `Count: ${count}`;
  }, [count]);

  return (
    <button onClick={() => setCount(count + 1)}>
      Count: {count}
    </button>
  );
}
```

## Core Concepts

### React Fundamentals
- **Components**: Functional and class components
- **JSX**: Syntax and rules
- **Props**: Component communication
- **State**: useState hook and state management
- **Effects**: useEffect hook lifecycle
- **Context**: Global state with Context API

### Modern JavaScript (ES6+)
- Arrow functions and destructuring
- Template literals and spread operator
- Async/await and promises
- Classes and prototypes
- Modules and imports
- Map, filter, reduce patterns

### State Management
- **useState**: Component state
- **useReducer**: Complex state logic
- **Context API**: Global state
- **Redux**: Predictable state management
- **Zustand**: Lightweight state
- **Recoil**: Atomic state

### Hooks Deep Dive
- **Built-in Hooks**: useState, useEffect, useContext, useReducer
- **Custom Hooks**: Creating reusable logic
- **Hook Rules**: Dependencies and cleanup
- **useCallback & useMemo**: Performance optimization
- **useRef**: Direct DOM access

### Component Patterns
- Container vs Presentational components
- Higher-Order Components (HOCs)
- Render props pattern
- Custom hooks pattern
- Compound components
- Controlled vs Uncontrolled

### Performance Optimization
- Code splitting with React.lazy
- Memoization with React.memo
- useCallback for function memoization
- useMemo for computation caching
- Virtual lists (react-window)
- Bundle analysis

### Testing React
- React Testing Library best practices
- Unit testing components
- Testing hooks
- Mocking APIs
- Snapshot testing considerations

## Advanced Topics

### Next.js & Server-Side Rendering
- File-based routing
- SSR (Server-Side Rendering)
- SSG (Static Site Generation)
- API routes
- Image optimization
- Performance metrics

### TypeScript with React
- Typing components
- Props interfaces
- Event typing
- Ref typing
- Generic components
- Utility types

### Styling Solutions
- CSS-in-JS (Styled Components, Emotion)
- Tailwind CSS
- CSS Modules
- BEM methodology
- Responsive design
- Theme management

## Common Patterns

### Authentication Flow
```javascript
const AuthContext = React.createContext();

function AuthProvider({ children }) {
  const [user, setUser] = useState(null);

  const login = async (email, password) => {
    const response = await fetch('/api/login', {
      method: 'POST',
      body: JSON.stringify({ email, password })
    });
    const data = await response.json();
    setUser(data.user);
  };

  return (
    <AuthContext.Provider value={{ user, login }}>
      {children}
    </AuthContext.Provider>
  );
}
```

### Data Fetching Pattern
```javascript
function useApi(url) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    fetch(url)
      .then(res => res.json())
      .then(data => setData(data))
      .catch(err => setError(err))
      .finally(() => setLoading(false));
  }, [url]);

  return { data, loading, error };
}
```

## Learning Resources

- **Official Docs**: react.dev (2023+ React documentation)
- **Interactive Tutorials**: React tutorial exercises
- **Project Ideas**: Build a todo app, GitHub profile viewer, chat application
- **Performance Tips**: React Profiler, Chrome DevTools
- **Community**: React forums, Discord communities

## Best Practices

✅ Use functional components with hooks
✅ Lift state up when needed
✅ Keep components small and focused
✅ Use TypeScript for type safety
✅ Optimize performance with React.memo and hooks
✅ Write tests for critical components
✅ Use error boundaries for error handling
✅ Keep API logic in custom hooks

❌ Don't use index as key in lists
❌ Don't call hooks conditionally
❌ Don't mutate state directly
❌ Don't forget dependencies in useEffect
❌ Don't create new objects in render
❌ Don't ignore performance warnings

## Related Skills
- TypeScript Mastery
- Testing Frameworks
- System Architecture

## Next Steps
Build a React application, master hooks, and explore Next.js for full-stack development.
