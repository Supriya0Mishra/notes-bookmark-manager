# notes-bookmark-manager
# Personal Notes & Bookmark Manager

A full-stack web application for organizing notes and bookmarks with smart features like auto-tagging, search, and user authentication.

![Tech Stack](https://img.shields.io/badge/MongoDB-Atlas-green?logo=mongodb)
![Tech Stack](https://img.shields.io/badge/Express-4.18-blue?logo=express)
![Tech Stack](https://img.shields.io/badge/Next.js-14-black?logo=next.js)
![Tech Stack](https://img.shields.io/badge/Node.js-22-green?logo=node.js)

## Features

### Core Functionality
- ✅ **Full CRUD Operations** - Create, read, update, delete notes and bookmarks
- ✅ **Smart Search** - Search across titles, content, and descriptions
- ✅ **Tag-based Filtering** - Organize with tags and filter by multiple tags
- ✅ **User Authentication** - JWT-based secure authentication
- ✅ **User Isolation** - Each user sees only their own data

### Standout Features
- 🎯 **Auto-Tag Suggestions** - Analyzes note content to suggest relevant tags
- 🔖 **Auto-Fetch Bookmark Titles** - Automatically extracts page titles from URLs
- ⭐ **Favorites System** - Pin important items to the top
- 🔍 **Real-time Search** - Instant filtering as you type
- 📱 **Responsive Design** - Works seamlessly on desktop, tablet, and mobile

## Tech Stack

**Backend:**
- Node.js & Express.js - RESTful API server
- MongoDB Atlas - Cloud database
- Mongoose - ODM for data modeling
- JWT - Secure authentication
- express-validator - Input validation
- Axios & Cheerio - Web scraping for metadata

**Frontend:**
- Next.js 14 - React framework with SSR
- Tailwind CSS - Utility-first styling
- Axios - HTTP client
- React Hooks - State management

## Prerequisites

- Node.js 14+ 
- MongoDB Atlas account (free tier)
- npm or yarn

## Quick Start

### 1. Clone the Repository
```bash
git clone <your-repo-url>
cd notes-bookmark-manager
```

### 2. Backend Setup
```bash
cd backend
npm install
```

Create `.env` file:
```env
PORT=5000
NODE_ENV=development
MONGODB_URI=your_mongodb_atlas_connection_string
JWT_SECRET=your_jwt_secret_key
JWT_EXPIRE=7d
CLIENT_URL=http://localhost:3000
```

**Important:** Replace `your_mongodb_atlas_connection_string` with your actual MongoDB Atlas URI.

Start backend:
```bash
npm run dev
```

Backend runs on **http://localhost:5000**

### 3. Frontend Setup

Open a new terminal:
```bash
cd frontend
npm install
```

Create `.env.local` file:
```env
NEXT_PUBLIC_API_URL=http://localhost:5000/api
```

Start frontend:
```bash
npm run dev
```

Frontend runs on **http://localhost:3000**

## API Documentation

### Base URL
```
http://localhost:5000/api
```

### Notes Endpoints

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| GET | `/notes` | Get all notes | Optional |
| GET | `/notes/:id` | Get single note | Optional |
| POST | `/notes` | Create note | Optional |
| PUT | `/notes/:id` | Update note | Optional |
| DELETE | `/notes/:id` | Delete note | Optional |

**Query Parameters:**
- `q` - Search term (searches title & content)
- `tags` - Comma-separated tags (e.g., `work,important`)

**Example:**
```bash
# Get all notes
curl http://localhost:5000/api/notes

# Search notes
curl http://localhost:5000/api/notes?q=meeting&tags=work

# Create note
curl -X POST http://localhost:5000/api/notes \
  -H "Content-Type: application/json" \
  -d '{
    "title": "My Note",
    "content": "Note content here",
    "tags": ["personal", "ideas"]
  }'
```

### Bookmarks Endpoints

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| GET | `/bookmarks` | Get all bookmarks | Optional |
| GET | `/bookmarks/:id` | Get single bookmark | Optional |
| POST | `/bookmarks` | Create bookmark | Optional |
| PUT | `/bookmarks/:id` | Update bookmark | Optional |
| DELETE | `/bookmarks/:id` | Delete bookmark | Optional |

**Example:**
```bash
# Create bookmark (auto-fetches title if empty)
curl -X POST http://localhost:5000/api/bookmarks \
  -H "Content-Type: application/json" \
  -d '{
    "url": "https://github.com",
    "description": "Code hosting platform",
    "tags": ["development", "tools"]
  }'
```

### Authentication Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/auth/register` | Register new user |
| POST | `/auth/login` | Login user |
| GET | `/auth/me` | Get current user (Protected) |

## 🏗️ Project Structure
```
notes-bookmark-manager/
├── backend/
│   ├── config/
│   │   └── db.js                 # MongoDB connection
│   ├── controllers/
│   │   ├── authController.js     # Auth logic
│   │   ├── noteController.js     # Notes CRUD
│   │   └── bookmarkController.js # Bookmarks CRUD
│   ├── middleware/
│   │   └── auth.js               # JWT middleware
│   ├── models/
│   │   ├── User.js               # User schema
│   │   ├── Note.js               # Note schema
│   │   └── Bookmark.js           # Bookmark schema
│   ├── routes/
│   │   ├── auth.js               # Auth routes
│   │   ├── notes.js              # Notes routes
│   │   └── bookmarks.js          # Bookmarks routes
│   ├── utils/
│   │   ├── metadata.js           # URL title fetching
│   │   └── tagSuggester.js       # Auto-tag logic
│   ├── .env.example
│   ├── package.json
│   └── server.js                 # Entry point
│
└── frontend/
    ├── components/
    │   ├── Layout.js             # App layout
    │   ├── SearchBar.js          # Search component
    │   ├── NoteCard.js           # Note display
    │   ├── BookmarkCard.js       # Bookmark display
    │   ├── NoteModal.js          # Note form
    │   └── BookmarkModal.js      # Bookmark form
    ├── context/
    │   └── AuthContext.js        # Auth state
    ├── pages/
    │   ├── index.js              # Home page
    │   ├── notes.js              # Notes page
    │   ├── bookmarks.js          # Bookmarks page
    │   └── auth.js               # Login/Register
    ├── styles/
    │   └── globals.css           # Global styles
    ├── utils/
    │   └── api.js                # API client
    └── package.json
```

## Key Technical Decisions

### Why MongoDB Atlas?
- Cloud-hosted, no local setup required
- Free tier suitable for development
- Easy scaling for production
- Built-in backup and monitoring

### Why Next.js?
- Server-side rendering for better SEO
- File-based routing
- Built-in API routes capability
- Excellent developer experience

### Why JWT Authentication?
- Stateless authentication
- Scalable across multiple servers
- Industry-standard security
- Easy to implement and maintain

## Troubleshooting

### Backend won't start

**Error:** `URI must include hostname, domain name, and tld`

**Solution:** Check your `MONGODB_URI` in `.env`. Ensure:
- Special characters in password are URL-encoded (e.g., `@` → `%40`)
- Database name is included (e.g., `/notesdb`)
- Format: `mongodb+srv://user:password@cluster.mongodb.net/dbname`

### Frontend can't connect to backend

**Error:** `ERR_CONNECTION_REFUSED`

**Solution:** 
- Ensure backend is running on port 5000
- Check `NEXT_PUBLIC_API_URL` in frontend `.env.local`
- Verify CORS settings in backend

### MongoDB connection fails

**Error:** `IP not whitelisted`

**Solution:**
- Go to MongoDB Atlas → Network Access
- Add your IP or use `0.0.0.0/0` for development

## Future Enhancements

- [ ] Rich text editor for notes
- [ ] Export notes to PDF/Markdown
- [ ] Collaborative notes (sharing)
- [ ] Mobile app (React Native)
- [ ] Browser extension for quick bookmarking
- [ ] AI-powered content summarization

## Testing
```bash
# Backend health check
curl http://localhost:5000/api/health

# Expected response:
# {"success":true,"message":"API is running"}
```

## License

MIT

## Author
Supriya Mishra
mishrasupriya1807@gmail.com

## Acknowledgments

- Built as part of a technical assessment
- Inspired by modern productivity tools like Notion and Obsidian
