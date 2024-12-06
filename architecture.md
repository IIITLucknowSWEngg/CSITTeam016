### Architecture of Hashcode Platform

#### Introduction
This document provides a comprehensive overview of the architecture of the Hashcode platform, detailing various components and their interactions. The diagrams aim to be highly detailed to reflect a real-world project setup.

### System Context Diagram
![image](https://github.com/user-attachments/assets/3ff339ec-6b59-46c3-afd1-90d1d8e2457f)



```plantuml
@startuml
actor User
actor Admin
actor Developer
actor Sponsor
actor Educator
actor Mentor

package "Hashcode Platform" {
    [Web Interface]
    [Application Server]
    [Database]
    [Authentication Service]
    [Payment Gateway]
    [Cache Layer]
}

User --> [Web Interface]
Admin --> [Web Interface]
Developer --> [Web Interface]
Sponsor --> [Web Interface]
Educator --> [Web Interface]
Mentor --> [Web Interface]
[Web Interface] --> [Application Server]
[Application Server] --> [Database]
[Application Server] --> [Authentication Service]
[Application Server] --> [Payment Gateway]
[Application Server] --> [Cache Layer]
@enduml
```

### Container Diagram

![image](https://github.com/user-attachments/assets/276243f2-1491-4490-b0d2-226795122001)



```plantuml
@startuml
actor User
actor Admin
actor Developer
actor Sponsor
actor Educator
actor Mentor

node "Web Server" {
    [Web Interface] <<Front-end>> as UI
}

node "Application Server" {
    [Backend API] <<Back-end>> as API
    [Contest Engine] <<Service>> as CE
    [Judge System] <<Service>> as JS
    [Wallet Service] <<Service>> as WS
}

node "Database Server" {
    [PostgreSQL] <<Database>> as DB
}

node "Authentication Server" {
    [Auth Service] <<Service>> as Auth
}

node "Payment Gateway" {
    [Payment Processor] <<Service>> as PP
}

node "Cache Layer" {
    [Redis] <<Cache>> as Cache
}

User --> UI
Admin --> UI
Developer --> UI
Sponsor --> UI
Educator --> UI
Mentor --> UI
UI --> API
API --> CE
API --> JS
API --> WS
API --> DB
API --> Auth
API --> PP
API --> Cache
@enduml
```

### Code Component Diagram
![image](https://github.com/user-attachments/assets/6e694d9c-31a0-4db8-9c3f-359366d40721)

```plantuml
@startuml
package "Web Interface" {
    class ReactApp {
        +render()
        +handleSubmit()
    }
}

package "Backend API" {
    class NodeApp {
        +handleRequest()
        +validateData()
    }
    class ContestEngine {
        +createContest()
        +manageContest()
    }
    class JudgeSystem {
        +evaluateCode()
    }
    class WalletService {
        +handleTransactions()
        +processPayments()
    }
}

package "Database" {
    class PostgreSQL {
        +storeData()
        +retrieveData()
    }
}

package "Auth Service" {
    class Auth {
        +login()
        +register()
    }
}

package "Payment Processor" {
    class Payment {
        +processEntryFees()
        +distributePrizes()
    }
}

package "Cache Layer" {
    class Redis {
        +cacheData()
        +retrieveCache()
    }
}

ReactApp -> NodeApp : sends request
NodeApp -> ContestEngine : delegates contest logic
NodeApp -> JudgeSystem : delegates code evaluation
NodeApp -> WalletService : handles financial transactions
NodeApp -> PostgreSQL : interacts with database
NodeApp -> Auth : handles authentication
NodeApp -> PaymentProcessor : handles payments
NodeApp -> Redis : caches data

@enduml
```

### Use Case Diagram
![image](https://github.com/user-attachments/assets/88fc900b-d551-402f-b852-14be6fb59d37)

```plantuml
@startuml
actor User
actor Admin
actor Developer
actor Sponsor
actor Educator
actor Mentor

User -> (Register)
User -> (Login)
User -> (Participate in Contest)
User -> (Submit Code)
User -> (View Results)
Admin -> (Create Contest)
Admin -> (Manage Contest)
Developer -> (Deploy Code)
Developer -> (Monitor System)
Sponsor -> (Sponsor Contest)
Educator -> (Bulk Student Registration)
Mentor -> (Track Student Progress)

@enduml
```

### Sequence Diagram
![image](https://github.com/user-attachments/assets/111f6f97-a84a-4c8f-941e-110c6d2cb8c5)

```plantuml
@startuml
actor User
participant "Web Interface" as UI
participant "Application Server" as AS
participant "Contest Engine" as CE
participant "Judge System" as JS
participant "Database" as DB
participant "Authentication" as Auth
participant "Payment Processor" as PP
participant "Wallet Service" as WS

User -> UI: Access Platform
UI -> Auth: Validate User
Auth -> DB: Fetch User Data
DB -> Auth: Return User Data
Auth -> UI: Auth Token
UI -> User: Access Granted

User -> UI: Participate in Contest
UI -> AS: Get Contest Details
AS -> CE: Retrieve Contest Info
CE -> DB: Fetch Contest Data
DB -> CE: Return Contest Data
CE -> AS: Contest Info
AS -> UI: Display Contest Info

User -> UI: Submit Code
UI -> AS: Submit Code
AS -> JS: Validate and Run Tests
JS -> DB: Fetch Test Cases
DB -> JS: Return Test Cases
JS -> AS: Test Results
AS -> UI: Display Results

User -> UI: Pay Entry Fee
UI -> PP: Process Payment
PP -> WS: Handle Transaction
WS -> DB: Update Wallet
PP -> UI: Payment Confirmation

@enduml
```

### Activity Diagram
![image](https://github.com/user-attachments/assets/1a10142b-bcf7-45a1-901e-fd4a975cde16)

```plantuml
@startuml
start
:User Accesses Platform;
:Login/Register;
if (Valid User?) then (yes)
  :Access Granted;
else (no)
  :Access Denied;
endif
:Participate in Contest;
:Submit Code;
:Evaluate Code;
if (Valid Code?) then (yes)
  :Display Results;
else (no)
  :Show Errors;
endif
:Pay Entry Fee;
:Process Payment;
if (Payment Successful?) then (yes)
  :Confirm Participation;
else (no)
  :Show Payment Error;
endif
stop
@enduml
```

### Conclusion
The detailed architecture of the Hashcode platform is designed to be modular, scalable, and efficient, ensuring a robust environment for competitive programming. The use of PlantUML diagrams helps in visualizing the interactions and structure of the platform's components.

---

Documented by Team InnovateCS  
IIIT Lucknow - Software Engineering Project 2024
