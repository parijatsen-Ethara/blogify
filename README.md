# Ethara Blog

Ethara Blog is a polished full-stack publishing platform built for modern content creators. It combines a smooth, animated frontend with a practical backend so you can publish articles, manage categories and tags, collect newsletter signups, and handle contact submissions without losing the human touch.

## What you get

- **A polished reader experience** with animated page transitions, a reading progress bar, and a clean content-first layout.
- **A rich editor workflow** powered by TipTap, so posts can include formatted text, links, images, and other content-rich elements.
- **A usable admin area** for managing posts, categories, tags, subscribers, comments, and contact submissions.
- **Built-in search and filtering** so readers can find articles quickly.
- **Email-driven communication** for contact form messages and newsletter signups.
- **Secure basics** including JWT-based auth, rate limiting, and sanitization for user input.

## Project structure

```text
blogify/
├── backend/   # Express + MongoDB API
└── frontend/  # Next.js + TypeScript UI
```

## Prerequisites

- Node.js 18+
- MongoDB (local or MongoDB Atlas)
- A Cloudinary account for image uploads
- A Gmail account with an app password for email sending

## Getting started

### 1. Install dependencies

```bash
cd backend
npm install

cd ../frontend
npm install
```

### 2. Set up environment variables

Create a backend environment file and add the values your app needs:

```bash
cp backend/.env.example backend/.env
```

Use the following variables as a guide:

```env
PORT=5000
NODE_ENV=development
MONGODB_URI=mongodb://localhost:27017/ethara-blog
JWT_SECRET=replace-with-a-long-random-secret
JWT_EXPIRES_IN=7d
ADMIN_EMAIL=you@example.com
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_SECURE=false
SMTP_USER=your_gmail@gmail.com
SMTP_PASS=your_gmail_app_password
CLOUDINARY_CLOUD_NAME=your_cloud_name
CLOUDINARY_API_KEY=your_api_key
CLOUDINARY_API_SECRET=your_api_secret
CORS_ORIGINS=http://localhost:3000
```

Create a frontend environment file as well:

```bash
cp frontend/.env.example frontend/.env.local
```

Example values:

```env
NEXT_PUBLIC_API_URL=http://localhost:5000/api
NEXT_PUBLIC_SITE_URL=http://localhost:3000
NEXT_PUBLIC_SITE_NAME=Ethara Blog
NEXT_PUBLIC_SITE_DESCRIPTION=A modern blog platform for thoughtful stories and practical ideas.
```

### 3. Seed the database

The seed script will clear the current data and create a small starter dataset for local development.

```bash
cd backend
npm run seed
```

This creates:

- one admin user
- starter categories and tags
- sample published posts
- a few newsletter subscribers
- a couple of contact submissions

The default admin login is:

- **Email:** `alex@ethara.blog`
- **Password:** `Admin@1234`

### 4. Run the app locally

Open two terminals and start both services:

```bash
cd backend
npm run dev
```

```bash
cd frontend
npm run dev
```

Then open the app at:

- **Frontend:** `http://localhost:3000`
- **Backend health check:** `http://localhost:5000/api/health`

## Admin access

After seeding the database, sign in here:

- `http://localhost:3000/admin/login`

Use the seeded admin credentials above to log in.

## Email setup

If you want the contact and newsletter notifications to work, use Gmail SMTP with an app password.

1. Turn on two-step verification in your Google account.
2. Create an app password for mail.
3. Paste that password into `SMTP_PASS` in the backend environment file.

## Cloudinary setup

1. Create a free Cloudinary account.
2. Copy your cloud name, API key, and API secret.
3. Add them to your backend environment file.

## Deployment notes

For a simple Railway setup, treat the frontend and backend as two separate services in the same project.

### Frontend service

- Root directory: `frontend`
- Build command: `npm run build`
- Start command: `npm start`
- Add all `NEXT_PUBLIC_*` variables

### Backend service

- Root directory: `backend`
- Build command: `npm install`
- Start command: `npm start`
- Add the backend environment variables
- Attach a MongoDB plugin if you do not already have one

### Connect the services

- Set the frontend `NEXT_PUBLIC_API_URL` to your backend public URL, for example:
  `https://your-backend.railway.app/api`
- Set backend `CORS_ORIGINS` to your frontend URL.

## Useful API endpoints

### Public

- `GET /api/posts`
- `GET /api/posts/:slug`
- `POST /api/comments/:postId`
- `POST /api/contact`
- `POST /api/newsletter`
- `GET /api/search?q=query`
- `POST /api/auth/login`

### Admin

- `POST /api/posts`
- `PUT /api/posts/:id`
- `DELETE /api/posts/:id`
- `GET /api/admin/stats`
- `GET /api/admin/contacts`
- `GET /api/admin/subscribers`
- `GET /api/admin/comments`
- `POST /api/upload`

## Tech stack

- **Frontend:** Next.js 16, React 19, TypeScript, Tailwind CSS
- **Animations:** Framer Motion
- **Editor:** TipTap
- **Forms:** React Hook Form and Zod
- **Data fetching:** SWR and Axios
- **Backend:** Node.js, Express, MongoDB, Mongoose
- **Authentication:** JWT
- **Email:** Nodemailer
- **Media uploads:** Cloudinary
- **Security:** rate limiting, sanitization, and input validation

## License

MIT

