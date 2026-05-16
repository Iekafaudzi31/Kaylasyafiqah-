# Kaylasyafiqah-

E-commerce product catalog for browsing and displaying barang (goods/items) for sale.

Built with Next.js 14 (App Router), React, TypeScript, and CSS Modules. Product data is served via Next.js API routes — no separate backend required.

## Prerequisites

- Node.js 20+
- npm 10+

## Setup

```bash
# Clone the repository
git clone https://github.com/Iekafaudzi31/Kaylasyafiqah-.git
cd Kaylasyafiqah-

# Install dependencies
npm install

# Start the development server
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

## Available Scripts

| Command | Description |
|---|---|
| `npm run dev` | Start development server with hot reload |
| `npm run build` | Build for production |
| `npm start` | Start production server (requires build first) |
| `npx tsc --noEmit` | Type-check without emitting files |

## Project Structure

```
src/
├── app/            # Pages, layouts, and API routes (Next.js App Router)
├── components/     # Shared UI components
├── lib/            # Utilities and data fetching helpers
└── types/          # Shared TypeScript types
```

See [AGENTS.md](./AGENTS.md) for full directory map and development conventions.

## Environment Variables

Copy `.env.example` to `.env.local` and fill in the values before running the app.

```bash
cp .env.example .env.local
```
