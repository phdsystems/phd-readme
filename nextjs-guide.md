# Complete Guide to Creating a Next.js Application

## Prerequisites
- Install **Node.js** (version 18.17.0 or later)  
- Ensure **npm** (comes with Node.js) or **yarn** is installed  

---

## 1. Create a New Next.js Project

Use the official `create-next-app` tool with flags to skip prompts:

```bash
npx create-next-app@latest my-nextjs15-app \
  --typescript \
  --tailwind \
  --eslint \
  --app \
  --src-dir \
  --turbopack \
  --no-import-alias
This answers “Yes” to TypeScript, Tailwind CSS, ESLint, App Router, Turbopack, and “No” to customizing the import alias.

2. Navigate to Your Project
bash
Copy
Edit
cd my-nextjs15-app
3. Project Structure
arduino
Copy
Edit
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
    │   ├── globals.css     ← Tailwind’s base imports  
    │   ├── layout.tsx      ← Root layout & metadata  
    │   └── page.tsx        ← Home page  
    ├── components/         
    │   └── Example.tsx     ← Reusable React components  
    └── styles/             
        ├── globals.css     ← (optional split)  
        └── Home.module.css ← CSS modules  
.gitignore – ignores node_modules/, .next/, etc.

next.config.js – project configuration (Turbopack enabled).

postcss.config.js & tailwind.config.js – Tailwind setup.

tsconfig.json – TypeScript settings (no custom import aliases).

.eslintrc.json – ESLint rules.

public/ – static assets (favicon, images, etc.).

All application code lives under src/.

4. Run the Development Server
bash
Copy
Edit
npm run dev
# or
yarn dev
Your app will be available at http://localhost:3000.

5. Create Pages or Routes
App Router (Recommended)
Home page: src/app/page.tsx

Nested route: src/app/about/page.tsx → /about

Pages Router (Optional)
Home page: src/pages/index.tsx

About page: src/pages/about.tsx → /about

6. Basic Page Component Example
tsx
Copy
Edit
// src/app/page.tsx
export default function HomePage() {
  return (
    <div className="p-8">
      <h1 className="text-3xl font-bold">Welcome to Next.js</h1>
      <p className="mt-4">This is my first Next.js application!</p>
    </div>
  );
}
7. Adding Styling
Global CSS: Import in src/app/globals.css (App Router) or src/pages/_app.tsx (Pages Router).

CSS Modules: Create [name].module.css files alongside components.

Tailwind CSS: Already configured; use utility classes.

CSS-in-JS: Optionally add styled-components or Emotion.

8. Creating API Routes
App Router
ts
Copy
Edit
// src/app/api/hello/route.ts
export async function GET(request: Request) {
  return new Response(JSON.stringify({ message: 'Hello from the API' }), {
    headers: { 'Content-Type': 'application/json' }
  });
}
Pages Router
ts
Copy
Edit
// src/pages/api/hello.ts
import type { NextApiRequest, NextApiResponse } from 'next';

export default function handler(req: NextApiRequest, res: NextApiResponse) {
  res.status(200).json({ message: 'Hello from the API' });
}
9. Building for Production
bash
Copy
Edit
npm run build
# or
yarn build
10. Starting Production Server
bash
Copy
Edit
npm run start
# or
yarn start
11. Deployment Options
Vercel (recommended)

Netlify

AWS Amplify

Custom Node.js server

12. Additional Features
Data Fetching
App Router: React Server Components, fetch with built-in caching.

Pages Router: getServerSideProps, getStaticProps, getStaticPaths.

Image Optimization
tsx
Copy
Edit
import Image from 'next/image';

<Image
  src="/profile.jpg"
  width={500}
  height={300}
  alt="Profile Image"
/>
Font Optimization
tsx
Copy
Edit
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
Dynamic & Catch-All Routes
Dynamic: src/app/blog/[slug]/page.tsx

Catch-All: src/app/docs/[...slug]/page.tsx

Middleware
ts
Copy
Edit
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
13. Environment Variables
Create a .env.local file:

ini
Copy
Edit
API_KEY=your_api_key_here
Use in code via process.env.API_KEY.

14. Common Next.js Commands
npx create-next-app@latest — create a new project

npm run dev — start dev server

npm run build — build for production

npm run start — start production server

npm run lint — run ESLint

npx next info — show environment info
