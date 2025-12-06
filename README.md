# 🤖 RAG-Powered News Chatbot

A comprehensive full-stack intelligent news chatbot that leverages Retrieval-Augmented Generation (RAG) to provide real-time insights from 100+ news sources across 10 major categories with source attribution.

[![Live Demo](https://img.shields.io/badge/demo-live-success)](https://aguru-sireesha-rag-chatbot.vercel.app)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Node.js](https://img.shields.io/badge/node-%3E%3D16-brightgreen)](https://nodejs.org/)

### 🚀 Repositories
- Frontend: [RAG-Powered-Chatbot-Frontend](https://github.com/sireesha-siri/RAG-Powered-Chatbot-Frontend)
- Backend: [RAG-Powered-Chatbot-Backend](https://github.com/sireesha-siri/RAG-Powered-Chatbot-Backend)

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Features](#-features)
- [Architecture](#-architecture)
- [Tech Stack](#-tech-stack)
- [Project Structure](#-project-structure)
- [Quick Start](#-quick-start)
- [Frontend Documentation](#-frontend)
- [Backend Documentation](#-backend)
- [API Documentation](#-api-documentation)
- [Testing](#-testing)
- [Deployment](#-deployment)
- [Troubleshooting](#-troubleshooting)
- [Contributing](#-contributing)
- [Acknowledgments](#-acknowledgments)

## 🎯 Overview

This project combines a modern React frontend with a powerful Node.js backend to create an AI-powered news chatbot that:

- **Ingests** articles from 100+ RSS feeds across 10 categories
- **Embeds** content using Jina AI v3 (1024-dimensional vectors)
- **Stores** vectors in Qdrant for lightning-fast similarity search
- **Retrieves** relevant articles using semantic search
- **Generates** intelligent responses using Google Gemini
- **Attributes** sources with clickable links to original articles
- **Persists** chat sessions across page refreshes

## ✨ Features

### Frontend Features
- 🤖 **Intelligent Chat Interface** - Clean, responsive UI with real-time messaging
- 🎨 **Modern Design** - Dark/light theme support with smooth animations
- 📱 **Mobile Optimized** - Touch-friendly, fully responsive design
- 💾 **Session Persistence** - Chat history survives page refreshes
- 🔗 **Source Attribution** - Clickable links to original news articles
- ⌨️ **Accessibility** - ARIA labels, keyboard navigation, high contrast support

### Backend Features
- 📰 **Comprehensive Coverage** - 100+ RSS feeds across 10 categories
- 🧠 **Advanced RAG Pipeline** - Jina v3 + Qdrant + Google Gemini
- 🔍 **Semantic Search** - 1024-dimensional vector similarity matching
- 🗂️ **Category Intelligence** - Context-aware responses across all domains
- 💬 **Session Management** - Redis-powered with auto-expiration
- 📊 **Real-time Health Monitoring** - Detailed system status endpoints

## 🏗️ Architecture

```
User Input → Frontend (React)
                ↓
          Express API Server
                ↓
         RAG Pipeline
        /      |      \
   Qdrant   Gemini   Redis
   (Search)  (AI)  (Sessions)
        \      |      /
          Category-Aware
           Response
                ↓
    Frontend (with sources)
```

### Data Flow
1. **Ingestion**: RSS feeds → Article extraction → Jina v3 embeddings → Qdrant storage
2. **Query**: User question → Embedding → Vector search → Top 5 relevant articles
3. **Generation**: Articles + query → Gemini AI → Contextual response
4. **Attribution**: Response + source links → Frontend display

## 🛠️ Tech Stack

| Component | Technology | Purpose |
|-----------|-----------|---------|
| **Frontend** | React 18 + SCSS | Modern UI with responsive design |
| **Backend** | Node.js + Express | REST API server |
| **Embeddings** | Jina AI v3 | 1024-dim semantic vectors |
| **Vector DB** | Qdrant Cloud | Fast similarity search |
| **AI Model** | Google Gemini | Response generation |
| **Sessions** | Redis Cloud | Session management |
| **Logging** | Winston | Structured logging |
| **Deployment** | Vercel + Railway/Render | Cloud hosting |

## 📁 Project Structure

```
rag-chatbot/
├── frontend/                    # React frontend
│   ├── public/
│   │   ├── index.html
│   │   └── favicon.ico
│   ├── src/
│   │   ├── components/
│   │   │   └── ChatUI.js       # Main chat component
│   │   ├── styles/
│   │   │   └── chat-ui.scss    # Complete styling
│   │   ├── config/
│   │   │   └── api.js          # API configuration
│   │   ├── App.js
│   │   └── index.js
│   ├── package.json
│   └── .env.example
│
├── backend/                     # Node.js backend
│   ├── src/
│   │   ├── services/
│   │   │   ├── SessionManager.js        # Redis sessions
│   │   │   ├── RAGService.js            # Core RAG logic
│   │   │   ├── EmbeddingService.js      # Jina v3 integration
│   │   │   └── NewsIngestionService.js  # RSS feed ingestion
│   │   ├── routes/
│   │   │   ├── chat.js                  # Chat endpoints
│   │   │   └── sessions.js              # Session endpoints
│   │   └── utils/
│   │       └── logger.js                # Centralized logging
│   ├── scripts/
│   │   └── ingestNews.js       # News ingestion script
│   ├── server.js               # Main server file
│   ├── package.json
│   └── .env.example
│
└── README.md                    # This file
```

## 🚀 Quick Start

### Prerequisites

- **Node.js** v16 or higher
- **npm** or **yarn**
- **Redis** instance (Redis Cloud free tier works)
- **Qdrant** instance (Qdrant Cloud free tier works)
- **API Keys**:
  - Google Gemini API key
  - Jina AI API key (v3 compatible)

### Installation

```bash
# Clone the repository
git clone https://github.com/sireesha-siri/RAG-Powered-Chatbot.git
cd RAG-Powered-Chatbot

# Install backend dependencies
cd backend
npm install
cp .env.example .env
# Edit .env with your API keys and service URLs

# Install frontend dependencies
cd ../frontend
npm install
cp .env.example .env
# Edit .env with your backend URL
```

### Backend Configuration

Edit `backend/.env`:

```env
# Cloud Service URLs (REQUIRED)
REDIS_URL=redis://default:password@your-redis-instance:6379
QDRANT_URL=https://your-cluster.qdrant.io:6333
QDRANT_API_KEY=your-qdrant-api-key

# API Keys (REQUIRED)
GEMINI_API_KEY=your-gemini-api-key
JINA_API_KEY=your-jina-v3-api-key

# Server Configuration
PORT=5000
NODE_ENV=development

# Enhanced Configuration
TARGET_ARTICLES=60
INGESTION_STRATEGY=comprehensive
```

### Frontend Configuration

Edit `frontend/.env`:

```env
# Backend API URL
VITE_API_URL=http://localhost:5000

# App Configuration
VITE_APP_NAME="News Chatbot"
VITE_APP_VERSION=1.0.0
```

### Running the Application

```bash
# Terminal 1 - Start Backend
cd backend
npm run ingest    # Populate database (one-time setup)
npm run dev       # Start backend server

# Terminal 2 - Start Frontend
cd frontend
npm start         # Start frontend development server
```

Access the application at `http://localhost:3000`

## 🎨 Frontend

### Features Overview
- **Component Architecture**: Single-file ChatUI component with clean state management
- **Styling**: SCSS with CSS custom properties for theming
- **Session Management**: Auto-save to localStorage with backend sync
- **Responsive Design**: Mobile-first with breakpoints for all devices
- **Theme Support**: Dark/light mode with smooth transitions
- **Accessibility**: WCAG 2.1 AA compliant

### Key Frontend Commands

```bash
cd frontend

# Development
npm start              # Start dev server (port 3000)
npm run build          # Production build
npm test               # Run tests

# Deployment
npm run build          # Create optimized build
serve -s build         # Test production build locally
```

### Frontend Environment Variables

```env
VITE_API_URL=http://localhost:5000           # Backend URL
VITE_APP_NAME="News Chatbot"                 # App display name
VITE_APP_VERSION=1.0.0                       # Version number
```

### Component Structure

```javascript
// src/components/ChatUI.js
- State management (messages, session, theme)
- API integration (fetch messages, send queries)
- Real-time updates (typing indicators, loading states)
- Error handling (connection issues, API errors)
- Source attribution (clickable news links)
```

## 🔧 Backend

### Features Overview
- **RAG Pipeline**: Complete implementation with 5-stage processing
- **100+ RSS Feeds**: Organized across 10 major categories
- **Jina v3 Embeddings**: 1024-dimensional semantic vectors
- **Qdrant Integration**: Optimized vector storage and search
- **Redis Sessions**: Fast session management with TTL
- **Health Monitoring**: Detailed system status endpoints

### News Categories

1. **Major News** - BBC, CNN, Reuters, NPR, Al Jazeera
2. **Technology** - TechCrunch, Wired, The Verge, Ars Technica
3. **Business** - Forbes, CNBC, Bloomberg, Financial Times
4. **Sports** - ESPN, BBC Sport, Sky Sports, Sports Illustrated
5. **Entertainment** - Variety, Billboard, Rolling Stone, Hollywood Reporter
6. **Health** - WHO, Healthline, Medical News Today, WebMD
7. **Science** - NASA, Nature, Scientific American, Space.com
8. **Travel** - Lonely Planet, Conde Nast, Travel + Leisure
9. **Hobbies** - IGN, Kotaku, Vogue, GQ
10. **Web Development** - WordPress, CSS Tricks, Smashing Magazine

### Key Backend Commands

```bash
cd backend

# Development
npm run dev            # Start with hot reload
npm start              # Production mode
npm run ingest         # Ingest news articles

# Ingestion options
npm run ingest -- --test              # Test RSS feeds
npm run ingest -- --clear             # Clear and re-ingest
npm run ingest -- --target=80         # Custom article count

# Testing
npm test                               # Run tests
curl http://localhost:5000/health     # Check health
```

### Backend Environment Variables

```env
# Required Services
REDIS_URL=redis://...                  # Redis connection
QDRANT_URL=https://...                 # Qdrant cluster URL
QDRANT_API_KEY=...                     # Qdrant API key
GEMINI_API_KEY=...                     # Google Gemini key
JINA_API_KEY=...                       # Jina AI key

# Configuration
PORT=5000                              # Server port
NODE_ENV=development                   # Environment
TARGET_ARTICLES=60                     # Articles per ingestion
INGESTION_STRATEGY=comprehensive       # Ingestion mode
```

### RAG Pipeline Details

```javascript
// 1. News Ingestion
NewsIngestionService → 100+ RSS feeds → Parse articles

// 2. Embedding Generation
EmbeddingService → Jina v3 → 1024-dim vectors

// 3. Vector Storage
RAGService → Qdrant → Store with metadata

// 4. Semantic Search
Query → Embedding → Qdrant search → Top 5 articles

// 5. AI Generation
Context + Query → Gemini → Response + sources
```

## 📡 API Documentation

### Session Endpoints

```bash
# Create new session
POST /api/sessions
Response: { sessionId, timestamp }

# Get session history
GET /api/sessions/:id/history
Response: { messages: [...], sessionId }

# Clear chat history
DELETE /api/sessions/:id/history
Response: { success: true, sessionId }

# Delete session
DELETE /api/sessions/:id
Response: { success: true, deleted: sessionId }
```

### Chat Endpoints

```bash
# Send message and get AI response
POST /api/chat/:sessionId
Body: { message: "Your question here" }
Response: {
  response: "AI generated answer...",
  sources: [
    {
      title: "Article Title",
      source: "BBC News",
      url: "https://...",
      similarity: 0.89
    }
  ],
  sessionId: "abc-123",
  timestamp: "2024-01-01T12:00:00Z"
}

# Get suggested questions
GET /api/chat/:sessionId/suggestions
Response: { suggestions: [...] }

# Submit feedback
POST /api/chat/:sessionId/feedback
Body: { messageId, rating, comment }
```

### Health & Admin Endpoints

```bash
# Basic health check
GET /health
Response: { status: "healthy", timestamp }

# Detailed health status
GET /api/health/detailed
Response: {
  status: "healthy",
  services: {
    redis: { status: "connected" },
    qdrant: { status: "connected", collections: 1 },
    gemini: { status: "available" }
  },
  feeds: { total: 100, working: 54 }
}

# Category statistics
GET /api/stats/categories
Response: {
  technology: { articles: 7, avgSimilarity: 0.72 },
  business: { articles: 7, avgSimilarity: 0.68 },
  ...
}

# Cleanup expired sessions
POST /api/sessions/cleanup
Response: { deleted: 5, remaining: 10 }
```

## 🧪 Testing

### Frontend Testing

```bash
cd frontend

# Test checklist
✓ App loads and creates session
✓ Can send messages and receive responses
✓ Sources display as clickable links
✓ Chat history persists on refresh
✓ Reset session button works
✓ Theme toggle works
✓ Mobile responsive design
✓ Error states display properly
```

### Backend Testing

```bash
cd backend

# Test RSS feeds
npm run ingest -- --test

# Test specific category
node -e "
const NewsService = require('./src/services/NewsIngestionService');
const news = new NewsService();
news.testCategoryFeeds('technology', 3).then(console.log);
"

# Test RAG pipeline
node -e "
const RAGService = require('./src/services/RAGService');
const rag = new RAGService();
rag.initialize().then(() => {
  return rag.retrieveRelevantPassages('AI news', 3);
}).then(console.log);
"

# Health check
curl http://localhost:5000/health
curl http://localhost:5000/api/health/detailed
```

### Test Questions

Try these to verify functionality across categories:

```
# Technology
"What's the latest news about AI and technology?"
"Tell me about recent developments in artificial intelligence"

# Business
"How is the stock market performing?"
"Any news about major tech companies?"

# General News
"What's happening in the world today?"
"Tell me about breaking news"

# Sports
"Recent sports headlines?"
"What's new in football?"

# Entertainment
"Latest entertainment news?"
"What's trending in music?"
```

## 🚀 Deployment

### Frontend Deployment (Vercel)

```bash
cd frontend

# Build for production
npm run build

# Deploy to Vercel
vercel deploy --prod

# Environment variables in Vercel dashboard:
VITE_API_URL=https://your-backend-url.com
VITE_APP_NAME="News Chatbot"
```

### Backend Deployment (Railway/Render)

```bash
cd backend

# Set environment variables in hosting dashboard
# All variables from .env.example

# Build command
npm install

# Start command
npm start

# Health check endpoint
/health
```

### Production Checklist

- [ ] All environment variables configured
- [ ] CORS settings updated for production domain
- [ ] Redis and Qdrant cloud instances provisioned
- [ ] API keys secured (not in repository)
- [ ] Rate limiting enabled
- [ ] Logging configured
- [ ] Health monitoring set up
- [ ] SSL certificates configured
- [ ] Database populated with articles

## 🐛 Troubleshooting

### Common Issues

**"Connecting..." Forever**
```bash
# Check backend is running
curl http://localhost:5000/health

# Verify CORS configuration
# Check VITE_API_URL in frontend/.env
```

**No AI Responses**
```bash
# Backend needs ingestion first
cd backend
npm run ingest

# Check for API key errors in logs
tail -f logs/combined.log
```

**Sources Not Showing**
- Normal for some queries (RAG only shows confident matches)
- Try more specific, news-related questions
- Check if backend has recent articles
- Run `npm run ingest` to refresh data

**Session Expires Quickly**
- Sessions auto-expire after 1 hour (Redis TTL)
- Check Redis connection in backend
- Verify `REDIS_URL` in backend/.env

**Build Errors**
```bash
# Clear cache and reinstall
rm -rf node_modules package-lock.json
npm install

# Clear npm cache
npm cache clean --force
```

### Debug Mode

```bash
# Frontend debug
cd frontend
REACT_APP_DEBUG=true npm start

# Backend debug
cd backend
LOG_LEVEL=debug npm run dev

# Monitor logs
tail -f backend/logs/combined.log
```

## 🤝 Contributing

We welcome contributions! Here's how to get started:

### Development Workflow

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Make your changes
4. Test thoroughly (both frontend and backend)
5. Commit with descriptive messages (`git commit -m 'Add amazing feature'`)
6. Push to your branch (`git push origin feature/amazing-feature`)
7. Open a Pull Request

### Code Style

- **Frontend**: Prettier + ESLint
- **Backend**: ESLint with Node.js rules
- **Commits**: Conventional Commits format
- **Comments**: JSDoc for functions

### Testing Requirements

- [ ] Frontend: Manual testing checklist completed
- [ ] Backend: All endpoints tested with curl/Postman
- [ ] Integration: Full user flow tested
- [ ] Mobile: Responsive design verified
- [ ] Accessibility: WCAG compliance checked

## 📊 Performance Metrics

### Current Performance

- **RSS Feed Success**: 55% average (54/100 feeds working)
- **Embedding Speed**: ~1 article/second
- **Query Response**: <2 seconds end-to-end
- **Vector Search**: <100ms similarity queries
- **Frontend Load**: <3 seconds initial load

### Optimization Targets

- Increase feed success rate to 70%
- Reduce query response to <1 second
- Implement response caching
- Add WebSocket for real-time updates

## 🔮 Future Enhancements

### Planned Features

- [ ] **Real-time Updates**: WebSocket integration
- [ ] **Voice Input**: Speech-to-text capability
- [ ] **Multi-language**: International news sources
- [ ] **Image Analysis**: Process article images
- [ ] **Trending Topics**: Identify breaking stories
- [ ] **Custom Sources**: User-configurable RSS feeds
- [ ] **Advanced Analytics**: Usage tracking and insights
- [ ] **Export Chat**: Download conversation history
- [ ] **Push Notifications**: Breaking news alerts

### Technical Improvements

- [ ] GraphQL API for flexible queries
- [ ] Kubernetes deployment
- [ ] Advanced caching strategies
- [ ] Unit and E2E test suites
- [ ] CI/CD pipeline automation
- [ ] Performance monitoring (Datadog/New Relic)
- [ ] Load balancing for high traffic

## 🙏 Acknowledgments

This project was developed with assistance from AI-powered development tools:

- **Anthropic Claude** - RAG pipeline architecture, component design, and comprehensive documentation
- **ChatGPT** - API integration patterns, error handling, and best practices
- **Cursor AI** - Real-time code suggestions and refactoring
- **GitHub Copilot** - Code completion and boilerplate generation

These tools accelerated development while maintaining code quality and modern best practices.

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 📞 Support

### Getting Help

- **Issues**: Open a GitHub issue with detailed description
- **Discussions**: Use GitHub Discussions for questions
- **Documentation**: Check README sections thoroughly
- **Logs**: Always include relevant log output

### Contact

- **Developer**: Sireesha Aguru
- **GitHub**: [@sireesha-siri](https://github.com/sireesha-siri)
- **Demo**: [Live Application](https://aguru-sireesha-rag-chatbot.vercel.app)

---

<div align="center">

**Built with ❤️ using React, Node.js, and AI**

[Live Demo](https://aguru-sireesha-rag-chatbot.vercel.app) • [Report Bug](https://github.com/sireesha-siri/RAG-Powered-Chatbot/issues) • [Request Feature](https://github.com/sireesha-siri/RAG-Powered-Chatbot/issues)

</div>
