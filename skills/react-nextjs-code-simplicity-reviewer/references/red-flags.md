# Red Flags: Complexity Patterns to Catch

## 1. Unnecessary Dependencies (Strongly Recommend)

**Pattern:** Adding a new package to `package.json`

**Questions to ask:**
- Can this be done in <50 lines of code?
- Is the package actively maintained?
- How many transitive dependencies does it bring?
- Is it solving a real problem or just saving 10 minutes?

**Examples of unnecessary deps:**
- `lodash` for one utility function — write it yourself
- `classnames` — template literals work fine: `` `${base} ${active && 'active'}` ``
- `moment`/`dayjs` for simple formatting — use `Intl.DateTimeFormat`
- `uuid` — `crypto.randomUUID()` is native
- `axios` — `fetch` is built-in

**When deps are OK:**
- Complex domains (auth, payments, rich text editing)
- Significant time savings on well-maintained, low-dep packages
- Team already uses it consistently elsewhere

## 2. Over-Engineered Abstractions (Strongly Recommend)

**Pattern:** Creating generic utilities, wrapper components, or "helper" files for code that's only used once or twice.

**Red flags:**
- New files named `utils.ts`, `helpers.ts`, `common.ts`
- Generic wrapper components: `<Button>` wrapping `<button>` with no added value
- Abstract factories, builders, or providers without clear need
- "Config-driven" patterns for simple logic

**Rule of thumb:** Don't abstract until you've written it three times and the pattern is clear.

**Bad:**
```tsx
// components/Button.tsx - 50 lines wrapping a button
// used in 2 places
```

**Good:**
```tsx
// Just use <button> with Tailwind classes inline
// Abstract later if a clear pattern emerges
```

## 3. Deeply Nested Logic (Worth Fixing)

**Pattern:** More than 2-3 levels of nesting in conditionals, callbacks, or JSX.

**Red flags:**
- Ternary inside ternary
- `.then().then().then()` chains
- Callbacks inside callbacks
- Deeply nested JSX (3+ levels of custom components)

**Fixes:**
- Early returns to flatten conditionals
- Extract nested logic into named functions
- Use async/await instead of promise chains
- Break complex JSX into clearly-named sub-components

**Bad:**
```tsx
{isLoading ? (
  <Spinner />
) : error ? (
  <Error message={error} />
) : data ? (
  data.items.length > 0 ? (
    <List items={data.items} />
  ) : (
    <Empty />
  )
) : null}
```

**Good:**
```tsx
if (isLoading) return <Spinner />;
if (error) return <Error message={error} />;
if (!data?.items.length) return <Empty />;
return <List items={data.items} />;
```

## 4. Clever Code (Worth Fixing)

**Pattern:** Code that requires mental gymnastics to understand.

**Red flags:**
- Long reduce chains
- Nested spreads: `{ ...a, ...b, x: { ...a.x, ...b.x } }`
- Implicit behavior relying on falsy coercion
- Regex without comments
- One-liners that should be 5 lines

**Rule:** If it needs a comment to explain, it should probably be rewritten.

**Bad:**
```tsx
const result = items.reduce((acc, item) => ({
  ...acc,
  [item.category]: [...(acc[item.category] || []), item]
}), {});
```

**Good:**
```tsx
const result: Record<string, Item[]> = {};
for (const item of items) {
  if (!result[item.category]) {
    result[item.category] = [];
  }
  result[item.category].push(item);
}
```

## 5. Inconsistent Patterns (Nitpick to Worth Fixing)

**Pattern:** Doing something differently than the rest of the codebase.

**Questions:**
- Does the codebase use a different state management approach?
- Are other components structured differently?
- Is this a new pattern that should be discussed first?

**Examples:**
- Using `useState` when the codebase uses Zustand
- Class components in a hooks-based codebase
- Different file/folder naming conventions
- Different error handling approaches

## 6. Premature Optimization (Nitpick)

**Pattern:** Adding `useMemo`, `useCallback`, `React.memo` without measured performance issues.

**Red flags:**
- Memoizing simple computations
- `useCallback` on functions passed to native elements
- `React.memo` on components that already render fast
- Complex caching logic for data that's fetched once

**Rule:** Measure first. Most React apps don't need aggressive memoization.

## 7. Type Gymnastics (Nitpick)

**Pattern:** TypeScript types that are harder to read than the code they describe.

**Red flags:**
- Multiple levels of generics: `Record<string, Partial<Pick<T, K>>>`
- `as` casts scattered through the code
- Complex conditional types for simple use cases
- Overly strict types that require constant casting

**Good types:** Simple, readable, document intent. When types fight you, reconsider the data model.