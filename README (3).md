# App Builder Core

A full-stack web-based app-building studio that converts natural-language instructions into **real installable Android .apk files** via GitHub + GitHub Actions.

## 🎯 Features

- **Natural Language App Generation**: Type what you want, get a working Android app
- **GitHub Integration**: Automatic repo creation, CI/CD, and artifact downloads
- **Modular Interface**: Six core modules for complete control
- **Real Android Apps**: Native Kotlin apps built via Gradle
- **Terminal-Like Console**: High-level command interface for power users
- **Template System**: Reusable app blueprints and specs

## 🏗️ Architecture

```
app-builder-core/
├── client/              # React + TypeScript frontend
├── server/              # Node.js + TypeScript backend
├── android-template/    # Base Android Kotlin project
└── docs/                # Documentation
```

### Tech Stack

**Frontend:**
- React 18 + TypeScript
- Vite for fast development
- React Router for navigation
- Tailwind CSS for styling

**Backend:**
- Node.js + Express + TypeScript
- SQLite for data storage
- GitHub REST API integration
- JWT authentication

**Android:**
- Kotlin + Jetpack Compose
- Gradle build system
- Material Design 3

**CI/CD:**
- GitHub Actions for automated builds
- Artifact upload/download
- Build status tracking

## 🚀 Quick Start

### Prerequisites

- Node.js 18+ and npm
- Git
- GitHub account
- (Optional) Android Studio for template modifications

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/app-builder-core.git
   cd app-builder-core
   ```

2. **Install dependencies**
   ```bash
   # Install server dependencies
   cd server
   npm install
   
   # Install client dependencies
   cd ../client
   npm install
   ```

3. **Configure environment**
   ```bash
   # Server configuration
   cd ../server
   cp .env.example .env
   # Edit .env with your GitHub OAuth credentials
   ```

4. **Initialize database**
   ```bash
   cd server
   npm run db:init
   ```

5. **Start development servers**
   ```bash
   # Terminal 1: Start backend
   cd server
   npm run dev
   
   # Terminal 2: Start frontend
   cd client
   npm run dev
   ```

6. **Open in browser**
   ```
   http://localhost:5173
   ```

## 📋 Core Modules

### 1. Dashboard
- Overview of all projects
- Quick actions for app creation
- Build status monitoring
- Direct APK downloads

### 2. Project Hub
- GitHub account connection (OAuth)
- Project management
- Build triggers
- Repository links

### 3. Dev Console
- Terminal-like command interface
- Supported commands:
  - `help` - List available commands
  - `apps` - List all projects
  - `open <name>` - Set active project
  - `status` - Show CI status
  - `build` - Trigger new build
  - `logs` - View build logs
  - `new-app "<desc>"` - Create via AI

### 4. Template Library
- Built-in app templates (To-Do, Notes, Timer, etc.)
- Spec storage and management
- Import/Export functionality
- Template customization

### 5. Quick Builder
- Step-by-step wizard:
  1. App basics (name, package)
  2. Screen selection
  3. Features & data
  4. Theme customization
- AI-assisted field filling
- Real-time spec preview

### 6. AI Assistant
- Natural language to app spec conversion
- Chat-style interface
- Clarifying questions
- Direct app generation

## 🔧 GitHub OAuth Setup

1. **Create GitHub OAuth App**
   - Go to GitHub Settings → Developer settings → OAuth Apps
   - Click "New OAuth App"
   - Fill in:
     - Application name: `App Builder Core`
     - Homepage URL: `http://localhost:5173`
     - Authorization callback URL: `http://localhost:3000/api/auth/github/callback`
   - Click "Register application"

2. **Configure credentials**
   - Copy Client ID and Client Secret
   - Add to `server/.env`:
     ```
     GITHUB_CLIENT_ID=your_client_id
     GITHUB_CLIENT_SECRET=your_client_secret
     GITHUB_CALLBACK_URL=http://localhost:3000/api/auth/github/callback
     ```

## 🏃 End-to-End Flow

1. **Connect GitHub** (Project Hub)
2. **Create App Spec** (Quick Builder or AI Assistant)
3. **Generate Project** (Backend scaffolds from template)
4. **Push to GitHub** (New repo created automatically)
5. **CI Build** (GitHub Actions builds APK)
6. **Download APK** (Artifact available in Dashboard)

## 📁 Project Structure

### Client (`/client`)
```
client/
├── src/
│   ├── components/       # Reusable UI components
│   ├── pages/            # Page components (Dashboard, ProjectHub, etc.)
│   ├── services/         # API client services
│   ├── types/            # TypeScript type definitions
│   ├── utils/            # Helper functions
│   ├── App.tsx           # Main app component
│   └── main.tsx          # Entry point
├── public/               # Static assets
└── package.json
```

### Server (`/server`)
```
server/
├── src/
│   ├── routes/           # API route handlers
│   ├── services/         # Business logic (GitHub, project generation)
│   ├── models/           # Database models
│   ├── middleware/       # Express middleware
│   ├── utils/            # Helper utilities
│   └── index.ts          # Server entry point
├── database/             # SQLite database
└── package.json
```

### Android Template (`/android-template`)
```
android-template/
├── app/
│   ├── src/main/
│   │   ├── java/         # Kotlin source code
│   │   └── res/          # Resources (layouts, colors, strings)
│   └── build.gradle.kts
├── gradle/
└── build.gradle.kts
```

## 🔌 API Endpoints

### Authentication
- `GET /api/auth/github` - Initiate GitHub OAuth
- `GET /api/auth/github/callback` - OAuth callback
- `GET /api/auth/status` - Check auth status
- `POST /api/auth/logout` - Logout

### Projects
- `GET /api/projects` - List all projects
- `POST /api/projects` - Create new project
- `GET /api/projects/:id` - Get project details
- `DELETE /api/projects/:id` - Delete project
- `POST /api/projects/:id/build` - Trigger build
- `GET /api/projects/:id/status` - Get build status
- `GET /api/projects/:id/logs` - Get build logs

### Templates
- `GET /api/templates` - List templates
- `GET /api/templates/:id` - Get template details
- `POST /api/specs` - Save app spec
- `GET /api/specs/:id` - Get app spec

### Console
- `POST /api/console/command` - Execute console command

### AI Assistant
- `POST /api/ai/spec` - Generate spec from description
- `POST /api/ai/suggest` - Get AI suggestions for fields

## 🎨 Customizing the Android Template

The Android template uses Jetpack Compose for modern UI. To customize:

1. **Modify base screens** (`android-template/app/src/main/java/`)
2. **Update theme** (`res/values/colors.xml`, `Theme.kt`)
3. **Add new screen types** (Update template processor in server)
4. **Change build configuration** (`build.gradle.kts`)

## 🧪 Testing

```bash
# Backend tests
cd server
npm test

# Frontend tests
cd client
npm test

# Build Android template
cd android-template
./gradlew assembleDebug
```

## 📦 Deployment

### Backend
```bash
cd server
npm run build
npm start
```

### Frontend
```bash
cd client
npm run build
# Serve the dist/ folder with any static host
```

### Environment Variables (Production)
```
NODE_ENV=production
PORT=3000
DATABASE_URL=path/to/production.db
GITHUB_CLIENT_ID=prod_client_id
GITHUB_CLIENT_SECRET=prod_client_secret
GITHUB_CALLBACK_URL=https://yourdomain.com/api/auth/github/callback
JWT_SECRET=your_secure_random_secret
FRONTEND_URL=https://yourdomain.com
```

## 🛠️ Development

### Adding a New Template

1. Create template spec in `server/src/data/templates.ts`
2. Add template metadata
3. Create template processor in `server/src/services/template-processor.ts`
4. Update Android template with new screen type (if needed)

### Adding a New Console Command

1. Add command handler in `server/src/services/console-service.ts`
2. Update command list in help text
3. Add TypeScript types in `shared-types.ts`

### Adding a New Screen Type

1. Create Compose screen in `android-template/app/src/main/java/screens/`
2. Add navigation route
3. Update template processor to inject screen
4. Add to Quick Builder screen options

## 📚 Documentation

- [Architecture Guide](docs/architecture.md)
- [API Reference](docs/api.md)
- [Template Guide](docs/templates.md)
- [Console Commands](docs/console.md)
- [Deployment Guide](docs/deployment.md)

## 🤝 Contributing

This is an internal tool. For contributions:
1. Create a feature branch
2. Make your changes
3. Test thoroughly
4. Submit a pull request

## 📄 License

Proprietary - All rights reserved

## 🆘 Troubleshooting

### GitHub OAuth not working
- Verify Client ID and Secret in `.env`
- Check callback URL matches GitHub app settings
- Ensure ports 3000 and 5173 are not blocked

### Build failing on GitHub Actions
- Check Gradle version compatibility
- Verify Android SDK components are installed
- Review workflow logs in GitHub Actions tab

### APK not downloading
- Ensure artifact retention period hasn't expired
- Check GitHub API rate limits
- Verify artifact URL is valid

## 📞 Support

For issues or questions, contact the development team.

---

Built with ❤️ by the App Builder Core Team
