# Bookmark Manager

A full-stack bookmark management application built with Next.js and Supabase, featuring secure Google OAuth authentication, row-level security, and cross-tab synchronization.

## 🚀 Live Demo

**Production URL**: [https://your-vercel-url.vercel.app](https://your-vercel-url.vercel.app)

## ✨ Features

- Google OAuth authentication (Supabase Auth)
- Secure Row-Level Security (RLS) for user data isolation
- Create and delete bookmarks
- Cross-tab synchronization (no manual refresh required)
- Optimistic UI updates for responsive UX
- Fully deployed on Vercel

## 🛠️ Tech Stack

**Frontend**
- Next.js 14 (App Router)
- React 18
- TypeScript
- Tailwind CSS

**Backend**
- Supabase (PostgreSQL + Auth)
- Row Level Security (RLS)

**Deployment**
- Vercel

## 🏗️ Architecture Overview

The application uses:
- **Next.js App Router** for routing and layout management
- **Supabase Auth** for OAuth-based authentication
- **PostgreSQL with RLS** to enforce per-user data isolation
- **Client-side data fetching** with controlled synchronization logic
- **Environment-based configuration** for development and production

All sensitive credentials are handled via environment variables and never committed to version control.

## 🔒 Security Design

Row-Level Security policies ensure:
- Users can only read their own bookmarks
- Users can only insert bookmarks tied to their `auth.uid()`
- Users can only delete their own records

Example policy logic:
```sql
auth.uid() = user_id
```

This guarantees strict data isolation at the database level.

## 🚧 Challenges Faced & Solutions

### 1️⃣ Cross-Tab Synchronization

**Problem**: Bookmarks needed to reflect across multiple open tabs without requiring manual refresh.

**Solution**: Implemented periodic synchronization combined with optimistic UI updates. This ensures:
- Immediate feedback in the active tab
- Automatic state consistency across tabs
- No full page reload required

This approach prioritizes reliability and simplicity while maintaining performance for the project scope.

### 2️⃣ Google OAuth Configuration Across Environments

**Problem**: OAuth redirects behaved differently between localhost (development) and Vercel (production). Incorrect redirect URIs caused authentication to fallback to the hosted login page.

**Solution**:
- Configured **Authorized JavaScript Origins** in Google Cloud Console
- Added Supabase callback URL: `https://<project-id>.supabase.co/auth/v1/callback`
- Set correct **Site URL** in Supabase Auth configuration
- Used dynamic redirect handling:
```typescript
redirectTo: `${window.location.origin}/dashboard`
```

This ensured environment-aware OAuth redirection.

### 3️⃣ Deployment Configuration

**Problem**: Initial Vercel deployment failed due to missing environment variables.

**Solution**:
- Added `NEXT_PUBLIC_SUPABASE_URL`
- Added `NEXT_PUBLIC_SUPABASE_ANON_KEY`
- Configured environment variables in Vercel dashboard
- Created `.env.local` for development

This separated development and production configuration properly.

## ⚙️ Setup Instructions

### Prerequisites
- Node.js 18+
- Supabase account
- Google Cloud Console account

### 1️⃣ Clone Repository
```bash
git clone <repository-url>
cd bookmark-manager
npm install
```

### 2️⃣ Configure Supabase

1. Create a project at [https://supabase.com](https://supabase.com)
2. Run the SQL script from `supabase-setup.sql` in SQL Editor
3. Enable Google provider in **Authentication → Providers**
4. Add your Google OAuth Client ID and Secret

### 3️⃣ Setup Google OAuth

1. Go to [Google Cloud Console](https://console.cloud.google.com)
2. Create OAuth 2.0 Client ID
3. Add **Authorized redirect URI**:
   ```
   https://<your-project>.supabase.co/auth/v1/callback
   ```
4. Copy Client ID and Client Secret to Supabase

### 4️⃣ Environment Variables

Create `.env.local`:
```bash
NEXT_PUBLIC_SUPABASE_URL=your_supabase_project_url
NEXT_PUBLIC_SUPABASE_ANON_KEY=your_supabase_anon_key
```

Get these from: **Supabase Dashboard → Settings → API**

### 5️⃣ Run Development Server
```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000)

### 6️⃣ Deploy to Vercel

1. Push code to GitHub
2. Import project in Vercel
3. Add environment variables in Vercel dashboard
4. Deploy

## 📁 Project Structure

```
app/
├── page.tsx              # Login page with Google OAuth
├── dashboard/page.tsx    # Main application with CRUD operations
├── layout.tsx            # Root layout with metadata
└── globals.css           # Global styles and animations
lib/
└── supabase.ts           # Supabase client configuration
supabase-setup.sql        # Database schema and RLS policies
```

## 🔐 Security Features

- **Row Level Security (RLS)**: Database-level access control
- **OAuth Authentication**: No password storage, delegated to Google
- **Environment Variables**: Sensitive credentials isolated from codebase
- **Session Management**: Handled by Supabase Auth

## 📝 Future Enhancements

- Edit bookmark functionality
- Search and filter capabilities
- Tags and categories
- Export to JSON/CSV

---

**Built with Next.js, Supabase & TypeScript**
