


# System Context Diagram of HashCode

## Overview

The System Context Diagram provides a high-level view of the Upsolve platform, showing the interactions between external actors (like users and administrators) and the core system components. 

![image](https://github.com/user-attachments/assets/e4d2a01f-93be-4804-99b4-411c98298b92)

## Key Elements

- **External Actors**
  - **Users**: Interact with the platform to practice problems, participate in contests, and engage with community features.
  - **Administrators**: Manage user accounts, contests, and problem sets, ensuring smooth operations and content moderation.

- **System Components**
  - **Frontend (React)**: The user interface where users log in, navigate problems, participate in contests, and view leaderboards.
  - **Backend Services (Golang, Rust, Node.js)**: Handle user management, problem retrieval, contest updates, code submissions, and evaluation.
  - **Database Layer (Redis, PostgreSQL)**: Stores user data, contest results, problem sets, and manages caching for high-speed data access.
  - **Code Evaluation Engine**: Sandboxed environment to securely run and evaluate code submissions in real time.
  - **Cloud Infrastructure (AWS)**: Hosts the application with Docker for containerization and Kubernetes for orchestration, ensuring scalability and fault tolerance.

---

> **Note**: This context diagram serves as a high-level view of Upsolve’s architecture. It illustrates the relationships between users, system components, and external services, providing an overall picture of how the platform operates.
