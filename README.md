# ALX PROJECT NEXUS

# Poll System Backend API

A Django REST API for creating and managing online polls with real-time voting and results.

[![Django](https://img.shields.io/badge/Django-5.0.1-green.svg)](https://www.djangoproject.com/)
[![DRF](https://img.shields.io/badge/DRF-3.14.0-red.svg)](https://www.django-rest-framework.org/)
[![Python](https://img.shields.io/badge/Python-3.12-blue.svg)](https://www.python.org/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-15+-blue.svg)](https://www.postgresql.org/)
[![Deployed on Railway](https://img.shields.io/badge/Deployed%20on-Railway-blueviolet)](https://railway.app/)

---

## 🌐 Live Demo

**🔗 Production API:** https://web-production-c2365.up.railway.app

**📚 Interactive API Documentation:**
- **Swagger UI:** https://web-production-c2365.up.railway.app/api/docs/
- **ReDoc:** https://web-production-c2365.up.railway.app/api/redoc/

**✨ Try It Out:**
- Create polls, cast votes, and view real-time results
- Test all endpoints with interactive documentation
- Full JWT authentication flow
- Live database with PostgreSQL

---

## 🚀 Features

- **Poll Management**: Create, read, update, and delete polls with multiple options
- **Voting System**: Support for both authenticated and anonymous voting
- **Real-time Results**: Live vote counting with percentage calculations
- **Duplicate Prevention**: Database-level constraints prevent duplicate votes
- **JWT Authentication**: Secure token-based authentication
- **Privacy Protection**: Anonymous voter IP addresses are hashed
- **REST API**: Full CRUD operations with Django REST Framework
- **Interactive Docs**: Swagger UI and ReDoc API documentation
- **Query Optimization**: Efficient database queries with select_related and prefetch_related
- **Production Ready**: Deployed on Railway with PostgreSQL database

---

## 📋 Table of Contents

- [Live Demo](#-live-demo)
- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [Installation](#-installation)
- [Environment Variables](#-environment-variables)
- [Database Setup](#-database-setup)
- [Running the Application](#-running-the-application)
- [API Documentation](#-api-documentation)
- [API Endpoints](#-api-endpoints)
- [API Usage Examples](#-api-usage-examples)
- [Running Tests](#-running-tests)
- [Project Structure](#-project-structure)
- [Database Schema](#-database-schema)
- [Security Features](#-security-features)
- [Deployment](#-deployment)
- [Contributing](#-contributing)
- [License](#-license)
- [Author](#-author)

---

## 🛠 Tech Stack

- **Backend**: Django 5.0.1
- **API Framework**: Django REST Framework 3.14.0
- **Database**: PostgreSQL 15+
- **Authentication**: JWT (djangorestframework-simplejwt)
- **Documentation**: drf-spectacular
- **Language**: Python 3.12
- **Deployment**: Railway
- **Web Server**: Gunicorn

---

## 📦 Installation

### Prerequisites

- Python 3.12+
- PostgreSQL 15+
- pip
- virtualenv (recommended)

### Setup Steps

1. **Clone the repository**
```bash
git clone https://github.com/perodaah/ALX-project-nexus.git
cd ALX-project-nexus
```

2. **Create virtual environment**
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. **Install dependencies**
```bash
pip install -r requirements.txt
```

4. **Set up environment variables**
```bash
cp .env.example .env
# Edit .env with your configuration
```

---

## 🔐 Environment Variables

Create a `.env` file in the project root:

```env
# General settings
DEBUG=True
SECRET_KEY=your-secret-key-here

# Local PostgreSQL database (used when DEBUG=True)
DB_NAME=poll_system_db
DB_USER=poll_admin
DB_PASSWORD=your_secure_password
DB_HOST=localhost
DB_PORT=5432

# Production hosts (used when DEBUG=False)
ALLOWED_HOSTS=your-domain.com
CORS_ALLOWED_ORIGINS=https://your-domain.com
```

**Generate a secret key:**
```bash
python -c "from django.core.management.utils import get_random_secret_key; print(get_random_secret_key())"
```

---

## 🗄 Database Setup

1. **Create PostgreSQL database and user**
```sql
CREATE DATABASE poll_system_db;
CREATE USER poll_admin WITH PASSWORD 'your_secure_password';
ALTER DATABASE poll_system_db OWNER TO poll_admin;
GRANT ALL PRIVILEGES ON DATABASE poll_system_db TO poll_admin;
GRANT ALL ON SCHEMA public TO poll_admin;
```

2. **Run migrations**
```bash
python manage.py migrate
```

3. **Create superuser (optional)**
```bash
python manage.py createsuperuser
```

---

## 🚀 Running the Application

### Development Server
```bash
python manage.py runserver
```

The API will be available at: `http://localhost:8000/api/`

### Access Points

- **API Root**: http://localhost:8000/api/
- **Admin Panel**: http://localhost:8000/admin/
- **Swagger Docs**: http://localhost:8000/api/docs/
- **ReDoc**: http://localhost:8000/api/redoc/

---

## 📖 API Documentation

### Live Production Documentation
- **Swagger UI**: https://web-production-c2365.up.railway.app/api/docs/
- **ReDoc**: https://web-production-c2365.up.railway.app/api/redoc/

### Local Development Documentation
- **Swagger UI**: http://localhost:8000/api/docs/
- **ReDoc**: http://localhost:8000/api/redoc/

Interactive API documentation with:
- ✅ Try-it-out functionality for all endpoints
- ✅ Request/response examples
- ✅ Authentication flows
- ✅ Model schemas

---

## 🔌 API Endpoints

### Authentication

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| POST | `/api/auth/register/` | Register new user | No |
| POST | `/api/auth/login/` | Login and get JWT tokens | No |
| POST | `/api/auth/refresh/` | Refresh access token | No |
| GET | `/api/auth/profile/` | Get user profile | Yes |

### Polls

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| GET | `/api/polls/` | List all active polls | No |
| POST | `/api/polls/` | Create new poll | Yes |
| GET | `/api/polls/{id}/` | Get poll details | No |
| PUT/PATCH | `/api/polls/{id}/` | Update poll | Yes (Owner) |
| DELETE | `/api/polls/{id}/` | Delete poll | Yes (Owner) |

### Voting

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| POST | `/api/polls/{id}/vote/` | Cast a vote | No |
| GET | `/api/polls/{id}/results/` | Get poll results | No |

---

## 📝 API Usage Examples

### Register a User
```bash
curl -X POST https://web-production-c2365.up.railway.app/api/auth/register/ \
  -H "Content-Type: application/json" \
  -d '{
    "username": "johndoe",
    "email": "john@example.com",
    "password": "SecurePass123!",
    "password2": "SecurePass123!"
  }'
```

### Login
```bash
curl -X POST https://web-production-c2365.up.railway.app/api/auth/login/ \
  -H "Content-Type: application/json" \
  -d '{
    "username": "johndoe",
    "password": "SecurePass123!"
  }'
```

### Create a Poll
```bash
curl -X POST https://web-production-c2365.up.railway.app/api/polls/ \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
  -d '{
    "title": "Favorite Programming Language?",
    "description": "Vote for your favorite language",
    "options": [
      {"text": "Python", "order_index": 1},
      {"text": "JavaScript", "order_index": 2},
      {"text": "Go", "order_index": 3}
    ]
  }'
```

### Cast a Vote
```bash
curl -X POST https://web-production-c2365.up.railway.app/api/polls/1/vote/ \
  -H "Content-Type: application/json" \
  -d '{"option_id": 1}'
```

### Get Results
```bash
curl https://web-production-c2365.up.railway.app/api/polls/1/results/
```

---

## 🧪 Running Tests

### Run all tests
```bash
python manage.py test
```

### Run specific test file
```bash
python manage.py test polls.tests
```

### Run integration tests
```bash
python test_auth.py
python test_polls.py
python test_voting.py
```

### Test coverage
```bash
pip install coverage
coverage run --source='.' manage.py test
coverage report
```

---

## 📁 Project Structure

```
ALX-project-nexus/
├── manage.py                  # Django management script
├── Procfile                   # Railway deployment config
├── runtime.txt                # Python version specification
├── requirements.txt           # Project dependencies
├── .env                       # Environment variables (not in git)
├── .env.example              # Environment variables template
├── pollsystem/               # Django settings package
│   ├── __init__.py
│   ├── settings.py           # Project configuration
│   ├── urls.py               # Main URL routing
│   ├── wsgi.py               # WSGI entry point
│   └── asgi.py               # ASGI entry point
├── polls/                    # Polls application
│   ├── __init__.py
│   ├── models.py             # Database models (Poll, Option, Vote)
│   ├── serializers.py        # DRF serializers
│   ├── views.py              # API views and viewsets
│   ├── permissions.py        # Custom permissions
│   ├── urls.py               # App URL routing
│   ├── admin.py              # Django admin configuration
│   ├── apps.py               # App configuration
│   ├── tests.py              # Unit tests
│   └── migrations/           # Database migrations
├── test_auth.py              # Authentication integration tests
├── test_polls.py             # Poll API integration tests
├── test_voting.py            # Voting system integration tests
├── .gitignore               # Git ignore rules
└── README.md                # This file
```

---

## 🗃 Database Schema

### Models

- **User**: Django's built-in user model for authentication
- **Poll**: Poll questions with title, description, creator, and expiry
- **Option**: Poll answer choices with ordering
- **Vote**: Individual votes with duplicate prevention

### Relationships

```
User (1) ──── (Many) Poll
Poll (1) ──── (Many) Option
Poll (1) ──── (Many) Vote
Option (1) ──── (Many) Vote
```

### Key Features

- **Duplicate Prevention**: Unique constraint on `(poll, voter_identifier)`
- **Cascade Deletion**: Deleting a poll removes all options and votes
- **Indexed Fields**: Optimized queries on frequently accessed fields
- **Voter Privacy**: IP addresses hashed for anonymous users

---

## 🔒 Security Features

- ✅ JWT token-based authentication
- ✅ Password hashing with PBKDF2
- ✅ Database-level duplicate vote prevention
- ✅ IP address hashing for anonymous voters
- ✅ Owner-only permissions for poll updates/deletes
- ✅ CORS configuration for cross-origin requests
- ✅ SQL injection protection (Django ORM)
- ✅ CSRF protection
- ✅ Secure cookies in production

---

## 🚀 Deployment

### ✅ Currently Deployed On: Railway

**Live API:** https://web-production-c2365.up.railway.app

This project is successfully deployed and production-ready!

### Deployment Configuration

**Procfile:**
```
web: gunicorn pollsystem.wsgi --log-file -
```

**Predeploy Command (Railway Settings):**
```bash
python manage.py migrate --noinput
```

**Environment Variables (Railway):**
- `DEBUG=False`
- `SECRET_KEY=<production-secret>`
- `DATABASE_URL=<railway-postgres-url>`
- `ALLOWED_HOSTS=web-production-c2365.up.railway.app`
- `CORS_ALLOWED_ORIGINS=https://web-production-c2365.up.railway.app`

### Other Deployment Options

This project can also be deployed to:
- Render
- Heroku
- AWS (Elastic Beanstalk, ECS)
- Azure (App Service)
- GCP (Cloud Run, App Engine)
- DigitalOcean (App Platform)

---

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

### Code Style
- Follow PEP 8 for Python code
- Write meaningful commit messages
- Add tests for new features
- Update documentation as needed

---

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

---

## 👨‍💻 Author

**Perodaah**

- GitHub: [@perodaah](https://github.com/perodaah)
- Project: [ALX-project-nexus](https://github.com/perodaah/ALX-project-nexus)

---

## 🙏 Acknowledgments

- **Django Documentation** - Comprehensive framework documentation
- **Django REST Framework** - Powerful toolkit for building Web APIs
- **Railway** - Seamless deployment platform
- **ALX Africa - Project Nexus** - Learning opportunity and project foundation
- **drf-spectacular** - Beautiful API documentation

---

## 📊 Project Stats

- **Lines of Code**: ~2,500+
- **API Endpoints**: 10+
- **Database Tables**: 4 (User, Poll, Option, Vote)
- **Test Coverage**: Comprehensive integration tests
- **Documentation**: Full Swagger/ReDoc integration

---

## 🎯 Future Enhancements

- [ ] Real-time notifications with WebSockets
- [ ] Poll analytics dashboard
- [ ] Social media sharing integration
- [ ] Multi-language support
- [ ] Poll templates
- [ ] Advanced voting options (ranked choice, etc.)
- [ ] Export results to CSV/PDF

---

## 📞 Support

If you have any questions or run into issues:

1. Check the [API Documentation](https://web-production-c2365.up.railway.app/api/docs/)
2. Open an issue on GitHub
3. Review the integration tests for usage examples

---

**🔗 Live Demo:** https://web-production-c2365.up.railway.app/api/docs/
