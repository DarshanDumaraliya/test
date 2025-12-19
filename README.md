# Repurpose AI - Video POC Frontend

A React-based frontend application for video annotation and project management. Create video editing projects, upload final videos, import CapCut/Final Cut Pro project files, and annotate source videos with detailed metadata.

## 🚀 Quick Start

### Prerequisites

- Node.js 18+ and npm
- Backend server running (see [backend README](../video-poc-backend/README.md))

### Installation

```bash
# Install dependencies
npm install

# Create .env file
echo "VITE_API_BASE_URL=http://localhost:55000" > .env

# Start development server
npm run dev
```

The application will be available at `http://localhost:3001`

## 📁 Project Structure

```
src/
├── components/     # Reusable UI components
├── pages/          # Page components (routes)
├── hooks/          # Custom React hooks
├── store/          # Zustand state management
├── utils/          # Utilities (API, parsers, validators)
└── types.ts        # TypeScript definitions
```

## 🛠️ Technology Stack

- **React 19.2** with TypeScript
- **Vite** - Build tool
- **Zustand** - State management
- **React Router** - Routing
- **Material-UI** - UI components
- **Tailwind CSS** - Styling
- **IndexedDB** - Local storage

## ⚙️ Environment Variables

Create a `.env` file in the root directory:

```env
VITE_API_BASE_URL=http://localhost:55000
```

## 📝 Available Scripts

| Command | Description |
|---------|-------------|
| `npm run dev` | Start development server (port 3001) |
| `npm run build` | Build for production |
| `npm run preview` | Preview production build |
| `npm run lint` | Run ESLint |

## 🎯 Key Features

- ✅ User authentication (JWT-based)
- ✅ Multi-step project creation workflow
- ✅ Video editor integration (CapCut & Final Cut Pro)
- ✅ Video preview and annotation
- ✅ Offline support with IndexedDB
- ✅ Admin dashboard
- ✅ Responsive dark theme UI

## 🔄 Application Flow

1. **Authentication**: Signup/Login with JWT tokens
2. **Project Creation**: 4-step workflow
   - Step 1: Project details (name, description, goal)
   - Step 2: Upload final edited video
   - Step 3: Import project file & annotate sources/segments
   - Step 4: Submit project to backend
3. **Dashboard**: View, edit, and manage projects
4. **Admin**: Oversight and validation tools

## 🔌 API Integration

The frontend communicates with the backend API. Key endpoints:

- `POST /users` - User signup
- `POST /auth/login` - User login
- `POST /projects` - Create/update project (with video upload)
- `GET /projects` - Get user projects
- `POST /projects/:id/submit` - Submit project
- `GET /projects/admin/all-projects` - Admin: Get all projects

All authenticated requests require JWT token in `Authorization: Bearer <token>` header.

## 📦 Build for Production

```bash
npm run build
```

Output will be in the `dist/` directory.

## 🌐 Browser Support

- Chrome/Edge (full support including File System Access API)
- Firefox (supported)
- Safari (supported)

## 📚 Documentation

For detailed documentation, see [FRONTEND_DOCUMENTATION.md](./FRONTEND_DOCUMENTATION.md)

## 🔒 Security Notes

- JWT tokens stored in localStorage
- All API calls include authentication headers
- Protected routes require valid tokens
- CORS configured on backend

## 🐛 Troubleshooting

**Port already in use?**
```bash
npm run dev -- --port 3002
```

**Environment variables not loading?**
- Ensure variables are prefixed with `VITE_`
- Restart dev server after changing `.env`

**API connection errors?**
- Verify backend is running
- Check `VITE_API_BASE_URL` in `.env`
- Verify CORS is enabled on backend

## 📄 License

Private project - All rights reserved
