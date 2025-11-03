# Jira-Clone

A comprehensive, full-stack project management system inspired by Jira. This application is built with a Flask backend and a React frontend, designed to help teams manage projects, epics, stories, and tasks efficiently. It features a robust backend with role-based access control (RBAC), a multi-level approval workflow for new users, and a detailed project hierarchy.

---

## 🚀 Features

This project includes a wide range of features for effective team and project management:

* **Authentication & Security:**
    * User registration and login system.
    * Secure authentication using **JSON Web Tokens (JWT)**.
    * Password handling (storage is abstracted in `models/login.py`).

* **Role-Based Access Control (RBAC):**
    * Pre-defined roles: **Employee**, **Manager**, and **Super Admin**.
    * Protected routes and actions based on user roles.
    * Employees can request a role "raise" to become a manager, which must be approved by a Super Admin.

* **User Approval Workflow:**
    * **Managers:** Require approval from a **Super Admin**.
    * **Employees:** Require a two-step approval: first by a **Super Admin**, then by their designated **Team Manager**.
    * Users cannot log in until their account is fully approved.

* **Project & Team Management:**
    * **Projects:** Create, view, and manage projects. Assign projects to one or more teams.
    * **Teams:** Create teams and manage member assignments.
    * Managers and Super Admins have permissions to create projects and teams.

* **Agile Task Hierarchy:**
    * **Epics:** High-level features or large bodies of work. Epics contain stories.
    * **Stories:** User stories or features that deliver value. Stories are part of an Epic and are broken down into tasks.
    * **Tasks:** The smallest unit of work, such as bugs, improvements, or sub-tasks. Each task belongs to a story.

* **Dashboards & Views:**
    * **Main Dashboard:** An overview of assigned projects and tasks.
    * **Kanban Board:** A board to visualize task progress (`To Do`, `In Progress`, `In Review`, `Done`) for a specific project.
    * **Task Lists:** View all tasks for a project or just tasks assigned to you.
    * **Epic & Story Views:** View lists of all epics or stories within a project.
    * **Detail Pages:** Drill down to see details for specific Epics, Stories, and Tasks.

* **Task-Level Features:**
    * **Comments:** Add comments to tasks for collaboration.
    * **Time Logging:** Log hours spent on specific tasks.
    * **Activity Log:** View a feed of your recent activities, such as task creation or status changes.

* **Administrative Dashboards:**
    * **Admin Dashboard:** For Super Admins to approve new users (Managers/Employees) and handle role raise requests.
    * **Manager Dashboard:** For Managers to give the second-level approval for employees joining their teams.
    * **Super Admin Dashboard:** A high-level view of *all* projects and teams in the system.

---

## 🛠️ Tech Stack

### Backend (Python)

* **Framework:** **Flask**
* **Authentication:** **Flask-JWT-Extended** for managing access tokens.
* **Database (ORM):** **Flask-SQLAlchemy**
* **Database Migration:** **Flask-Migrate**
* **Database Driver:** **psycopg2-binary** (for PostgreSQL)
* **CORS:** **Flask-Cors**

### Frontend (JavaScript)

* **Framework:** **React.js**
* **Routing:** **React Router**
* **HTTP Client:** **Axios**
* **Styling:** **Tailwind CSS**
* **UI Components:** **daisyUI**
* **Notifications:** **React Hot Toast**
* **Bundler:** **Vite**

---

## ⚙️ Setup & Installation

### Backend (`jira-backend-main`)

1.  **Clone the repository:**
    ```sh
    git clone [https://github.com/nishannn07/jira-clone.git](https://github.com/nishannn07/jira-clone.git)
    cd nishannn07/jira-clone/Jira-Clone-4709bebc2342891f45b85c7fd97a54310ea2d2e4/jira-backend-main
    ```

2.  **Create a virtual environment and activate it:**
    ```sh
    python -m venv venv
    source venv/bin/activate  # On Windows: venv\Scripts\activate
    ```

3.  **Install dependencies:**
    ```sh
    pip install -r requirements.txt
    ```

4.  **Set up environment variables:**
    Create a `.env` file in the `jira-backend-main` directory and add the following variables. See `config.py` and `create_super_admin.py` for reference.

    ```env
    # URL for your PostgreSQL or SQLite database
    # Example for SQLite: DATABASE_URL="sqlite:///app.db"
    DATABASE_URL="postgresql://user:password@localhost/jira_clone_db" 
    
    # Strong, random secret keys
    JWT_SECRET_KEY="your-jwt-secret-key"
    SECRET_KEY="your-flask-secret-key"
    
    # Credentials for the initial super admin account
    USERNAME="superadmin"
    EMAIL="admin@example.com"
    PASSWORD="yourstrongpassword"
    ```

5.  **Initialize and migrate the database:**
    ```sh
    flask db init  # Only if running for the first time
    flask db migrate -m "Initial migration"
    flask db upgrade
    ```

6.  **Seed the database with initial data:**
    ```sh
    flask seed-roles             # Creates the basic user roles
    flask create-super-admin     # Creates the first admin user from your .env variables
    ```

7.  **Run the backend server:**
    ```sh
    flask run
    ```
    The backend API will be running at `http://127.0.0.1:5000`.

### Frontend (`jira-frontend-final-main`)

1.  **Navigate to the frontend directory:**
    ```sh
    # From the root directory
    cd nishannn07/jira-clone/Jira-Clone-4709bebc2342891f45b85c7fd97a54310ea2d2e4/jira-frontend-final-main
    ```

2.  **Install dependencies:**
    (Using `pnpm` based on `pnpm-lock.yaml`, but `npm` or `yarn` will also work)
    ```sh
    pnpm install
    # OR
    npm install
    ```

3.  **Set up environment variables:**
    Create a `.env.local` file in the `jira-frontend-final-main` directory:

    ```env
    VITE_URL="[http://127.0.0.1:5000](http://127.0.0.1:5000)"
    ```

4.  **Run the frontend development server:**
    ```sh
    pnpm run dev
    # OR
    npm run dev
    ```
    The React application will be available at `http://localhost:5173` (or another port if 5173 is busy).

---
