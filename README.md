# Med-Flow-Front

Frontend (Next.js / TypeScript) for **Assistant Médical Intelligent**, a multi-tenant clinic management platform: patient records, consultations, billing, and role-based dashboards (admin / doctor / patient). Built with a 4-person team.

Pairs with the Django REST API backend: [medflow-backend](https://github.com/MalakBenHassine/medflow-backend).

## Stack

Next.js, TypeScript, NextAuth, Tailwind CSS

## Getting started

```
npm run dev
# or
yarn dev
# or
pnpm dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

---

## Authentication workflow

This project integrates **NextAuth** with a **Django REST API** for authentication, session management, and role-based access control.

### 1. Login process

`User → Login Page (/login) → signIn() → authorize() → Django API`

- The user fills out the login form.
- The `signIn()` method (provided by **NextAuth**) sends credentials to the backend.
- The `authorize()` function in `NextAuthConfig.tsx` sends a POST request to `/api/accounts/login/`.
- If Django validates the credentials, it returns user data and a JWT token.

### 2. Session & JWT callbacks

`NextAuth → jwt callback → session callback → Available in useSession()`

- The `jwt` callback stores extra user data (`role`, `id`, `accessToken`) inside the token.
- The `session` callback exposes these values in the client session.
- Session data is accessible anywhere with:

```ts
import { useSession } from "next-auth/react";
const { data: session } = useSession();
console.log(session?.user);
```

### 3. Route protection

Protected routes (e.g. `/admin/dashboard`) are handled through `middleware.ts`.

- If the user is **not authenticated**, they are redirected to `/login`.
- Role-based logic ensures users only access authorized pages (e.g. Admin → `/admin/dashboard`, Doctor → `/doctor/dashboard`, Patient → `/patient/profile`).

## Key files

- `src/app/api/auth/NextAuthConfig.tsx` — login logic and token creation
- `src/middleware.ts` — route protection and role-based redirection
- `src/app/login/page.tsx` — login page UI and `signIn()` handler
- `src/app/admin/dashboard/page.tsx` — example of a protected admin route

## Environment variables

Create a `.env.local` file:

```
BACKEND_URL=http://127.0.0.1:8000
NEXTAUTH_URL=http://localhost:3000
NEXTAUTH_SECRET=your_generated_secret
```

Generate a secure secret with `npx auth secret`.

## Summary

- Secure login using a Django backend
- JWT-based session management via NextAuth
- Role-based route protection with middleware
- No localStorage — uses encrypted cookies

## Learn more

- [Next.js Docs](https://nextjs.org/docs)
- [NextAuth.js Docs](https://next-auth.js.org)
- [Django REST Framework](https://www.django-rest-framework.org)
