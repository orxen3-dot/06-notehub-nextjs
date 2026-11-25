# NoteHub

<p align="center">
  <strong>A simple note-taking application built with Next.js.</strong><br />
  Create, organize, search, and browse personal notes through a multi-page interface.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Next.js-16.4.6-black?logo=next.js" alt="Next.js" />
  <img src="https://img.shields.io/badge/React-19-149ECA?logo=react" alt="React" />
  <img src="https://img.shields.io/badge/TypeScript-5-3178C6?logo=typescript" alt="TypeScript" />
  <img src="https://img.shields.io/badge/TanStack_Query-v5-FF4154?logo=reactquery" alt="TanStack Query" />
  <img src="https://img.shields.io/badge/Styling-CSS_Modules-000000" alt="CSS Modules" />
</p>

## Overview

NoteHub is a note-management application built with the Next.js App Router. It communicates with a REST API, combines server-side rendering with client-side interactions, and uses TanStack Query to manage and synchronize server data.

The application includes a home page, a searchable and paginated notes list, and a dedicated page for viewing an individual note.

## Features

- Browse notes retrieved from the NoteHub REST API.
- Search notes by keyword with debounced input.
- Navigate through paginated note results.
- Create notes with a title, content, and tag.
- Delete notes.
- View an individual note on its own details page.
- Validate the note creation form with Formik and Yup.
- Display loading and error states for data requests.
- Prefetch data on the server and hydrate the TanStack Query cache on the client.

## Pages and routes

| Route | Description |
| --- | --- |
| `/` | Home page with an introduction to NoteHub. |
| `/notes` | Notes list with search, pagination, and note creation. |
| `/notes/[id]` | Details page for an individual note. |

A shared layout provides header navigation and a footer across all routes.

## Tech stack

| Technology | Purpose |
| --- | --- |
| [Next.js](https://nextjs.org/) (App Router) | Application framework, routing, and server rendering |
| [React](https://react.dev/) | User interface |
| [TypeScript](https://www.typescriptlang.org/) | Static typing |
| [TanStack Query](https://tanstack.com/query/latest) | Server-state management, prefetching, and cache hydration |
| [Axios](https://axios-http.com/) | HTTP requests |
| [Formik](https://formik.org/) | Form management |
| [Yup](https://github.com/jquense/yup) | Form validation |
| [CSS Modules](https://nextjs.org/docs/app/getting-started/css) | Component-level styling |
| [Prettier](https://prettier.io/) | Code formatting |

## Getting started

### Prerequisites

- [Node.js](https://nodejs.org/) (LTS recommended)
- npm
- A NoteHub API token

### 1. Clone the repository

```bash
git clone https://github.com/orxen3-dot/06-notehub-nextjs.git
cd 06-notehub-nextjs
```

### 2. Install dependencies

```bash
npm install
```

### 3. Set up the environment

Create a `.env.local` file in the project root:

```env
NEXT_PUBLIC_NOTEHUB_TOKEN=your_notehub_api_token
```

Replace the placeholder with your API token. The API client in `lib/api.ts` reads this variable and sends it as a Bearer token.

Do not commit your real token to the repository.

### 4. Run the development server

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

## Available scripts

| Command | Description |
| --- | --- |
| `npm run dev` | Start the development server. |
| `npm run build` | Create a production build. |
| `npm run start` | Start the production server after building. |
| `npm run lint` | Run ESLint. |
| `npx prettier --check .` | Check code formatting. |
| `npx prettier --write .` | Format supported project files. |

## Project structure

```
06-notehub-nextjs/
├── app/
│   ├── notes/
│   │   ├── [id]/
│   │   │   ├── NoteDetails.client.tsx
│   │   │   └── page.tsx
│   │   ├── Notes.client.tsx
│   │   └── page.tsx
│   ├── layout.tsx
│   ├── loading.tsx
│   └── page.tsx
├── components/
│   ├── Footer/
│   ├── Header/
│   ├── Modal/
│   ├── NoteForm/
│   ├── NoteList/
│   ├── Pagination/
│   ├── SearchBox/
│   └── TanStackProvider/
├── lib/
│   └── api.ts
├── types/
│   └── note.ts
├── .env.local
├── package.json
└── README.md
```

## Data fetching and rendering

The project combines server and client components:

- The `/notes` server page prefetches the first page of notes with TanStack Query.
- The `/notes/[id]` server page prefetches the requested note using the dynamic route parameter.
- `HydrationBoundary` transfers the prefetched query cache to the client.
- Client components use `useQuery` for interactive data access.
- Creating or deleting a note invalidates the notes query so the list can refresh.

API request functions are centralized in `lib/api.ts`, while shared note types are defined in `types/note.ts`.

## API

NoteHub uses the [NoteHub public API](https://notehub-public.goit.study/api/docs). The API client is configured in `lib/api.ts` and authenticates requests with the `NEXT_PUBLIC_NOTEHUB_TOKEN` environment variable.

---

<p align="center">
  Built as a learning project with Next.js, React, and TypeScript.
</p>
