Smart Bookmark App:

Production-Ready Full-Stack Application built with Next.js, Supabase & Vercel

🔗 Live Demo:
https://smart-bookmark-app-fawn-two.vercel.app

🔗 GitHub Repository:
https://github.com/ritiksachan24/smart-bookmark-app

-----------------------------------------------------------------------------------------------

Project Overview:

Smart Bookmark App is a secure, real-time bookmark manager built using modern full-stack technologies.

The application demonstrates:

> OAuth-based authentication (Google)
> Secure database design with Row Level Security (RLS)
> Real-time data synchronization
> Production-grade deployment workflow
> Clean, responsive UI using Tailwind CSS

This project reflects real-world engineering practices including authentication configuration, environment management, database-level security enforcement and CI/CD deployment.

-----------------------------------------------------------------------------------------------

Features:

1. Google OAuth Authentication (Supabase Auth)
2. Add bookmarks (Title + URL)
3. Delete bookmarks
4. User-specific private data (Row Level Security)
5. Real-time updates across multiple tabs
6. Modern responsive UI
7. Deployed on Vercel with CI/CD

-----------------------------------------------------------------------------------------------

Tech Stack:

Layer	                                          Technology

> Frontend	                                      Next.js (App Router)
> Styling                                         Tailwind CSS
> Backend-as-a-Service	                          Supabase
> Database	                                      PostgreSQL
> Authentication	                              Google OAuth
> Deployment	                                  Vercel

-----------------------------------------------------------------------------------------------

Database Schema:

create table bookmarks (
  id uuid primary key default uuid_generate_v4(),
  user_id uuid references auth.users on delete cascade,
  title text not null,
  url text not null,
  created_at timestamp with time zone default now()
);

> Row Level Security Policies-

create policy "Users can view their own bookmarks"
on bookmarks for select
using (auth.uid() = user_id);

create policy "Users can insert their own bookmarks"
on bookmarks for insert
with check (auth.uid() = user_id);

create policy "Users can delete their own bookmarks"
on bookmarks for delete
using (auth.uid() = user_id);

This ensures complete data isolation per user at the database level.

-----------------------------------------------------------------------------------------------

Real-Time Implementation:

1. Implemented Supabase postgres_changes subscription
2. Updates are reflected instantly across browser tabs
3. Optimistic UI update ensures immediate feedback on insert

-----------------------------------------------------------------------------------------------

Authentication Flow:

1. User logs in via Google OAuth.
2. Supabase manages session securely.
3. RLS ensures users access only their own bookmarks.
4. Logout invalidates the session and redirects to login page.

-----------------------------------------------------------------------------------------------

Deployment Architecture:

> Development Flow:
Local Development → GitHub → Vercel Auto Deploy


> Production Configuration Includes:

1. Environment variable management
2. Supabase project URL and public key setup
3. Google OAuth domain configuration
4. Supabase redirect URL configuration

-----------------------------------------------------------------------------------------------

Environment Variables:

The following variables are required:

NEXT_PUBLIC_SUPABASE_URL
NEXT_PUBLIC_SUPABASE_ANON_KEY


Configured in:

> .env.local (local development)
> Vercel Dashboard (production)

-----------------------------------------------------------------------------------------------

Engineering Challenges & Solutions:

1. OAuth Redirect Mismatch

Resolved by correctly configuring:
> Google Authorized JavaScript Origins
> Supabase Redirect URLs
> Production domain whitelisting

2. Supabase Auth Lock Timeout

Resolved by clearing stale sessions and improving session handling.

3. Tailwind Configuration Conflict

Downgraded to stable Tailwind v3 for compatibility with Next.js App Router.

4. Real-time Not Updating in Production

Enabled Supabase Realtime replication and added optimistic UI updates.

-----------------------------------------------------------------------------------------------

Future Enhancements:

> Edit bookmark feature
> Search & filter functionality
> Bookmark categories/tags
> Dark mode support
> Toast notifications
> Unit & integration testing