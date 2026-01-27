# AI Study Planner

An intelligent study planner web app that integrates with Canvas LMS to help students organize their assignments and create optimized study schedules.

## Features

### MVP (Current Version)
- **Google OAuth Authentication** - Secure login with Convex Auth
- **Canvas LMS Integration** - Sync courses and assignments automatically
- **Smart Schedule Generation** - Rule-based algorithm creates personalized study schedules
- **Interactive Calendar** - Visual weekly calendar with react-big-calendar
- **Assignment Dashboard** - Track assignments, deadlines, and completion status
- **Study Sessions** - Manage and complete scheduled study sessions

### Phase 2 (Coming Soon)
- **AI-Powered Analysis** - Transformers.js for difficulty scoring and intelligent scheduling
- **Google Calendar Sync** - Create calendar events with reminders
- **Analytics Dashboard** - Track study time, completion rates, and productivity insights
- **Advanced Features** - Drag-and-drop rescheduling, personalization

## Tech Stack

- **Frontend**: React 18 + Vite + Tailwind CSS
- **Backend/Database**: Convex (real-time serverless)
- **Authentication**: Convex Auth with Google OAuth
- **APIs**: Canvas LMS API, react-big-calendar
- **Hosting**: Vercel (frontend), Convex (backend)

## Prerequisites

Before you begin, you'll need:

1. **Node.js** (v20 or higher)
2. **npm** or **yarn**
3. **Convex Account** (free tier) - [Sign up at convex.dev](https://convex.dev)
4. **Google OAuth Credentials** - [Google Cloud Console](https://console.cloud.google.com)
5. **Canvas API Token** - From your Canvas LMS account

## Setup Instructions

### 1. Clone and Install Dependencies

\`\`\`bash
git clone <your-repo-url>
cd ai-study-planner
npm install
\`\`\`

### 2. Set Up Convex

\`\`\`bash
# Initialize Convex project
npx convex dev
\`\`\`

This will:
- Create a new Convex project (or link to existing)
- Generate your Convex deployment URL
- Start the Convex dev server

Copy your deployment URL (e.g., `https://your-project.convex.cloud`)

### 3. Configure Google OAuth

#### Create OAuth Credentials:

1. Go to [Google Cloud Console](https://console.cloud.google.com)
2. Create a new project or select existing
3. Navigate to **APIs & Services** → **Credentials**
4. Click **Create Credentials** → **OAuth 2.0 Client ID**
5. Configure consent screen if prompted
6. Choose **Web application** as application type
7. Add authorized redirect URIs:
   - Development: `http://localhost:5173`
   - Production: `https://your-app.vercel.app`

8. Copy your **Client ID** and **Client Secret**

#### Add to Convex Environment:

In your Convex dashboard (dashboard.convex.dev):

1. Go to your project
2. Click **Settings** → **Environment Variables**
3. Add:
   - `AUTH_GOOGLE_ID` = Your Google Client ID
   - `AUTH_GOOGLE_SECRET` = Your Google Client Secret

### 4. Create Environment File

Copy the example environment file:

\`\`\`bash
cp .env.local.example .env.local
\`\`\`

Edit `.env.local`:

\`\`\`bash
VITE_CONVEX_URL=https://your-project.convex.cloud
VITE_APP_URL=http://localhost:5173
\`\`\`

### 5. Start Development Servers

You need to run **two terminals**:

**Terminal 1** - Convex Dev Server:
\`\`\`bash
npx convex dev
\`\`\`

**Terminal 2** - Vite Dev Server:
\`\`\`bash
npm run dev
\`\`\`

The app will be available at `http://localhost:5173`

## User Setup (First-Time Login)

### 1. Sign In with Google

1. Open the app
2. Click "Sign in with Google"
3. Authorize the app

### 2. Connect Canvas Account

After signing in, you'll be prompted to connect Canvas:

1. **Canvas Base URL**: Enter your Canvas instance URL
   - Examples: `https://canvas.instructure.com`
   - Or: `https://[your-school].instructure.com`

2. **Canvas API Token**: Get from Canvas
   - Log in to Canvas
   - Go to **Account** → **Settings**
   - Scroll to **Approved Integrations**
   - Click **+ New Access Token**
   - Set purpose: "AI Study Planner"
   - Copy the generated token

3. Click **Test Connection** to verify
4. Click **Continue** to save

### 3. Sync Assignments

1. Navigate to **Dashboard**
2. Click **Sync Canvas** button
3. Your assignments will be imported automatically

### 4. Generate Study Schedule

1. Go to **Schedule Generator**
2. Set your preferences:
   - Study hours per day
   - Preferred time slots (morning/afternoon/evening)
   - Break duration
3. Click **Generate Schedule**
4. Review the generated schedule
5. Click **Confirm & Save Schedule**

### 5. View Calendar

1. Navigate to **Calendar**
2. See your study sessions in weekly view
3. Click on a session to:
   - Mark as complete
   - Delete session
4. Switch between month/week/day views

## Project Structure

\`\`\`
ai-study-planner/
├── src/
│   ├── components/
│   │   └── ui/          # Reusable UI components
│   ├── pages/           # Route pages
│   ├── utils/           # API utilities
│   ├── App.jsx          # Main app with routing
│   ├── main.jsx         # Entry point with providers
│   └── index.css        # Global styles
├── convex/
│   ├── schema.ts        # Database schema
│   ├── auth.config.ts   # Auth configuration
│   ├── users.ts         # User CRUD functions
│   ├── assignments.ts   # Assignment functions
│   ├── studySessions.ts # Study session functions
│   └── analytics.ts     # Analytics functions
├── public/
├── .env.local           # Environment variables
├── package.json
├── vite.config.js
├── tailwind.config.js
└── README.md
\`\`\`

## Deployment

### Deploy to Vercel

1. **Push to GitHub**:
   \`\`\`bash
   git init
   git add .
   git commit -m "Initial commit"
   git remote add origin <your-github-repo>
   git push -u origin main
   \`\`\`

2. **Deploy on Vercel**:
   - Go to [vercel.com](https://vercel.com)
   - Click **Import Project**
   - Select your GitHub repository
   - Configure:
     - Framework Preset: **Vite**
     - Build Command: `npm run build`
     - Output Directory: `dist`

3. **Add Environment Variables**:
   In Vercel dashboard:
   - `VITE_CONVEX_URL` = Your Convex deployment URL
   - `VITE_APP_URL` = Your Vercel app URL

4. **Update Google OAuth**:
   - Add your Vercel URL to authorized redirect URIs in Google Cloud Console

5. **Deploy**: Vercel will auto-deploy on every push to main

### Convex Deployment

Convex automatically deploys when you run `npx convex dev`. For production:

\`\`\`bash
npx convex deploy
\`\`\`

## Troubleshooting

### "Not authenticated" errors
- Make sure you're signed in with Google
- Check that Convex Auth is properly configured
- Verify Google OAuth credentials in Convex dashboard

### Canvas sync fails
- Verify Canvas API token is valid
- Check Canvas base URL is correct
- Ensure Canvas API is accessible (not blocked by firewall)

### Calendar not showing sessions
- Generate a schedule first from Schedule Generator
- Check that you have pending assignments
- Refresh the page

### Convex connection issues
- Verify `VITE_CONVEX_URL` in `.env.local`
- Make sure Convex dev server is running
- Check Convex dashboard for deployment status

## Development

### Run Tests
\`\`\`bash
npm test
\`\`\`

### Build for Production
\`\`\`bash
npm run build
\`\`\`

### Preview Production Build
\`\`\`bash
npm run preview
\`\`\`

## Free Tier Limits

All services used have generous free tiers:

- **Convex**: 100K function calls/month
- **Vercel**: 100 GB bandwidth/month
- **Google OAuth**: Unlimited
- **Canvas API**: Subject to Canvas rate limits

## Roadmap

### Phase 2 Features
- [ ] Transformers.js AI analysis
- [ ] Google Calendar API integration
- [ ] Analytics dashboard with charts
- [ ] Drag-and-drop calendar rescheduling
- [ ] Email notifications
- [ ] Mobile app (React Native)

## Contributing

Contributions are welcome! Please open an issue or submit a pull request.

## License

MIT License - See LICENSE file for details

## Support

For issues or questions:
- Open a GitHub issue
- Check the troubleshooting section above

## Acknowledgments

- Built with [Convex](https://convex.dev)
- Calendar powered by [react-big-calendar](https://github.com/jquense/react-big-calendar)
- Canvas LMS API documentation
