# Complete Guide to Creating a Next.js Application

## Prerequisites
- Install Node.js (version 18.17.0 or later)
- Ensure npm (comes with Node.js) or yarn is installed

## 1. Create a New Next.js Project
Using the official create-next-app tool (recommended):

```bash
npx create-next-app@latest my-next-app
```

During setup, you'll be asked several configuration questions:
- Would you like to use TypeScript? (Yes/No)
- Would you like to use ESLint? (Yes/No)
- Would you like to use Tailwind CSS? (Yes/No)
- Would you like to use the App Router? (Yes/No)
- Would you like to customize the default import alias? (Yes/No)

## 2. Navigate to Your Project
```bash
cd my-next-app
```

## 3. Project Structure
Basic structure of a Next.js app:

- `app/` or `pages/` - Contains routes and pages
- `public/` - Static assets (images, fonts, etc.)
- `components/` - Reusable React components
- `styles/` - CSS and styling files
- `next.config.js` - Next.js configuration
- `package.json` - Project dependencies and scripts

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
