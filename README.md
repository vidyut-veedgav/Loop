# Loop

A minimalist productivity app with only two states: **Now** and **Next**. Built to combat the Zeigarnik effect by helping you offload mental clutter without the pressure to categorize or schedule.

## Tech Stack

- **Language:** TypeScript
- **Framework:** Next.js
- **Frontend:** React, Tailwind CSS, Shadcn
- **Backend:** Supabase
- **ORM:** Prisma
- **Deployment:** Vercel

---

## Setup Instructions

### 1. Clone Repository

```bash
git clone <your-repo-url>
cd loop
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Environment Configuration

Create a `.env` file in the project root:

```env
NEXT_PUBLIC_SUPABASE_URL=""
NEXT_PUBLIC_SUPABASE_ANON_KEY=""
DATABASE_URL=""
DIRECT_URL=""
```

**Where to find these:**
- `NEXT_PUBLIC_SUPABASE_URL` and `NEXT_PUBLIC_SUPABASE_ANON_KEY`: Supabase Dashboard → Project Settings → API
- `DATABASE_URL` (Transaction Pooler): Supabase Dashboard → Connect → Transaction Pooler
- `DIRECT_URL` (Session Pooler): Supabase Dashboard → Connect → Session Pooler

### 4. Install Prisma

```bash
npm install @prisma/client@6.19.2
npm install -D prisma@6.19.2
npx prisma init
```

### 5. Set Up Database Schema

After creating your `prisma/schema.prisma` file:

```bash
npx prisma generate
npx prisma db push
```

### 6. Install Supabase Client

```bash
npm install @supabase/ssr@^0.8.0 @supabase/supabase-js@^2.94.1
```

### 7. Install Shadcn UI

```bash
npx shadcn@latest init
```

Add components as needed:

```bash
npx shadcn@latest add button
npx shadcn@latest add input
npx shadcn@latest add card
```

### 8. Run Development Server

```bash
npm run dev
```

Visit `http://localhost:3000`

---

## Deployment

### Vercel Setup

1. Import your GitHub repo to Vercel
2. Configure environment variables:
   - Add `NEXT_PUBLIC_SUPABASE_URL` and `NEXT_PUBLIC_SUPABASE_ANON_KEY` from **dev** instance
   - Uncheck "Production" for these variables (keep Preview + Development)
   - Add the same variables again using **prod** instance credentials
   - Check only "Production" for prod variables
3. Deploy

### Deploy to Production

```bash
git push origin main
```

Vercel automatically deploys on push to main branch.

---

## Project Structure

```
loop/
├── app/
│   ├── page.tsx              # Home page (Now | Next view)
│   ├── actions/
│   │   └── tasks.ts          # Server actions (CRUD)
│   └── layout.tsx
├── components/
│   ├── ui/                   # Shadcn components
│   ├── task-input.tsx
│   ├── task-list.tsx
│   └── task-item.tsx
├── lib/
│   ├── supabase/
│   │   ├── client.ts
│   │   └── server.ts
│   └── prisma/
│       └── prisma.ts
├── prisma/
│   └── schema.prisma
├── middleware.ts
└── .env
```

---

## Data Schema

```
users(id, email, created_at)
tasks(id, user_id, content, state, position, created_at, completed_at)
```

**States:** `'now'` | `'next'`

---

## Common Commands

### Prisma

```bash
# Generate Prisma client
npx prisma generate

# Push schema to database
npx prisma db push

# Open Prisma Studio (database GUI)
npx prisma studio

# Reset database (⚠️ deletes all data)
npx prisma db push --force-reset
```

### Next.js

```bash
# Run development server
npm run dev

# Build for production
npm run build

# Start production server
npm run start
```

### Shadcn

```bash
# Add a component
npx shadcn@latest add <component-name>

# List available components
npx shadcn@latest add
```

---

## Official Documentation

### Core Tools
- **Next.js**: https://nextjs.org/docs
- **React**: https://react.dev
- **TypeScript**: https://www.typescriptlang.org/docs
- **Tailwind CSS**: https://tailwindcss.com/docs

### Backend & Database
- **Supabase**: https://supabase.com/docs
- **Prisma**: https://www.prisma.io/docs

### UI & Components
- **Shadcn UI**: https://ui.shadcn.com
- **Lucide Icons**: https://lucide.dev

### Deployment
- **Vercel**: https://vercel.com/docs

### Design
- **Figma**: https://help.figma.com

---

## Development Tips

- Use `'use client'` directive for components that handle user interactions
- Server components (pages) can directly query the database
- Server actions automatically trigger UI revalidation
- Keep Prisma schema as source of truth for database structure

---

## Troubleshooting

**Port already in use:**
```bash
lsof -ti:3000 | xargs kill -9
```

**Prisma client out of sync:**
```bash
npx prisma generate
```

**Supabase connection issues:**
- Verify environment variables are set correctly
- Check that DATABASE_URL uses Transaction Pooler
- Check that DIRECT_URL uses Session Pooler

**Type errors:**
- Install TypeScript language support in your editor
- Run `npm run build` to check for type errors