# Samadhan Portal

A comprehensive backend solution for managing grievance redressal and complaint resolution systems. Built with modern web technologies to ensure secure, scalable, and efficient handling of user complaints and their resolution.

---

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Technology Stack](#technology-stack)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [API Endpoints](#api-endpoints)
- [Database Schema](#database-schema)
- [Security](#security)
- [Contributing](#contributing)
- [License](#license)
- [Author](#author)

---

##  Overview

**Samadhan Portal** is a robust backend application designed to streamline complaint and grievance management. It provides a centralized platform for users to lodge complaints, track their status, and receive timely resolutions. The system ensures data security through encryption, secure authentication, and comprehensive session management.

### Key Objectives:
- Efficient complaint registration and tracking
- Automated email notifications for complaint updates
- Secure user authentication and session management
- Role-based access control
- Real-time complaint status updates

---

##  Features

- **User Authentication**: Secure login/signup with bcrypt password hashing
- **Complaint Management**: Create, update, and track complaint status
- **Email Notifications**: Automated email alerts using Nodemailer
- **Session Management**: Express session with MongoDB store for persistent sessions
- **File Upload**: Support for document attachments using Multer
- **CORS Support**: Cross-origin resource sharing for frontend integration
- **MongoDB Integration**: Scalable NoSQL database for data persistence
- **Error Handling**: Comprehensive error handling and validation
- **Environment Configuration**: Secure configuration using environment variables

---

##  Technology Stack

| Technology | Version | Purpose |
|-----------|---------|---------|
| **Node.js** | Latest LTS | JavaScript runtime |
| **Express.js** | ^5.1.0 | Web framework |
| **MongoDB** | Latest | NoSQL database |
| **Mongoose** | ^8.17.1 | ODM for MongoDB |
| **Bcrypt** | ^6.0.0 | Password hashing |
| **Nodemailer** | ^7.0.5 | Email service |
| **Multer** | ^2.0.2 | File upload handling |
| **CORS** | ^2.8.5 | Cross-origin requests |
| **Express Session** | ^1.18.2 | Session management |
| **Connect Mongo** | ^5.1.0 | MongoDB session store |
| **Dotenv** | ^17.2.1 | Environment variables |

---

##  Prerequisites

Before setting up the project, ensure you have:

- **Node.js** (v14 or higher) - [Download](https://nodejs.org/)
- **npm** (v6 or higher) - Comes with Node.js
- **MongoDB** (v4.4 or higher) - [Download](https://www.mongodb.com/try/download/community)
- **Git** - [Download](https://git-scm.com/)

---

##  Installation

### 1. Clone the Repository

```bash
git clone https://github.com/Mujeem8410/Samadhan-Portal.git
cd Samadhan-Portal
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Set Up Environment Variables

Create a `.env` file in the root directory and add the following variables:

```env
# Server Configuration
PORT=5000
NODE_ENV=development

# Database Configuration
MONGODB_URI=mongodb://localhost:27017/samadhan-portal

# Session Configuration
SESSION_SECRET=your_session_secret_key_here

# Email Configuration (Nodemailer)
EMAIL_SERVICE=gmail
EMAIL_USER=your_email@gmail.com
EMAIL_PASSWORD=your_app_password

# JWT Configuration (Optional)
JWT_SECRET=your_jwt_secret_key_here

# Frontend URL (CORS)
FRONTEND_URL=http://localhost:3000
```

### 4. Ensure MongoDB is Running

```bash
# On Windows
mongod

# On macOS (Homebrew)
brew services start mongodb-community

# On Linux
sudo systemctl start mongod
```

---

##  Configuration

### Environment Variables

| Variable | Description | Example |
|----------|-------------|---------|
| `PORT` | Server port | `5000` |
| `NODE_ENV` | Environment type | `development` or `production` |
| `MONGODB_URI` | MongoDB connection string | `mongodb://localhost:27017/db` |
| `SESSION_SECRET` | Secret for session encryption | Random string |
| `EMAIL_SERVICE` | Email service provider | `gmail`, `outlook`, etc. |
| `EMAIL_USER` | Email account username | `your_email@gmail.com` |
| `EMAIL_PASSWORD` | Email account password or app password | Your password |
| `FRONTEND_URL` | Frontend application URL | `http://localhost:3000` |

---

##  Usage

### Starting the Server

**Development Mode** (with hot reload):
```bash
npm run dev
```

**Production Mode**:
```bash
npm start
```

The server will start on the configured `PORT` (default: 5000).

### Example Request

```bash
# Health Check
curl http://localhost:5000/

# User Registration
curl -X POST http://localhost:5000/api/auth/register \
  -H "Content-Type: application/json" \
  -d '{
    "name": "John Doe",
    "email": "john@example.com",
    "password": "securePassword123"
  }'
```

---

##  Project Structure

```
Samadhan-Portal/
├── config/                 # Configuration files
│   └── database.js        # MongoDB connection
├── models/                # Mongoose schemas
│   ├── User.js
│   └── Complaint.js
├── routes/                # API routes
│   ├── auth.js
│   └── complaints.js
├── controllers/           # Business logic
│   ├── authController.js
│   └── complaintController.js
├── middleware/            # Custom middleware
│   ├── auth.js
│   └── errorHandler.js
├── uploads/               # File upload directory
├── server.js              # Main entry point
├── .env                   # Environment variables
├── .gitignore             # Git ignore rules
├── package.json           # Project dependencies
└── README.md              # This file
```

---

##  API Endpoints

### Authentication
```
POST   /api/auth/register      - User registration
POST   /api/auth/login         - User login
POST   /api/auth/logout        - User logout
GET    /api/auth/profile       - Get user profile
```

### Complaints
```
POST   /api/complaints         - Create new complaint
GET    /api/complaints         - Get all complaints (for user)
GET    /api/complaints/:id     - Get complaint details
PUT    /api/complaints/:id     - Update complaint
DELETE /api/complaints/:id     - Delete complaint
```

---

## 🗄️ Database Schema

### User Model
```javascript
{
  name: String,
  email: String (unique),
  password: String (hashed),
  phone: String,
  role: String (enum: ['user', 'admin']),
  createdAt: Date,
  updatedAt: Date
}
```

### Complaint Model
```javascript
{
  userId: ObjectId (ref: User),
  title: String,
  description: String,
  category: String,
  status: String (enum: ['pending', 'in-progress', 'resolved', 'rejected']),
  priority: String (enum: ['low', 'medium', 'high']),
  attachments: [String],
  createdAt: Date,
  updatedAt: Date
}
```

---

## 🔒 Security

The application implements multiple security measures:

1. **Password Encryption**: Bcrypt hashing (rounds: 10+)
2. **Session Management**: Secure session storage with MongoDB
3. **CORS Protection**: Configurable cross-origin policies
4. **Environment Variables**: Sensitive data in `.env` file
5. **Input Validation**: Server-side request validation
6. **Error Handling**: Generic error responses to prevent information leakage

### Best Practices:
- Never commit `.env` file to version control
- Use strong session secrets
- Keep dependencies updated
- Regularly review and audit code
- Use HTTPS in production

---

##  Contributing

We welcome contributions! Please follow these guidelines:

1. **Fork** the repository
2. **Create** a feature branch (`git checkout -b feature/amazing-feature`)
3. **Commit** your changes (`git commit -m 'Add amazing feature'`)
4. **Push** to the branch (`git push origin feature/amazing-feature`)
5. **Open** a Pull Request

### Code Standards:
- Follow ESLint conventions
- Add comments for complex logic
- Write meaningful commit messages
- Test your changes before submitting

---

##  License

This project is licensed under the **ISC License**. See the [LICENSE](LICENSE) file for details.

---

## 👤 Author

**Mujeem**

- GitHub: [@Mujeem8410](https://github.com/Mujeem8410)
- Repository: [Samadhan-Portal](https://github.com/Mujeem8410/Samadhan-Portal)

---

##  Support

For issues, bugs, or feature requests, please:
- Open an [Issue](https://github.com/Mujeem8410/Samadhan-Portal/issues)
- Check existing documentation
- Contact the maintainer

---

## 🔄 Version History

| Version | Date | Changes |
|---------|------|---------|
| 1.0.0 | 2025-08-15 | Initial release |

---

##  Additional Resources

- [Express.js Documentation](https://expressjs.com/)
- [MongoDB Documentation](https://docs.mongodb.com/)
- [Mongoose Documentation](https://mongoosejs.com/)
- [Nodemailer Documentation](https://nodemailer.com/)

---

**Last Updated**: June 2026  
**Status**: Active Development
