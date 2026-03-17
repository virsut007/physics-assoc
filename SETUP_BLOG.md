# Blog CMS Setup Instructions

This branch introduces a fully integrated, built-in blog page and a custom Content Management System (CMS) powered by Supabase. 

It replaces the old external GitHub Pages blog with a modern Next.js implementation matching the current website theme.

## Architecture Overview
- **Storage & Auth:** Supabase (PostgreSQL + Supabase Auth)
- **Content Rendering:** Markdown (`react-markdown` + `remark-gfm`)
- **Public Routes:** `/blog`, `/blog/[slug]`
- **Protected Admin Routes:** `/admin`, `/admin/login`, `/admin/editor`

## Required Production Setup
To merge this into production, the repository owner must complete the following infrastructure setup. The blog will crash in production if these environment variables are missing.

### 1. Create the Supabase Project
1. Navigate to supabase.com and create a new, free project.
2. In the Supabase Dashboard, open the "SQL Editor".
3. Copy the contents of the `supabase-schema.sql` file (included in the root of this repository).
4. Paste it into the SQL Editor and click "Run". This sets up the `articles` table and the required Row Level Security (RLS) policies.

### 2. Configure Environment Variables
1. In the Supabase Dashboard, navigate to Settings > API.
2. Copy the "Project URL" and the "anon public" key.
3. Open the Vercel Dashboard for this project.
4. Navigate to Settings > Environment Variables.
5. Add the following two variables:
   - `NEXT_PUBLIC_SUPABASE_URL` = (Your Project URL)
   - `NEXT_PUBLIC_SUPABASE_ANON_KEY` = (Your anon key)

### 3. Create Administrator Accounts
To allow users to log in to the CMS to publish articles:
1. In the Supabase Dashboard, navigate to Authentication > Users.
2. Click "Add User" and provide an email and password for the authorized administrator.

## Usage after Deployment
Once the above is configured and the code is deployed via Vercel:
- Authorized users can navigate to `https://yourdomain.com/admin/login` to access the dashboard.
- From the dashboard, they can draft, edit, and publish articles using the built-in markdown editor.
- Published articles will immediately appear on `https://yourdomain.com/blog`.
