Write it, but change Claude Agent to OptiDev Agent

  OptiDev Cloud Documentation Plan (Revised)

  Target Audience: Users with light technical experience (can write basic SQL, copy API keys) but may not understand environment variables or infrastructure concepts.

  Writing Approach: Lead with "what you can do" and "how to do it" with UI-focused instructions. Technical details at the end of each page as optional reference.

  ---
  1. How to Use (optidev-cloud/how-to-use.mdx)

  Sections:

  What is OptiDev Cloud

  - A ready-to-use backend for your app - includes a database to store data, user login system, and file storage
  - No separate accounts or setup needed - activate it with one click from your project
  - Works automatically with Claude Agent - just ask Claude to "save user data" or "add login" and it handles the rest

  Activating OptiDev Cloud

  - Open your project, click the "OptiDev Cloud" tab, then click "Activate OptiDev Cloud"
  - Pick a region closest to your users (e.g., US East for North America, Frankfurt for Europe)
  - Wait 1-2 minutes for setup - you'll see a green "Active" badge when it's ready

  Finding Your Connection Details

  - After activation, the "Connection Info" tab shows your API URL and keys
  - Click the "Copy" button next to any value to copy it to your clipboard
  - The "Connect" button shows your database connection string for tools like database clients

  For Developers (Technical Reference)

  - Environment variables VITE_SUPABASE_URL and VITE_SUPABASE_PUBLISHABLE_KEY are auto-injected into .env.local
  - Use the Supabase JavaScript client (@supabase/supabase-js) for frontend integration
  - Connection string uses session pooler (port 5432) for PostgreSQL compatibility

  ---
  2. Database (optidev-cloud/database.mdx)

  Sections:

  What is the Database

  - A place to store and organize your app's data in tables (like spreadsheets with rows and columns)
  - Query your data using SQL - a simple language for asking questions like "show me all users" or "find orders over $100"
  - Your data is automatically backed up and can be accessed from anywhere in the world

  Browsing Your Tables

  - Click the "Database" tab to see all your tables listed in the left sidebar
  - Click any table name to see its data - it automatically loads the first 10 rows
  - Use the pagination controls at the bottom to browse through more rows (10, 25, 50, or 100 at a time)

  Writing and Running Queries

  - Type SQL in the editor area, for example: SELECT * FROM users WHERE created_at > '2024-01-01'
  - Click "Execute Query" (or press the play button) to run your query and see results
  - Double-click any cell in the results to edit it directly - press Enter to save or Escape to cancel

  Exporting Your Data

  - Click the menu icon (three dots) above results to export data as JSON, CSV, or Excel files
  - Select specific rows using checkboxes, then export just those rows
  - Use "Copy as SQL" to get INSERT statements you can run elsewhere

  For Developers (Technical Reference)

  - Tables are created in the public schema; use information_schema queries for metadata
  - Cell editing requires an id column in the table for row identification
  - Direct SQL execution via pg client with session pooler connection

  ---
  3. Edge Functions (optidev-cloud/edge-functions.mdx)

  Sections:

  What are Edge Functions

  - Small pieces of code that run on the server - useful for things you can't do in the browser (like sending emails or processing payments)
  - They run close to your users worldwide, making your app faster
  - Write them in TypeScript (similar to JavaScript) and deploy with one click

  Creating Your First Function

  - Click "Create Sample Function" to generate a hello-world example in your project
  - Find it in your project files under supabase/functions/hello-world/index.ts
  - Edit the code in your editor - Claude Agent can help you modify it for your needs

  Deploying Functions

  - In the "Edge Functions" tab, you'll see functions in your workspace listed under "Workspace Functions"
  - Click "Deploy" next to any function to publish it to OptiDev Cloud
  - Once deployed, you'll see it under "Deployed Functions" with a green checkmark

  Testing Your Functions

  - Click "Test" next to any deployed function to open the test panel
  - Choose the HTTP method (GET, POST, etc.) and add any data your function expects
  - Click "Send Request" to see the response - useful for debugging before connecting to your app

  Calling Functions from Your App

  - Click "Copy URL" to get the function's web address
  - Call this URL from your app using fetch or any HTTP library
  - The function runs on the server and returns data to your app

  For Developers (Technical Reference)

  - Functions use Deno runtime with TypeScript support
  - CORS headers must be handled in your function code (sample includes this)
  - Access secrets via Deno.env.get('SECRET_NAME') - manage secrets in the Secrets tab

  ---
  4. Storage (optidev-cloud/storage.mdx)

  Sections:

  What is Storage

  - A place to store files like images, PDFs, videos, and documents for your app
  - Files are delivered fast worldwide through a CDN (content delivery network)
  - Control who can access files - make them public for everyone or private for logged-in users only

  Understanding Buckets

  - Files are organized into "buckets" - think of them like folders for different types of content
  - Create buckets for different purposes (e.g., "avatars" for profile pictures, "documents" for uploads)
  - Each bucket can have its own access rules - public or private

  Uploading Files

  - Use the Supabase client in your app to upload files from user input (like file pickers)
  - Files get a unique URL you can save to your database and display in your app
  - Large files are handled automatically with progress tracking

  Getting File URLs

  - Public files have a direct URL anyone can access - great for images on your website
  - Private files need a "signed URL" that expires after a set time - good for sensitive documents
  - Copy file URLs from the dashboard or generate them in code

  For Developers (Technical Reference)

  - Storage is S3-compatible with Supabase Storage API wrapper
  - Use supabase.storage.from('bucket').upload() for uploads with RLS policy checks
  - Signed URLs support custom expiration times (default 60 seconds)

  ---
  5. Auth (optidev-cloud/auth.mdx)

  Sections:

  What is Auth

  - A complete login system for your app - lets users create accounts and sign in securely
  - Supports email/password, phone number (SMS codes), and "Sign in with Google"
  - Handles password resets, email verification, and session management automatically

  Enabling Sign-in Methods

  - Click the "Auth" tab and you'll see available sign-in methods: Email, Phone, and Google
  - Click on any method to see its settings and toggle it on or off
  - Each method shows "Enabled" or "Disabled" - click to configure

  Email Sign-in

  - The most common option - users enter email and password to create an account or log in
  - "Confirm Email" setting requires users to click a link in their email before accessing your app
  - Great for most apps where you want to verify real email addresses

  Phone Sign-in

  - Users enter their phone number and receive a one-time code via SMS
  - Good for apps where users prefer not to remember passwords
  - Requires SMS provider setup (configured in the Phone settings panel)

  Google Sign-in

  - Users click "Sign in with Google" and use their existing Google account
  - Fastest option for users - no new password to create or remember
  - Requires setting up Google OAuth credentials (the settings panel guides you through this)

  User Management Settings

  - "Allow New Users to Sign Up" - turn off to prevent new registrations (useful for invite-only apps)
  - "Enable Anonymous Users" - let people use your app without creating an account first
  - "Allowed URLs" - list the web addresses where sign-in redirects are allowed

  For Developers (Technical Reference)

  - Auth integrates with Row Level Security (RLS) policies using auth.uid() in PostgreSQL
  - JWT tokens are managed automatically by the Supabase client
  - Use supabase.auth.signInWithPassword(), signInWithOtp(), or signInWithOAuth() for each method

  ---
  This revised structure:
  - Leads with plain-language explanations of what things do
  - Uses UI-focused step-by-step instructions
  - Puts technical details in clearly labeled "For Developers" sections at the end
  - Avoids jargon in the main content (no "environment variables" until the tech section)