# 🚀 Scalable API Project

A production-ready API built with Node.js and Express, designed for scalability, security, and modern DevOps workflows.

## ⚙️ Tech Stack
- Backend: Node.js, Express.js  
- Database: Neon Postgres + Drizzle ORM  
- Validation: Zod  
- Security: Arcjet  
- DevOps: Docker, CI/CD (GitHub Actions)  
- Tooling: ESLint, Prettier, Jest  

## 🔋 Features
- RESTful API with full CRUD functionality  
- JWT authentication & role-based access  
- Request validation with Zod  
- PostgreSQL integration with migrations  
- Dockerized (dev & prod environments)  
- Automated CI/CD pipeline  
- Testing with Jest & Supertest  
- Structured logging & health checks  

## 🤸 Quick Start
```bash
git clone https://github.com/Stamkopoulos/acquisitions
cd acquisitions
npm install
```

Create a `.env` file:
```env
# Server Configuration
PORT=3000
NODE_ENV=development
LOG_LEVEL=info

# Database Configuration
DATABASE_URL=

# Arcjet
ARCJET_KEY=
```

Run locally:
```bash
npm run dev
```

API runs at: http://localhost:3000

## 📦 Notes
This project demonstrates how to take an API from development to production using modern tools like Docker and CI/CD pipelines.
