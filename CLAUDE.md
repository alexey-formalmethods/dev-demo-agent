# CLAUDE.md

This file provides comprehensive guidance to Claude Code when working with code in this repository. Follow these instructions as a senior Python engineer to maintain consistency and quality.

## Project Architecture

### Backend Architecture

**Core Stack:**
- **Runtime**: Python 3.9+
- **Framework**: FastAPI (async web framework)
- **Authentication**: JWT (JSON Web Tokens)
- **Database**: PostgreSQL (production) / SQLite (development)
- **ORM**: SQLAlchemy with Alembic migrations
- **Validation**: Pydantic models
- **Testing**: pytest with coverage
- **Code Quality**: black, isort, flake8, mypy

**Project Structure:**
```
backend/
├── app/
│   ├── __init__.py
│   ├── main.py              # FastAPI application entry point
│   ├── core/
│   │   ├── __init__.py
│   │   ├── config.py        # Application configuration
│   │   ├── security.py      # JWT and authentication logic
│   │   └── database.py      # Database connection and session management
│   ├── api/
│   │   ├── __init__.py
│   │   ├── deps.py          # Dependency injection for routes
│   │   └── v1/
│   │       ├── __init__.py
│   │       ├── auth.py      # Authentication endpoints
│   │       └── users.py     # User management endpoints
│   ├── models/
│   │   ├── __init__.py
│   │   ├── base.py          # Base SQLAlchemy model
│   │   └── user.py          # User model
│   ├── schemas/
│   │   ├── __init__.py
│   │   ├── user.py          # Pydantic schemas for users
│   │   └── token.py         # JWT token schemas
│   └── utils/
│       ├── __init__.py
│       └── helpers.py       # Utility functions
├── tests/
│   ├── conftest.py          # pytest configuration and fixtures
│   ├── test_auth.py         # Authentication tests
│   └── test_users.py        # User endpoint tests
├── alembic/                 # Database migrations
├── requirements.txt         # Python dependencies
└── pyproject.toml          # Project configuration
```

### Frontend Architecture

**Core Stack:**
- **Framework**: React 18+ with TypeScript
- **UI Library**: Ant Design (antd)
- **State Management**: Redux Toolkit + RTK Query (for API calls)
- **Routing**: React Router v6
- **Forms**: Ant Design Form + React Hook Form
- **Styling**: CSS Modules + Ant Design theming
- **Build Tool**: Vite
- **Testing**: Jest + React Testing Library
- **Code Quality**: ESLint, Prettier, TypeScript

**Project Structure:**
```
frontend/
├── src/
│   ├── components/
│   │   ├── common/          # Reusable UI components
│   │   ├── layout/          # Layout components
│   │   └── forms/           # Form components
│   ├── pages/
│   │   ├── Auth/            # Login/Register pages
│   │   ├── Dashboard/       # Main dashboard
│   │   └── Profile/         # User profile
│   ├── store/
│   │   ├── index.ts         # Redux store configuration
│   │   ├── authSlice.ts     # Authentication state
│   │   └── api/             # RTK Query API definitions
│   ├── hooks/               # Custom React hooks
│   ├── utils/               # Utility functions
│   ├── types/               # TypeScript type definitions
│   └── styles/              # Global styles and themes
├── public/                  # Static assets
├── tests/
│   ├── components/          # Component tests
│   ├── pages/               # Page tests
│   └── utils/               # Utility tests
├── package.json
└── tsconfig.json
```

## Development Approach

### Memory Bank System

The memory bank system captures institutional knowledge through multiple channels:

**1. Code Documentation:**
- **Functions**: Use Google-style docstrings for all functions
- **Classes**: Document purpose, attributes, and usage examples
- **Modules**: Include module-level docstrings explaining functionality
- **API Endpoints**: OpenAPI/Swagger documentation with examples

**2. Architecture Decision Records (ADRs):**
- Store in `docs/adr/` directory
- Document significant architectural decisions
- Include context, options considered, and rationale

**3. API Documentation:**
- FastAPI automatically generates OpenAPI docs at `/docs`
- Include request/response examples
- Document error responses and status codes

**4. Component Documentation:**
- Storybook for React components (when applicable)
- JSDoc comments for TypeScript interfaces
- Usage examples in component files

### Documentation Standards

**Backend Documentation:**
```python
def authenticate_user(email: str, password: str) -> Optional[User]:
    """
    Authenticate a user with email and password.
    
    Args:
        email (str): User's email address
        password (str): Plain text password
        
    Returns:
        Optional[User]: User object if authentication successful, None otherwise
        
    Raises:
        AuthenticationError: If credentials are invalid
        
    Example:
        user = authenticate_user("user@example.com", "password123")
        if user:
            print(f"Welcome {user.name}")
    """
```

**Frontend Documentation:**
```typescript
/**
 * UserProfile component for displaying and editing user information
 * 
 * @param user - User object containing profile data
 * @param onUpdate - Callback function called when user data is updated
 * @param readonly - Whether the component should be in read-only mode
 * 
 * @example
 * <UserProfile 
 *   user={currentUser} 
 *   onUpdate={handleUserUpdate}
 *   readonly={false}
 * />
 */
interface UserProfileProps {
  user: User;
  onUpdate: (user: User) => void;
  readonly?: boolean;
}
```

### Breadcrumb System for Issue Tracking

Use standardized comment markers to track unresolved issues and technical debt:

**1. Agent Hints:**
```python
# AGENT HINT: This function needs optimization for large datasets
# Current implementation has O(n²) complexity, consider using hash map
```

**2. Technical Debt:**
```typescript
// TODO: Implement proper error boundary for this component
// REQUIRES: React Error Boundary setup in parent component
```

**3. Security Considerations:**
```python
# SECURITY: Validate input parameters to prevent SQL injection
# Current implementation trusts user input - needs sanitization
```

**4. Performance Issues:**
```typescript
// PERFORMANCE: This component re-renders too frequently
// Consider memoization or state optimization
```

**5. Documentation Gaps:**
```python
# DOCS: Add comprehensive docstring explaining the algorithm
# Include complexity analysis and usage examples
```

## Testing Requirements

### Backend Testing (Target: 80% Coverage)

**Test Structure:**
```
tests/
├── unit/
│   ├── test_models.py       # Model unit tests
│   ├── test_services.py     # Business logic tests
│   └── test_utils.py        # Utility function tests
├── integration/
│   ├── test_api.py          # API endpoint tests
│   ├── test_database.py     # Database integration tests
│   └── test_auth.py         # Authentication flow tests
└── e2e/
    └── test_workflows.py    # End-to-end user workflows
```

**Testing Standards:**
- All new functions must have unit tests
- API endpoints require integration tests
- Critical user flows need E2E tests
- Mock external dependencies
- Use factories for test data generation

### Frontend Testing (Target: 70% Coverage)

**Test Structure:**
```
tests/
├── components/
│   ├── __tests__/           # Component unit tests
│   └── __mocks__/           # Component mocks
├── pages/
│   └── __tests__/           # Page integration tests
├── hooks/
│   └── __tests__/           # Custom hook tests
└── e2e/
    └── cypress/             # End-to-end tests
```

**Testing Standards:**
- Component behavior testing with React Testing Library
- User interaction testing with fireEvent/userEvent
- API integration testing with MSW (Mock Service Worker)
- Accessibility testing with jest-axe
- Visual regression testing (when applicable)

## Common Development Commands

### Backend Commands
```bash
# Development
pip install -r requirements.txt
uvicorn app.main:app --reload --host 0.0.0.0 --port 8000

# Database
alembic upgrade head
alembic revision --autogenerate -m "Description"

# Testing
pytest --cov=app tests/
pytest --cov=app --cov-report=html tests/

# Code Quality
black .
isort .
flake8 .
mypy .
```

### Frontend Commands
```bash
# Development
npm install
npm run dev

# Testing
npm test
npm run test:coverage
npm run test:e2e

# Build
npm run build
npm run preview

# Code Quality
npm run lint
npm run format
npm run type-check
```

## Security Guidelines

### Backend Security
- Use JWT tokens with appropriate expiration
- Implement rate limiting on API endpoints
- Validate and sanitize all input data
- Use parameterized queries to prevent SQL injection
- Implement proper CORS configuration
- Hash passwords with bcrypt
- Use HTTPS in production

### Frontend Security
- Sanitize user input to prevent XSS
- Implement CSP (Content Security Policy)
- Validate data from API responses
- Store sensitive data securely (avoid localStorage for tokens)
- Implement proper error handling to avoid information leakage

## Performance Guidelines

### Backend Performance
- Use async/await for I/O operations
- Implement database query optimization
- Use connection pooling
- Implement caching where appropriate (Redis)
- Monitor API response times

### Frontend Performance
- Implement code splitting and lazy loading
- Optimize bundle size with tree shaking
- Use React.memo for expensive components
- Implement proper state management to avoid unnecessary re-renders
- Optimize images and assets

## Branch and PR Strategy

### Branch Naming Convention
```
feature/issue-{number}-{short-description}
bugfix/issue-{number}-{short-description}
hotfix/{short-description}
```

### PR Requirements
- Every change must be in a separate branch
- All tests must pass before merging
- Code coverage must not decrease
- At least one code review required
- Squash commits before merging
- Include issue reference in PR description

### Commit Message Format
```
type(scope): description

Body explaining the change

Closes #issue-number
```

## Error Handling

### Backend Error Handling
```python
from fastapi import HTTPException, status

class UserNotFoundError(Exception):
    """Raised when user is not found"""
    pass

@app.exception_handler(UserNotFoundError)
async def user_not_found_handler(request, exc):
    raise HTTPException(
        status_code=status.HTTP_404_NOT_FOUND,
        detail="User not found"
    )
```

### Frontend Error Handling
```typescript
// Error boundary for component tree
class ErrorBoundary extends React.Component {
  // Implementation for catching React errors
}

// API error handling
const handleApiError = (error: any) => {
  if (error.response?.status === 401) {
    // Handle authentication error
  } else if (error.response?.status >= 500) {
    // Handle server error
  }
};
```

## Development Workflow

1. **Issue Assignment**: Every task starts with a GitHub issue
2. **Branch Creation**: Create feature branch from main
3. **Development**: Implement changes following guidelines
4. **Testing**: Ensure all tests pass and coverage targets met
5. **Documentation**: Update relevant documentation
6. **Code Review**: Submit PR for review
7. **Merge**: Squash and merge after approval

Remember: Act as a senior Python engineer - prioritize code quality, maintainability, security, and comprehensive testing throughout the development process.