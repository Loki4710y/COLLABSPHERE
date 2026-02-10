# CollabSphere - Student Resource Sharing Platform

## Overview

CollabSphere is a collaborative resource-sharing web application designed for student teams. It enables users to upload, organize, and share educational resources (PDFs, images, documents, links) within projects. The platform features user authentication, project-based organization, resource commenting, and a modern, responsive UI built with React and Tailwind CSS.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture
- **Framework**: React 18 with TypeScript
- **Routing**: Wouter (lightweight React router)
- **State Management**: TanStack React Query for server state management
- **Styling**: Tailwind CSS with shadcn/ui component library (New York style)
- **Build Tool**: Vite with hot module replacement

The frontend follows a component-based architecture with:
- Pages in `client/src/pages/` (Dashboard, Landing, ResourceDetail)
- Reusable components in `client/src/components/`
- Custom hooks in `client/src/hooks/` for data fetching and auth
- UI primitives from shadcn/ui in `client/src/components/ui/`

### Backend Architecture
- **Runtime**: Node.js with Express
- **Language**: TypeScript with ES modules
- **API Design**: RESTful endpoints defined in `shared/routes.ts` with Zod validation
- **File Uploads**: Multer middleware storing files in `uploads/` directory

The server architecture includes:
- Express routes registered in `server/routes.ts`
- Database operations abstracted in `server/storage.ts`
- Replit Auth integration in `server/replit_integrations/auth/`

### Data Storage
- **Database**: PostgreSQL with Drizzle ORM
- **Schema**: Defined in `shared/schema.ts` with tables for users, sessions, resources, projects, and comments
- **Migrations**: Managed via `drizzle-kit push` command

Key database tables:
- `users` - User accounts (required for Replit Auth)
- `sessions` - Session storage (required for Replit Auth)
- `resources` - Uploaded files and links with metadata
- `projects` - Project/group organization
- `comments` - Comments on resources

### Authentication
- **Primary**: Replit OpenID Connect (OIDC) authentication
- **Session Management**: Express sessions with PostgreSQL store (connect-pg-simple)
- **Demo Mode**: `/api/demo-login` endpoint for development/testing without OAuth

### Shared Code
The `shared/` directory contains code used by both frontend and backend:
- `schema.ts` - Drizzle database schema and Zod validation schemas
- `routes.ts` - API route definitions with type-safe request/response schemas
- `models/auth.ts` - User and session table definitions

## External Dependencies

### Database
- PostgreSQL database (configured via `DATABASE_URL` environment variable)
- Drizzle ORM for type-safe database operations
- drizzle-zod for generating Zod schemas from database tables

### Authentication
- Replit OIDC provider for user authentication
- Passport.js with OpenID Connect strategy
- express-session for session management
- connect-pg-simple for PostgreSQL session storage

### File Storage
- Local file system storage in `uploads/` directory
- Multer for handling multipart form data uploads

### Environment Variables Required
- `DATABASE_URL` - PostgreSQL connection string
- `SESSION_SECRET` - Secret for signing session cookies
- `ISSUER_URL` - Replit OIDC issuer (defaults to https://replit.com/oidc)
- `REPL_ID` - Replit environment identifier

### Key NPM Packages
- Frontend: React, Wouter, TanStack Query, Tailwind CSS, Radix UI primitives
- Backend: Express, Drizzle ORM, Passport, Multer
- Shared: Zod for validation, date-fns for date formatting