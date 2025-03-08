# Next.js Project

A modern web application built with Next.js, React, and Node.js.

## Prerequisites

Ensure you have the correct Node.js version required for Next.js:
* Required Node.js version: **^18.18.0 || ^19.8.0 || >= 20.0.0**
* Check your current version: `node -v`

## Getting Started

### Setting Up Node.js

#### Using NVM (Recommended)

**For Linux & macOS:**
```bash
curl -fsSL https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.5/install.sh | bash

# After installation, restart your terminal or run:
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
```

**For Windows:**
1. Download and install **nvm-windows** from: https://github.com/coreybutler/nvm-windows/releases
2. Restart your terminal after installation.

**Installing the required Node.js version:**
```bash
nvm install 20
nvm use 20
nvm alias default 20
```

#### Manual Installation

Download the latest LTS version from: https://nodejs.org/en/download

### Installing Dependencies

```bash
# Using npm
npm install

# Using Yarn
yarn

# Using pnpm
pnpm install
```

### Environment Variables

Create a `.env.local` file in the root directory with the following variables:
```
NEXT_PUBLIC_API_URL=your_api_url_here
```

### Running the Development Server

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

## Project Structure

```
├── public/            # Static files
├── src/               # Source files
│   ├── app/           # App router
│   ├── components/    # React components
│   ├── lib/           # Utility functions
│   └── styles/        # CSS files
├── .env.local         # Local environment variables
├── next.config.js     # Next.js configuration
└── package.json       # Project dependencies
```

## Available Scripts

- `npm run dev` - Run development server
- `npm run build` - Build for production
- `npm start` - Start production server
- `npm run lint` - Run ESLint
- `npm run test` - Run tests

## Deployment

This project can be deployed on [Vercel](https://vercel.com/), the platform created by the creators of Next.js.

For more information on deployment options, see the [Next.js deployment documentation](https://nextjs.org/docs/deployment).

## Learn More

To learn more about Next.js, take a look at the following resources:

- [Next.js Documentation](https://nextjs.org/docs) - learn about Next.js features and API.
- [Learn Next.js](https://nextjs.org/learn) - an interactive Next.js tutorial.

## Troubleshooting

- If `nvm: command not found`, restart your terminal and try again.
- If `node -v` still shows the old version, ensure `nvm use 20` has been run.
- If using Windows, make sure **nvm-windows** is installed and restart your system.
