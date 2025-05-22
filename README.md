# TaskMaster 📋

A comprehensive full-stack project management system designed for educational institutions to manage student projects and tasks efficiently.

![TaskMaster Banner](https://github.com/TaskMaster78/TaskMaster-Report/blob/main/Dashboard.png?raw=true)

## 🌟 Features

### For Administrators
- **Project Management**: Create and oversee multiple academic projects
- **Student Assignment**: Assign students to specific projects and tasks
- **Task Monitoring**: Track task progress and completion status
- **Dashboard Analytics**: View comprehensive statistics and project metrics
- **Real-time Communication**: Direct messaging with students

### For Students
- **Project Access**: View assigned projects and their details
- **Task Management**: Update task status and view assignments
- **Profile Management**: Maintain personal academic profile
- **Messaging System**: Communicate with administrators and peers
- **Progress Tracking**: Monitor personal task completion rates

### System Features
- **Role-based Access Control**: Secure admin and student interfaces
- **Real-time Updates**: WebSocket-powered live notifications
- **Responsive Design**: Mobile-first UI with modern components
- **Secure Authentication**: JWT-based authentication system
- **GraphQL API**: Efficient data fetching and manipulation

## 🚀 Tech Stack

### Backend
- **Node.js** - Runtime environment
- **Express.js** - Web application framework
- **GraphQL** - API query language and runtime
- **MongoDB** - NoSQL database with Mongoose ODM
- **Socket.IO** - Real-time communication
- **JWT** - JSON Web Token authentication
- **bcrypt** - Password hashing
- **TypeScript** - Static type checking

### Frontend
- **React 18** - Component-based UI library
- **TypeScript** - Type-safe development
- **TailwindCSS** - Utility-first CSS framework
- **shadcn/ui** - Modern component library
- **Apollo Client** - GraphQL client for React
- **Socket.IO Client** - Real-time communication
- **React Router** - Client-side routing
- **React Hook Form** - Form management

## 📁 Project Structure

```
taskmaster/
├── backend/                    # Node.js + GraphQL backend
│   ├── src/
│   │   ├── models/            # MongoDB models
│   │   │   ├── User.ts
│   │   │   ├── Project.ts
│   │   │   └── Task.ts
│   │   ├── schema/            # GraphQL schema
│   │   │   ├── schema.ts
│   │   │   └── resolvers.ts
│   │   ├── types/             # TypeScript definitions
│   │   └── index.ts           # Server entry point
│   ├── package.json
│   └── tsconfig.json
├── frontend/                   # React + TailwindCSS frontend
│   ├── src/
│   │   ├── components/        # Reusable UI components
│   │   ├── pages/            # Route components
│   │   ├── hooks/            # Custom React hooks
│   │   ├── graphql/          # GraphQL queries & mutations
│   │   ├── types/            # TypeScript interfaces
│   │   └── App.tsx           # Main application component
│   ├── package.json
│   └── tailwind.config.js
└── README.md
```

## 🛠️ Installation & Setup

### Prerequisites
- Node.js (v16 or higher)
- MongoDB Atlas account or local MongoDB installation
- Git

### 1. Clone the Repository
```bash
git clone https://github.com/yourusername/taskmaster.git
cd taskmaster
```

### 2. Frontend/Backend Setup

```bash
# Install dependencies
npm install

# Create environment file
cp .env.example .env
```

**Configure your `.env` file:**
```env
MONGO_URI=your_mongodb_connection_string
JWT_SECRET=your_super_secret_jwt_key
PUBLIC_URL=http://localhost:3000
```

```bash
# Start development server
npm run dev
```

The backend will be running at `http://localhost:4000/graphql`

### 3. Frontend Setup

```bash
# Navigate to frontend directory (from root)
cd frontend

# Install dependencies
npm install

# Create environment file
cp .env.example .env.local
```

**Configure your `.env.local` file:**
```env
NEXT_PUBLIC_URL=http://localhost:4000
```

```bash
# Start development server
npm start
```

The frontend will be running at `http://localhost:3000`

## 📚 API Documentation

### GraphQL Endpoint
Access the GraphQL playground at `http://localhost:4000/graphql`

### Authentication
All protected routes require a JWT token in the Authorization header:
```
Authorization: Bearer <your_jwt_token>
```

### Sample Queries

#### Authentication
```graphql
# Login
mutation {
  login(username: "admin", password: "password") {
    token
    role
  }
}

# Register new user
mutation {
  signup(
    username: "student1"
    password: "securepass"
    name: "John Doe"
    universityId: "ST001"
    role: student
  ) {
    id
    username
    role
  }
}
```

#### Projects
```graphql
# Get all projects (Admin only)
query {
  allProjects {
    id
    title
    description
    status
    selectedStudents
  }
}

# Get my projects (Student)
query {
  myProjects {
    id
    title
    description
    status
  }
}

# Create project (Admin only)
mutation {
  createProject(
    title: "Web Development Project"
    description: "Build a full-stack application"
    category: "Computer Science"
    selectedStudents: ["student_id_1", "student_id_2"]
  ) {
    id
    title
  }
}
```

#### Tasks
```graphql
# Get user tasks
query {
  tasks {
    id
    taskName
    description
    status
    dueDate
    projectTitle
  }
}

# Create task
mutation {
  createTask(
    projectId: "project_id"
    projectTitle: "Web Development Project"
    taskName: "Setup React App"
    description: "Initialize React application with TypeScript"
    assignedStudent: "student_id"
    dueDate: "2024-12-31"
  ) {
    id
    taskName
    status
  }
}

# Update task
mutation {
  updateTask(
    id: "task_id"
    status: "Completed"
  ) {
    id
    status
    updatedAt
  }
}
```

## 🔐 Authentication & Authorization

### User Roles
- **Admin**: Full system access, project creation, user management
- **Student**: Limited access to assigned projects and personal tasks

### Protected Routes
- All GraphQL mutations require authentication
- Role-based query filtering for sensitive data
- JWT token validation on each request

## 🌐 WebSocket Events

### Client Events
```javascript
// Join user room
socket.emit('join', { userId: 'user_id' });

// Send message
socket.emit('sendMessage', {
  recipientId: 'recipient_id',
  message: 'Hello!',
  senderId: 'sender_id'
});
```

### Server Events
```javascript
// Receive message
socket.on('receiveMessage', (message) => {
  console.log('New message:', message);
});
```

## 🚀 Deployment

### Backend Deployment (Heroku/Railway/DigitalOcean)

1. **Set environment variables** in your hosting platform
2. **Build the application:**
   ```bash
   npm run build
   ```
3. **Start the production server:**
   ```bash
   npm start
   ```

### Frontend Deployment (Vercel/Netlify)

1. **Build the application:**
   ```bash
   npm run build
   ```
2. **Deploy the `build` folder** to your hosting service
3. **Configure environment variables** for production API endpoints

### Database Setup
- Create a MongoDB Atlas cluster
- Configure network access and database users
- Update connection strings in environment variables

## 📊 Project Status

### Current Features ✅
- [x] User authentication and authorization
- [x] Project management system
- [x] Task assignment and tracking
- [x] Real-time messaging
- [x] Role-based access control
- [x] Responsive web interface
- [x] GraphQL API
- [x] WebSocket integration

### Upcoming Features 🚧
- [ ] File upload for project resources
- [ ] Advanced notification system
- [ ] Project templates
- [ ] Mobile application
- [ ] Analytics dashboard
- [ ] Email notifications
- [ ] Bulk operations
- [ ] Advanced search and filtering

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Development Guidelines
- Follow TypeScript best practices
- Write meaningful commit messages
- Add tests for new features
- Update documentation as needed
- Follow the existing code style

## 🐛 Bug Reports

Please use the [GitHub Issues](https://github.com/yourusername/taskmaster/issues) page to report bugs or request features.

**Bug Report Template:**
- Environment (OS, Node version, Browser)
- Steps to reproduce
- Expected behavior
- Actual behavior
- Screenshots (if applicable)

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👥 Team

- [Hadi Irshaid](https://github.com/Hadi87s)
- [Zahi Abu Shalbak](https://github.com/Zahi-abushalbak)
- [Zahi Qudu](https://github.com/ZahiQudu)
- [Hamza Kobari](https://github.com/HamzaK90)

## 🙏 Acknowledgments

- [React](https://reactjs.org/) - UI library
- [GraphQL](https://graphql.org/) - Query language
- [MongoDB](https://www.mongodb.com/) - Database
- [TailwindCSS](https://tailwindcss.com/) - CSS framework
- [shadcn/ui](https://ui.shadcn.com/) - Component library
- [Socket.IO](https://socket.io/) - Real-time communication
