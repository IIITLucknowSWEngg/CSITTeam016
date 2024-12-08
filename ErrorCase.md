
# Hashcode Platform - User Journey and Error Flows

## Overview

This document outlines the user journey and associated error flows for the Hashcode competitive programming platform. It includes processes for user authentication, contest participation, code submission, and reward distribution, ensuring clarity in user interactions and system behaviors.

---

![image](https://github.com/user-attachments/assets/4fb5ace3-ea02-49c3-93ee-5c1b5bebac62)


## Flow Breakdown

### **1. User Authentication**
The authentication process ensures secure access for users.

#### **Steps**:
1. **User Action**:
   - The user attempts to log in using their credentials.
2. **System Validation**:
   - The Authentication Service verifies the credentials.

#### **Scenarios**:
- **Successful Authentication**:
  - Generates a session token and redirects the user to the dashboard.
  - _Example_: A user logs in successfully and accesses their account.
  
- **Authentication Failure**:
  - Displays an error message with a maximum of 3 login attempts allowed.
  - _Example_: Incorrect password entered three times; user account locked.

---

### **2. Contest Participation**
Users can browse and join contests based on eligibility and payment.

#### **Steps**:
1. **User Action**:
   - Browses the list of available contests.
2. **Eligibility Check**:
   - Contest Management validates the user's rating and other criteria.
3. **Payment Integration**:
   - Eligible users are prompted to pay the entry fee.

#### **Scenarios**:
- **Successful Participation**:
  - Payment is confirmed, and contest details are sent to the user.
  - _Example_: User pays the fee and receives the contest start time and rules.
  
- **Payment Failure**:
  - Displays a payment error due to insufficient funds or technical issues.
  - _Example_: User's card transaction fails; they must retry.

- **Eligibility Error**:
  - Shows an error if the user's skill level does not match the contest.
  - _Example_: A beginner tries to join an advanced-level contest.

---

### **3. Code Submission**
The core feature of the platform is evaluating user-submitted solutions.

#### **Steps**:
1. **User Action**:
   - Submits a solution for a contest problem.
2. **System Validation**:
   - The Code Evaluation Engine checks for compilation errors.
3. **Sandbox Execution**:
   - Executes the code in a secure, isolated environment.
4. **Plagiarism Detection**:
   - Ensures submission originality.

#### **Scenarios**:
- **Successful Execution**:
  - The solution passes and is recorded as a valid submission.
  - _Example_: User's solution produces correct results for all test cases.
  
- **Compilation Error**:
  - Displays syntax or structural issues in the user's code.
  - _Example_: A missing semicolon in C++ prevents compilation.
  
- **Runtime Error**:
  - Indicates performance or logic issues during execution.
  - _Example_: Infinite loop causing timeout.
  
- **Plagiarism Detected**:
  - Disqualifies the submission due to integrity violations.
  - _Example_: Identical code found between multiple submissions.

---

### **4. Reward Distribution**
Rewards are calculated and distributed based on performance.

#### **Steps**:
1. **Performance Evaluation**:
   - Reward Distribution evaluates contest results.
2. **Prize Calculation**:
   - Determines the prize pool and distributes rewards.

#### **Scenarios**:
- **Successful Reward Distribution**:
  - Credits the user's wallet and sends a notification.
  - _Example_: User wins first place and receives prize money.
  
- **Disputed Results**:
  - Requires manual review of the submission.
  - _Example_: Suspicion of unfair play prompts investigation.

---

## PUML Code

Below is the PlantUML code representing the flow:

```puml
@startuml HashcodeUserFlow
!theme blueprint
skinparam linetype ortho
skinparam backgroundColor #F5F5F5
skinparam roundcorner 10
skinparam maxmessagesize 80

title Hashcode Platform - User Journey and Error Flows

actor User #AliceBlue
participant "Authentication Service" as Auth #LightBlue
participant "User Dashboard" as Dashboard #LightGreen
participant "Contest Management" as Contest #LightYellow
participant "Code Evaluation Engine" as CodeEngine #LightPink
participant "Payment Gateway" as Payment #LightSalmon
participant "Reward Distribution" as Rewards #LightCyan

header **Hashcode Platform Flow Diagram**

== User Authentication ==
User -> Auth: Attempt Login
activate Auth

alt Successful Authentication
    Auth --> User: Generate Session Token
    Auth -> Dashboard: Redirect to User Dashboard
    note right: Login Success, Session Token Active
else Authentication Failure
    Auth -> User: Show Error Message
    note right: Max 3 login attempts
end
deactivate Auth

== Contest Participation ==
User -> Contest: Browse Available Contests
activate Contest

alt Contest Eligibility Check
    Contest -> User: Validate User Rating
    
    alt User Meets Criteria
        Contest -> Payment: Initiate Contest Entry
        activate Payment
        
        alt Payment Successful
            Payment -> Contest: Confirm Entry
            Contest -> User: Send Contest Details
        else Payment Failed
            Payment -> User: Show Payment Error
            note right: Insufficient funds or transaction issue
        end
        deactivate Payment
    else Rating Mismatch
        Contest -> User: Show Eligibility Error
        note right: Skill level not matching contest
    end
end
deactivate Contest

== Code Submission ==
User -> CodeEngine: Submit Solution
activate CodeEngine

alt Code Validation
    CodeEngine -> CodeEngine: Compile Check
    
    alt Compilation Successful
        CodeEngine -> CodeEngine: Run Sandbox Execution
        
        alt Execution Passed
            CodeEngine -> CodeEngine: Plagiarism Check
            
            alt Original Solution
                CodeEngine -> Contest: Record Submission
                Contest -> Rewards: Track Performance
            else Plagiarism Detected
                CodeEngine -> User: Disqualify Submission
                note right: Integrity violation
            end
        else Execution Failed
            CodeEngine -> User: Show Runtime Error
            note right: Performance or logic issues
        end
    else Compilation Error
        CodeEngine -> User: Show Compilation Errors
        note right: Syntax or structural problems
    end
end
deactivate CodeEngine

== Reward Distribution ==
Rewards -> Contest: Evaluate Performance
activate Rewards

alt Reward Calculation
    Rewards -> Rewards: Calculate Prize Pool
    
    alt Valid Submission
        Rewards -> Payment: Credit Wallet
        Payment -> User: Notify Earnings
    else Disputed Results
        Rewards -> Contest: Review Submission
        note right: Manual intervention required
    end
end
deactivate Rewards

footer Generated on %date("yyyy-MM-dd")
@enduml
```

---

## Conclusion

This document provides a detailed view of the user journey and error flows for the Hashcode platform. It ensures a comprehensive understanding of platform functionalities and edge cases, facilitating better development and user experience.
