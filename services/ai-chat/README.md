# AI Chat Service

Real-time conversational AI service with multi-user support and conversation persistence.

## 📁 Structure

```
ai-chat/
├── frontend/               # React application
│   ├── src/
│   │   ├── components/    # Chat UI components
│   │   ├── hooks/         # Custom React hooks
│   │   ├── pages/         # Page components
│   │   ├── services/      # API services
│   │   ├── store/         # State management
│   │   └── styles/        # CSS/Tailwind
│   ├── Dockerfile
│   ├── package.json
│   └── vite.config.ts
│
├── backend/                # Express API
│   ├── src/
│   │   ├── controllers/   # Request handlers
│   │   ├── services/      # Business logic
│   │   ├── models/        # Database models
│   │   ├── routes/        # API routes
│   │   ├── middleware/    # Custom middleware
│   │   ├── websocket/     # WebSocket handlers
│   │   └── utils/         # Utilities
│   ├── Dockerfile
│   ├── package.json
│   └── tsconfig.json
│
├── database/               # Database artifacts
│   ├── migrations/
│   │   └── 001_create_conversations.sql
│   ├── schemas/
│   │   └── chat_schema.sql
│   └── seeds/
│
└── docker-compose.yml
```

## 🚀 Quick Start

### Prerequisites
- Node.js 18+
- Docker & Docker Compose

### Local Development

```bash
# Start services
docker-compose up -d

# Install dependencies
pnpm install

# Run backend
cd backend && pnpm dev

# Run frontend (in another terminal)
cd frontend && pnpm dev
```

Access the application at `http://localhost:5001`

## 🎯 Features

- **Real-time Chat**: Live message exchange with WebSocket support
- **Multi-user Conversations**: Support for group chats
- **Conversation History**: Persistent message storage
- **AI Integration**: Powered by LLM Router
- **Message Formatting**: Markdown support, code highlighting
- **User Profiles**: User management and preferences
- **Search**: Message and conversation search
- **Notifications**: Real-time notifications

## 📊 Database Schema

### Conversations Table
```sql
CREATE TABLE conversations (
  id UUID PRIMARY KEY,
  title VARCHAR(255),
  description TEXT,
  created_by UUID REFERENCES users(id),
  created_at TIMESTAMP,
  updated_at TIMESTAMP,
  is_archived BOOLEAN DEFAULT false
);
```

### Messages Table
```sql
CREATE TABLE messages (
  id UUID PRIMARY KEY,
  conversation_id UUID REFERENCES conversations(id),
  user_id UUID REFERENCES users(id),
  content TEXT,
  role ENUM('user', 'assistant'),
  created_at TIMESTAMP,
  updated_at TIMESTAMP
);
```

## 🔌 API Endpoints

### Conversations
- `GET /api/conversations` - List conversations
- `POST /api/conversations` - Create conversation
- `GET /api/conversations/:id` - Get conversation details
- `PATCH /api/conversations/:id` - Update conversation
- `DELETE /api/conversations/:id` - Delete conversation

### Messages
- `GET /api/conversations/:id/messages` - Get messages
- `POST /api/conversations/:id/messages` - Send message
- `PATCH /api/messages/:id` - Edit message
- `DELETE /api/messages/:id` - Delete message
- `POST /api/messages/:id/react` - Add reaction

### WebSocket
- `ws://localhost:3001/chat/:conversationId` - Join chat room

## 🔧 Configuration

```env
# Database
DATABASE_URL=postgresql://user:pass@localhost:5432/ai_chat

# API
PORT=3001
API_URL=http://localhost:3001

# Frontend
REACT_APP_API_URL=http://localhost:3001
REACT_APP_WS_URL=ws://localhost:3001

# LLM Configuration
LLM_MODEL=gpt-4
LLM_TEMPERATURE=0.7
MAX_TOKENS=2000
```

## 🧪 Testing

```bash
# Run tests
pnpm test

# Integration tests
pnpm test:integration

# E2E tests
pnpm test:e2e
```

## 📚 API Documentation

OpenAPI documentation available at `http://localhost:3001/api/docs`

## 🚢 Deployment

```bash
# Build Docker image
docker build -t agentics-ai-chat:latest .

# Push to registry
docker push agentics-ai-chat:latest

# Deploy to Kubernetes
kubectl apply -f k8s/
```

## 🤝 Contributing

See main [Contributing Guide](../../CONTRIBUTING.md)

---

**Part of Agentics Labs Platform**
