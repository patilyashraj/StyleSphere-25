# StyleSphere Project Setup Guide

This is a full-stack e-commerce application with three separate applications:
- **Backend** - Express.js API server
- **Frontend** - React customer-facing application
- **Admin** - React admin panel

## Prerequisites

- **Node.js** (v14 or higher recommended)
- **npm** or **yarn** package manager
- **MongoDB** database (local or cloud instance like MongoDB Atlas)
- **Cloudinary** account (for image storage)
- **Stripe** account (for payment processing - optional)
- **Gmail** account (for email notifications - optional)

## Step 1: Install Dependencies

Install dependencies for all three applications:

```bash
# Install backend dependencies
cd backend
npm install

# Install frontend dependencies
cd ../frontend
npm install

# Install admin panel dependencies
cd ../admin
npm install
```

## Step 2: Environment Variables Setup

### Backend Environment Variables

Create a `.env` file in the `backend` directory with the following variables:

```env
# Server Configuration
PORT=4000

# MongoDB Database
MONGODB_URI=mongodb://localhost:27017
# OR for MongoDB Atlas:
# MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net

# JWT Secret (use a strong random string)
JWT_SECRET=your_super_secret_jwt_key_here

# Admin Credentials
ADMIN_EMAIL=admin@example.com
ADMIN_PASSWORD=your_admin_password

# Cloudinary Configuration
CLOUDINARY_NAME=your_cloudinary_cloud_name
CLOUDINARY_API_KEY=your_cloudinary_api_key
CLOUDINARY_SECRET_KEY=your_cloudinary_secret_key

# Stripe Payment Gateway
STRIPE_SECRET_KEY=sk_test_your_stripe_secret_key
```

### Frontend Environment Variables

Create a `.env` file in the `frontend` directory:

```env
VITE_BACKEND_URL=http://localhost:4000
```

### Admin Panel Environment Variables

Create a `.env` file in the `admin` directory:

```env
VITE_BACKEND_URL=http://localhost:4000
```

## Step 3: Start the Applications

You need to run all three applications simultaneously. Open **three separate terminal windows/tabs**.

### Terminal 1 - Backend Server

```bash
cd backend
npm start
# OR for development with auto-reload:
npm run server
```

The backend server will start on `http://localhost:4000`

### Terminal 2 - Frontend Application

```bash
cd frontend
npm run dev
```

The frontend will start on `http://localhost:5173` (or the next available port)

### Terminal 3 - Admin Panel

```bash
cd admin
npm run dev
```

The admin panel will start on `http://localhost:5174` (or the next available port)

## Step 4: Verify Installation

1. **Backend**: Visit `http://localhost:4000` - You should see "API Working"
2. **Frontend**: Visit `http://localhost:5173` - You should see the customer-facing e-commerce site
3. **Admin Panel**: Visit `http://localhost:5174` - You should see the admin login page

## Quick Start Script (Optional)

You can create a script to start all three applications at once. Create a `start-all.js` file in the root directory:

```javascript
const { spawn } = require('child_process');

const apps = [
  { name: 'Backend', command: 'npm', args: ['start'], cwd: './backend' },
  { name: 'Frontend', command: 'npm', args: ['run', 'dev'], cwd: './frontend' },
  { name: 'Admin', command: 'npm', args: ['run', 'dev'], cwd: './admin' }
];

apps.forEach(app => {
  const proc = spawn(app.command, app.args, {
    cwd: app.cwd,
    shell: true,
    stdio: 'inherit'
  });
  
  console.log(`Started ${app.name}`);
});
```

Then run: `node start-all.js`

## Troubleshooting

### MongoDB Connection Issues
- Ensure MongoDB is running locally, or
- Verify your MongoDB Atlas connection string is correct
- Check that your IP is whitelisted in MongoDB Atlas (if using cloud)

### Port Already in Use
- Change the PORT in backend `.env` file
- Vite will automatically use the next available port for frontend/admin

### Environment Variables Not Loading
- Ensure `.env` files are in the correct directories
- Restart the servers after creating/modifying `.env` files
- For Vite apps (frontend/admin), variables must start with `VITE_`

### CORS Errors
- Ensure backend CORS is configured (already set in `server.js`)
- Verify `VITE_BACKEND_URL` matches your backend URL

## Project Structure

```
StyleSphere-25/
├── backend/          # Express.js API server
│   ├── config/       # Database and service configurations
│   ├── controllers/  # Route controllers
│   ├── middleware/   # Auth and file upload middleware
│   ├── models/       # MongoDB models
│   ├── routes/       # API routes
│   └── server.js     # Entry point
├── frontend/         # Customer-facing React app
│   └── src/
│       ├── components/
│       ├── pages/
│       └── context/
├── admin/            # Admin panel React app
│   └── src/
│       ├── components/
│       └── pages/
└── SETUP.md          # This file
```

## Default Admin Login

Use the credentials you set in the backend `.env` file:
- Email: `ADMIN_EMAIL` value
- Password: `ADMIN_PASSWORD` value

## Next Steps

1. Set up your MongoDB database
2. Configure Cloudinary for image uploads
3. Set up Stripe for payment processing (optional)
4. Configure email settings in `orderController.js` (currently using Gmail)
5. Start adding products through the admin panel!

