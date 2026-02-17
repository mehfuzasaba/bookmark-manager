# Bookmark Manager

A full-stack bookmark management application with real-time synchronization and secure authentication.

## Features

- Google OAuth authentication
- Real-time bookmark synchronization across devices
- Row-level security for data isolation
- CRUD operations (Create, Read, Delete)
- Responsive UI with Tailwind CSS

## Tech Stack

- **Frontend**: Next.js 14 (App Router), React 18, TypeScript
- **Backend**: Supabase (PostgreSQL, Auth, Realtime)
- **Styling**: Tailwind CSS
- **Deployment**: Vercel

## Setup

### 1. Install Dependencies

```bash
npm install
```

### 2. Configure Supabase

1. Create a project at [supabase.com](https://supabase.com)
2. Run the SQL script from `supabase-setup.sql` in the SQL Editor
3. Enable Realtime for the `bookmarks` table (Database → Replication)
4. Enable Google OAuth provider (Authentication → Providers)

### 3. Environment Variables

Create `.env.local`:

```bash
NEXT_PUBLIC_SUPABASE_URL=your_supabase_project_url
NEXT_PUBLIC_SUPABASE_ANON_KEY=your_supabase_anon_key
```

Get credentials from Supabase Dashboard → Settings → API

### 4. Run Development Server

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000)

## Project Structure

```
app/
├── page.tsx              # Login page
├── dashboard/page.tsx    # Main application
├── layout.tsx            # Root layout
└── globals.css           # Styles
lib/
└── supabase.ts           # Supabase client
supabase-setup.sql        # Database schema
```

## Key Features

- **Row Level Security**: Database-level user isolation
- **Real-time Subscriptions**: Instant updates across devices
- **OAuth Authentication**: Secure Google login
- **TypeScript**: Type-safe codebase
