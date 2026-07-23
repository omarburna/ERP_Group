# HR Job Application System

A comprehensive Human Resource Module System for managing job applications based on BPMN flowchart methodology.

## Features

This system implements the complete job application flowchart:
- **Post Job**: Admins can create and post new job openings
- **Receive Application**: Applicants can submit applications for available positions
- **Shortlist**: HR can review and shortlist candidates
- **Interview**: Schedule and conduct interviews with shortlisted candidates
- **Pass/Fail Decision**: Mark candidates as passed or failed after interviews
- **Prepare Offer**: Create and prepare job offers for successful candidates
- **Issue Offer**: Send offers to candidates
- **Onboard**: Complete the onboarding process for hired candidates

## Tech Stack

### Backend
- Node.js
- Express.js
- MongoDB (Mongoose)
- JWT Authentication
- CORS

### Frontend
- React
- React Router
- Axios
- Lucide React (Icons)

## Project Structure

```
erp project/
├── backend/
│   ├── models/
│   │   ├── Job.js          # Job posting model
│   │   ├── Application.js  # Application model with flowchart status
│   │   └── User.js         # Admin user model
│   ├── routes/
│   │   ├── jobs.js         # Job CRUD operations
│   │   ├── applications.js # Application management
│   │   └── auth.js         # Authentication endpoints
│   ├── .env                # Environment variables
│   ├── package.json
│   └── server.js           # Main server file
├── frontend/
│   ├── public/
│   │   └── index.html
│   ├── src/
│   │   ├── components/
│   │   │   └── Navbar.js
│   │   ├── pages/
│   │   │   ├── Home.js           # Landing page
│   │   │   ├── JobList.js        # View available jobs
│   │   │   ├── ApplyJob.js       # Submit application
│   │   │   ├── AdminDashboard.js # Full HR management dashboard
│   │   │   ├── PostJob.js        # Create new job posting
│   │   │   └── Login.js          # Admin authentication
│   │   ├── App.js
│   │   ├── index.js
│   │   └── index.css
│   └── package.json
├── package.json
└── README.md
```

## Installation & Setup

### Prerequisites
- Node.js (v14 or higher)
- MongoDB (installed and running)

### Step 1: Install Dependencies

```bash
# Install root dependencies
npm install

# Install backend dependencies
cd backend
npm install

# Install frontend dependencies
cd ../frontend
npm install
```

### Step 2: Configure Environment Variables

Edit `backend/.env` file:

```
PORT=5000
MONGODB_URI=mongodb://localhost:27017/hr-job-system
JWT_SECRET=your-secret-key-change-this
```

### Step 3: Start MongoDB

Make sure MongoDB is running on your system:
```bash
# On Windows
net start MongoDB

# On Mac/Linux
sudo systemctl start mongod
# or
mongod
```

### Step 4: Run the Application

#### Option A: Run both frontend and backend together
```bash
# From root directory
npm run dev
```

#### Option B: Run separately
```bash
# Terminal 1 - Backend
cd backend
npm run dev

# Terminal 2 - Frontend
cd frontend
npm start
```

The application will be available at:
- Frontend: http://localhost:3000
- Backend API: http://localhost:5000

## Default Admin Credentials

```
Username: admin
Password: admin123
```

To create a new admin user, you can use the registration endpoint or manually create one in MongoDB.

## Application Flow

### For Applicants
1. Visit the home page
2. Browse available jobs
3. Click "Apply Now" on a job
4. Fill out the application form
5. Submit application

### For HR/Admin
1. Login to the admin dashboard
2. View all applications
3. **Shortlist** promising candidates
4. **Schedule Interview** for shortlisted candidates
5. After interview, mark as **Pass** or **Reject**
6. For passed candidates, **Prepare Offer**
7. **Issue Offer** to candidate
8. Once accepted, **Onboard** the new hire

## API Endpoints

### Jobs
- `GET /api/jobs` - Get all active jobs
- `GET /api/jobs/:id` - Get single job
- `POST /api/jobs` - Create new job (Admin)
- `PUT /api/jobs/:id` - Update job (Admin)
- `DELETE /api/jobs/:id` - Delete job (Admin)

### Applications
- `GET /api/applications` - Get all applications
- `GET /api/applications/job/:jobId` - Get applications for specific job
- `GET /api/applications/:id` - Get single application
- `POST /api/applications` - Submit new application
- `PUT /api/applications/:id/status` - Update application status
- `DELETE /api/applications/:id` - Delete application

### Authentication
- `POST /api/auth/register` - Register new admin
- `POST /api/auth/login` - Login admin

## Application Status Flow

The application status follows this flowchart:

```
received → shortlisted → interview_scheduled → interview_passed → 
offer_prepared → offer_issued → onboarded

At any point, applications can be marked as 'rejected'
```

## Database Schema

### Job Model
- title: String
- description: String
- requirements: String
- location: String
- salary: String
- status: Enum ['active', 'closed']

### Application Model
- jobId: ObjectId (ref: Job)
- applicantName: String
- email: String
- phone: String
- resume: String
- coverLetter: String
- status: Enum (flowchart statuses)
- interviewDate: Date
- interviewNotes: String
- offerDetails: String
- onboardingDate: Date

### User Model
- username: String
- password: String (hashed)
- role: Enum ['admin', 'hr']

## Features Implemented

✅ Job posting and management
✅ Application submission
✅ Application shortlisting
✅ Interview scheduling
✅ Interview pass/fail decisions
✅ Offer preparation
✅ Offer issuance
✅ Onboarding process
✅ Status tracking throughout the flowchart
✅ Admin authentication
✅ Responsive design
✅ Modern UI with gradient backgrounds

## Troubleshooting

### MongoDB Connection Issues
- Ensure MongoDB is running
- Check the MONGODB_URI in .env file
- Verify MongoDB is accessible on the specified port

### Port Already in Use
- Change PORT in backend/.env
- Change frontend port in package.json (scripts.start)

### CORS Errors
- Ensure backend CORS is configured correctly
- Check that frontend is making requests to the correct backend URL

## License

This project is part of an ERP system assignment for educational purposes.
