# Viati ✈️

> Plan your trips in one place. Discover places, organize your itinerary, and keep the details of your journey together.

Viati is a mobile travel-planning app in development. Its long-term goal is to bring trip planning, place discovery, itinerary organization, and travel budgeting into one clear experience.

The current development focus is **MVP POC 1**: establish a reliable foundation for authentication, personal trip management, and itinerary planning before expanding into collaborative and discovery features.

## Contents

- [Vision](#vision)
- [MVP scope](#mvp-scope)
- [Development status](#development-status)
- [Technology stack](#technology-stack)
- [Repository structure](#repository-structure)
- [Getting started](#getting-started)
- [Environment variables](#environment-variables)
- [Available scripts](#available-scripts)
- [Security principles](#security-principles)
- [Roadmap](#roadmap)
- [Project documentation](#project-documentation)

## Vision

Travel planning is often scattered across maps, notes, messaging apps, booking confirmations, and spreadsheets. Viati aims to make the process easier by bringing the essential information for a trip together.

The product is being designed primarily for independent travelers and small groups who want to organize trips without juggling several disconnected tools.

**Product direction:** connect exploration, itinerary planning, and travel budget tracking in one mobile companion.

## MVP scope

The first milestone is deliberately focused on validating the core trip-planning journey.

### Planned for MVP POC 1

- **Authentication:** sign up, sign in, and account access.
- **Personal trip dashboard:** view and access your trips.
- **Trip management:** create, view, edit, and delete trips.
- **Itinerary management:** add, edit, remove, and reorder itinerary stops.
- **Trip details:** organize dates, locations, notes, and manually entered booking references.
- **Reliable states:** clear validation, loading, empty, and error states.
- **Data protection:** ensure users can only access their own private trip data.

These are **target capabilities**, not a claim that every feature is already implemented.

### Planned for later releases

- Place discovery and richer exploration experiences.
- Collaborative trips and group member management.
- Shared expenses and group budget settlement.
- Advanced interactive maps and route optimization.
- Notifications, reminders, and richer trip attachments.
- AI-assisted planning and external booking synchronization.

These items are outside the initial MVP scope and will be prioritized as the project evolves.

## Development status

The repository contains two generations of the project:

| Directory | Purpose | Status |
| --- | --- | --- |
| `viati/` | New Expo and React Native mobile app | Current development target |
| `date-planner/` | Earlier Next.js web prototype | Kept for reference during the transition |

The mobile app has an Expo Router application structure, a Supabase client setup, initial navigation screens, and a Supabase migrations directory. The application is still in development; the presence of screens or configuration does not mean the corresponding end-to-end feature is complete.

## Technology stack

The mobile application uses the following selected technologies:

| Technology | Role |
| --- | --- |
| [Expo](https://expo.dev/) | React Native development platform and tooling |
| [React Native](https://reactnative.dev/) | Cross-platform mobile UI |
| [TypeScript](https://www.typescriptlang.org/) | Static typing |
| [Expo Router](https://docs.expo.dev/router/introduction/) | File-based navigation |
| [Supabase](https://supabase.com/docs) | PostgreSQL backend and authentication platform |
| [Zod](https://zod.dev/) | Runtime data validation |
| [Jest](https://jestjs.io/) + [jest-expo](https://docs.expo.dev/develop/unit-testing/) | Automated test foundation |

The exact architecture, database model, testing coverage, and deployment workflow will be documented further as implementation progresses.

## Repository structure

The repository is organized as follows:

```text
Viati/
├── README.md
├── viati/                       # Current mobile application
│   ├── src/
│   │   ├── app/                 # Expo Router routes and screens
│   │   ├── components/          # Shared UI components
│   │   ├── constants/           # Shared constants and theme
│   │   ├── hooks/               # React hooks
│   │   └── lib/                 # Client and integration setup
│   ├── supabase/
│   │   ├── migrations/          # Database migrations
│   │   └── seed.sql             # Seed data, if configured
│   ├── assets/                  # App icons and image assets
│   ├── app.json
│   ├── package.json
│   └── tsconfig.json
└── date-planner/                # Legacy web prototype
```

## Getting started

### Prerequisites

Install the following before starting:

- [Node.js](https://nodejs.org/) compatible with the installed Expo SDK.
- npm (included with Node.js).
- [Expo Go](https://expo.dev/go) for a quick device preview, or an Android emulator / iOS simulator.
- A Supabase project for backend-connected functionality.

For iOS simulator development, a Mac with Xcode is generally required. You can also test on a physical device with Expo Go where supported.

### 1. Clone the repository

```bash
git clone https://github.com/Reytis/Viati.git
cd Viati/viati
```

### 2. Install dependencies

```bash
npm install
```

### 3. Configure environment variables

Create a `.env` file in the `viati/` directory:

```dotenv
EXPO_PUBLIC_SUPABASE_URL=https://your-project.supabase.co
EXPO_PUBLIC_SUPABASE_PUBLISHABLE_KEY=your-supabase-publishable-key
```

Replace the example values with the URL and publishable key from your Supabase project. See [Environment variables](#environment-variables) below.

### 4. Start the development server

```bash
npm start
```

Then follow the Expo CLI instructions to open the app in Expo Go, an emulator, or a simulator.

Platform-specific commands are also available:

```bash
npm run android
npm run ios
npm run web
```

Web support is available through Expo tooling, but Viati's primary target is mobile.

## Environment variables

The mobile app's Supabase client expects:

| Variable | Required | Description |
| --- | --- | --- |
| `EXPO_PUBLIC_SUPABASE_URL` | Yes | URL of your Supabase project |
| `EXPO_PUBLIC_SUPABASE_PUBLISHABLE_KEY` | Yes | Supabase publishable key used by the client |

**Important:** Expo variables prefixed with `EXPO_PUBLIC_` are bundled into the client application and must not contain secrets. Never put a Supabase service-role key, database password, or other server-side secret in this file.

Keep local `.env` files out of version control. Configure production values through the appropriate build and deployment environment when that workflow is established.

## Available scripts

Run these commands from the `viati/` directory:

| Command | Description |
| --- | --- |
| `npm start` | Start the Expo development server |
| `npm run android` | Start the app for Android |
| `npm run ios` | Start the app for iOS |
| `npm run web` | Start the web version |
| `npm run lint` | Run Expo linting |
| `npm test` | Run Jest tests |
| `npm run test:watch` | Run Jest in watch mode |

Test and lint scripts are configured, but their existence does not imply that the project already has comprehensive test coverage or a clean lint run.

## Security principles

Security requirements for the MVP include:

- Use Supabase authentication for user identity.
- Enforce access permissions at the database/backend layer, not only in the UI.
- Configure Row Level Security (RLS) for private user and trip data before relying on real user data.
- Ensure itinerary stops inherit the access rules of their parent trip.
- Validate input at runtime and handle invalid or unauthorized requests safely.
- Never commit credentials or server-side secrets.

These are implementation requirements to verify before a production release, not a certification that all security controls are already complete.

## Roadmap

The work is organized around incremental releases:

1. **Foundation** — app structure, environment setup, navigation, validation, backend connection, and testing baseline.
2. **MVP POC 1** — authentication, personal trips, itinerary management, persistence, and access control.
3. **V1** — expand the validated core experience with higher-value discovery, usability, and planning capabilities.
4. **Future releases** — collaboration, shared expenses, richer maps, route tools, and other advanced experiences.

The detailed roadmap, task dependencies, acceptance criteria, projects, and release associations are maintained in the [Viati Notion workspace](https://app.notion.com/p/3f4f63d25726805eb313dd12bff4219c).

## Project documentation

- **Roadmap:** [Viati — Roadmap](https://app.notion.com/p/3f4f63d25726805eb313dd12bff4219c)
- **Resources and decisions:** [Viati — Resources & Decisions](https://app.notion.com/p/3f4f63d25726807e998cee27b5f0d32f)
- **Source repository:** [Reytis/Viati on GitHub](https://github.com/Reytis/Viati)

## License

MIT License
