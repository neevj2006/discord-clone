# Discord Clone — Full-Stack Real-Time Communication Platform

This project implements a **Full-Stack Discord Clone** that enables real-time messaging, voice/video communication, and server-based community management using modern web technologies.  
It combines **Next.js 13**, **Socket.io** for real-time functionality, **Prisma ORM**, and **TailwindCSS** for a production-ready communication platform.

---

## Project Overview

Modern communication platforms require robust real-time data synchronization and scalable infrastructure.  
This project demonstrates a **complete full-stack application** capable of:

- Enabling real-time messaging with instant updates across all connected clients
- Supporting text, audio, and video communication channels
- Managing server communities with role-based permissions
- Providing 1:1 direct messaging and video calls between members
- Handling file attachments and media sharing

Built with **Next.js 13 App Router**, this application showcases modern React patterns, WebSocket communication, and production-grade database management.

---

## Key Features

- **Real-Time Messaging** — Implements Socket.io for instant message delivery with websocket fallback to polling for reliability
- **Media Attachments** — Supports file uploads and sharing through UploadThing integration
- **Live Message Management** — Edit and delete messages with real-time updates propagated to all users
- **Multi-Channel Support** — Create dedicated text, audio, and video channels within servers
- **Direct Communication** — 1:1 conversations and video calls between individual members
- **Member Management** — Role-based permissions with ability to kick members and assign Guest/Moderator roles
- **Invite System** — Generate unique invite links with full working invitation flow
- **Infinite Scroll** — Optimized message loading in batches using TanStack Query for performance
- **Server Customization** — Create and personalize servers with custom names and settings
- **Modern UI/UX** — Beautiful interface built with TailwindCSS and ShadcnUI component library
- **Responsive Design** — Full mobile optimization with adaptive layouts
- **Theme Support** — Light and dark mode with seamless switching
- **Authentication** — Secure user authentication powered by Clerk

---

## Technologies Used

| Component                | Purpose                                    |
| ------------------------ | ------------------------------------------ |
| **Next.js 13**           | React framework with App Router            |
| **React 18**             | UI component library                       |
| **Socket.io**            | Real-time bidirectional communication      |
| **Prisma**               | Type-safe ORM for database operations      |
| **MySQL**                | Relational database (PlanetScale)          |
| **TailwindCSS**          | Utility-first CSS framework                |
| **ShadcnUI**             | Accessible component library               |
| **Clerk**                | Authentication and user management         |
| **UploadThing**          | File upload handling                       |
| **LiveKit**              | Real-time video/audio infrastructure       |
| **TanStack Query**       | Data fetching and caching                  |
| **TypeScript**           | Type safety and developer experience       |

---

## System Architecture

```plaintext
Client (Next.js)
   │
   ├─► Authentication (Clerk) → User Session
   │
   ├─► WebSocket (Socket.io) → Real-Time Updates
   │      │
   │      ├─► Message Events
   │      ├─► Channel Updates
   │      └─► Member Status
   │
   ├─► REST API (Next.js API Routes)
   │      │
   │      ├─► Server Management
   │      ├─► Channel CRUD
   │      └─► Member Operations
   │
   └─► Database Layer (Prisma + MySQL)
          │
          ├─► Users & Profiles
          ├─► Servers & Channels
          ├─► Messages & Conversations
          └─► Members & Permissions
```

---

## Implementation Architecture

The application is structured into five main layers:

### 1. Frontend Layer (Next.js 13 + React)

- Server components for optimal performance and SEO
- Client components for interactive features
- TailwindCSS for responsive styling
- ShadcnUI for consistent, accessible UI components

### 2. Real-Time Communication Layer (Socket.io)

- WebSocket connections for instant message delivery
- Event-driven architecture for channel updates
- Automatic fallback to polling when WebSockets unavailable
- Real-time presence indicators and typing status

### 3. API Layer (Next.js API Routes)

- RESTful endpoints for CRUD operations
- Server and channel management
- Member role assignment and permissions
- Invite link generation and validation

### 4. Data Layer (Prisma ORM)

- Type-safe database queries with auto-generated types
- Efficient relation handling between entities
- Migration management for schema evolution
- Connection pooling for performance

### 5. External Services Integration

- **Clerk**: User authentication and session management
- **UploadThing**: File upload and storage
- **LiveKit**: Video and audio call infrastructure
- **PlanetScale**: Serverless MySQL database hosting

---

## Database Schema

```plaintext
Core Entities:
├─ Profile (User data from Clerk)
├─ Server (Community workspace)
│  ├─ Member (User roles: ADMIN, MODERATOR, GUEST)
│  └─ Channel (TEXT, AUDIO, VIDEO)
├─ Message (Channel messages with attachments)
└─ Conversation (1:1 direct messaging)
   └─ DirectMessage (Private messages between members)
```

**Key Relations:**
- Server → Many Channels, Many Members
- Member → Belongs to Server, Has Role
- Channel → Many Messages
- Conversation → Two Members, Many DirectMessages

---

## Feature Breakdown

### Server Management
```
- Create new servers with custom names
- Upload server icons and banners
- Manage server settings and permissions
- Generate unique invite codes
- Delete or leave servers
```

### Channel System
```
- Create TEXT channels for messaging
- Create AUDIO channels for voice chat
- Create VIDEO channels for video meetings
- Edit and delete channels
- Set channel-specific permissions
```

### Messaging Features
```
- Send text messages in real-time
- Upload and share file attachments
- Edit sent messages (real-time updates)
- Delete messages with confirmation
- Infinite scroll pagination (10 messages/batch)
- @mention members in messages
```

### Member Management
```
- View all server members
- Assign MODERATOR role
- Demote to GUEST role
- Kick members from server
- Track online/offline status
```

### Direct Communication
```
- Start 1:1 conversations with any member
- Send private direct messages
- Initiate video calls between two users
- Real-time delivery notifications
```

---

## Installation & Setup

### Prerequisites

```bash
Node.js 18.x.x or higher
npm or yarn package manager
MySQL database (PlanetScale recommended)
Clerk account for authentication
UploadThing account for file uploads
LiveKit account for video/audio
```

### Installation Steps

```bash
# Clone repository
git clone https://github.com/neevj2006/discord-clone.git
cd discord-clone

# Install dependencies
npm install

# Set up environment variables (see Configuration section)
# Create .env file with required keys

# Generate Prisma client
npx prisma generate

# Push database schema
npx prisma db push

# Start development server
npm run dev
```

### Configuration

Create a `.env` file in the project root:

```env
# Clerk Authentication
NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=pk_test_xxxxx
CLERK_SECRET_KEY=sk_test_xxxxx
NEXT_PUBLIC_CLERK_SIGN_IN_URL=/sign-in
NEXT_PUBLIC_CLERK_SIGN_UP_URL=/sign-up
NEXT_PUBLIC_CLERK_AFTER_SIGN_IN_URL=/
NEXT_PUBLIC_CLERK_AFTER_SIGN_UP_URL=/

# Database
DATABASE_URL=mysql://username:password@host/database

# UploadThing (File Uploads)
UPLOADTHING_SECRET=sk_live_xxxxx
UPLOADTHING_APP_ID=your_app_id

# LiveKit (Video/Audio)
LIVEKIT_API_KEY=your_api_key
LIVEKIT_API_SECRET=your_api_secret
NEXT_PUBLIC_LIVEKIT_URL=wss://your-project.livekit.cloud
```

---

## How to Run

```bash
# Development mode with hot reload
npm run dev

# Production build
npm run build

# Start production server
npm start

# Open browser
# Navigate to http://localhost:3000
```

---

## API Service Setup

### Clerk (Authentication)
1. Visit [clerk.com](https://clerk.com) and create account
2. Create new application
3. Copy publishable and secret keys
4. Configure redirect URLs in Clerk dashboard

### PlanetScale (Database)
1. Sign up at [planetscale.com](https://planetscale.com)
2. Create new database
3. Generate connection string
4. Add to `DATABASE_URL` environment variable

### UploadThing (File Uploads)
1. Register at [uploadthing.com](https://uploadthing.com)
2. Create new app
3. Copy API keys to environment variables

### LiveKit (Video/Audio)
1. Create account at [livekit.io](https://livekit.io)
2. Generate API key and secret
3. Note your LiveKit server URL

---

## Available Scripts

| Command      | Description                            |
| ------------ | -------------------------------------- |
| `npm run dev` | Starts development server on port 3000 |
| `npm run build` | Creates optimized production build   |
| `npm start`  | Runs production server                 |
| `npx prisma studio` | Opens Prisma database GUI       |
| `npx prisma generate` | Regenerates Prisma client       |
| `npx prisma db push` | Syncs schema with database       |

---

## Performance Optimizations

- **Infinite Scroll**: Messages loaded in batches of 10 using TanStack Query
- **Optimistic Updates**: Instant UI feedback before server confirmation
- **Server Components**: Reduced JavaScript bundle size with Next.js 13
- **Image Optimization**: Automatic image optimization via Next.js Image component
- **Connection Pooling**: Efficient database connections with Prisma
- **Caching Strategy**: React Query caching for reduced API calls

---

## Project Structure

```plaintext
discord-clone/
├── app/                    # Next.js 13 App Router
│   ├── (auth)/            # Authentication pages
│   ├── (main)/            # Main application pages
│   ├── api/               # API routes
│   └── layout.tsx         # Root layout
├── components/            # React components
│   ├── ui/               # ShadcnUI components
│   ├── modals/           # Modal dialogs
│   └── providers/        # Context providers
├── lib/                   # Utility functions
│   ├── db.ts             # Prisma client
│   └── utils.ts          # Helper functions
├── prisma/               # Database schema
│   └── schema.prisma     # Prisma schema definition
├── hooks/                # Custom React hooks
├── pages/api/socketio.ts # Socket.io server
└── public/               # Static assets
```

---

## Future Enhancements

- **Message Search**: Full-text search across all channels
- **Thread Support**: Nested conversations within messages
- **Screen Sharing**: Share screen during video calls
- **Emoji Reactions**: React to messages with emojis
- **Voice Messages**: Record and send audio messages
- **Message Pinning**: Pin important messages to channel
- **User Profiles**: Customizable user profiles with status
- **Server Templates**: Pre-configured server setups
- **Bot Integration**: Support for custom bots
- **Mobile Apps**: Native iOS and Android applications

---

## Troubleshooting

### Database Connection Issues
```bash
# Verify DATABASE_URL format
# Test connection
npx prisma db push
```

### WebSocket Connection Failures
- Check firewall settings
- Verify Socket.io server is running
- Ensure proper CORS configuration

### Authentication Errors
- Validate Clerk API keys
- Check redirect URL configuration
- Clear browser cookies and cache

### File Upload Issues
- Verify UploadThing credentials
- Check file size limits
- Ensure proper MIME type configuration

---

## License

The MIT License (MIT)

Copyright (c) 2025 Neev Jain

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

---
