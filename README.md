# Food Ordering System - Group 12

A comprehensive online food ordering system for restaurants with two separate frontend applications:

1. **Customer Frontend**: Web application for customers to browse menus, place orders, and track order status through QR code scanning or direct table access
2. **Staff Dashboard**: Management system for restaurant staff to handle orders, manage tables, configure menu items, and monitor restaurant operations

### Key Features
- **QR Code Integration**: Customers scan QR codes at tables to access ordering interface
- **Alternative Access**: Direct table access via `/admin/qr` route for easy testing without QR scanning
- **Real-time Updates**: Live order status updates using WebSocket connections
- **Order Management**: Complete order lifecycle from placement to completion
- **Menu Management**: Staff can add, edit, and manage menu items with image uploads
- **Table Management**: Track table availability and customer sessions

## Team Members

- Kankorn  Chirachaihirun 650610746
- Jiraphat Ponrat 650610752
- Nathapat Nerangsi 650610758

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
# IMPORTANT: Configure Google OAuth and Cloudinary credentials before starting the application
```

**Required Environment Variables:**
- `GOOGLE_CLIENT_ID` and `GOOGLE_CLIENT_SECRET` - For Google OAuth authentication
- `CLOUDINARY_CLOUD_NAME`, `CLOUDINARY_API_KEY`, `CLOUDINARY_API_SECRET` - For image upload functionality

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
  - Main customer interface for ordering food
  - QR code scanning interface
  - **Development Route**: `/admin/qr` - Direct access to table selection for testing without QR scanning
- **Staff Frontend**: http://localhost:[PORT_STAFF]
  - Staff dashboard for order management
  - Menu item configuration
  - Table management and QR code generation
- **Backend API**: http://localhost:3000
- **Database**: localhost:5432

### How to Use the System

#### For Customers:
1. **QR Code Method**: Scan the QR code at your table to start ordering
2. **Development Method**: Visit `http://localhost:[PORT_CUSTOMER]/admin/qr` and click on any table button to simulate table access
3. Browse the menu and add items to your cart
4. Place your order and track its status in real-time

#### For Restaurant Staff:
1. Login to the staff dashboard using the admin account
2. Manage incoming orders and update their status
3. Add new menu items with descriptions and images
4. Generate and print QR codes for tables
5. Monitor table occupancy and customer sessions

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

Use this admin account to:
- Access the staff frontend system
- Configure restaurant settings
- Add menu items through the settings page
- Manage tables and orders

### Seeded Data
- 10 tables (Table 1-10) with QR Code tokens
- Admin account for staff system access

### Development Useful Commands

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