

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

### **4.1 Frontend Interface Design**
- **Home Page**: Displays contests, leaderboard highlights, and quick links to problem sets.
- **Contest Page**: Includes timers, rules, and a live scoreboard.
- **Problem Page**: Features syntax-highlighting editors (e.g., Monaco), live input/output previews, and submission tracking.
- **Profile Page**: Contains performance metrics, badges, and past submissions.

### **4.2 Backend Logic**
- RESTful API endpoints:
  - `GET /contests`: Fetch available contests.
  - `POST /submit`: Submit code for evaluation.
  - `GET /results/{contestId}`: Fetch contest results.
- WebSocket for real-time updates:
  - Live scoreboard.
  - Notifications for submission results.
- Contest Timer: Centralized contest state management using Redis.

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


#### Tables:
- **Users**:  
  ```sql
  CREATE TABLE Users (
    userId SERIAL PRIMARY KEY,
    username VARCHAR(50) UNIQUE NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    passwordHash VARCHAR(255) NOT NULL,
    rating INT DEFAULT 0
  );
  ```

- **Contests**:  
  ```sql
  CREATE TABLE Contests (
    contestId SERIAL PRIMARY KEY,
    title VARCHAR(100) NOT NULL,
    startTime TIMESTAMP NOT NULL,
    endTime TIMESTAMP NOT NULL
  );
  ```

- **Submissions**:  
  ```sql
  CREATE TABLE Submissions (
    submissionId SERIAL PRIMARY KEY,
    userId INT REFERENCES Users(userId),
    contestId INT REFERENCES Contests(contestId),
    problemId INT NOT NULL,
    status VARCHAR(50),
    timestamp TIMESTAMP DEFAULT NOW()
  );
  ```

---




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
