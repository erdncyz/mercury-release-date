# Mercury Release Date

A React application for tracking project transitions and release dates with a real JSON database backend.

## Features

- Track project transitions with detailed information
- Admin panel for managing transitions
- Responsive design with table and card views
- Search functionality
- Contact information display for managers and assistants
- Real JSON database backend with Express.js API
- Persistent data storage in `data.json` file

## Architecture

This application uses a **full-stack architecture**:

- **Frontend**: React.js with TypeScript
- **Backend**: Express.js API server
- **Database**: JSON file (`data.json`)
- **Ports**: Frontend (3000), Backend (3001)

## Getting Started

### Prerequisites

- Node.js (v14 or higher)
- npm or yarn

### Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd mercury-release-date
```

2. Install dependencies:
```bash
npm install
```

3. Start both frontend and backend (Recommended):
```bash
npm run dev
```

This will start:
- **Frontend**: `http://localhost:3000` (or your IP address)
- **Backend**: `http://localhost:3001` (or your IP address)

### Alternative Startup Methods

#### Start Both Services Separately
```bash
# Terminal 1 - Start backend
npm run server

# Terminal 2 - Start frontend
npm start
```

#### Frontend Only (Different Ports)
```bash
# Use port 3001
npm run start:3001

# Use port 3002  
npm run start:3002

# Use port 80 (requires sudo)
npm run start:80
```

## Database System

This application uses a **hybrid database system** with **Redis cache** and **file-based JSON backup** for optimal performance and reliability:

### 🔴 Redis Cache (Primary)
- **Redis Server**: 'Write your redis info'
- **High Performance**: In-memory caching for fast data access
- **Automatic Fallback**: If Redis is unavailable, falls back to file system
- **1-hour TTL**: Data expires after 1 hour for cache management

### 📁 File System Backup (Secondary)
- **JSON Database**: `data.json` file for persistent storage
- **Automatic Sync**: Data is automatically synced between Redis and file system
- **Easy Backup**: Single file backup and restore
- **Portable**: Can be moved between environments easily

### Database Features
- **Hybrid Storage**: Redis + File system with automatic fallback
- **REST API**: Full CRUD operations
- **Real-time Updates**: Immediate data persistence
- **Backup/Restore**: Database backup functionality

### Database Structure
```json
{
  "transitions": [
    {
      "id": "1234567890",
      "projectName": "E-Ticaret Platformu",
      "color": "#3B82F6",
      "taskLink": "https://jira.company.com/browse/PROJ-123",
      "transitionTime": "05:00 - 07:00",
      "lastTestSubmissionDate": "2024-01-10",
      "lastPackageBindingDate": "2024-01-12",
      "regressionDeliveryDate": "2024-01-20",
      "transitionDate": "2024-01-25",
      "transitionManager": "Ahmet Yılmaz",
      "transitionAssistant": "Fatma Demir",
      "managerEmail": "ahmet.yilmaz@company.com",
      "managerPhone": "+90 532 123 4567",
      "assistantEmail": "fatma.demir@company.com",
      "assistantPhone": "+90 533 987 6543"
    }
  ],
  "adminCredentials": {
    "username": "admin",
    "password": "admin123"
  },
  "settings": {
    "version": "1.0.0",
    "lastUpdated": "2024-01-01T00:00:00.000Z"
  }
}
```

### API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/transitions` | Get all transitions |
| POST | `/api/transitions` | Add new transition |
| PUT | `/api/transitions/:id` | Update transition |
| DELETE | `/api/transitions/:id` | Delete transition |
| GET | `/api/admin/credentials` | Get admin credentials |
| PUT | `/api/admin/credentials` | Update admin credentials |
| GET | `/api/database/info` | Get database information |
| GET | `/api/database/backup` | Backup database |
| POST | `/api/database/restore` | Restore database |
| GET | `/api/health` | Health check |

## Admin Setup

### Setting Up Admin Credentials

You can set up admin credentials without starting the project using the provided setup script:

#### Interactive Setup
```bash
npm run setup-admin
```
This will prompt you to enter username and password interactively.

#### Default Setup
```bash
npm run setup-admin:default
```
This will set up default credentials (username: `admin`, password: `admin123`).

#### Custom Setup Example
```bash
npm run setup-admin
# Enter username: erdnc
# Enter password: 12345
```

#### View Current Credentials
```bash
npm run setup-admin:show
```

#### View Database Information
```bash
npm run setup-admin:info
```

## Available Scripts

### Development
- `npm run dev` - Start both frontend and backend (Recommended)
- `npm start` - Start frontend only (port 3000)
- `npm run server` - Start backend only (port 3000)
- `npm run start:3001` - Start frontend on port 3001
- `npm run start:3002` - Start frontend on port 3002
- `npm run start:80` - Start frontend on port 80 (requires sudo)

### Production (PM2)
- `npm run pm2:start` - Build and start with PM2
- `npm run pm2:stop` - Stop PM2 process
- `npm run pm2:restart` - Restart PM2 process
- `npm run pm2:delete` - Delete PM2 process
- `npm run pm2:logs` - View PM2 logs
- `npm run pm2:status` - Check PM2 status
- `npm run pm2:monit` - Monitor PM2 processes

### Build & Test
- `npm run build` - Build for production
- `npm run test` - Run tests
- `npm run eject` - Eject from Create React App

### Admin Management
- `npm run setup-admin` - Interactive admin credential setup
- `npm run setup-admin:default` - Set default admin credentials
- `npm run setup-admin:show` - Show current admin credentials
- `npm run setup-admin:info` - Show database information

## Project Structure

```
mercury-release-date/
├── src/
│   ├── components/          # React components
│   ├── contexts/           # React contexts
│   ├── pages/              # Page components
│   ├── types/              # TypeScript interfaces
│   └── utils/
│       ├── api.ts          # API utility functions
│       ├── database.ts     # Database utilities (legacy)
│       └── mockData.ts     # Data management functions
├── server.js               # Express.js backend server
├── data.json               # Database file
├── setup-admin.js          # Admin setup script
└── package.json
```

## Usage

1. **Start the application**: `npm run dev`
2. **Access the app**: Open `http://localhost:3000`
3. **Admin login**: Click "Admin Login" and use credentials
4. **Add transitions**: Use the admin panel to add/edit/delete transitions
5. **View data**: All data is automatically saved to `data.json`

## Troubleshooting

### Port Already in Use
If you get "address already in use" errors:

```bash
# Kill existing processes
pkill -f "react-scripts"
pkill -f "node server.js"

# Then restart
npm run dev
```

### Database Issues
If the database gets corrupted:

```bash
# Backup current data
cp data.json data.json.backup

# Reset database
rm data.json
npm run setup-admin:default
```

### Backend Connection Issues
If frontend can't connect to backend:

1. Check if backend is running: `curl http://localhost:3001/api/health` (or your IP address)
2. Restart backend: `npm run server`
3. Check for port conflicts

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## License

This project is licensed under the MIT License.
