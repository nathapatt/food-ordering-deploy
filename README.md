# Food Ordering System

A comprehensive online food ordering system for restaurants, featuring a customer web application for placing orders and a staff management system for handling orders, tables, and menu items.

## Team Members

- Member 1
- Member 2
- Member 3
- Member 4

## Technology Stack

### Frontend
- **Customer Frontend**: React 19, TypeScript, Vite, TailwindCSS, React Router DOM, React Query, Socket.io Client, QR Code Generator
- **Staff Frontend**: React 19, TypeScript, Vite, Ant Design, React Router DOM, Socket.io Client, Day.js

### Backend
- **API Server**: NestJS, TypeScript, Prisma ORM, PostgreSQL, JWT Authentication, Passport.js, Google OAuth, Socket.io, Cloudinary (image upload), bcryptjs

### Database
- **PostgreSQL 17** (Alpine Linux container)

### DevOps & Deployment
- **Docker & Docker Compose** for containerization
- **Nginx** for reverse proxy in frontend containers

## Development Setup

### Prerequisites
- Docker and Docker Compose
- Git

### Installation Steps

1. Clone the project
```bash
git clone <repository-url>
cd food-ordering-deploy
```

2. Setup environment variables
```bash
cp .env.example .env
# Edit the .env file according to your needs
```

3. Start the system
```bash
docker-compose up -d
```

4. Wait for containers to be ready
```bash
docker-compose ps
```

### System Access
- **Customer Frontend**: http://localhost:[PORT_CUSTOMER]
- **Staff Frontend**: http://localhost:[PORT_STAFF]
- **Backend API**: http://localhost:3000
- **Database**: localhost:5432

## Database Seeding

After the system is running, execute the following commands to create initial data:

```bash
# Enter the backend container
docker exec -it food_ordering_backend bash

# Run the seed command
npm run seed
```

### Admin Account
After running the seed, you will have an admin account for accessing the staff system:
- **Email**: admin@restaurant.com
- **Password**: admin123

### Seeded Data
- 10 tables (Table 1-10) with QR Code tokens
- Admin account for staff system access

## Development

### Project Structure
```
.
├── customer-ordering-frontend/     # Customer frontend application
├── admin-ordering-frontend/        # Staff frontend application
│   └── staff-fullstack-website/
├── customer-ordering-backend/      # Backend API
│   └── food_ordering_backend/
└── food-ordering-deploy/          # Docker deployment
    ├── docker-compose.yml
    └── README.md
```

### Useful Commands

```bash
# View service logs
docker-compose logs -f [service_name]

# Restart service
docker-compose restart [service_name]

# Enter container
docker exec -it [container_name] bash

# Stop system
docker-compose down

# Stop and remove volumes
docker-compose down -v
```