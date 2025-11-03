Jira-CloneA comprehensive, full-stack project management system inspired by Jira. This application is built with a Flask backend and a React frontend, designed to help teams manage projects, epics, stories, and tasks efficiently. It features a robust backend with role-based access control (RBAC), a multi-level approval workflow for new users, and a detailed project hierarchy.🚀 FeaturesThis project includes a wide range of features for effective team and project management:Authentication & Security:User registration and login system.Secure authentication using JSON Web Tokens (JWT).Password handling (storage is abstracted in models/login.py).Role-Based Access Control (RBAC):Pre-defined roles: Employee, Manager, and Super Admin.Protected routes and actions based on user roles.Employees can request a role "raise" to become a manager, which must be approved by a Super Admin.User Approval Workflow:Managers: Require approval from a Super Admin.Employees: Require a two-step approval: first by a Super Admin, then by their designated Team Manager.Users cannot log in until their account is fully approved.Project & Team Management:Projects: Create, view, and manage projects. Assign projects to one or more teams.Teams: Create teams and manage member assignments.Managers and Super Admins have permissions to create projects and teams.Agile Task Hierarchy:Epics: High-level features or large bodies of work. Epics contain stories.Stories: User stories or features that deliver value. Stories are part of an Epic and are broken down into tasks.Tasks: The smallest unit of work, such as bugs, improvements, or sub-tasks. Each task belongs to a story.Dashboards & Views:Main Dashboard: An overview of assigned projects and tasks.Kanban Board: A board to visualize task progress (To Do, In Progress, In Review, Done) for a specific project.Task Lists: View all tasks for a project or just tasks assigned to you.Epic & Story Views: View lists of all epics or stories within a project.Detail Pages: Drill down to see details for specific Epics, Stories, and Tasks.Task-Level Features:Comments: Add comments to tasks for collaboration.Time Logging: Log hours spent on specific tasks.Activity Log: View a feed of your recent activities, such as task creation or status changes.Administrative Dashboards:Admin Dashboard: For Super Admins to approve new users (Managers/Employees) and handle role raise requests.Manager Dashboard: For Managers to give the second-level approval for employees joining their teams.Super Admin Dashboard: A high-level view of all projects and teams in the system.🛠️ Tech StackBackend (Python)Framework: FlaskAuthentication: Flask-JWT-Extended for managing access tokens.Database (ORM): Flask-SQLAlchemyDatabase Migration: Flask-MigrateDatabase Driver: psycopg2 (for PostgreSQL)CORS: Flask-CorsFrontend (JavaScript)Framework: React.jsRouting: React RouterHTTP Client: AxiosStyling: Tailwind CSSUI Components: daisyUINotifications: React Hot ToastBundler: Vite⚙️ Setup & InstallationBackend (jira-backend-main)Clone the repository:git clone [https://github.com/nishannn07/jira-clone.git](https://github.com/nishannn07/jira-clone.git)
cd nishannn07/jira-clone/Jira-Clone-4709bebc2342891f45b85c7fd97a54310ea2d2e4/jira-backend-main
Create a virtual environment and activate it:python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
Install dependencies:pip install -r requirements.txt
Set up environment variables:Create a .env file in the jira-backend-main directory and add the following variables. See config.py and create_super_admin.py for reference.# URL for your PostgreSQL or SQLite database
DATABASE_URL="postgresql://user:password@localhost/jira_clone_db" 

# Strong, random secret keys
JWT_SECRET_KEY="your-jwt-secret-key"
SECRET_KEY="your-flask-secret-key"

# Credentials for the initial super admin account
USERNAME="superadmin"
EMAIL="admin@example.com"
PASSWORD="yourstrongpassword"
Initialize and migrate the database:flask db init  # Only if running for the first time
flask db migrate -m "Initial migration"
flask db upgrade
Seed the database with initial data:flask seed-roles             # Creates the basic user roles
flask create-super-admin     # Creates the first admin user from your .env variables
Run the backend server:flask run
The backend API will be running at http://127.0.0.1:5000.Frontend (jira-frontend-final-main)Navigate to the frontend directory:# From the root directory
cd nishannn07/jira-clone/Jira-Clone-4709bebc2342891f45b85c7fd97a54310ea2d2e4/jira-frontend-final-main
Install dependencies:(Using pnpm based on pnpm-lock.yaml, but npm or yarn will also work if you delete the lock file)pnpm install
# OR
npm install
Set up environment variables:Create a .env.local file in the jira-frontend-final-main directory:VITE_URL="[http://127.0.0.1:5000](http://127.0.0.1:5000)"
Run the frontend development server:pnpm run dev
# OR
npm run dev
The React application will be available at http://localhost:5173 (or another port if 5173 is busy).📁 Project StructureJira-Clone-4709bebc2342891f45b85c7fd97a54310ea2d2e4/
├── jira-backend-main/
│   ├── controllers/            # Business logic (e.g., user_controller.py, task_controller.py)
│   │   ├── activity_controller.py
│   │   ├── epic_controller.py
│   │   ├── project_controller.py
│   │   ├── story_controller.py
│   │   ├── task_controller.py
│   │   ├── team_controller.py
│   │   └── user_controller.py
│   ├── models/                 # SQLAlchemy database models (e.g., user.py, task.py, epic.py)
│   │   ├── __init__.py
│   │   ├── activity_log.py
│   │   ├── association.py
│   │   ├── comment.py
│   │   ├── epic.py
│   │   ├── project.py
│   │   ├── story.py
│   │   ├── task.py
│   │   ├── team.py
│   │   └── user.py
│   ├── routes/                 # API endpoint definitions (e.g., user_routes.py, task_routes.py)
│   │   ├── __init__.py
│   │   ├── epic_routes.py
│   │   ├── project_routes.py
│   │   ├── story_routes.py
│   │   ├── task_routes.py
│   │   ├── team_routes.py
│   │   └── user_routes.py
│   ├── seed/                   # Database seeding scripts
│   │   ├── create_super_admin.py
│   │   └── role_seeder.py
│   ├── app.py                  # Main Flask application entry point
│   ├── config.py               # Configuration settings (keys, DB URI)
│   ├── rba_decoder.py          # Role-Based Access Control decorator
│   └── requirements.txt        # Python dependencies
│
├── jira-frontend-final-main/
│   ├── public/                 # Static assets
│   ├── src/
│   │   ├── Auth/               # Authentication components (Login.jsx, Signup.jsx)
│   │   ├── assets/             # Images and SVGs
│   │   ├── AdminDashboard.jsx
│   │   ├── App.jsx             # Main component with React Router routes
│   │   ├── Dashboard.jsx
│   │   ├── EpicDetails.jsx
│   │   ├── EpicForm.jsx
│   │   ├── EpicList.jsx
│   │   ├── KanbanBoard.jsx
│   │   ├── ManagerDashboard.jsx
│   │   ├── Navbar.jsx
│   │   ├── ProjectForm.jsx
│   │   ├── Sidebar.jsx
│   │   ├── StoryDetails.jsx
│   │   ├── StoryForm.jsx
│   │   ├── StoryList.jsx
│   │   ├── SuperAdminDashboard.jsx
│   │   ├── TaskComment.jsx
│   │   ├── TaskDetails.jsx
│   │   ├── TaskForm.jsx
│   │   ├── TaskList.jsx
│   │   ├── TaskLogTime.jsx
│   │   ├── TeamForm.jsx
│   │   └── main.jsx            # React app entry point
│   ├── index.html              # Main HTML file
│   ├── package.json            # Frontend dependencies
│   ├── pnpm-lock.yaml          # PNPM lock file
│   ├── tailwind.config.js      # Tailwind CSS configuration
│   └── vite.config.js          # Vite configuration
│
└── README.md                   # This file
