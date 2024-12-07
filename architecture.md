### Architecture of Hashcode Platform

#### Introduction
This document provides an in-depth architectural overview of the Hashcode platform, a next-generation competitive programming ecosystem. It focuses on detailing the various components and their interactions, with the intent to ensure scalability, reliability, and optimal user experience. The architectural diagrams are meticulously crafted to reflect a real-world implementation.

### System Context Diagram

This diagram outlines the key stakeholders and their interaction with the Hashcode platform. It provides a high-level understanding of the platform’s major components and the flow of information.

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

The container diagram provides a detailed breakdown of the components that form the Hashcode platform, emphasizing their roles and relationships.

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

The component diagram represents the logical organization of the Hashcode platform, delineating the responsibilities of each module.

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

This diagram illustrates the primary actions that various users can perform on the platform.

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

The sequence diagram maps out the interactions between components when a user accesses the platform, participates in a contest, and submits a solution.


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

The activity diagram outlines the sequence of operations a user performs on the platform.

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
### Deployment Diagram

The deployment diagram provides an infrastructure-level view of the Hashcode platform, ensuring it meets requirements for scalability, fault tolerance, and performance.

![d1](https://github.com/user-attachments/assets/14e5f632-aaa4-4941-92ee-24d3b4627390)

```plantuml
@startuml
!define SPRITESURL https://raw.githubusercontent.com/Drakemor/RedhatDiagramIcons/master/icons/

left to right direction
skinparam linetype polyline
skinparam nodesep 20
skinparam ranksep 20

node "Load Balancer" <<Load Balancer>> as LB {
  [Nginx Proxy]
}

cloud "Cloud Provider (AWS)" {
  node "Frontend Cluster" <<Container Cluster>> as FrontendCluster {
    [React Web App] as WebApp
  }

  node "Backend Microservices" <<Kubernetes Cluster>> as BackendCluster {
    node "Service 1" <<Docker Container>> {
      [Rust API Gateway]
    }
    node "Service 2" <<Docker Container>> {
      [Contest Engine]
    }
    node "Service 3" <<Docker Container>> {
      [Judge System]
    }
  }

  database "Database Cluster" <<High Availability>> as DBCluster {
    [PostgreSQL Primary]
    [PostgreSQL Replica 1]
    [PostgreSQL Replica 2]
  }

  node "Cache Layer" <<Distributed Cache>> as CacheLayer {
    [Redis Cluster]
  }

  node "Authentication Service" <<Secure Service>> as AuthService {
    [OAuth/JWT Service]
  }

  node "Payment Gateway" <<Secure Service>> as PaymentGateway {
    [Payment Processor]
  }
}

node "Monitoring System" <<Monitoring>> as Monitoring {
  [Prometheus]
  [Grafana Dashboard]
}

node "Log Management" <<Log Aggregation>> as LogManagement {
  [ELK Stack]
}

LB --> WebApp : route traffic
WebApp --> [NodeJS API Gateway] : API calls
[NodeJS API Gateway] --> [Contest Engine]
[NodeJS API Gateway] --> [Judge System]
[NodeJS API Gateway] --> DBCluster
[NodeJS API Gateway] --> CacheLayer
[NodeJS API Gateway] --> AuthService
[NodeJS API Gateway] --> PaymentGateway

[NodeJS API Gateway] ..> Monitoring : metrics
[NodeJS API Gateway] ..> LogManagement : logs

@enduml
```


### Conclusion
The architecture of the Hashcode platform is designed to be modular, scalable, and resilient, ensuring a seamless experience for all users. By leveraging industry-standard tools and practices, this architecture lays a strong foundation for future growth and feature expansions.

---

Documented by Team InnovateCS  
IIIT Lucknow - Software Engineering Project 2024
