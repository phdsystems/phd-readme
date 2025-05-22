# Complete Guide to Creating a Next.js 15 Application

## Prerequisites
- Install **Node.js** (version 18.17.0 or later)  
- Ensure **npm** (comes with Node.js) or **yarn** is installed  

## 1. Create a New Next.js Project

Use the official `create-next-app` tool with flags to skip prompts:

```bash
npx create-next-app@latest phd-next \
  --typescript \
  --tailwind \
  --eslint \
  --app \
  --src-dir \
  --turbopack \
  --no-import-alias


The --api flag tells the Next.js CLI to scaffold a minimal API endpoint for you in the new project.
```

This answers "Yes" to TypeScript, Tailwind CSS, ESLint, App Router, Turbo (for Turbopack), and "No" to customizing the import alias.

## 2. Navigate to Your Project

```bash
cd my-nextjs15-app
```

## 3. Project Structure

```
my-nextjs15-app/
├── .gitignore
├── README.md
├── next.config.js
├── package.json
├── postcss.config.js
├── tailwind.config.js
├── tsconfig.json
├── .eslintrc.json
├── public/
│   ├── favicon.ico
│   └── vercel.svg
└── src/
    ├── app/                
    │   ├── globals.css     ← Tailwind's base imports  
    │   ├── layout.tsx      ← Root layout & metadata  
    │   └── page.tsx        ← Home page  
    ├── components/         
    │   └── Example.tsx     ← Reusable React components  
    └── styles/             
        ├── globals.css     ← (optional split)  
        └── Home.module.css ← CSS modules  
```

- `.gitignore` – ignores node_modules/, .next/, etc.
- `next.config.js` – project configuration (can be `.ts` since Next.js 15).
- `postcss.config.js` & `tailwind.config.js` – Tailwind setup.
- `tsconfig.json` – TypeScript settings (no custom import aliases).
- `.eslintrc.json` – ESLint rules (supports ESLint 9 since Next.js 15).
- `public/` – static assets (favicon, images, etc.).
- All application code lives under `src/`.

## 4. Run the Development Server

```bash
npm run dev
# or
yarn dev
```

This will use Turbopack if you used the `--turbo` flag during setup. Alternatively, modify your `package.json` scripts to explicitly use Turbopack:

```json
"scripts": {
  "dev": "next dev --turbo",
  "build": "next build",
  "start": "next start",
  "lint": "next lint"
}
```

Your app will be available at http://localhost:3000.

## 5. Create Pages or Routes

### App Router (Recommended)
- Home page: `src/app/page.tsx`
- Nested route: `src/app/about/page.tsx` → `/about`

### Pages Router (Optional)
- Home page: `src/pages/index.tsx`
- About page: `src/pages/about.tsx` → `/about`

## 6. Basic Page Component Example

```tsx
// src/app/page.tsx
export default function HomePage() {
  return (
    <div className="p-8">
      <h1 className="text-3xl font-bold">Welcome to Next.js</h1>
      <p className="mt-4">This is my first Next.js application!</p>
    </div>
  );
}
```

## 7. Adding Styling

- **Global CSS**: Import in `src/app/globals.css` (App Router) or `src/pages/_app.tsx` (Pages Router).
- **CSS Modules**: Create `[name].module.css` files alongside components.
- **Tailwind CSS**: Already configured; use utility classes.
- **CSS-in-JS**: Optionally add styled-components or Emotion.

## 8. Creating API Routes

### App Router

```ts
// src/app/api/hello/route.ts
export async function GET(request: Request) {
  return new Response(JSON.stringify({ message: 'Hello from the API' }), {
    headers: { 'Content-Type': 'application/json' }
  });
}
```

### Pages Router

```ts
// src/pages/api/hello.ts
import type { NextApiRequest, NextApiResponse } from 'next';

export default function handler(req: NextApiRequest, res: NextApiResponse) {
  res.status(200).json({ message: 'Hello from the API' });
}
```

## 9. Building for Production

```bash
npm run build
# or
yarn build
```

Since Next.js 15.3, Turbopack for builds is available in alpha. You can try it with:

```bash
npm run build --turbopack
# or
yarn build --turbopack
```

Alternatively, update your `package.json` scripts:

```json
"scripts": {
  "dev": "next dev --turbo",
  "build": "next build --turbopack",
  "start": "next start",
  "lint": "next lint"
}
```

Note: Turbopack builds are still in alpha and recommended for testing/preview environments, not mission-critical production applications yet.

## 10. Starting Production Server

```bash
npm run start
# or
yarn start
```

## 11. Deployment Options

- Vercel (recommended)
- Netlify
- AWS Amplify
- Custom Node.js server

## 12. Additional Features

### Data Fetching
- **App Router**: React Server Components, fetch with built-in caching.
- **Pages Router**: getServerSideProps, getStaticProps, getStaticPaths.

### Static Route Indicator
Next.js 15 displays a visual indicator during development to help identify which routes are static or dynamic, making it easier to optimize performance.

### Client Instrumentation
Next.js 15.3 added a client instrumentation hook for adding monitoring and analytics code:

```tsx
// src/app/instrumentation.client.ts
export function register() {
  console.log('Client instrumentation registered');
  // Add analytics or monitoring code here
}
```

### Image Optimization

```tsx
import Image from 'next/image';

<Image
  src="/profile.jpg"
  width={500}
  height={300}
  alt="Profile Image"
/>
```

### Font Optimization

```tsx
// src/app/layout.tsx
import { Inter } from 'next/font/google';
const inter = Inter({ subsets: ['latin'] });

export default function RootLayout({ children }: { children: React.ReactNode }) {
  return (
    <html lang="en" className={inter.className}>
      <body>{children}</body>
    </html>
  );
}
```

### Dynamic & Catch-All Routes
- Dynamic: `src/app/blog/[slug]/page.tsx`
- Catch-All: `src/app/docs/[...slug]/page.tsx`

### Middleware

```ts
// middleware.ts
import { NextResponse } from 'next/server';
import type { NextRequest } from 'next/server';

export function middleware(request: NextRequest) {
  // custom logic
  return NextResponse.next();
}

export const config = {
  matcher: '/api/:path*',
};
```

## 13. Environment Variables

Create a `.env.local` file:

```ini
API_KEY=your_api_key_here
```

Use in code via `process.env.API_KEY`.

## 14. Turbopack Configuration

Since Next.js 15.3, you can configure Turbopack in your `next.config.js` or `next.config.ts`:

```js
/** @type {import('next').NextConfig} */
const nextConfig = {
  // Turbopack specific config
  turbopack: {
    // Define additional webpack loaders
    rules: [
      // Example loader configuration
    ],
    // Create manual aliases (like resolve.alias in webpack)
    resolveAlias: {
      // Example aliases
    }
  }
};

module.exports = nextConfig;
```

## 15. Navigation Hooks

Next.js 15.3 introduced new navigation hooks for improved client-side routing:

```tsx
// Example using navigation hooks
import { useRouter, usePathname, useSearchParams } from 'next/navigation';
import { onNavigate, useLinkStatus } from 'next/link';

function MyComponent() {
  const router = useRouter();
  const pathname = usePathname();
  const searchParams = useSearchParams();
  const linkStatus = useLinkStatus('/some-path');

  // Register navigation callback
  onNavigate(({ url, type }) => {
    console.log(`Navigation to ${url} (${type})`);
    // Add analytics tracking here
  });

  return (
    <div>
      {/* Component content */}
    </div>
  );
}
```

## 16. Common Next.js Commands

- `npx create-next-app@latest` — create a new project
- `npm run dev` — start dev server
- `npm run dev --turbo` — start dev server with Turbopack
- `npm run build` — build for production
- `npm run build --turbopack` — build for production with Turbopack (alpha)
- `npm run start` — start production server
- `npm run lint` — run ESLint
- `npx @next/codemod@latest upgrade` — upgrade to latest Next.js version
- `npx next info` — show environment info
