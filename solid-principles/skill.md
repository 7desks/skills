---
name: solid-principles-pattern
description: Applies SOLID principles when building or refactoring React/Next.js/frontend components. Use when the user asks to build components, improve code quality, design reusable UI, structure folders, add new functionality without breaking existing code, or review frontend architecture.
---

# Always Apply solid principles for coding

| Principle | Frontend rule                                                 |
| --------- | ------------------------------------------------------------- |
| S         | One component = one concern (UI / data / logic or algorithm)  |
| O         | Extend via variants, composition; avoid if/else for new types |
| L         | Child components replaceable for parent; same contract        |
| I         | Small, specific props; avoid fat shared props                 |
| D         | Depend on abstractions (hooks, services); inject data sources |

## Bad vs Good (per principle)

### S – Single Responsibility

**Bad:** One component does UI + fetch + logic

```tsx
function UserList() {
  const [users, setUsers] = useState([])
  useEffect(() => {
    fetch("/api/users")
      .then((r) => r.json())
      .then(setUsers)
  }, [])
  return users.filter((u) => u.active).map((u) => <div>{u.name}</div>)
}
```

**Good:** Component (UI only) + hook (logic) + service (data)

```tsx
// UserList.tsx
const { users } = useActiveUsers()
return users.map((u) => <UserRow key={u.id} user={u} />)
```

### O – Open/Closed

**Bad:** if/else for each new type

```tsx
function Button({ type }) {
  if (type === "primary") return <button className="bg-blue-500" />
  if (type === "secondary") return <button className="bg-gray-500" />
  if (type === "danger") return <button className="bg-red-500" />
}
```

**Good:** Variant prop; extend via config, not branches. Prefer design tokens (see design-to-frontend skill).

```tsx
const variants = {
  primary: "bg-primary-600",
  secondary: "bg-neutral-600",
  danger: "bg-error-600"
}
function Button({ variant = "primary", ...props }) {
  return <button className={variants[variant]} {...props} />
}
```

### L – Liskov Substitution

**Bad:** Child breaks parent's expected behavior

```tsx
<Modal onClose={handleClose}>
  <SpecialModalChild onClose={null} /> // ignores onClose, different contract
</Modal>
```

**Good:** Child honors same contract; swappable

```tsx
<Modal onClose={handleClose}>
  <ConfirmModalBody onClose={handleClose} message="Delete?" />
</Modal>
// Any body that accepts onClose can replace ConfirmModalBody
```

### I – Interface Segregation

**Bad:** Fat shared props

```tsx
<Card title="x" subtitle="y" avatarUrl="z" tags={[]} actions={[]} meta={{}}
  onClick onHover loading error ... />
```

**Good:** Small, specific props

```tsx
<Card title="x" subtitle="y" />
<CardHeader avatarUrl="z" />
<CardActions actions={items} />
```

### D – Dependency Inversion

**Bad:** Components directly calls fetch

```tsx
function ProductList() {
  const [data, setData] = useState([])
  useEffect(() => {
    fetch("/api/products")
      .then((r) => r.json())
      .then(setData)
  }, [])
  return (
    <ul>
      {data.map((p) => (
        <li>{p.name}</li>
      ))}
    </ul>
  )
}
```

**Good:** Depends on injected service / hook

```tsx
function ProductList({ productService }: { productService: ProductApi }) {
  const { products } = useProducts(productService)
  return (
    <ul>
      {products.map((p) => (
        <li key={p.id}>{p.name}</li>
      ))}
    </ul>
  )
}
```

## When to Activate This Skill

Activate this skill when the user asks to:

- build website section code (HTML5 / CSS3 / Javascript / tailwindcss)
- build or refactor a (React / Next.js / Remix / React Native / Expo) components
- improve frontend code quality
- design reusable UI components
- structure frontend folders
- add new functionality without breaking existing code
- review frontend architecture or PRs

## project Rules (Strict)

1. Prefer **composition over inheritance**
2. Separate **UI, logic, and data access**
3. Avoid **god components**
4. Extend behavior without modifying stable code
5. Depend on **abstractions, not implementations**
6. Keep logic **testable and reusable**
7. Optimize for **readability over cleverness**

#### Apply SRP Like This

- Component → UI only
- Hook → state + interaction logic
- Service / Repo → API & side effects
- Utils → pure transformations

#### Error handling

- **Fetcher:** Throw typed errors; handle non-JSON error bodies (e.g. `response.text()` fallback)
- **Hooks:** Return `{ data, error, loading }`; handle errors in the hook, not in the component
- **Components:** Render error UI from hook state; keep UI dumb (no try/catch in render)
- **Error boundaries:** Use for uncaught render errors; keep per-route or per-section

**Bad:** Component catches, fetcher assumes JSON

```tsx
// Bad: component does error handling
function UserList() {
  try {
    const data = await fetchUsers()
    return <ul>...</ul>
  } catch (e) {
    return <div>Error!</div>
  }
}
```

**Good:** Hook returns error; component renders based on state

```tsx
// Good: hook owns error state
const { users, error, loading } = useUsers()
if (loading) return <Skeleton />
if (error) return <ErrorState message={error.message} onRetry={refetch} />
return <UserListItems users={users} />
```

```tsx
src/
├── app/                          # Routes only (pages/layouts)
│   ├── layout.tsx
│   ├── page.tsx
│   ├── (auth)/
│   │   ├── login/page.tsx
│   │   └── register/page.tsx
│   ├── (dashboard)/
│   │   ├── dashboard/page.tsx
│   │   └── settings/page.tsx
│   └── api/                      # optional (only if calling Next route handlers)
│
│
├── components/                    # Shared reusable UI components (dumb)
│   ├── ui/                        # Buttons, Inputs, Modal, Toast
│   ├── layout/                    # Header, Sidebar, Footer
│   └── icons/                     # custom icons export (svg | png | jpg | gif)
│
├── styles/                        # Optional extra styles
│   └── tokens.css                 # design tokens / CSS vars
│
├── services/                  # services for calling api or other services  from frontend
│   ├── endpoints.ts           # endpoint constants
│   ├── auth.service.ts        # auth services
│   ├── user.service.ts        # user services
│   ├── product.service.ts     # product services
│   ├── order.service.ts       # order services
│   ├── payment.service.ts     # payment services
│   ├── notify.service.ts      # notify services
│   └── index.ts               # index file for services
│
├── hooks/
│   ├── auth/                     # auth hooks
│   │   ├── useLogout
│   │   └── useLoginWithGmail
│   ├── global/                  # Global reusable hooks (non-feature specific)
│       └── useDebounce.ts
│       └── useMediaQuery.ts
│
├── lib/                           # Frontend utilities/configs
│   ├── fetcher.ts                 # fetch wrapper
│   ├── constants.ts               # Constant Variable name and values set like (ROLE | USER_PROFILE) etc
│   ├── format.ts                  # use for format like (Time | Date | currency etc)
│   └── validators.ts              #
│
├── .env.production                # env for production variables
├── .env.development               # env for developer development variables
├── .env.staging                   # env for staging variables for testing
├── .example-env                   # This file push to git with constant variable key
│
├── store/                         # Zustand/Redux (global state)
│   ├── index.ts
│   └── auth.store.ts
│
└── types/                         # Global shared TS types (rare)
    └── global.d.ts

```

## Example of code for lib/fetcher.ts

Native fetch Wrapper (Recommended for Next.js) for API calls

```ts
type HttpMethod = "GET" | "POST" | "PUT" | "PATCH" | "DELETE"

interface FetchOptions<TBody> {
  method?: HttpMethod
  body?: TBody
  headers?: HeadersInit
  cache?: RequestCache
  next?: NextFetchRequestConfig
}

/**
 * Core fetch wrapper
 * Responsibility: HTTP communication only
 */
async function request<TResponse, TBody = unknown>(
  endpoint: string,
  options: FetchOptions<TBody> = {}
): Promise<TResponse> {
  const { method = "GET", body, headers, cache = "no-store", next } = options

  const response = await fetch(
    `${process.env.NEXT_PUBLIC_API_URL}${endpoint}`,
    {
      method,
      cache,
      next,
      credentials: "include",
      headers: {
        "Content-Type": "application/json",
        ...headers
      },
      body: body ? JSON.stringify(body) : undefined
    }
  )

  if (!response.ok) {
    let err: unknown
    try {
      err = await response.json()
    } catch {
      err = { message: response.statusText }
    }
    throw err
  }

  return response.json()
}

/**
 * Public API client
 * Open for extension, closed for modification
 */
export const apiClient = {
  get: <T>(url: string, options?: FetchOptions<never>) =>
    request<T>(url, { ...options, method: "GET" }),

  post: <T, B>(url: string, body: B, options?: FetchOptions<B>) =>
    request<T, B>(url, { ...options, method: "POST", body }),

  put: <T, B>(url: string, body: B, options?: FetchOptions<B>) =>
    request<T, B>(url, { ...options, method: "PUT", body }),

  patch: <T, B>(url: string, body: B, options?: FetchOptions<B>) =>
    request<T, B>(url, { ...options, method: "PATCH", body }),

  delete: <T>(url: string, options?: FetchOptions<never>) =>
    request<T>(url, { ...options, method: "DELETE" })
}
```

Optional: Auth Token Header (If Needed)

```ts
const headers = {
  Authorization: `Bearer ${token}`
}
```

## Example this page code (Best Pattern)

**src/app/(dashboard)/dashboard/page.tsx**

```tsx
import DashboardView from "@/components/dashboard/DashboardView"

export default function Page() {
  return <DashboardView />
}
```

**src/components/dashboard/DashboardView.tsx**

```tsx
import StatsSection from "@/components/StatsSection"
import RecentOrdersSection from "@/components/RecentOrdersSection"

export default function DashboardView() {
  return (
    <>
      <StatsSection />
      <RecentOrdersSection />
    </>
  )
}
```

Example of code for services folder

```bash
├── services/                  # services for calling api or other services  from frontend
│   ├── endpoints.ts           # endpoint constants
│   ├── auth.service.ts        # auth services
│   ├── user.service.ts        # user services
│   ├── product.service.ts     # product services
│   ├── order.service.ts       # order services
│   ├── payment.service.ts     # payment services
│   ├── notify.service.ts      # notify services
│   └── index.ts               # index file for services
```

**src/services/auth.service.ts**

```ts
import { AuthResponse, LoginPayload, RegisterPayload } from "@/types/auth.types"
import { apiClient } from "@/lib/fetcher"

/**
 * Auth API service
 * Responsibility: Handle auth-related HTTP requests only
 */
export const authApi = {
  login: async (payload: LoginPayload): Promise<AuthResponse> => {
    const response = await apiClient.post("/auth/login", payload)
    return response
  },

  register: async (payload: RegisterPayload): Promise<AuthResponse> => {
    const response = await apiClient.post("/auth/register", payload)
    return response
  },

  logout: async (): Promise<void> => {
    await apiClient.post("/auth/logout")
  },

  me: async (): Promise<AuthResponse> => {
    const response = await apiClient.get("/auth/me")
    return response
  }
}
```
