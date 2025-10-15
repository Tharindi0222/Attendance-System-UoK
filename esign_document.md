Document – University Attendance System
🧭 Overview

This document describes the system architecture, database design, and data flow of the University Attendance System, developed as part of the Full Stack Development module.
The system aims to automate student attendance tracking using QR-based check-ins, real-time dashboards, and secure authentication for students, lecturers, and administrators.

🧩 1. System Architecture

🏗️ Architecture Type: 3-Tier (Full Stack) Architecture

The project follows a three-layered architecture:

Layer	Description	Technologies

Frontend (Client Layer)	User interface that allows students, lecturers, and admins to interact with the system.	HTML5, CSS3, JavaScript, React.js / Flutter Web
Backend (Application Layer)	Handles logic, authentication, attendance processing, and API requests.	Node.js (Express.js) / PHP (Laravel)
Database (Data Layer)	Stores user accounts, attendance logs, and course details.	MySQL / PostgreSQL

Additional Services:
•	QR Code Service: Generates and validates attendance QR codes.
•	Authentication Service: Implements JWT or OTP-based login for enhanced security.
•	API Gateway: Handles communication between frontend and backend via REST APIs.
Deployment Model:
•	Hosted on GitHub + Render / Firebase Hosting / AWS EC2
•	Database hosted on Cloud MySQL (PlanetScale / Railway)

🧮 2. Database Design

🗂️ ER Diagram (Conceptual Overview)
Entities and Relationships:
STUDENT (student_id, name, email, password, course_id)
COURSE  (course_id, course_name, lecturer_id)
LECTURER (lecturer_id, name, email, password)
ATTENDANCE (attendance_id, student_id, course_id, date, status, location)
ADMIN (admin_id, name, email, password)

Relationships:
•	A student enrolls in many courses.
•	A lecturer teaches many courses.
•	Each attendance record links a student, course, and date.
•	Admin manages lecturer and student records.

📋 Example Table Structures
1. Students
Field	Type	       Description
student_id	       INT (PK)	             Unique student ID
name	           VARCHAR(100)	           Student full name
email	           VARCHAR(100)	           University email
password	       VARCHAR(255)	           Hashed password
course_id	       INT (FK)	               Linked course

3. Attendance

Field	Type	        Description
attendance_       id	INT (PK)	                 Unique ID
student_id	      INT (FK)	                   Student who checked in
course_id	        INT (FK)	                   Course attended
date	            DATE	                       Attendance date
time	            TIME	                       Check-in time
status	          ENUM('Present','Absent')	   Attendance status
location	        VARCHAR(100)	               GPS or classroom

🔄 3. Data Flow Diagram (DFD)

[Student] ---> (Attendance System) <--- [Lecturer]
                       ^
                       |
                   [Admin]

Shows main entities interacting with the system.
 
Level 1: Functional Breakdown
1. Student Flow
•	Logs in → Scans QR → System validates → Record stored in DB → Confirmation message
2. Lecturer Flow
•	Logs in → Selects course → Views/edits attendance → Updates database
3. Admin Flow
•	Logs in → Manages users and courses → Generates reports

Data Flow Summary

StepSource	       Process	                Destination
1	Student	       Scan QR code	               Attendance DB
2	Lecturer	     View/Edit Attendance	       Database
3	Admin          Generate Report	           Dashboard
4	System	       Alert Low Attendance	       Student Email

⚙️ 4. Technology Stack Summary
Layer	             Technology	                           Description
Frontend	        React.js / Flutter	             Responsive UI for web/mobile
Backend           Node.js + Express / PHP	         Handles logic & API endpoints
Database	        MySQL	                           Stores user and attendance data
Authentication	  JWT / Firebase Auth	             Secure login system
QR Handling 	    npm / Google Charts API	         QR generation & scanning
Hosting	          Render / Firebase / AWS	         Cloud deployment

📈 5. Future Enhancements
•	Integration with University LMS (e.g., Moodle)
•	Face recognition for attendance verification
•	Real-time analytics dashboard for admins
•	SMS/email alerts for absentees

