# Cyber Smart Week 2026 Word Find

Public GitHub Pages game with a privacy-protected Supabase leaderboard.

## Privacy design

- The GitHub repository and game are public.
- The Supabase browser publishable/anon key may be present in `config.js`; its permissions are restricted by database grants and Row Level Security.
- The source table stores leaderboard name, email, score and completion time.
- Anonymous visitors have INSERT-only access to the source table. They cannot directly select, update or delete its rows.
- The public leaderboard calls a restricted database function that returns only leaderboard name, score and time.
- Email address, record ID and completion timestamp are not returned by the public function.
- Never place a `service_role` key, secret key or database password in GitHub.

## Setup

1. Create a Supabase project.
2. Open **SQL Editor**, paste the complete contents of `supabase_setup.sql`, then select **Run**.
3. In Supabase project settings, copy the **Project URL** and browser-safe **publishable/anon key**.
4. Replace the two placeholders in `config.js`. Do not use the service-role key.
5. Upload `index.html`, `config.js`, `supabase_setup.sql`, `README.md` and `.nojekyll` to the root of the GitHub repository.
6. Make the repository public.
7. In GitHub go to **Settings > Pages**. Select **Deploy from a branch**, branch **main**, folder **/(root)**, then save.

## Required privacy test before launch

1. Submit a result using a test email address.
2. Confirm the row appears in Supabase **Table Editor > word_find_leaderboard**.
3. Confirm the public leaderboard shows the leaderboard name, score and time only.
4. In a private/incognito browser window, confirm no email address is visible.
5. Do not launch with real participant data if a public client can directly read `word_find_leaderboard`.

## Files

- `index.html`: game and safe leaderboard integration
- `config.js`: browser-safe Supabase URL and publishable/anon key placeholders
- `supabase_setup.sql`: protected table, RLS insert policy and email-free Top 10 function
- `.nojekyll`: serves the repository as a plain static site
