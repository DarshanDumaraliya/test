# Repurpose AI - Video POC Frontend

A React-based frontend application for video annotation and project management. Create video editing projects, upload final videos, import CapCut/Final Cut Pro project files, and annotate source videos with detailed metadata.

## 🚀 Quick Start

### Prerequisites

- Node.js 18+ and npm
- Backend server running

### Installation

```bash
# Install dependencies
npm install

# Create .env file
echo "VITE_API_BASE_URL=http://localhost:3000" > .env

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
VITE_API_BASE_URL=http://localhost:3000
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



# Repurpose AI - Video POC Backend

NestJS-based RESTful API server for video annotation and project management. Handles authentication, project CRUD operations, file uploads, and administrative functions.

## 🚀 Quick Start

### Prerequisites

- Node.js 18+ and npm
- MySQL 5.7+ (or MySQL 8.0+)

### Installation

```bash
# Install dependencies
npm install

# Create .env file (see Environment Variables section)

# Create MySQL database
mysql -u root -p
CREATE DATABASE video_poc CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;

# Start development server
npm run start:dev
```

The server will be available at `http://localhost:3000`

## 📁 Project Structure

```
src/
├── modules/
│   ├── auth/        # Authentication module (JWT)
│   ├── users/       # User management
│   └── projects/    # Project CRUD operations
├── common/          # Shared utilities
├── database/        # Database configuration
└── main.ts          # Application entry point
```

## 🛠️ Technology Stack

- **NestJS 11** - Node.js framework
- **TypeScript** - Type safety
- **TypeORM** - ORM for MySQL
- **Passport JWT** - Authentication
- **bcrypt** - Password hashing
- **class-validator** - Input validation

## ⚙️ Environment Variables

Create a `.env` file in the root directory:

```env
# Server
PORT=3000

# Database
DB_TYPE=mysql
DB_HOST=localhost
DB_PORT=3306
DB_USERNAME=root
DB_PASSWORD=your_password
DB_NAME=video_poc

# JWT
JWT_SECRET=your_jwt_secret_key_here
JWT_EXPIRES_IN=7d

# AWS s3 bucket
AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
AWS_REGION=
S3_BUCKET_NAME=

# CORS (optional)
CORS_ORIGIN=http://localhost:3001
```

**Generate JWT Secret:**
```bash
node -e "console.log(require('crypto').randomBytes(32).toString('hex'))"
```

## 📝 Available Scripts

| Command | Description |
|---------|-------------|
| `npm run start:dev` | Start development server with watch mode |
| `npm run start:prod` | Start production server |
| `npm run build` | Compile TypeScript to JavaScript |
| `npm run format` | Format code with Prettier |
| `npm run lint` | Run ESLint |

## 🎯 Key Features

- ✅ JWT-based authentication
- ✅ User management (signup, login)
- ✅ Project CRUD operations
- ✅ File upload handling (videos, max 500MB)
- ✅ Admin endpoints for project oversight
- ✅ Input validation with DTOs
- ✅ MySQL database integration
- ✅ CORS enabled

## 🔌 API Endpoints

### Public Endpoints

- `POST /users` - User signup
- `POST /auth/login` - User login

### Authenticated Endpoints

- `POST /projects` - Create project (with video upload)
- `GET /projects` - Get user projects (with pagination & filters)
- `GET /projects/:id` - Get project by ID
- `PATCH /projects/:id` - Update project
- `DELETE /projects/:id` - Delete project
- `POST /projects/:id/submit` - Submit project

### Admin Endpoints

- `GET /projects/admin/all-projects` - Get all projects
- `POST /projects/admin/update-project-status` - Update project status
- `POST /projects/admin/validate-project` - Validate project

**Authentication:** Include JWT token in header: `Authorization: Bearer <token>`

## 📊 Database

The application uses TypeORM with automatic schema synchronization in development. Main tables:

- **users** - User accounts
- **user_projects** - User-project relationships

## 📁 File Storage

Use S3 cloud storage.

## 🔒 Security

- Password hashing with bcrypt
- JWT token authentication
- SQL injection prevention (TypeORM)
- Input validation with class-validator
- CORS configuration

## 🚀 Deployment

### Production Build

```bash
npm run build
npm run start:prod
```

## 🧪 Testing API

### Using cURL

```bash
# Login
curl -X POST http://localhost:3000/auth/login \
  -H "Content-Type: application/json" \
  -d '{"email":"user@example.com","password":"password123"}'

# Create Project (with token)
curl -X POST http://localhost:3000/projects \
  -H "Authorization: Bearer YOUR_TOKEN" \
  -F "project={\"name\":\"Test Project\"}" \
  -F "video=@/path/to/video.mp4"
```

## 🐛 Troubleshooting

**Database connection errors?**
- Verify MySQL is running
- Check database credentials in `.env`
- Ensure database exists

**Port already in use?**
```bash
# Change PORT in .env file
PORT=3001
```

**JWT token errors?**
- Verify `JWT_SECRET` is set in `.env`
- Check token expiration
- Verify token format in request header

## 📚 Documentation

For detailed documentation, see [BACKEND_DOCUMENTATION.md](./BACKEND_DOCUMENTATION.md)

