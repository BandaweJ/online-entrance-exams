# School Entrance Exam System

A comprehensive full-stack web application for managing school entrance examinations with AI-powered auto-marking, real-time exam taking, and comprehensive result management.

## 🚀 Features

### Admin Features
- **Exam Management**: Create, edit, publish, and manage exams with multiple sections
- **Question Management**: Add various question types (multiple choice, true/false, short answer, essay)
- **Student Management**: Register students and automatically generate login credentials
- **Result Management**: View and analyze exam results with detailed statistics
- **Real-time Monitoring**: Monitor ongoing exams and student progress

### Student Features
- **Exam Taking**: Take exams with real-time countdown timer
- **Question Navigation**: Navigate between questions, pause/resume exams
- **Answer Management**: Save and review answers before submission
- **Result Viewing**: View published results with detailed feedback

### System Features
- **AI Auto-Marking**: Integration with external AI services for automated grading
- **Email/SMS Notifications**: Send credentials and exam reminders
- **Real-time Timer**: Countdown timer with pause/resume functionality
- **Responsive Design**: Mobile-friendly interface using Angular Material
- **Role-based Access**: Separate interfaces for admins and students

## 🛠️ Tech Stack

### Backend
- **NestJS** - Node.js framework
- **TypeORM** - Object-Relational Mapping
- **PostgreSQL** - Database
- **JWT** - Authentication
- **bcrypt** - Password hashing
- **Nodemailer** - Email service
- **Twilio** - SMS service

### Frontend
- **Angular 20** - Frontend framework
- **Angular Material** - UI components
- **NgRx** - State management
- **RxJS** - Reactive programming
- **TypeScript** - Type safety

### DevOps
- **Docker** - Containerization
- **Docker Compose** - Multi-container orchestration
- **GitHub Actions** - CI/CD pipeline
- **Nginx** - Web server

## 📋 Prerequisites

- Node.js 18+
- PostgreSQL 15+
- Docker & Docker Compose (optional)
- npm or yarn

## 🚀 Quick Start

### Using Docker Compose (Recommended)

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd online-entrance-exams
   ```

2. **Set up environment variables**
   ```bash
   # The .env file is already present in the project root
   # Edit .env with your configuration
   nano .env
   ```

3. **Start the application**
   ```bash
   docker-compose up -d
   ```

4. **Access the application**
   - Frontend: http://localhost
   - Backend API: http://localhost:3000
   - Database: localhost:5432

### Manual Setup

#### Backend Setup

1. **Navigate to backend directory**
   ```bash
   cd backend
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Set up environment variables**
   ```bash
   # The .env file is already present in the project root
   # Edit .env with your database and other configurations
   nano .env
   ```

4. **Set up database**
   ```bash
   # Create PostgreSQL database
   createdb entrance_exam_db
   
   # Run migrations (if any)
   npm run migration:run
   ```

5. **Seed admin user**
   ```bash
   npm run seed
   ```

6. **Start the backend**
   ```bash
   # Option 1: Use the startup script (recommended)
   ./start-backend.sh
   
   # Option 2: Run directly
   npm run start:dev
   ```

#### Frontend Setup

1. **Navigate to frontend directory**
   ```bash
   cd frontend
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Start the frontend**
   ```bash
   # Option 1: Use the startup script (recommended)
   ./start-frontend.sh
   
   # Option 2: Run directly
   npm start
   ```

4. **Access the application**
   - Frontend: http://localhost:4200
   - Backend API: http://localhost:3000

## 🔧 Configuration

### Environment Variables

Create a `.env` file in the root directory with the following variables:

```env
# Database Configuration
DB_HOST=localhost
DB_PORT=5432
DB_USERNAME=postgres
DB_PASSWORD=password
DB_NAME=entrance_exam_db

# JWT Configuration
JWT_SECRET=your-super-secret-jwt-key-here
JWT_EXPIRES_IN=24h

# Email Configuration (Gmail SMTP)
EMAIL_HOST=smtp.gmail.com
EMAIL_PORT=587
EMAIL_USER=your-email@gmail.com
EMAIL_PASSWORD=your-app-password

# SMS Configuration (Twilio)
TWILIO_ACCOUNT_SID=your-twilio-account-sid
TWILIO_AUTH_TOKEN=your-twilio-auth-token
TWILIO_FROM_NUMBER=+1234567890

# AI Grader Configuration
AI_GRADER_API_URL=https://api.example.com/grade
AI_GRADER_API_KEY=your-ai-grader-api-key

# Application Configuration
PORT=3000
NODE_ENV=development
FRONTEND_URL=http://localhost:4200
```

## 📚 API Documentation

### Authentication Endpoints
- `POST /api/auth/login` - User login
- `POST /api/auth/register` - User registration
- `GET /api/auth/profile` - Get user profile
- `POST /api/auth/change-password` - Change password

### Exam Management
- `GET /api/exams` - Get all exams
- `POST /api/exams` - Create exam
- `GET /api/exams/:id` - Get specific exam
- `PATCH /api/exams/:id` - Update exam
- `DELETE /api/exams/:id` - Delete exam

### Student Management
- `GET /api/students` - Get all students
- `POST /api/students` - Create student
- `PATCH /api/students/:id` - Update student
- `DELETE /api/students/:id` - Delete student

### Exam Taking
- `POST /api/attempts` - Start exam attempt
- `PATCH /api/attempts/:id/pause` - Pause attempt
- `PATCH /api/attempts/:id/resume` - Resume attempt
- `PATCH /api/attempts/:id/submit` - Submit attempt

### Answer Management
- `POST /api/answers` - Submit answer
- `GET /api/answers/attempt/:id` - Get answers for attempt
- `PATCH /api/answers/:id` - Update answer

For detailed API examples, see [docs/api-examples.http](docs/api-examples.http)

## 🗄️ Database Schema

The application uses PostgreSQL with the following main entities:
- **Users** - Authentication and user management
- **Students** - Student information and credentials
- **Exams** - Exam definitions and metadata
- **Sections** - Exam sections and organization
- **Questions** - Individual questions with various types
- **Exam Attempts** - Student exam sessions
- **Answers** - Student responses to questions
- **Results** - Calculated scores and grades

For the complete database schema, see [docs/sql-schema.sql](docs/sql-schema.sql)

## 🧪 Testing

### Backend Tests
```bash
cd backend
npm run test
npm run test:e2e
```

### Frontend Tests
```bash
cd frontend
npm run test
```

### Run All Tests
```bash
# From root directory
npm run test
```

## 🚀 Deployment

### Using Docker Compose

1. **Production deployment**
   ```bash
   docker-compose -f docker-compose.prod.yml up -d
   ```

2. **Scale services**
   ```bash
   docker-compose up -d --scale backend=3
   ```

### Manual Deployment

1. **Build frontend**
   ```bash
   cd frontend
   npm run build
   ```

2. **Build backend**
   ```bash
   cd backend
   npm run build
   ```

3. **Deploy to server**
   - Upload built files to server
   - Set up reverse proxy (Nginx)
   - Configure environment variables
   - Start services

## 🔒 Security Features

- JWT-based authentication
- Password hashing with bcrypt
- Role-based access control
- Input validation and sanitization
- CORS configuration
- Security headers
- SQL injection prevention

## 📱 Mobile Support

The application is fully responsive and works on:
- Desktop browsers
- Tablet devices
- Mobile phones
- Progressive Web App (PWA) capabilities

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🆘 Support

For support and questions:
- Create an issue in the GitHub repository
- Check the documentation in the `docs/` folder
- Review the API examples in `docs/api-examples.http`

## 🗺️ Roadmap

- [ ] Advanced analytics and reporting
- [ ] Multi-language support
- [ ] Offline exam taking capability
- [ ] Advanced AI grading features
- [ ] Mobile app development
- [ ] Integration with learning management systems
- [ ] Advanced proctoring features

## 🙏 Acknowledgments

- Angular team for the excellent framework
- NestJS team for the robust backend framework
- Material Design team for the beautiful UI components
- PostgreSQL team for the reliable database
- All open-source contributors
