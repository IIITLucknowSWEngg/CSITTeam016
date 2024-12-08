```mermaid
flowchart TD
    %% Entry Points
    A[Start: Landing Page] --> B{User Authentication}
    
    %% Authentication Flow
    B --> |New User| C[Registration Page]
    B --> |Existing User| D[Login Page]
    
    %% Registration Detailed Flow
    C --> E[Personal Information]
    E --> F[Email Verification]
    F --> G[Profile Creation]
    G --> H[Select User Category]
    H --> I{User Type}
    
    I --> |Competitive Programmer| J[Skill Assessment Test]
    I --> |Student| K[Educational Institution Verification]
    I --> |Mentor| L[Professional Credentials]
    I --> |Casual User| M[Basic Profile Setup]
    
    %% Login Detailed Flow
    D --> N[Authentication]
    N --> |Success| O[User Dashboard]
    N --> |Failed| P[Password Recovery/Retry]
    
    %% Dashboard Core Flows
    O --> Q{User Actions}
    
    %% Contest Participation Flow
    Q --> |Join Contest| R[Contest Categories]
    R --> S[Filter Options]
    S --> T[Contest Details]
    T --> U[Registration/Eligibility Check]
    U --> V[Contest Preparation]
    V --> W[Contest Start]
    W --> X[Problem Solving]
    X --> Y[Solution Submission]
    Y --> Z[Real-time Evaluation]
    Z --> AA[Provisional Results]
    AA --> AB[Final Scoring]
    
    %% Problem Solving Flow
    Q --> |Practice Problems| AC[Problem Repository]
    AC --> AD[Problem Filters]
    AD --> AE[Difficulty Levels]
    AE --> AF[Problem Selection]
    AF --> AG[Problem Statement]
    AG --> AH[Code Submission]
    AH --> AI[Automated Judging]
    AI --> AJ[Detailed Feedback]
    AJ --> AK[Solution Analysis]
    
    %% Ranking and Achievements
    Q --> |View Rankings| AL[Ranking Systems]
    AL --> AM[Global Rankings]
    AL --> AN[Category Rankings]
    AL --> AO[Personal Performance]
    
    %% Profile Management
    Q --> |Profile Settings| AP[User Profile]
    AP --> AQ[Personal Information]
    AP --> AR[Learning Tracks]
    AP --> AS[Achievement Showcase]
    AP --> AT[Performance Analytics]
    
    %% Advanced Features
    Q --> |Learning Resources| AU[Educational Content]
    AU --> AV[Tutorials]
    AU --> AW[Video Lessons]
    AU --> AX[Recommended Problems]
    
    %% Mentorship and Coaching
    Q --> |Mentorship| AY[Mentor Matching]
    AY --> AZ[Mentor Profile]
    AZ --> BA[Request Coaching]
    BA --> BB[Coaching Session]
    
    %% Connectivity and Social
    Q --> |Community| BC[Community Forums]
    BC --> BD[Discussion Threads]
    BC --> BE[Problem Discussions]
    BC --> BF[User Interactions]
