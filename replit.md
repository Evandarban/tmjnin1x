# tmnjnin1x Gaming Community Website

## Overview

A modern gaming community website for the Discord server "tmnjnin1x" (short: "n1x"). The site features a cyberpunk/futuristic aesthetic with dark mode, neon accents, glassmorphism effects, and animated elements. Key features include a hero section with glitch effects, live community stats dashboard, leaderboard, events timeline, video clips gallery, and server rules accordion.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture
- **Framework**: React 18 with TypeScript
- **Routing**: Wouter (lightweight React router)
- **State Management**: TanStack React Query for server state
- **Styling**: Tailwind CSS with custom CSS variables for theming
- **Component Library**: shadcn/ui (Radix UI primitives with custom styling)
- **Animations**: AOS (Animate On Scroll) library loaded via CDN
- **Build Tool**: Vite with React plugin

### Backend Architecture
- **Runtime**: Node.js with Express
- **Language**: TypeScript (ESM modules)
- **Development**: tsx for TypeScript execution
- **Build**: esbuild for production bundling

### Project Structure
```
├── client/           # Frontend React application
│   ├── src/
│   │   ├── components/ui/  # shadcn/ui components
│   │   ├── hooks/          # Custom React hooks
│   │   ├── lib/            # Utilities and query client
│   │   └── pages/          # Page components
├── server/           # Backend Express server
├── shared/           # Shared types and schemas (Zod)
└── migrations/       # Database migrations (Drizzle)
```

### Design System
- **Fonts**: Orbitron (headings), Poppins (body text)
- **Colors**: Deep dark background (#0f0f12), neon purple primary, electric blue secondary
- **Effects**: Glassmorphism cards, glowing buttons, hover animations
- **Theme**: Dark mode only with CSS custom properties

### Data Layer
- **ORM**: Drizzle ORM configured for PostgreSQL
- **Schema Validation**: Zod with drizzle-zod integration
- **Object Storage**: Replit Object Storage for video uploads
- **Database Tables**:
  - `member_stats`: Discord member statistics
  - `featured_videos`: Video clips (YouTube URLs or uploaded videos)
  - `site_events`: Community events
  - `admin_sessions`: Admin authentication tokens
  - `roast_counts`: Tracks how many times each member has been roasted
  - `tournaments`: Tournament metadata (title, game, maxPlayers, status)
  - `tournament_registrations`: Player registrations (tournamentId, discordId, status, seed)
  - `tournament_matches`: Bracket matches (round, matchNumber, player1/2RegId, winnerRegId, nextMatchId)

### AI Roast Master Feature
- **Location**: Profile pages (`/profile/:username`)
- **Integration**: OpenAI via Replit AI Integrations (gpt-4o-mini model)
- **Style**: Darija (Moroccan Arabic) + English mixed roasts based on player stats
- **API**: POST `/api/roast` generates roast and increments roast count
- **Wall of Shame**: Homepage displays top 5 most roasted members ("ضحايا القمع")
- **Data Tracked**: discordId, username, displayName, avatarUrl, roastCount, lastRoastedAt

### Tournament Management System
- **Route**: `/tournaments`
- **Features**:
  - Admin can create tournaments (title, game, max players)
  - Players can register by searching their Discord username
  - Waiting list for overflow registrations
  - Auto bracket generation (Fisher-Yates shuffle)
  - Supports 8, 16, or 32 player brackets
  - Visual bracket display with glowing connectors
  - Admin can select match winners to advance players
  - Tournament statuses: registration, in_progress, completed
- **API Endpoints**:
  - GET `/api/tournaments` - List all tournaments
  - GET `/api/tournaments/:id` - Get tournament with registrations and matches
  - POST `/api/admin/tournaments` - Create tournament (admin)
  - PUT `/api/admin/tournaments/:id` - Update tournament (admin)
  - DELETE `/api/admin/tournaments/:id` - Delete tournament (admin)
  - POST `/api/tournaments/:id/register` - Register player
  - POST `/api/admin/tournaments/:id/generate-bracket` - Generate bracket (admin)
  - PATCH `/api/admin/tournaments/:id/matches/:matchId/winner` - Set winner (admin)

### Admin Dashboard
- **Route**: `/admin`
- **Authentication**: Password-based login (ADMIN_PASSWORD env var)
- **Features**:
  - Video management: Upload videos (max 50MB, 1 minute) or add YouTube URLs
  - Event management: Create, edit, delete community events
  - Session-based auth with 24-hour token expiry

### Video Upload Flow
1. Client validates file (50MB max, 1 minute max duration)
2. Client requests presigned PUT URL from `/api/uploads/request-url`
3. Client uploads directly to GCS via presigned URL
4. Client saves object path to database via admin API
5. Home page fetches signed GET URL (1-hour TTL) when user clicks to play
6. Video plays in modal using temporary signed URL

### Draw & Guess Multiplayer Game
- **Route**: `/draw`
- **Technology**: Socket.io for real-time WebSocket communication
- **Database Tables**:
  - `drawing_rooms`: Room metadata (roomCode, hostId, status, currentRound, roundPhase, currentArtist, currentPrompt)
  - `drawing_players`: Players in rooms (roomId, discordId, username, score, isConnected)
  - `drawing_guesses`: Round guesses (roomId, round, playerId, guess, votes, isCorrect)
- **Game Flow**:
  1. **Waiting Phase**: Host creates room, players join (max 8 players)
  2. **Drawing Phase (60s)**: Artist draws based on random prompt, canvas synced in real-time
  3. **Guessing Phase (30s)**: Non-artists submit text guesses
  4. **Voting Phase (20s)**: All players vote for funniest/best guess
  5. **Results Phase (10s)**: Scores revealed, winner announced per round
  6. **Game End**: After all rounds, final scores displayed
- **Scoring**:
  - Correct guess: +100 points
  - Artist (when someone guesses correctly): +50 points
  - Each vote received: +25 points
- **Features**:
  - 14-color palette with 4 brush sizes
  - Eraser tool
  - Clear canvas option
  - Touch support for mobile
  - Player list with scores
  - Room codes for easy sharing
  - 50 built-in drawing prompts

## External Dependencies

### Database
- PostgreSQL (via DATABASE_URL environment variable)
- Drizzle Kit for schema migrations (`db:push` script)

### Frontend Libraries
- Radix UI primitives (dialogs, accordions, tooltips, etc.)
- react-icons for social media icons
- embla-carousel-react for carousels
- react-day-picker for calendar components
- recharts for data visualization
- AOS (Animate On Scroll) via CDN

### Development Tools
- Replit-specific Vite plugins (runtime error overlay, cartographer, dev banner)
- TypeScript with strict mode
- PostCSS with Tailwind and Autoprefixer