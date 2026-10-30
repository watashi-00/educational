# educational
Java 21, Spring Boot, Prometheus, Grafana, Relational Database (pgress)

# roles
- Education Manager
- Director
- Director 2nd
- Teacher
- Responsible
- Student

# features
- OCR/HTR attachments
- Offline Clients and local infrastructure
- CRUD all roles
- Login (user/mail/org-mail/student-id) + password
- Send notifications and messages to all or single roles/accounts

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
    classDef gateway fill:#7c3aed,color:#fff,stroke:#6d28d9
    classDef local fill:#0f766e,color:#fff,stroke:#115e59
    classDef client fill:#475569,color:#fff,stroke:#334155

    class PS primary
    class EP gateway
    class LS1,LS2,LSN local
    class C1,C2,CN,LC1,LC2,LCN client
```
