# ReMobix Admin Dashboard — Setup Guide

This project contains a responsive storefront and Supabase-backed admin dashboard for ReMobix, Hyderabad, Sindh. WhatsApp contact is set to **03173144018** (international link format `923173144018`).

## Files
- `index.html`: storefront + admin dashboard (add/edit/delete inventory)
- `config.js`: Supabase project URL and public anon key placeholders
- `schema.sql`: database schema and access policies

## A. Connect the database
1. Create a project at https://supabase.com/.
2. In the Supabase dashboard, open **SQL Editor**, paste the entire `schema.sql`, and run it.
3. Open **Project Settings → API** and copy your **Project URL** and **anon/public key**.
4. Edit `config.js`; replace `YOUR_SUPABASE_PROJECT_URL` and `YOUR_SUPABASE_ANON_PUBLIC_KEY` with those values.
5. Never put a `service_role` or secret key in browser code.

## B. Create your private admin account
1. Open **Authentication → Users** in Supabase and create a user with your email and a strong password. Disable public sign-ups if you don't want public account creation.
2. Copy the UUID for that user.
3. In SQL Editor, run: `insert into public.remobix_admins(user_id) values ('PASTE-REAL-USER-UUID-HERE');`
4. Open your website, click **Open admin**, and sign in. Only user IDs listed in `remobix_admins` can change stock.

## C. Publish on Netlify
1. Keep `index.html` and `config.js` together in the same folder.
2. Create an account at https://www.netlify.com/.
3. Use Netlify's manual deploy flow to upload the folder, or upload the project to GitHub and connect the repository to Netlify.
4. Netlify gives you a public `*.netlify.app` address. Test the storefront, WhatsApp links, admin login, add/edit/delete, and mark-as-sold on your phone.
5. Optional: buy a domain and connect it in Netlify domain settings.

## Admin dashboard features
- Add a phone with brand, model, storage, price, condition, PTA status, available/sold status, image URL and description.
- Edit a listing, mark it sold (it disappears from the public store), or delete it.
- Product photos currently use a direct image URL; uploads can be added later with Supabase Storage.

## Before launch
- Set the real Supabase configuration and run `schema.sql`.
- Create an admin auth user and add its UUID to `remobix_admins`.
- Add only real stock you own or are authorized to resell; confirm condition, ownership and PTA/DIRBS status.
- Add your business terms, returns/warranty policy and privacy notice if applicable.
- Current site has no payment checkout or delivery integration. Customers enquire on WhatsApp.
