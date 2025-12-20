# {{ cookiecutter.project_name }} - Frontend

<p align="center">
  <img src="https://img.shields.io/badge/Next.js-15-black?logo=next.js&logoColor=white" alt="Next.js">
  <img src="https://img.shields.io/badge/React-19-61DAFB?logo=react&logoColor=white" alt="React">
  <img src="https://img.shields.io/badge/TypeScript-5-3178C6?logo=typescript&logoColor=white" alt="TypeScript">
  <img src="https://img.shields.io/badge/Tailwind-4-06B6D4?logo=tailwindcss&logoColor=white" alt="Tailwind">
  <img src="https://img.shields.io/badge/Bun-latest-F9F1E1?logo=bun&logoColor=black" alt="Bun">
</p>

<p align="center">
  Next.js 15 frontend for <b>{{ cookiecutter.project_name }}</b>
</p>

---

## Tech Stack

| Technology | Version | Purpose |
|------------|---------|---------|
| [Next.js](https://nextjs.org) | 15.x | React framework with App Router |
| [React](https://react.dev) | 19.x | UI library with Server Components |
| [TypeScript](https://www.typescriptlang.org) | 5.x | Type safety |
| [Tailwind CSS](https://tailwindcss.com) | 4.x | Utility-first styling |
| [Zustand](https://zustand-demo.pmnd.rs) | 5.x | State management |
| [TanStack Query](https://tanstack.com/query) | 5.x | Server state & data fetching |
| [Bun](https://bun.sh) | Latest | Package manager & runtime |

---

## Quick Start

### Prerequisites

- [Bun](https://bun.sh) installed (`curl -fsSL https://bun.sh/install | bash`)

### Installation

```bash
# Install dependencies
bun install

# Copy environment file
cp .env.example .env.local
```

### Development

```bash
bun dev
```

Open [http://localhost:{{ cookiecutter.frontend_port }}](http://localhost:{{ cookiecutter.frontend_port }}) in your browser.

### Build & Production

```bash
# Build for production
bun build

# Start production server
bun start
```

---

## Project Structure

```
frontend/
├── src/
│   ├── app/                      # Next.js App Router
│   │   ├── layout.tsx            # Root layout
│   │   ├── page.tsx              # Home page
│   │   ├── providers.tsx         # Client providers (React Query, etc.)
│   │   ├── (auth)/               # Auth route group (public)
│   │   │   ├── layout.tsx
│   │   │   ├── login/page.tsx
│   │   │   └── register/page.tsx
│   │   ├── (dashboard)/          # Dashboard route group (protected)
│   │   │   ├── layout.tsx
│   │   │   ├── dashboard/page.tsx
{%- if cookiecutter.enable_ai_agent %}
│   │   │   ├── chat/page.tsx
{%- endif %}
│   │   │   └── profile/page.tsx
│   │   └── api/                  # API routes (BFF proxy)
│   │       ├── auth/
│   │       │   ├── login/route.ts
│   │       │   ├── logout/route.ts
│   │       │   ├── register/route.ts
│   │       │   ├── refresh/route.ts
│   │       │   └── me/route.ts
{%- if cookiecutter.enable_conversation_persistence %}
│   │       └── conversations/
│   │           └── route.ts
{%- endif %}
│   │
│   ├── components/
│   │   ├── ui/                   # Base UI components
│   │   │   ├── button.tsx
│   │   │   ├── input.tsx
│   │   │   ├── card.tsx
│   │   │   ├── badge.tsx
│   │   │   └── label.tsx
│   │   ├── layout/               # Layout components
│   │   │   ├── header.tsx
│   │   │   └── sidebar.tsx
│   │   ├── auth/                 # Auth components
│   │   │   ├── login-form.tsx
│   │   │   └── register-form.tsx
{%- if cookiecutter.enable_ai_agent %}
│   │   ├── chat/                 # Chat components
│   │   │   ├── chat-container.tsx
│   │   │   ├── chat-input.tsx
│   │   │   ├── message-list.tsx
│   │   │   ├── message-item.tsx
│   │   │   └── tool-call-card.tsx
{%- endif %}
│   │   └── theme/                # Theme components
│   │       ├── theme-provider.tsx
│   │       └── theme-toggle.tsx
│   │
│   ├── hooks/                    # Custom React hooks
│   │   ├── use-auth.ts           # Authentication hook
{%- if cookiecutter.enable_ai_agent %}
│   │   ├── use-websocket.ts      # WebSocket connection
│   │   ├── use-chat.ts           # Chat functionality
{%- endif %}
{%- if cookiecutter.enable_conversation_persistence %}
│   │   └── use-conversations.ts  # Conversation management
{%- endif %}
│   │
│   ├── stores/                   # Zustand state stores
│   │   ├── auth-store.ts         # Auth state
│   │   ├── theme-store.ts        # Theme state
{%- if cookiecutter.enable_ai_agent %}
│   │   └── chat-store.ts         # Chat messages state
{%- endif %}
│   │
│   ├── lib/                      # Utilities
│   │   ├── api-client.ts         # Fetch wrapper
│   │   ├── server-api.ts         # Server-side API calls
│   │   ├── utils.ts              # Helper functions (cn, etc.)
│   │   └── constants.ts          # App constants
│   │
│   ├── types/                    # TypeScript types
│   │   ├── api.ts
│   │   ├── auth.ts
{%- if cookiecutter.enable_ai_agent %}
│   │   └── chat.ts
{%- endif %}
│   │
│   └── middleware.ts             # Auth middleware
│
├── e2e/                          # Playwright E2E tests
│   ├── auth.setup.ts
│   ├── auth.spec.ts
│   ├── home.spec.ts
{%- if cookiecutter.enable_ai_agent %}
│   └── chat.spec.ts
{%- endif %}
│
{%- if cookiecutter.enable_i18n %}
├── messages/                     # i18n translations
│   ├── en.json
│   └── pl.json
{%- endif %}
│
├── public/                       # Static assets
├── .env.example                  # Environment template
├── next.config.ts
├── tailwind.config.ts
├── tsconfig.json
├── playwright.config.ts
├── vitest.config.ts
└── package.json
```

---

## Available Scripts

| Command | Description |
|---------|-------------|
| `bun dev` | Start development server (port {{ cookiecutter.frontend_port }}) |
| `bun build` | Build for production |
| `bun start` | Start production server |
| `bun lint` | Run ESLint |
| `bun lint:fix` | Fix ESLint issues |
| `bun format` | Format with Prettier |
| `bun type-check` | Run TypeScript type checking |
| `bun test` | Run unit tests (Vitest) |
| `bun test:run` | Run tests once (CI mode) |
| `bun test:coverage` | Run tests with coverage |
| `bun test:e2e` | Run E2E tests (Playwright) |
| `bun test:e2e:ui` | Run E2E tests with UI |
| `bun test:e2e:headed` | Run E2E tests in browser |

---

## Environment Variables

Create `.env.local` from `.env.example`:

```bash
# Backend API URL (server-side only)
BACKEND_URL=http://localhost:{{ cookiecutter.backend_port }}

# WebSocket URL (client-side)
NEXT_PUBLIC_WS_URL=ws://localhost:{{ cookiecutter.backend_port }}/api/v1/agent/ws
{%- if cookiecutter.enable_logfire %}

# OpenTelemetry (Logfire)
OTEL_EXPORTER_OTLP_ENDPOINT=https://logfire-api.pydantic.dev
OTEL_EXPORTER_OTLP_HEADERS=Authorization=your-write-token
{%- endif %}
```

---

## Authentication

### How It Works

1. **Login** - User submits credentials to `/api/auth/login`
2. **BFF Proxy** - Next.js API route calls backend, receives JWT tokens
3. **Cookies** - Tokens stored in HTTP-only cookies (secure)
4. **Auto-refresh** - Tokens refreshed automatically before expiry
5. **Middleware** - Protected routes check auth via middleware

### Auth Store (Zustand)

```typescript
// src/stores/auth-store.ts
import { useAuthStore } from '@/stores/auth-store';

// In components
const { user, isAuthenticated, logout } = useAuthStore();
```

### Auth Hook

```typescript
// src/hooks/use-auth.ts
import { useAuth } from '@/hooks/use-auth';

function MyComponent() {
  const { user, isLoading, login, logout } = useAuth();

  // ...
}
```

### Protected Routes

Middleware automatically redirects unauthenticated users:

```typescript
// src/middleware.ts
const protectedPaths = ['/dashboard', '/chat', '/profile'];
```

---
{%- if cookiecutter.enable_ai_agent %}

## AI Chat

### WebSocket Connection

The chat uses WebSocket for real-time streaming:

```typescript
// src/hooks/use-chat.ts
import { useChat } from '@/hooks/use-chat';

function ChatPage() {
  const { messages, isConnected, isStreaming, sendMessage } = useChat();

  return (
    <div>
      <MessageList messages={messages} />
      <ChatInput onSend={sendMessage} disabled={isStreaming} />
    </div>
  );
}
```

### Message Types

```typescript
interface Message {
  id: string;
  role: 'user' | 'assistant' | 'tool';
  content: string;
  tool_name?: string;
  created_at: Date;
}

interface StreamEvent {
  type: 'start' | 'token' | 'tool_call' | 'end' | 'error';
  content?: string;
  tool?: { name: string; args: Record<string, unknown> };
}
```

### Components

| Component | Description |
|-----------|-------------|
| `ChatContainer` | Main chat wrapper with WebSocket |
| `ChatInput` | Message input with send button |
| `MessageList` | Scrollable message container |
| `MessageItem` | Single message bubble |
| `ToolCallCard` | Tool invocation display |

---
{%- endif %}

## UI Components

Pre-built components following shadcn/ui patterns:

### Button

```tsx
import { Button } from '@/components/ui/button';

<Button variant="default">Click me</Button>
<Button variant="destructive">Delete</Button>
<Button variant="outline">Cancel</Button>
<Button variant="ghost">Ghost</Button>
<Button size="sm">Small</Button>
<Button size="lg">Large</Button>
```

### Input

```tsx
import { Input } from '@/components/ui/input';
import { Label } from '@/components/ui/label';

<div>
  <Label htmlFor="email">Email</Label>
  <Input id="email" type="email" placeholder="you@example.com" />
</div>
```

### Card

```tsx
import { Card, CardHeader, CardTitle, CardContent } from '@/components/ui/card';

<Card>
  <CardHeader>
    <CardTitle>Title</CardTitle>
  </CardHeader>
  <CardContent>
    Content here...
  </CardContent>
</Card>
```

---

## State Management

### Zustand Stores

```typescript
// Creating a store
import { create } from 'zustand';
import { persist } from 'zustand/middleware';

interface CounterState {
  count: number;
  increment: () => void;
  decrement: () => void;
}

export const useCounterStore = create<CounterState>()(
  persist(
    (set) => ({
      count: 0,
      increment: () => set((state) => ({ count: state.count + 1 })),
      decrement: () => set((state) => ({ count: state.count - 1 })),
    }),
    { name: 'counter-storage' }
  )
);
```

### Available Stores

| Store | Purpose |
|-------|---------|
| `auth-store` | User authentication state |
| `theme-store` | Dark/light mode preference |
{%- if cookiecutter.enable_ai_agent %}
| `chat-store` | Chat messages and state |
{%- endif %}
{%- if cookiecutter.enable_conversation_persistence %}
| `conversation-store` | Conversation list and selection |
{%- endif %}

---

## Dark Mode

Theme switching with system preference detection:

```tsx
import { useThemeStore } from '@/stores/theme-store';
import { ThemeToggle } from '@/components/theme/theme-toggle';

// Toggle component
<ThemeToggle />

// Manual control
const { theme, setTheme } = useThemeStore();
setTheme('dark');  // 'light' | 'dark' | 'system'
```

---
{%- if cookiecutter.enable_logfire %}

## Logfire Observability

[Logfire](https://logfire.pydantic.dev) provides frontend observability through OpenTelemetry instrumentation.

### What Gets Traced

- **Page navigations** - Route changes and load times
- **API calls** - Fetch requests to backend
- **Web Vitals** - Core Web Vitals metrics (LCP, FID, CLS)
- **Errors** - Client-side exceptions

### Configuration

Set environment variables in `.env.local`:

```bash
OTEL_EXPORTER_OTLP_ENDPOINT=https://logfire-api.pydantic.dev
OTEL_EXPORTER_OTLP_HEADERS=Authorization=your-write-token
```

### Manual Instrumentation

```typescript
import { trace } from '@opentelemetry/api';

const tracer = trace.getTracer('frontend');

async function processCheckout(order: Order) {
  const span = tracer.startSpan('checkout.process');
  try {
    span.setAttribute('order.id', order.id);
    await submitOrder(order);
    span.setStatus({ code: SpanStatusCode.OK });
  } catch (error) {
    span.setStatus({ code: SpanStatusCode.ERROR });
    throw error;
  } finally {
    span.end();
  }
}
```

> 📚 For more details, see [Logfire Browser Integration](https://logfire.pydantic.dev/docs/integrations/browser/).
{%- endif %}

---
{%- if cookiecutter.enable_i18n %}

## Internationalization (i18n)

Using `next-intl` for translations:

### Translation Files

```json
// messages/en.json
{
  "common": {
    "login": "Login",
    "logout": "Logout"
  },
  "auth": {
    "email": "Email",
    "password": "Password"
  }
}
```

### Usage in Components

```tsx
import { useTranslations } from 'next-intl';

function LoginForm() {
  const t = useTranslations('auth');

  return (
    <form>
      <Label>{t('email')}</Label>
      <Input name="email" />
    </form>
  );
}
```

### Language Switcher

```tsx
import { LanguageSwitcher } from '@/components/language-switcher';

<LanguageSwitcher />
```

---
{%- endif %}

## Testing

### Unit Tests (Vitest)

```bash
# Run tests
bun test

# Watch mode
bun test --watch

# With coverage
bun test:coverage

# UI mode
bun test:ui
```

Example test:

```typescript
// src/lib/utils.test.ts
import { describe, it, expect } from 'vitest';
import { cn } from './utils';

describe('cn utility', () => {
  it('merges class names', () => {
    expect(cn('foo', 'bar')).toBe('foo bar');
  });
});
```

### E2E Tests (Playwright)

```bash
# Run all E2E tests
bun test:e2e

# With browser UI
bun test:e2e:ui

# Headed mode (see browser)
bun test:e2e:headed

# Debug mode
bun test:e2e:debug

# Show report
bun test:e2e:report
```

Example test:

```typescript
// e2e/auth.spec.ts
import { test, expect } from '@playwright/test';

test('should login successfully', async ({ page }) => {
  await page.goto('/login');
  await page.fill('input[name="email"]', 'test@example.com');
  await page.fill('input[name="password"]', 'password123');
  await page.click('button[type="submit"]');

  await expect(page).toHaveURL('/dashboard');
});
```

---

## API Proxy (BFF Pattern)

All API calls go through Next.js API routes to:

1. **Hide backend URL** from browser
2. **Handle cookies** securely (HTTP-only)
3. **Add auth headers** automatically
4. **Transform responses** if needed

### Example API Route

```typescript
// src/app/api/auth/login/route.ts
import { NextRequest, NextResponse } from 'next/server';
import { cookies } from 'next/headers';

const API_URL = process.env.BACKEND_URL;

export async function POST(request: NextRequest) {
  const body = await request.json();

  const res = await fetch(`${API_URL}/api/v1/auth/login`, {
    method: 'POST',
    headers: { 'Content-Type': 'application/x-www-form-urlencoded' },
    body: new URLSearchParams({
      username: body.email,
      password: body.password,
    }),
  });

  if (!res.ok) {
    return NextResponse.json({ error: 'Invalid credentials' }, { status: 401 });
  }

  const data = await res.json();

  // Set HTTP-only cookies
  const cookieStore = await cookies();
  cookieStore.set('access_token', data.access_token, {
    httpOnly: true,
    secure: process.env.NODE_ENV === 'production',
    sameSite: 'lax',
    maxAge: 60 * 30,
  });

  return NextResponse.json({ user: data.user });
}
```

---

## Deployment

### Docker

```dockerfile
# Dockerfile
FROM oven/bun:1 AS builder
WORKDIR /app
COPY package.json bun.lockb ./
RUN bun install --frozen-lockfile
COPY . .
RUN bun build

FROM oven/bun:1-slim
WORKDIR /app
COPY --from=builder /app/.next ./.next
COPY --from=builder /app/public ./public
COPY --from=builder /app/package.json ./
CMD ["bun", "start"]
```

### Environment Variables for Production

```bash
BACKEND_URL=https://api.your-domain.com
NEXT_PUBLIC_WS_URL=wss://api.your-domain.com/api/v1/agent/ws
NODE_ENV=production
```

---

## Documentation

| Resource | Link |
|----------|------|
| Template Repository | [github.com/vstorm-co/full-stack-fastapi-nextjs-llm-template](https://github.com/vstorm-co/full-stack-fastapi-nextjs-llm-template) |
| Frontend Guide | [docs/frontend.md](https://github.com/vstorm-co/full-stack-fastapi-nextjs-llm-template/blob/main/docs/frontend.md) |
{%- if cookiecutter.enable_ai_agent %}
| AI Agent Guide | [docs/ai-agent.md](https://github.com/vstorm-co/full-stack-fastapi-nextjs-llm-template/blob/main/docs/ai-agent.md) |
{%- endif %}
{%- if cookiecutter.enable_logfire %}
| Observability Guide | [docs/observability.md](https://github.com/vstorm-co/full-stack-fastapi-nextjs-llm-template/blob/main/docs/observability.md) |
{%- endif %}
| Next.js Docs | [nextjs.org/docs](https://nextjs.org/docs) |
| Tailwind CSS Docs | [tailwindcss.com/docs](https://tailwindcss.com/docs) |

---

## License

MIT
