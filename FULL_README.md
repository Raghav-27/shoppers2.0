# Shoppers - E-commerce Product Aggregator 🛍️

A modern, async-powered web application that aggregates and compares products from multiple e-commerce platforms.

## 🚀 Features

- **Multi-Platform Search**: Search products across Meesho (more platforms coming soon)
- **Async Architecture**: Built with FastAPI and async Redis for high performance
- **Real-time Scraping**: Automatic product scraping with intelligent prefetching
- **User Authentication**: Secure session-based authentication with bcrypt password hashing
- **User Lists**: Wishlist, Cart, and Compare functionality
- **Smart Caching**: Redis-backed caching with automatic data refresh
- **Docker Support**: Fully containerized with Docker Compose

## 📋 Tech Stack

### Backend
- **FastAPI**: Modern async web framework
- **Uvicorn**: ASGI server for async operations
- **Redis**: Async data store and caching
- **httpx**: Async HTTP client for web scraping
- **bcrypt**: Secure password hashing
- **Pydantic**: Data validation

### Frontend
- **React 19**: Modern UI framework
- **React Hooks**: State management
- **CSS3**: Responsive styling

### Infrastructure
- **Docker & Docker Compose**: Containerization
- **Redis Commander**: Redis GUI management

## 🛠️ Installation

### Prerequisites
- Docker and Docker Compose
- Node.js 18+ (for local development)
- Python 3.11+ (for local development)

### Quick Start with Docker

1. **Clone the repository**
```bash
git clone <your-repo-url>
cd shoppers
```

2. **Create environment files**
```bash
# Backend environment
cp backend/.env.example backend/.env

# Frontend environment
cp .env.example .env
```

3. **Build and run with Docker Compose**
```bash
docker-compose up --build
```

4. **Access the applications**
- Frontend: http://localhost
- Backend API: http://localhost:5000
- API Docs: http://localhost:5000/docs
- Redis Commander: http://localhost:8081

### Local Development Setup

#### Backend Setup

```bash
cd backend

# Create virtual environment
python -m venv venv

# Activate virtual environment
# Windows:
venv\Scripts\activate
# Linux/Mac:
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt

# Copy environment file
cp .env.example .env

# Run Redis (or use Docker)
docker run -d -p 6379:6379 redis:7-alpine

# Start the API server
uvicorn api:app --reload --host 0.0.0.0 --port 5000
```

#### Frontend Setup

```bash
# Install dependencies
npm install

# Copy environment file
cp .env.example .env

# Start development server
npm start
```

## 📚 API Documentation

Once the backend is running, visit:
- **Swagger UI**: http://localhost:5000/docs
- **ReDoc**: http://localhost:5000/redoc

### Key Endpoints

#### Search
```http
GET /api/search?query=shoes&sort=relevance&page=1&per_page=10
```

#### Authentication
```http
POST /api/signup
POST /api/login
POST /api/logout
GET /api/validate-session
```

#### User Lists
```http
POST /api/user/wishlist
DELETE /api/user/wishlist
POST /api/user/cart
DELETE /api/user/cart
POST /api/user/compare
DELETE /api/user/compare
GET /api/user/lists
```

#### Health Check
```http
GET /health
```

## 🔧 Configuration

### Backend Environment Variables

See `backend/.env.example` for all available options:

```env
# Redis Configuration
REDIS_HOST=redis
REDIS_PORT=6379

# API Configuration
API_HOST=0.0.0.0
API_PORT=5000

# CORS Origins (comma-separated)
CORS_ORIGINS=http://localhost:3000,http://localhost:80

# Logging
LOG_LEVEL=INFO

# Session Settings
SESSION_EXPIRY_DAYS=7
```

### Frontend Environment Variables

See `.env.example`:

```env
# API URL (backend endpoint)
REACT_APP_API_URL=http://localhost:5000
```

## 🏗️ Architecture

### Async Architecture Benefits

- **Non-blocking I/O**: Redis and HTTP operations don't block the event loop
- **High Concurrency**: Handle 100+ concurrent requests with minimal resources
- **Efficient Scraping**: Parallel product scraping with intelligent rate limiting
- **Background Tasks**: Automatic prefetching without blocking user requests

### Data Flow

```
Frontend (React) 
    ↓
FastAPI Async Endpoints
    ↓
Async Redis Client ← → Async Scraper Module
    ↓
Redis Cache/Storage
```

### Scraper Architecture

The scraper module (`scraper_module.py`) is designed to be:
- **Importable**: Can be called directly as a Python module
- **Async-native**: Uses httpx for async HTTP requests
- **Intelligent**: Automatic prefetching and cursor-based pagination
- **Resilient**: Retry logic with exponential backoff

## 📁 Project Structure

```
shoppers/
├── backend/
│   ├── api.py                 # Main FastAPI application
│   ├── scraper_module.py      # Async scraper module
│   ├── sign_up.py             # Authentication utilities
│   ├── meesho_scraper.py      # Standalone scraper (legacy)
│   ├── requirements.txt       # Python dependencies
│   ├── Dockerfile             # Backend container config
│   ├── .env.example           # Environment template
│   └── tools/                 # Utility scripts
├── src/
│   ├── components/            # React components
│   ├── utils/                 # Frontend utilities
│   └── App.js                 # Main React app
├── public/                    # Static assets
├── docker-compose.yml         # Docker Compose configuration
├── Dockerfile                 # Frontend container config
├── package.json               # Node.js dependencies
└── README.md                  # This file
```

## 🐳 Docker Commands

```bash
# Build and start all services
docker-compose up --build

# Start services in background
docker-compose up -d

# View logs
docker-compose logs -f

# Stop all services
docker-compose down

# Remove volumes (clears data)
docker-compose down -v

# Rebuild specific service
docker-compose build backend
docker-compose up -d backend
```

## 🧪 Testing

```bash
# Backend tests (coming soon)
cd backend
pytest

# Frontend tests
npm test

# Coverage
npm test -- --coverage
```

## 🔒 Security Features

- **Bcrypt Password Hashing**: Secure password storage with salt
- **HTTP-Only Cookies**: Session tokens not accessible to JavaScript
- **CORS Protection**: Configurable allowed origins
- **Input Validation**: Pydantic models for request validation
- **Session Expiry**: Automatic session cleanup

## 🚀 Performance Optimizations

- **Async Redis**: Non-blocking database operations
- **Connection Pooling**: Reuse Redis connections
- **Smart Caching**: Automatic cache invalidation
- **Pagination**: Efficient data loading
- **Background Tasks**: Prefetching without blocking
- **Concurrent Scraping**: Parallel product fetching

## 📝 Development Status

### ✅ Completed
- [x] Async FastAPI backend
- [x] Async Redis integration
- [x] Direct scraper module import
- [x] Bcrypt password hashing
- [x] Structured logging
- [x] Health check endpoints
- [x] Docker Compose setup
- [x] Environment variable management
- [x] API documentation (Swagger)

### 🚧 In Progress
- [ ] WebSocket for real-time updates
- [ ] JWT token authentication
- [ ] Multi-platform scraper support
- [ ] Rate limiting
- [ ] Unit tests

### 📋 Planned
- [ ] Product comparison UI
- [ ] Advanced search filters
- [ ] User profile management
- [ ] Order history
- [ ] Price alerts

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 👥 Authors

- Aakash Raghav - Initial work

## 🙏 Acknowledgments

- FastAPI for the amazing async framework
- Redis for high-performance caching
- React team for the UI framework

## 📞 Support

For support, email aakashraghav23@gmail.com or open an issue in the repository.

---

**Made with ❤️ by the Shoppers Team**
