🛠️ Task Scheduling and Management App (MERN Stack)
This project is a task management system designed to efficiently schedule, prioritize, and assign tasks to team members. It supports customizable task priority, dynamic assignment to team members, and visual scheduling through a calendar view. The app helps identify overallocated team members and gives a clear overview of task distribution.

🚀 Project Setup
This is a MERN stack application with separate frontend and backend folders.

Backend (/backend)
Tech Stack: Node.js, Express.js, MongoDB (Mongoose)

Folder Structure:

/config: Database connection setup

/controllers: Logic for handling requests

/models: Mongoose schemas for TeamMembers and Tasks

/routes: API endpoints

server.js: Entry point for the server

Backend Setup
cd backend
npm install
npm run dev
Make sure MongoDB is running locally or set up a remote connection string in the .env file.

Frontend (/frontend)
Tech Stack: React.js

Folder Structure:

/components: Reusable components like CalendarView, TaskList

/pages: Main pages like DashboardPage

/styles: Custom CSS files

Frontend Setup
cd frontend
npm install
npm start
This will run the React app on http://localhost:3000.

🧠 Approaches & Functionality
1.1) 🧮 Overallocated Hours (Frontend-Only Calculation)
The logic is entirely handled on the frontend (DashboardPage.jsx).

It fetches all tasks and all team members.

For each team member, it sums up the estimatedHours of their assigned tasks grouped by day.

If the total exceeds 8 hours per day, that member is marked as overallocated.

✅ Example Test Cases
Case 1:

Member A has two tasks due on 2025-04-23 (5 hrs and 6 hrs) → Total = 11 hrs
Member A works 8 hrs per day 

🔴 Result: Member A is overallocated on 2025-04-23

Case 2:

Member B has three tasks due on different days (each 4 hrs)
Member B works 8 hrs per day 

🟢 Result: Member B is not overallocated on any day

1.2) ✅ Full CRUD Functionality
Both Team Members and Tasks can be:

Created

Updated

Deleted

Task assignments can be edited dynamically.

1.3) 📅 Calendar View (Visual Task Management)
Implemented using react-big-calendar with custom color coding based on task urgency:

js
Copy
Edit
if (task.state === 'Pending') {
  if (task.priority === 'High' && dueInDays <= 2) return '#dc3545'; // Red: Urgent
  if (task.priority === 'Medium' && dueInDays > 2) return '#ffc107'; // Yellow
  if (task.priority === 'Low' && dueInDays > 2) return '#ffc107'; // Yellow
}
Explanation:

Red: High-priority tasks due soon (<= 2 days)

Yellow: Medium/Low-priority tasks due later

Green (default): All others (e.g., completed or non-urgent)

This gives users a quick visual cue about which tasks need immediate attention.

🧩 Challenges Faced
Overallocation Calculation Strategy

Whether to calculate per day (strict) or weekly average (flexible)

Currently implemented as day-wise

Calendar View Scaling

Deciding between month, week, or day views

Month view can get crowded, so we also support week/day views with popup handling

📌 Conclusion
The app successfully combines scheduling logic with real-time task visualization.

Sample Overallocation Calculation:

Member X is assigned 3 tasks due on the same day with estimated hours: 4 + 3 + 2 = 9 hours → Since it exceeds 8 hours/day → Overallocated
