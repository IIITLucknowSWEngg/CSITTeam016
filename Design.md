

# **Design Document for HashCode**

## **Table of Contents**
| Section | Title |
| ------- | ----- |
| 1       | Introduction |
| 2       | Design Principles |
| 3       | System Architecture |
| 4       | Detailed Design |
| 5       | User Interface Design |
| 6       | Backend Design |
| 7       | Expected Design |

---

## **1. Introduction**

### **1.1 Purpose**  
This document defines the complete design specifications for the HashCode Competitive Programming Platform, covering both the system architecture and interface design. It serves as a guide for implementation while ensuring high usability, security, and maintainability.

### **1.2 Scope**  
HashCode aims to provide an intuitive, scalable, and efficient platform for competitive programming, delivering interactive features like those on Codeforces and LeetCode. This document details the **front-end appearance**, **back-end logic**, **database structure**, and **user workflows**.

---

## **2. Design Principles**

- **User-Centric Design**: Interfaces tailored for smooth navigation and user engagement.
- **Scalable Backend**: Efficiently handles a growing number of participants.
- **Interactive UI/UX**: Clear layouts, syntax-highlighting code editors, and real-time feedback.
- **Security First**: Robust encryption, secure data management, and JWT authentication.
- **Modularity**: Separation of concerns for independent scalability.
- **Real-Time Updates**: WebSocket-based live scoreboard and submission updates.

---

## **3. System Architecture**

The architecture includes the following components:

- **Frontend**:  
  Developed using React.js with TailwindCSS for a dynamic, responsive design.
- **Backend**:  
  Built with Node.js, Express for API management, and WebSocket for real-time data transfer.
- **Database**:  
  PostgreSQL is used with a schema optimized for contests, submissions, and analytics.
- **Authentication**:  
  Secure user management through OAuth and JWT.
- **Judge System**:  
  Dockerized environment to isolate code execution, integrated with pre-defined test cases.
- **CI/CD Pipelines**:  
  Automated deployment pipelines using GitHub Actions and Docker.

---

## **4. Detailed Design**

### 4.1 Frontend Interface Design  

1. **Home Page**  
   - **Description**: The main landing page providing a comprehensive overview of the platform.  
   - **Features**:  
     - **Contest Highlights**: Displays ongoing and upcoming contests with quick links to join or view details.  
     - **Leaderboard Snippets**: Showcases top-performing contestants in real-time.  
     - **Quick Links**: Navigation to curated problem sets, trending problems, and tutorials for practice.  
     - **Search Bar**: Allows users to search for specific contests, problems, or users.  

2. **Contest Page**  
   - **Description**: A dedicated page for each contest.  
   - **Features**:  
     - **Contest Timer**: Real-time countdown to contest start and end.  
     - **Rules and Guidelines**: Detailed instructions for contestants.  
     - **Live Scoreboard**: Continuously updated with participant rankings, scores, and problem-wise performance.  
     - **Problem List**: Clickable links to the problems included in the contest.  

3. **Problem Page**  
   - **Description**: The core interface for solving programming problems.  
   - **Features**:  
     - **Syntax-Highlighting Code Editor**: Powered by Monaco, with autocomplete and error detection.  
     - **Live Input/Output Preview**: Real-time feedback for custom test cases.  
     - **Submission Tracker**: Displays past attempts, their statuses, and scores.  
     - **Hints and Resources**: Optional section providing curated hints and related reading material.  

4. **Profile Page**  
   - **Description**: User-centric page highlighting personal progress and achievements.  
   - **Features**:  
     - **Performance Metrics**: Graphical representation of contest scores, rankings, and problem-solving history.  
     - **Badges**: Visual representation of milestones and achievements.  
     - **Past Submissions**: Chronological list of all submissions with links to view details and explanations.  

---

### 4.2 Backend Logic  

1. **RESTful API Endpoints**  

   - **Contest Management**:  
     - `GET /contests`: Fetch a list of all active, upcoming, and completed contests.  
     - `GET /contests/{contestId}`: Fetch details of a specific contest.  
     - `POST /contests`: Create a new contest (admin only).  
     - `PUT /contests/{contestId}`: Update contest details (admin only).  
     - `DELETE /contests/{contestId}`: Delete a contest (admin only).  

   - **Problem Management**:  
     - `GET /problems`: Fetch a list of all problems.  
     - `GET /problems/{problemId}`: Retrieve details of a specific problem.  
     - `POST /problems`: Create a new problem (admin only).  
     - `PUT /problems/{problemId}`: Update problem details (admin only).  
     - `DELETE /problems/{problemId}`: Delete a problem (admin only).  

   - **Submission Handling**:  
     - `POST /submit`: Submit code for evaluation.  
     - `GET /submissions/{submissionId}`: Fetch details of a specific submission.  
     - `GET /submissions`: List all submissions for a user or contest.  

   - **Leaderboard and Results**:  
     - `GET /leaderboards/{contestId}`: Retrieve the leaderboard for a specific contest.  
     - `GET /results/{contestId}`: Fetch the results for a specific contest.  

   - **User Profile**:  
     - `GET /profile`: Fetch details of the currently authenticated user.  
     - `PUT /profile`: Update user profile information.  
     - `GET /profile/{userId}`: Fetch details of another user (limited data).  

   - **Authentication**:  
     - `POST /register`: Register a new user.  
     - `POST /login`: Log in a user and issue a token.  
     - `POST /logout`: Invalidate the current session token.  

2. **WebSocket for Real-Time Updates**  

   - **Live Scoreboard**:  
     - Enables real-time updates to contest leaderboards.  
     - Pushes changes in rank and scores as soon as submissions are evaluated.  

   - **Submission Notifications**:  
     - Notifies users of the status of their submissions (e.g., "Accepted," "Runtime Error").  

   - **Admin Announcements**:  
     - Real-time announcements or alerts during contests (e.g., problem clarifications).  

3. **Contest Timer**  
   - **Description**: Centralized management of contest timing and state.  
   - **Implementation**:  
     - **Redis**: Used to store contest states and ensure consistent updates across multiple servers.  
     - **Logic**:  
       - Triggers actions like contest start/end notifications, locking/unlocking problem sets, and freezing scoreboards before the contest ends.  

4. **Background Jobs**  
   - **Code Evaluation**:  
     - Handles submission processing asynchronously.  
     - Uses a job queue for execution, result generation, and updating scores.  
   - **Audit Logging**:  
     - Records user actions such as submissions, profile updates, and problem views for analytics and compliance.  

---

## **5. User Interface Design**

### **5.1 Key Pages**

#### **Home Page**
- **Layout**:  
  - Left: Navigation bar with links to "Contests," "Practice," and "Profile."
  - Center: Highlighted contests with a timer.
  - Right: Leaderboard snapshots.
- **Color Scheme**:  
  Dark mode default with accent colors in blue and orange for actionable elements.

#### **Contest Interface**
- **Components**:  
  - Problem List: Sidebar with question names and statuses (attempted/unattempted).  
  - Timer: Sticky at the top-right.  
  - Code Editor: Full-width with language selection.  

#### **Submission Results**
- Real-time status updates (e.g., "Running," "Accepted," "Wrong Answer").  
- Pop-up animations for successful submissions.

---

## **6. Backend and Database Design**

### **6.1 Backend Architecture**

- **Core Features**:
  - Microservice-based structure for scalability.
  - Worker queues for handling code execution (e.g., RabbitMQ).
  - Test case caching for commonly solved problems.

### **6.2 Database Schema**

#Architecture->
![image](https://github.com/user-attachments/assets/8cd0df10-dba2-40c8-8602-c72c48b59038)



## 7. Expected Design 

### **Wireframes**
- **Home Page**
  - Banner: Highlights upcoming contests with countdown timers.
  - Sections: Cards for "Top Participants," "Recent Activity," and "Tutorials."

- **Problem Page**
  - Left: Problem description.
  - Right: Code editor with split-pane for input/output.

### **Animations**
- Buttons: Ripple effects on clicks.
- Notifications: Slide-in alerts for updates like new contests or submission results.

### Codeforces Profile
![image](https://github.com/user-attachments/assets/bdf1d5f1-e05a-4908-bf7b-88ab825b8b31)

### Leetcode Profile
![image](https://github.com/user-attachments/assets/3a4b1dd2-c8a6-4af2-9b8e-c12c30f00f10)

### Leetcode Problems
![image](https://github.com/user-attachments/assets/2d80c319-60fe-47d3-8a9d-3aed87aa7283)

### Codeforces Contest
![image](https://github.com/user-attachments/assets/952c3355-1327-4eea-826c-bcd34992fbd1)

### Codechef Problem 
![image](https://github.com/user-attachments/assets/bb2fe9ea-4908-4ee4-9271-8ac33d7980a0)

### Leetcode Problem Interface
![image](https://github.com/user-attachments/assets/25902818-d73f-4b10-9e41-2e9e6c68cf50)

### Codeforces Problem Interface
![image](https://github.com/user-attachments/assets/7d4b24c9-e321-4b9a-80af-16ddce76e3a9)

### Submission Interface
![image](https://github.com/user-attachments/assets/6b254d70-7838-4664-8739-75912944a3e1)




## 8. References
- **Frontend Frameworks**:  
  React.js Documentation, TailwindCSS Guides.
- **Backend Best Practices**:  
  Node.js Official Documentation.
- **Database Design**:  
  PostgreSQL Optimization Techniques.
- **Real-Time Systems**:  
  WebSocket Implementation Best Practices.
- SWEBOK: [Software Engineering Body of Knowledge](https://www.computer.org/education/bodies-of-knowledge/software-engineering/v4)
- SDD Template: [SDD Template](https://wildart.github.io/MISG5020/standards/SDD_Template.pdf)
- IEEE 1016: [IEEE Standard for Information Technology](https://standards.ieee.org/ieee/1016/4502/)

---

Documented by Team InnovateCS  
IIIT Lucknow - Software Engineering Project 2024
