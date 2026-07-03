# CampusThrift - NITT Peer-to-Peer Student Marketplace

CampusThrift is a full-stack peer-to-peer student marketplace platform engineered specifically for the National Institute of Technology, Tiruchirappalli (NITT) community. The system enables students to securely list, request, negotiate, and transact second-hand items within the campus.

---

## Key Capabilities

- **NITT Directory Authentication**: User registration is restricted to verified `@nitt.edu` emails. Authentication incorporates secure JSON Web Tokens (JWT) coupled with One-Time Password (OTP) validation delivered via Brevo integrations.
- **Unified Communication System**: Real-time buyer-seller negotiation chat utilizing Socket.io. The messaging engine groups chats strictly by participant pairs to prevent duplicate inbox threads and injects active product inquiry cards directly into the message log.
- **Transaction Flow**: Incorporates buy request lifecycles and a Stripe payment gateway integration.
- **Trust Score System**: Calculates seller credibility scores based on confidential, post-transaction anonymous buyer reviews.
- **Moderation Engine**: Fine-grained administrative tools for listing deletion, user suspension, and global listing hide triggers on account block.
- **Fully Responsive Architecture**: Structured layout with responsive grid listings, unified drawer navigation, and clean image-to-video file uploads.

---

## System Architecture & Tech Stack

The application follows a decoupled client-server architecture:

### Frontend
- **Framework**: React 18 with Vite build tool.
- **State Management & Caching**: TanStack React Query for declarative data fetching, loading states, and mutations.
- **Styling**: Vanilla CSS with modern typography, dark theme panels, and CSS glassmorphism.
- **Routing**: React Router DOM (v6) with path guards.

### Backend
- **Platform**: Node.js with Express.js REST API.
- **Database**: MongoDB utilizing Mongoose schemas and compound indexes for query optimization.
- **Real-time Engine**: Socket.io event-driven layer for online indicator logs and instant messaging sync.
- **File Processing**: Multer memory storage parsed directly to Cloudinary storage buckets.

---

## Local Development Setup

### Prerequisites
- Node.js (v20 or higher)
- MongoDB server running locally or a MongoDB Atlas URI
- Brevo API key (for mail delivery)
- Cloudinary API credentials (for file hosting)

### 1. Clone and Navigate
```bash
git clone https://github.com/Ram-Choudhary-24/campusthrift.git
cd campusthrift
```

### 2. Backend Setup
1. Navigate to the server folder:
   ```bash
   cd server
   ```
2. Create your `.env` configuration file:
   ```bash
   cp .env.production.example .env
   ```
3. Populate the required environment variables in the newly created `.env` file.
4. Install server dependencies and launch the server:
   ```bash
   npm install
   npm run dev
   ```

### 3. Frontend Setup
1. In a separate terminal session, navigate to the client folder:
   ```bash
   cd ../client
   ```
2. Install client dependencies and run the Vite bundler:
   ```bash
   npm install
   npm run dev
   ```
3. The client application will be accessible at `http://localhost:5173`.

---

## Docker Deployment (Recommended)

The repository provides a production-ready Docker Compose configuration that sets up the database, server, and client services in unified containers.

### Setup and Startup
Run the following command in the project root directory:
```bash
docker compose up --build -d
```
This builds the client and server Dockerfiles, downloads the MongoDB image, and launches all containers in detached mode.

---

## Database Management Utilities

The codebase includes a utility script to reset test databases to a clean start state while preserving administrative developer credentials.

To run the database cleanup:
```bash
node server/src/utils/reset_database.js
```
*Note: This deletes all transaction histories, notifications, listings, and messages, but updates and preserves the registered admin emails (`205124076@nitt.edu` and `20514076@nitt.edu`).*

---

## Repository Structure

```
campus_thrift/
├── client/                  # React Frontend
│   ├── src/
│   │   ├── api/             # Axios Instance configuration
│   │   ├── components/      # Shared components
│   │   ├── hooks/           # Custom state hooks
│   │   ├── pages/           # Pages (Dashboard, Chat, etc.)
│   │   ├── store/           # Zustand stores
│   │   └── utils/           # Shared constants
│   └── vite.config.js
│
├── server/                  # Node.js/Express Backend
│   ├── src/
│   │   ├── config/          # Database configuration
│   │   ├── controllers/     # Controller handlers
│   │   ├── middleware/      # Auth, files middleware
│   │   ├── models/          # Mongoose database models
│   │   ├── routes/          # Express route definitions
│   │   ├── services/        # Sockets, mail integrations
│   │   └── utils/           # Custom helpers and utilities
│   └── Dockerfile
│
└── docker-compose.yml       # Production-ready compose configuration
```

---

## Authors & Contributors

- **Ram Choudhary** - NIT Trichy
