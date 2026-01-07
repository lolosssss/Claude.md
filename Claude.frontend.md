# Frontend: TypeScript/JavaScript (Node.js & React)

Language-specific instructions for TypeScript, JavaScript, Node.js, and React development.

## Package Managers

Detect and use the appropriate lock file:
- `package-lock.json` → use `npm`
- `yarn.lock` → use `yarn`
- `pnpm-lock.yaml` → use `pnpm`
- `bun.lockb` → use `bun`

## Common Commands

### Development
- `npm run dev` / `yarn dev` / `pnpm dev` - Start development server
- `npm run build` / `yarn build` / `pnpm build` - Build for production
- `npm run start` / `yarn start` / `pnpm start` - Run production build
- `npm run preview` / `yarn preview` / `pnpm preview` - Preview production build locally

### Type Checking & Linting
- `npm run typecheck` / `yarn typecheck` / `pnpm typecheck` - Run TypeScript type checker
- `npx tsc --noEmit` - Fallback typecheck command
- `npm run lint` / `yarn lint` / `pnpm lint` - Run linter
- `npm run lint:fix` / `yarn lint:fix` / `pnpm lint:fix` - Auto-fix lint issues
- `npm run format` / `yarn format` / `pnpm format` - Format code with Prettier/Biome

### Testing
- `npm test` / `yarn test` / `pnpm test` - Run tests in watch mode
- `npm run test:ci` / `yarn test:ci` / `pnpm test:ci` - Run tests once for CI
- `npm run test:coverage` / `yarn test:coverage` / `pnpm test:coverage` - Generate coverage report

## TypeScript

### Configuration
- Always check `tsconfig.json` for compiler options
- Respect strict mode settings (strictNullChecks, noImplicitAny, etc.)
- Use existing type definitions and avoid `any` unless absolutely necessary

### Type Safety
- Prefer explicit return types on exported functions
- Use interface for object shapes, type for unions/intersections
- Leverage utility types (Partial, Pick, Omit, Record, etc.)
- Use generics for reusable components

### Module Systems
- Prefer ES modules (`import`/`export`) over CommonJS (`require`)
- Use named exports for utilities, default exports for components
- Use path mapping/aliases defined in `tsconfig.json` for clean imports

## React Patterns

### Component Structure
- Prefer function components with hooks over class components
- Use `interface` for props definitions
- Extract custom hooks for reusable logic
- Keep components focused and small (<200 lines when possible)

### State Management
- Use `useState` for local component state
- Use `useReducer` for complex state logic
- Use `useContext` for dependency injection
- For global state, use existing state management (Redux, Zustand, Jotai, etc.)

### Performance
- Use `useMemo` for expensive computations
- Use `useCallback` for functions passed to child components
- Use `React.memo()` for pure components that re-render unnecessarily
- Code-split routes and heavy components with `React.lazy()`

### Common Patterns
- Use early returns to avoid nested conditions
- Destructure props at function signature
- Use conditional rendering with `&&` or ternary, never hide logic with comments
- Avoid inline function/objects in JSX (use `useCallback` or extract)

## Code Quality Tools

### Linting & Formatting
- **ESLint**: Run before committing, respect configuration in `.eslintrc.*`
- **Prettier**: Auto-format on save if configured, check `.prettierrc.*`
- **Biome**: If present, use instead of ESLint/Prettier (faster, all-in-one)

### Type Checking
Always run typecheck before committing significant changes:
```bash
npm run typecheck  # or npx tsc --noEmit
```

## Node.js Best Practices

### Async/Await
- Prefer `async`/`await` over raw promises
- Always handle errors with try/catch or `.catch()`
- Use `Promise.all()` for parallel async operations

### Error Handling
- Never swallow errors silently
- Use Error instances, not strings
- Include stack traces in development
- Sanitize error messages in production

### Dependencies
- Prefer dependencies over devDependencies only if needed at runtime
- Check `package.json` for available scripts before running commands
- Use exact versions in dependencies when required (avoid breaking changes)

## File Conventions

### File Naming
- React components: PascalCase (e.g., `UserProfile.tsx`)
- Utilities: camelCase (e.g., `formatDate.ts`)
- Hooks: camelCase with `use` prefix (e.g., `useAuth.ts`)
- Types: PascalCase with `.types.ts` suffix (e.g., `User.types.ts`)
- Constants: UPPER_SNAKE_CASE (e.g., `API_CONSTANTS.ts`)

### Import Order
1. React/external libraries
2. Internal aliases (if configured)
3. Relative imports
4. Types (separate if using `import type`)
5. CSS/assets (if collocated)

## Testing Patterns

### Unit Tests
- Test behavior, not implementation
- Mock external dependencies (APIs, databases)
- Use descriptive test names (`should return user when valid`)
- Arrange-Act-Assert pattern

### Integration Tests
- Test component interactions
- Use testing library queries (getByRole, getByText)
- Avoid testing implementation details
- Mock API responses with MSW or similar

## Framework-Specific Notes

### Next.js
- Check `next.config.js` for configuration
- Use App Router (app/) or Pages Router based on project structure
- Server Actions: use for mutations, not queries
- Route Handlers: for API endpoints
- Static vs Dynamic rendering: check `use client` directives

### Vite
- Hot Module Replacement (HMR) is automatic
- Environment variables: `import.meta.env.VARIABLE_NAME`
- Check `vite.config.ts` for aliases and plugins

## Build Verification

Before completing work, run in order:
1. Typecheck: `npm run typecheck`
2. Lint: `npm run lint`
3. Tests: `npm test`
4. Build: `npm run build`

If any step fails, fix issues before proceeding.

## When to Ask for Clarification

- Which state management library to use (if not already in use)
- Component architecture for new features
- Whether to use SSR/SSG/CSR for Next.js
- API design patterns (REST vs GraphQL)
- Testing approach for complex interactions
