# Educational Management System

## Technology Stack

- Java 21, Spring Boot, PostgreSQL, Prometheus, Grafana

## System Roles

| Role | Description |
|---|---|
| Education Manager | Global institution management |
| Director | School administration |
| Director 2nd | Assistant school administration |
| Teacher | Academic management |
| Responsible | Student supervision |
| Student | Academic activities and personal information |

---

## System Features

Features available across the platform, subject to role-based access control (RBAC).

### Authentication & Authorization
- User authentication using username, email, institutional email or student ID.
- Password-based authentication.
- Role-Based Access Control (RBAC).
- Account and credential management.
- Session management.
- Permission and access scope enforcement.

### User & Role Management
- CRUD operations for users and roles.
- Account activation and deactivation.
- User-role association.
- Institutional account management.

### Communication & Notifications
- Send notifications to all users.
- Send notifications to specific roles.
- Send notifications to individual accounts.
- Internal messaging system.
- Targeted announcements.

### Attachments & Document Processing
- Attachment upload and management.
- Attachment metadata extraction and storage.
- OCR (Optical Character Recognition).
- HTR (Handwritten Text Recognition).
- Document indexing and processing.
- RAG (Retrieval-Augmented Generation) over authorized attachments.
- Document access control.

### Offline Infrastructure
- Offline-capable clients.
- Local infrastructure and local servers.
- Data synchronization between local and primary infrastructure.
- Synchronization conflict handling.
- Local data persistence.
- Connection and synchronization status monitoring.

### Monitoring & Observability
- Application metrics through Prometheus.
- Infrastructure monitoring.
- Performance monitoring.
- Grafana dashboards.
- Operational health monitoring.

---

## Role-Specific Features

Features and operations available exclusively or specifically to each role, according to its permissions and institutional scope.

### 1. Education Manager

Global institutional administration.

#### Institutional Management
- CRUD all roles and users.
- Manage institution settings and configurations.
- Manage academic years and educational periods.
- Manage schools and departments.
- Assign Directors to schools or departments.
- Manage global access policies and permissions.

#### Administration & Monitoring
- Manage global notifications and announcements.
- Access institution-wide reports and analytics.
- Monitor local infrastructure synchronization.
- Access global audit logs and activity history.

### 2. Director

School-level administration.

#### School Management
- Manage Teachers, Responsible and Students.
- Manage classes, grades and school groups.
- Assign Teachers to classes and subjects.
- Manage student enrollment and transfers.
- Manage academic schedules and calendars.

#### Academic Oversight
- Monitor student attendance and performance.
- Access school-wide academic reports.
- Manage school-specific documents and attachments.
- Access school activity logs.

#### Communication
- Send notifications to all school members.
- Send targeted notifications to specific roles or accounts.

### 3. Director 2nd

Delegated administrative operations.

#### School Administration
- Manage Teachers, Responsible and Students.
- Manage class assignments.
- Manage student enrollment.
- Manage academic schedules.
- Manage attendance records.

#### Academic Oversight
- Access academic reports and dashboards.
- Manage school documents and attachments.
- Assist with student transfers and registration.

#### Communication
- Send notifications to school members.
- Send targeted notifications to specific roles or accounts.

### 4. Teacher

Academic and classroom management.

#### Classroom Management
- Manage assigned classes and subjects.
- Manage academic activities and assignments.
- Create and manage assessments and exams.
- Register and manage student grades.
- Register and manage student attendance.

#### Student Monitoring
- Track individual student performance.
- Access academic history within assigned classes.
- Review assignment submissions.
- Provide feedback on submitted assignments.

#### Communication
- Send messages to Students and Responsible.
- Send class-wide announcements.

#### Educational Materials
- Upload educational materials and attachments.
- Manage class-specific learning resources.

### 5. Responsible

Student supervision and academic monitoring.

#### Student Monitoring
- View linked Students.
- Access academic grades and performance.
- View attendance records.
- Access assignments, activities and assessments.
- View academic schedules and calendars.

#### Communication
- Receive notifications about linked Students.
- Communicate with Teachers and Directors.
- Access school announcements.

#### Documents & Account
- View documents and attachments shared with them.
- Submit requested documents and attachments.
- Manage personal contact information.

### 6. Student

Personal academic management.

#### Academic Information
- View personal academic information.
- Access assigned classes and subjects.
- View grades and academic performance.
- View attendance records.
- Access personal academic history.

#### Activities & Assignments
- Access assignments and educational materials.
- Submit assignments and attachments.
- Track assignment deadlines.
- View submission status.

#### Communication
- Receive notifications and announcements.
- Communicate with Teachers.

#### Schedule
- View academic schedules and calendars.

---

## Infrastructure

```mermaid
flowchart TB
    subgraph PRIMARY["Primary Infrastructure"]
        PS["Primary Server"]
        EP["EntryPoint<br/>Gateway / Load Balancer"]
        PS <--> EP
    end

    subgraph DIRECT["Direct Client Access"]
        C1["Client 1"]
        C2["Client 2"]
        CN["Client N"]
    end

    subgraph LOCAL["Local Infrastructure"]
        LS1["Local Server 1"]
        LS2["Local Server 2"]
        LSN["Local Server N"]

        LC1["Local Clients"]
        LC2["Local Clients"]
        LCN["Local Clients"]

        LS1 --> LC1
        LS2 --> LC2
        LSN --> LCN
    end

    C1 <--> EP
    C2 <--> EP
    CN <--> EP

    EP <--> LS1
    EP <--> LS2
    EP <--> LSN

    LS1 -. "Synchronization" .-> PS
    LS2 -. "Synchronization" .-> PS
    LSN -. "Synchronization" .-> PS

    classDef primary fill:#2563eb,color:#fff,stroke:#1d4ed8
    classDef gateway fill:#7c3aed,color:#fff,stroke:#6d28d8
    classDef local fill:#0f766e,color:#fff,stroke:#115e59
    classDef client fill:#475569,color:#fff,stroke:#334155

    class PS primary
    class EP gateway
    class LS1,LS2,LSN local
    class C1,C2,CN,LC1,LC2,LCN client
```

---

## Access Control Principles

- Every operation must be validated against the user's assigned role and permissions.
- Access must be restricted to the user's institutional scope.
- Directors must only access their assigned schools.
- Teachers must only access their assigned classes and subjects.
- Responsible users must only access their linked Students.
- Students must only access their own academic records.
- Administrative permissions must support delegation and explicit scope restrictions.
- Sensitive operations must be recorded in audit logs.

## License

This project is licensed under the GNU Affero General
Public License v3.0 (AGPL-3.0).

Commercial licensing is available for organizations
requiring proprietary use, private modifications,
or alternative distribution terms.

For commercial licensing inquiries, contact:<br>
licensing@studiosync.com.br - routing mail<br>
nova2948@gmail.com          - personal
