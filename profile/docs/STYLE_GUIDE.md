# 📋 Sipheric Code Style Guide

## Overview

This style guide ensures consistency, readability, and maintainability across all Sipheric projects. Following these guidelines helps create a unified codebase that's easy to understand and contribute to.

## 🎯 General Principles

- **Consistency** - Follow established patterns within the project
- **Readability** - Write code that tells a story
- **Simplicity** - Prefer clear, simple solutions over clever ones
- **Performance** - Consider performance implications of your code
- **Documentation** - Document complex logic and public APIs

## 📝 Naming Conventions

### Variables and Functions
```javascript
// Use camelCase for variables and functions
const userPreferences = {};
function calculateTotalPrice() {}

// Use descriptive names
const isUserLoggedIn = true; // Good
const flag = true; // Bad
```

### Constants
```javascript
// Use SCREAMING_SNAKE_CASE for constants
const API_BASE_URL = 'https://api.sipheric.com';
const MAX_RETRY_ATTEMPTS = 3;
```

### Classes and Components
```javascript
// Use PascalCase for classes and React components
class UserManager {}
const UserProfile = () => {};
```

### Files and Directories
```
components/
  UserProfile.jsx
  NavigationBar.jsx
utils/
  api-helpers.js
  date-formatter.js
```

## 🔧 Language-Specific Guidelines

### JavaScript/TypeScript

#### Function Declarations
```javascript
// Prefer arrow functions for short, pure functions
const add = (a, b) => a + b;

// Use function declarations for complex functions
function processUserData(userData) {
  // Complex logic here
  return processedData;
}
```

#### Object and Array Handling
```javascript
// Use destructuring when appropriate
const { name, email } = user;
const [first, second] = items;

// Use spread operator for copying
const newUser = { ...user, isActive: true };
const newItems = [...items, newItem];
```

#### Async/Await
```javascript
// Prefer async/await over promises
async function fetchUserData(userId) {
  try {
    const response = await api.get(`/users/${userId}`);
    return response.data;
  } catch (error) {
    console.error('Failed to fetch user data:', error);
    throw error;
  }
}
```

### React/JSX

#### Component Structure
```jsx
import React, { useState, useEffect } from 'react';
import PropTypes from 'prop-types';

const UserProfile = ({ userId, onUpdate }) => {
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    fetchUser();
  }, [userId]);

  const fetchUser = async () => {
    // Implementation
  };

  if (loading) return <div>Loading...</div>;

  return (
    <div className="user-profile">
      <h2>{user.name}</h2>
      <p>{user.email}</p>
    </div>
  );
};

UserProfile.propTypes = {
  userId: PropTypes.string.isRequired,
  onUpdate: PropTypes.func
};

export default UserProfile;
```

#### Hooks Guidelines
```jsx
// Custom hooks should start with 'use'
const useUserData = (userId) => {
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(true);
  
  // Hook logic
  
  return { user, loading, refetch };
};
```

### CSS/SCSS

#### Class Naming (BEM Methodology)
```css
/* Block */
.user-profile { }

/* Element */
.user-profile__avatar { }
.user-profile__name { }

/* Modifier */
.user-profile--compact { }
.user-profile__avatar--large { }
```

#### Property Order
```css
.component {
  /* Positioning */
  position: relative;
  top: 0;
  left: 0;
  
  /* Display & Box Model */
  display: flex;
  width: 100%;
  height: auto;
  margin: 0;
  padding: 1rem;
  
  /* Typography */
  font-family: 'Arial', sans-serif;
  font-size: 1rem;
  line-height: 1.5;
  
  /* Visual */
  background-color: #fff;
  border: 1px solid #ccc;
  border-radius: 4px;
  
  /* Animation */
  transition: all 0.3s ease;
}
```

## 📊 Code Organization

### File Structure
```
src/
├── components/
│   ├── common/
│   ├── forms/
│   └── layout/
├── hooks/
├── services/
├── utils/
├── styles/
└── tests/
```

### Import Order
```javascript
// 1. External libraries
import React from 'react';
import axios from 'axios';

// 2. Internal utilities and services
import { apiClient } from '../services/api';
import { formatDate } from '../utils/date';

// 3. Components
import Button from '../components/Button';
import Modal from '../components/Modal';

// 4. Styles
import './ComponentName.scss';
```

## 🧪 Testing Guidelines

### Test Structure
```javascript
describe('UserProfile Component', () => {
  beforeEach(() => {
    // Setup
  });

  it('should render user information correctly', () => {
    // Test implementation
  });

  it('should handle loading state', () => {
    // Test implementation
  });
});
```

### Test Naming
- Describe what the test does, not how it does it
- Use "should" statements for clarity
- Group related tests with `describe` blocks

## 🚫 Common Anti-Patterns to Avoid

### JavaScript
```javascript
// Don't use var
var x = 1; // Bad
const x = 1; // Good

// Don't modify function parameters
function updateUser(user) {
  user.lastUpdated = Date.now(); // Bad
}

function updateUser(user) {
  return { ...user, lastUpdated: Date.now() }; // Good
}
```

### React
```jsx
// Don't use array indices as keys
{items.map((item, index) => 
  <Item key={index} data={item} /> // Bad
)}

{items.map(item => 
  <Item key={item.id} data={item} /> // Good
)}
```

## 🔍 Code Review Checklist

- [ ] Code follows naming conventions
- [ ] Functions are small and focused
- [ ] Complex logic is documented
- [ ] Error handling is implemented
- [ ] Tests are included for new features
- [ ] No console.log statements in production code
- [ ] Accessibility considerations are addressed
- [ ] Performance implications are considered

## 🛠️ Tools and Configuration

### ESLint Configuration
```json
{
  "extends": ["@sipheric/eslint-config"],
  "rules": {
    "no-console": "warn",
    "no-unused-vars": "error",
    "prefer-const": "error"
  }
}
```

### Prettier Configuration
```json
{
  "semi": true,
  "trailingComma": "es5",
  "singleQuote": true,
  "printWidth": 80,
  "tabWidth": 2
}
```

## 📚 Resources

- [JavaScript Best Practices](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide)
- [React Documentation](https://reactjs.org/docs)
- [CSS Guidelines](https://cssguidelin.es/)
- [Accessibility Guidelines](https://www.w3.org/WAI/WCAG21/quickref/)

---

*This style guide is a living document. Please contribute improvements and updates as our practices evolve.*
