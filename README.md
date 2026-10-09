# S Chat — Hosting guide

This repository contains `frontend/` (React + Vite) and `backend/` (Express + Socket.IO). Recommended hosting: Vercel for the frontend, Render for the persistent Node/Socket.IO backend, and MongoDB Atlas for the database.

## 1. Push to GitHub

Keep both folders in the same repository. Do not commit `.env` files, passwords, JWT secrets, `node_modules`, or uploaded user files. The backend `.gitignore` excludes `backend/uploads/*`; the source ZIP has been cleaned of previously uploaded runtime files.

## 2. Configure MongoDB Atlas

Create/choose a database user and database, then copy the Atlas connection string into Render as `MONGO_URI`. Add the Render service's outbound IPs to the Atlas Network Access list if available. `0.0.0.0/0` permits access from anywhere and should only be used temporarily if you understand the security implications.

## 3. Deploy the backend to Render

Use the included `render.yaml` blueprint, or create a Web Service from the GitHub repository with Root Directory `backend`, Build Command `npm install`, and Start Command `npm start`. Add these environment variables in Render:

- `MONGO_URI`: your private Atlas connection string
- `JWT_SECRET`: a long random secret, at least 32 characters
- `JWT_EXPIRES_IN`: `7d` (optional)
- `CLIENT_URL`: exact Vercel origin, e.g. `https://your-project.vercel.app` (no path). For preview domains, add each origin comma-separated if you need them.
- `NODE_ENV`: `production`

After deployment, test `https://YOUR-RENDER-SERVICE.onrender.com/api/health`. It should return HTTP 200 and `database: connected`.

## 4. Deploy the frontend to Vercel

Import the same GitHub repository. Set Root Directory to `frontend`, Framework Preset to Vite, Build Command to `npm run build`, and Output Directory to `dist`. Add environment variables:

- `VITE_API_URL=https://YOUR-RENDER-SERVICE.onrender.com/api`
- `VITE_SOCKET_URL=https://YOUR-RENDER-SERVICE.onrender.com`

Replace the example hostname with the actual Render URL. Redeploy after adding or changing environment variables. `frontend/vercel.json` enables SPA route fallback.

## 5. Update backend CORS

Once Vercel provides the real production domain, set Render's `CLIENT_URL` to that exact origin and redeploy the backend. The value is the origin only: `https://your-project.vercel.app`, not a URL ending in `/dashboard`.

## 6. File upload persistence — important

The current upload implementation writes files to `backend/uploads`. This works locally, but ordinary ephemeral hosting filesystems can lose uploaded files on redeploy/restart. For production, configure a persistent disk mounted at the backend's uploads directory (where supported by your hosting plan), or migrate uploads to durable object storage such as Cloudinary or Amazon S3. Do not assume local disk uploads are durable on a free ephemeral service.

## 7. Local development

Backend: copy `backend/.env.example` to `backend/.env`, fill in real private values, then run `npm install` and `npm run dev` inside `backend/`. Frontend: run `npm install` and `npm run dev` inside `frontend/`. With no Vite variables set, the frontend defaults to `http://localhost:5000` for local API and Socket.IO.

## 8. Final smoke test

- Register and log in with two test accounts.
- Send messages in both directions and verify read/delivered states.
- Test groups, online status, typing, unread counts, and notification sound.
- Upload and open attachments; test profile images if used.
- Refresh a nested route such as `/dashboard`.
- Verify browser console/network tab has no CORS, mixed-content, or failed Socket.IO requests.

Never paste real MongoDB credentials or `JWT_SECRET` into public repositories or chats. If any secret has already been exposed, rotate it.
