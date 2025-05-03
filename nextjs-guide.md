# Complete Guide to Creating a Next.js Application

## Prerequisites
- Install Node.js (version 18.17.0 or later)
- Ensure npm (comes with Node.js) or yarn is installed

## 1. Create a New Next.js Project
Using the official create-next-app tool (recommended):

```bash
npx create-next-app@latest my-nextjs15-app \
  --typescript \
  --tailwind \
  --eslint \
  --app \
  --src-dir \
  --turbopack \
  --no-import-alias
```
During setup, you would normally be prompted with configuration questions below. Running create-next-app with flags as above answers yes to all but alias (--no-import-alias):
- Would you like to use TypeScript? (Yes/No)
- Would you like to use ESLint? (Yes/No)
- Would you like to use Tailwind CSS? (Yes/No)
- Would you like to use the App Router? (Yes/No)
- Would you like to customize the default import alias? (Yes/No)

## 2. Navigate to Your Project
```bash
cd my-nextjs15-app
```

## 3. Project Structure
Basic structure of a Next.js app:

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
    ├── app/                ← App Router  
    │   ├── globals.css     ← Tailwind’s base imports  
    │   ├── layout.tsx      ← Root layout & meta  
    │   └── page.tsx        ← Home page  
    ├── components/         ← Your React components  
    │   └── Example.tsx  
    └── styles/             ← Module & utility CSS  
        ├── globals.css     ← (if you split CSS here)  
        └── Home.module.css

Here’s what your project will look like, with everything under src/ and Tailwind + Turbopack enabled, no import alias:
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
    ├── app/                ← App Router  
    │   ├── globals.css     ← Tailwind’s base imports  
    │   ├── layout.tsx      ← Root layout & meta  
    │   └── page.tsx        ← Home page  
    ├── components/         ← Your React components  
    │   └── Example.tsx  
    └── styles/             ← Module & utility CSS  
        ├── globals.css     ← (if you split CSS here)  
        └── Home.module.css
```

.gitignore – ignores node_modules, .next, etc.

next.config.js – Next.js configuration (Turbopack enabled under the hood).

postcss.config.js & tailwind.config.js – Tailwind setup.

tsconfig.json – TypeScript settings (no custom import aliases).

.eslintrc.json – ESLint rules.

public/ – Static assets (favicon, logos, etc.).

Everything you write (pages, components, styles) lives inside src/. You can now:       

## 4. Run the Development Server
```bash
npm run dev
# or
yarn dev
```

This starts your app at http://localhost:3000

## 5. Create Pages or Routes
- For App Router (newer): Create folders in `app/` directory
  - `app/page.js` - Home page
  - `app/about/page.js` - About page (/about route)
  
- For Pages Router (traditional): Create files in `pages/` directory
  - `pages/index.js` - Home page
  - `pages/about.js` - About page (/about route)

## 6. Basic Page Component Example
```jsx
export default function HomePage() {
  return (
    <div>
      <h1>Welcome to Next.js</h1>
      <p>This is my first Next.js application!</p>
    </div>
  );
}
```

## 7. Adding Styling
- Global CSS: Import in `app/layout.js` or `pages/_app.js`
- CSS Modules: Create `[name].module.css` files
- Styled-components or other CSS-in-JS libraries
- Tailwind CSS (if selected during setup)

## 8. Creating API Routes
- App Router: Create route handlers in `app/api/[route]/route.js`
- Pages Router: Create API files in `pages/api/[route].js`

Example API route:
```javascript
// App Router (app/api/hello/route.js)
export async function GET(request) {
  return Response.json({ message: 'Hello from the API' });
}

// Pages Router (pages/api/hello.js)
export default function handler(req, res) {
  res.status(200).json({ message: 'Hello from the API' });
}
```

## 9. Building for Production
```bash
npm run build
# or
yarn build
```

## 10. Starting Production Server
```bash
npm run start
# or
yarn start
```

## 11. Deployment Options
- Vercel (recommended, built by Next.js creators)
- Netlify
- AWS Amplify
- Self-hosted on any Node.js server

## 12. Additional Features
- **Data Fetching**:
  - App Router: React Server Components, `fetch` with caching
  - Pages Router: `getServerSideProps`, `getStaticProps`, `getStaticPaths`

- **Image Optimization**:
  ```jsx
  import Image from 'next/image';
  
  <Image
    src="/profile.jpg"
    width={500}
    height={300}
    alt="Profile Image"
  />
  ```

- **Font Optimization**:
  ```jsx
  // app/layout.js
  import { Inter } from 'next/font/google';
  
  const inter = Inter({ subsets: ['latin'] });
  
  export default function RootLayout({ children }) {
    return (
      <html lang="en" className={inter.className}>
        <body>{children}</body>
      </html>
    );
  }
  ```

- **Routing**:
  - Dynamic routes: `app/blog/[slug]/page.js` or `pages/blog/[slug].js`
  - Catch-all routes: `app/docs/[...slug]/page.js` or `pages/docs/[...slug].js`

- **Middleware**:
  ```javascript
  // middleware.js
  export function middleware(request) {
    // Your middleware logic
  }
  
  export const config = {
    matcher: '/api/:path*',
  };
  ```

## 13. Environment Variables
Create `.env.local` file for environment variables:
```
API_KEY=your_api_key_here
```

Access with `process.env.API_KEY` in your code.

## 14. Common Next.js Commands
- `npx create-next-app@latest` - Create a new project
- `npm run dev` - Start development server
- `npm run build` - Build for production
- `npm run start` - Start production server
- `npm run lint` - Run ESLint
- `npx next info` - Print environment information

## 15. Useful Resources
- [Next.js Documentation](https://nextjs.org/docs)
- [Next.js GitHub Repository](https://github.com/vercel/next.js)
- [Vercel Platform](https://vercel.com) (for deployment)
- [Next.js Discord Community](https://nextjs.org/discord)
