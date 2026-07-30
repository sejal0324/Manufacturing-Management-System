# 🏭 Manufacturing Management System

> **Business Case Study | Software Design | System Architecture | Database Design**

![Status](https://img.shields.io/badge/Project-Business%20Case%20Study-blue)
![Domain](https://img.shields.io/badge/Domain-Manufacturing-success)
![Architecture](https://img.shields.io/badge/Architecture-Layered-orange)
![Database](https://img.shields.io/badge/Database-MySQL-blueviolet)
![Backend](https://img.shields.io/badge/Backend-Java-important)
![Frontend](https://img.shields.io/badge/Frontend-React-9cf)

---

## 📖 Overview

This repository presents a software engineering case study for a Manufacturing Management System designed for small and medium-sized manufacturing industries.

The objective of this project was to understand how software can improve manufacturing operations by analysing existing business processes and designing a centralized software solution.

Instead of developing the application, this project focuses on requirement analysis, software architecture, database planning, module design, and business workflow.

---

## 🏭 Business Scenario

A manufacturing company produces products in multiple production batches every day. Most operational activities are recorded manually using paper registers and Excel sheets.

As production increases, managing information manually becomes difficult and often leads to delays, duplicate records, and communication gaps between departments.

This case study proposes a centralized web-based system that helps manage production, inventory, maintenance, employees, and reporting from a single platform.

---

## ❗ Problem Statement

The existing workflow depends heavily on manual processes.

Some common challenges include:

- Manual production records
- Inventory mismatches
- Delayed report generation
- Machine maintenance not tracked properly
- No centralized dashboard
- Difficult communication between departments
- Time-consuming data retrieval

---

## 🎯 Objectives

- Digitize manufacturing operations
- Reduce paperwork
- Improve inventory visibility
- Track production in real time
- Schedule preventive maintenance
- Generate reports automatically
- Improve decision making using dashboards

---
## 🔄 Current Manufacturing Workflow

The following diagram represents a typical manufacturing workflow observed in small and medium-scale manufacturing industries.

```mermaid
flowchart TD

A[Supplier] --> B[Raw Material Received]

B --> C[Inventory Verification]

C --> D[Production Planning]

D --> E[Machine Allocation]

E --> F[Production Process]

F --> G[Quality Inspection]

G --> H{Quality Passed?}

H -->|Yes| I[Packaging]

H -->|No| J[Rework / Scrap]

I --> K[Finished Goods Inventory]

K --> L[Dispatch]

L --> M[Customer]
```

---

## 💡 Proposed Software Solution

The proposed Manufacturing Management System centralizes different business operations into a single platform.

Instead of maintaining separate Excel sheets and paper records, every department interacts with one integrated system.

The software is divided into multiple independent modules, making it scalable and easier to maintain.

---

## 📦 Proposed Modules

### 📊 Dashboard

Provides a quick overview of manufacturing activities.

Features:

- Daily Production Summary
- Machine Utilization
- Employee Attendance
- Inventory Alerts
- Pending Maintenance
- Recent Activities

---

### 🏭 Production Management

Responsible for handling daily production activities.

Features:

- Create Production Batch
- Assign Machine
- Assign Operator
- Track Production Status
- Close Production Batch
- View Production History

---

### 📦 Inventory Management

Maintains stock details for raw materials and finished products.

Features:

- Add New Items
- Update Stock
- Low Stock Alerts
- Supplier Information
- Stock Movement History

---

### 🔧 Maintenance Management

Helps track machine servicing and breakdown history.

Features:

- Preventive Maintenance Schedule
- Breakdown Reporting
- Maintenance History
- Machine Availability
- Service Log

---

### 👨‍💼 Employee Management

Stores employee information and manages attendance.

Features:

- Employee Records
- Shift Allocation
- Attendance
- Department Information

---

### 📑 Reports

Generates business reports automatically.

Reports include:

- Daily Production Report
- Monthly Production Report
- Inventory Report
- Machine Downtime Report
- Employee Attendance Report

---

## 👥 Stakeholders

The following users interact with the proposed system.

| User | Responsibilities |
|------|------------------|
| Plant Manager | Monitor production and reports |
| Production Supervisor | Manage production batches |
| Machine Operator | Update production status |
| Store Manager | Manage inventory |
| Maintenance Engineer | Handle machine servicing |
| HR | Employee records and attendance |
| Management | Business insights and analytics |

---

## ✅ Expected Benefits

- Centralized business data
- Reduced paperwork
- Faster report generation
- Better inventory tracking
- Improved maintenance planning
- Better communication between departments
- Increased operational efficiency
  # 🏗️ System Design

## Software Architecture

The proposed system follows a **3-tier architecture**, where the presentation layer communicates with the backend through REST APIs, and the backend manages all business logic and database operations.

```mermaid
flowchart TD

U[Users]

subgraph Client Layer
U
end

U --> A

subgraph Presentation Layer
A[React Web Application]
end

A -->|REST APIs| B

subgraph Business Layer
B[Java Spring Boot]

B --> S1[Authentication Service]
B --> S2[Production Service]
B --> S3[Inventory Service]
B --> S4[Maintenance Service]
B --> S5[Employee Service]
B --> S6[Reporting Service]
end

S1 --> DB
S2 --> DB
S3 --> DB
S4 --> DB
S5 --> DB
S6 --> DB

subgraph Database Layer
DB[(MySQL Database)]
end
```

---

# 👤 Use Case Diagram

The following diagram shows how different users interact with the system.

```mermaid
flowchart LR

Manager((Plant Manager))
Supervisor((Supervisor))
Operator((Operator))
Store((Store Manager))
HR((HR))
Maintenance((Maintenance Engineer))

System[Manufacturing Management System]

Manager --> System
Supervisor --> System
Operator --> System
Store --> System
HR --> System
Maintenance --> System

System --> UC1(View Dashboard)
System --> UC2(Manage Production)
System --> UC3(Manage Inventory)
System --> UC4(Update Attendance)
System --> UC5(Schedule Maintenance)
System --> UC6(Generate Reports)
```

---

# 🗄️ Entity Relationship Diagram

```mermaid
erDiagram

EMPLOYEE {
int employee_id
string name
string department
string role
}

MACHINE {
int machine_id
string machine_name
string status
}

PRODUCTION {
int batch_id
date production_date
int quantity
string status
}

INVENTORY {
int item_id
string item_name
int quantity
}

MAINTENANCE {
int maintenance_id
date maintenance_date
string issue
}

REPORT {
int report_id
date generated_on
string report_type
}

EMPLOYEE ||--o{ PRODUCTION : manages

MACHINE ||--o{ PRODUCTION : used_in

MACHINE ||--o{ MAINTENANCE : requires

PRODUCTION ||--o{ REPORT : generates

INVENTORY ||--o{ PRODUCTION : supplies
```

---

# 🔄 Activity Diagram

```mermaid
flowchart TD

Start([Start])

Start --> Login

Login --> Dashboard

Dashboard --> Choice{Select Module}

Choice --> Production

Choice --> Inventory

Choice --> Maintenance

Choice --> Reports

Production --> Save

Inventory --> Save

Maintenance --> Save

Reports --> View

Save --> Logout

View --> Logout

Logout --> End([End])
```

---

# 🚀 Deployment Diagram

```mermaid
flowchart TD

User[User Browser]

Internet((Internet))

Frontend[React Application]

Backend[Spring Boot Server]

Database[(MySQL)]

User --> Internet

Internet --> Frontend

Frontend --> Backend

Backend --> Database
```

---

## 📌 Design Approach

The proposed solution follows a modular architecture where each business function is implemented independently. This makes the application easier to maintain, extend, and test. Communication between the frontend and backend takes place through REST APIs, while all business data is stored in a centralized relational database.

The design allows future enhancements such as mobile applications, barcode integration, IoT-enabled machine monitoring, and predictive maintenance without major architectural changes.
