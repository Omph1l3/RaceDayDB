# RaceDay - Event Management System

## Project Overview

RaceDay is a full-stack event management system designed specifically for the South African road running, walking, and cycling community. The platform enables Event Organisers to create and manage events, define categories, and capture participant results, while Participants can browse events, enrol, and track their personal performance history.

---

## Table of Contents

- [Project Overview](#project-overview)
- [Features](#features)
- [Technologies Used](#technologies-used)
- [Roles](#roles)
- [Project Structure](#project-structure)
- [Part 1: System Planning and Database](#part-1-system-planning-and-database)
  - [ERD](#erd)
  - [API Endpoint Plan](#api-endpoint-plan)
  - [SQL Database Script](#sql-database-script)
- [CI/CD Pipeline](#cicd-pipeline)
- [Video Presentation](#video-presentation)
- [Setup Instructions](#setup-instructions)
- [References](#references)

---

## Features

### Part 1 (Completed)
- ✅ Entity Relationship Diagram (ERD) with 7 entities
- ✅ Comprehensive API Endpoint Plan with 25+ endpoints
- ✅ SQL Database Script with full schema, constraints, and seed data
- ✅ CI/CD validation workflow
- ✅ 20+ meaningful commits

### Part 2 (In Progress)
- 🚧 RESTful API with ASP.NET Core Web API
- 🚧 Role-based authentication and session management
- 🚧 Entity Framework Core with Code-First approach
- 🚧 Swagger integration
- 🚧 Unit testing with xUnit
- 🚧 GitHub Actions CI/CD

### Part 3 (Planned)
- 🚧 MVC Web Application
- 🚧 Azure Blob Storage integration
- 🚧 Docker containerisation
- 🚧 Role-specific interfaces

---

## Technologies Used

| Category | Technologies |
|----------|--------------|
| **Backend** | ASP.NET Core Web API, C#, Entity Framework Core |
| **Database** | SQL Server (SSMS), Azure SQL |
| **Frontend** | ASP.NET Core MVC, Bootstrap 5 |
| **Authentication** | Session-based authentication with password hashing |
| **Cloud Services** | Azure Blob Storage |
| **Containerisation** | Docker |
| **Version Control** | Git, GitHub |
| **CI/CD** | GitHub Actions |
| **Testing** | xUnit, Moq |
| **API Documentation** | Swagger/OpenAPI |

---

## Roles

### 1. Organiser
- Create, edit, and delete events
- Manage event categories
- View all event enrolments
- Capture participant results (finish times and positions)
- Upload event banner images

### 2. Participant
- Create an account and log in
- Browse upcoming events
- Enrol in events by selecting a category
- View personal enrolment history
- Track personal results and performance
- Update profile and upload profile picture

---

## Project Structure

```
RaceDay/
├── docs/                           # Documentation (Part 1)
│   ├── ERD.png                     # Entity Relationship Diagram
│   ├── EndpointPlan.md             # API Endpoint Plan
│   └── RaceDayDB.sql               # SQL Database Script
├── src/
│   ├── RaceDay.API/                # Part 2 - RESTful API
│   │   ├── Controllers/
│   │   ├── Models/
│   │   ├── Data/
│   │   ├── Services/
│   │   ├── Middleware/
│   │   └── Program.cs
│   ├── RaceDay.Tests/              # Unit Tests
│   └── RaceDay.MVC/                # Part 3 - MVC Web Application
│       ├── Controllers/
│       ├── Views/
│       ├── Models/
│       └── wwwroot/
├── .github/
│   └── workflows/
│       └── ci.yml                  # GitHub Actions workflow
├── Dockerfile                      # Docker configuration
├── README.md                       # This file
└── .gitignore
```

---

## Part 1: System Planning and Database

### ERD

The Entity Relationship Diagram includes the following 7 entities:

| Entity | Description |
|--------|-------------|
| **Users** | Stores user accounts linked to roles (Organiser/Participant) |
| **Roles** | Lookup table for Organiser and Participant roles |
| **Events** | Stores event information (name, description, date, location, distance, type) |
| **Categories** | Stores age-based or distance-based categories |
| **EventCategories** | Junction table for many-to-many relationship between Events and Categories |
| **Enrolments** | Records Participants entering Events with a selected Category |
| **Results** | Stores Participant results (finish time, finishing position) |

**Relationships:**
- Users → Roles: Many-to-One
- Users → Enrolments: One-to-Many
- Users → Events: One-to-Many (Organiser creates events)
- Events → Enrolments: One-to-Many
- Events → EventCategories: One-to-Many
- Categories → EventCategories: One-to-Many
- Enrolments → Results: One-to-One
- Enrolments → Categories: Many-to-One

The ERD is available at: [`docs/ERD.png`](docs/ERD.png)

### API Endpoint Plan

The system exposes **25+ endpoints** organised by resource:

| Resource | Endpoints |
|----------|-----------|
| **Authentication** | Register, Login |
| **User Profile** | Get, Update, Upload Picture |
| **Events** | CRUD operations, Get with filters, Upload Banner |
| **Categories** | CRUD operations |
| **Event Categories** | Add/Remove category from event |
| **Enrolments** | Get, Create, Update status, Get by event |
| **Results** | Get my results, Get event results, Create, Update, Delete |

Each endpoint includes:
- HTTP Method
- Route
- Description
- Role Required (Public, Any Logged-in, Organiser, Participant)
- Request Body
- Expected Response (success and failure codes)

Full plan available at: [`docs/EndpointPlan.md`](docs/EndpointPlan.md)

### SQL Database Script

The SQL script (`docs/RaceDayDB.sql`) includes:

1. **Database Creation**: `CREATE DATABASE RaceDayDB`
2. **Table Creation**: 7 tables with all constraints
   - Primary Keys, Foreign Keys, UNIQUE, NOT NULL, DEFAULT, CHECK constraints
3. **Indexes**: Performance optimisation
4. **Seed Data**:
   - 2 Organisers and 2 Participants
   - 3 Events (Soweto Marathon, Cape Town Cycle Tour, Two Oceans Marathon)
   - 6 Categories (Age-based and Distance-based)
   - Event-Category links
   - Sample Enrolments and Results

**Verification Queries** are included to validate the database setup.

---

## CI/CD Pipeline

GitHub Actions workflow (``.github/workflows/ci.yml`) is configured to:

- **Trigger**: On push to `main` and `develop` branches, and pull requests to `main`
- **Part 1 Validation**: Validates repository structure:
  - Checks `/docs` folder exists
  - Checks ERD file exists (PNG or PDF)
  - Checks Endpoint Plan exists (MD or PDF)
  - Checks SQL script exists
  - Validates SQL script contains `CREATE TABLE` statements
- **Build Status**: Green build required for all checks to pass

**Current Status**: ✅ [![CI Status](https://https://github.com/Omph1l3/RaceDayDB)

---

## Setup Instructions

### Prerequisites

- [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms)
- [Git](https://git-scm.com/downloads)
- [.NET SDK 6.0 or later](https://dotnet.microsoft.com/download) (for Parts 2 and 3)

### Step 1: Clone the Repository

```bash
git clone https://github.com/yourusername/RaceDay.git
cd RaceDay
```

### Step 2: Set Up the Database

1. Open SQL Server Management Studio (SSMS)
2. Connect to your SQL Server instance
3. Open the script: `docs/RaceDayDB.sql`
4. Execute the script (F5) to create and populate the database

**Expected Output**: A clean database with all tables, constraints, and seed data.

### Step 3: Verify Database

Run the verification queries at the end of the script to confirm:
- All 7 tables are created
- Roles, Users, Categories, Events, Enrolments, and Results are populated

### Step 4: Part 2 Setup (Coming Soon)

```bash
cd src/RaceDay.API
dotnet restore
dotnet run
```

### Step 5: Part 3 Setup (Coming Soon)

```bash
cd src/RaceDay.MVC
docker build -t raceday-mvc .
docker run -p 8080:80 raceday-mvc
```

---

## Commit History

**Minimum 20 meaningful commits** made for Part 1. The commit history demonstrates progressive development:

- Initial repository setup
- Adding ERD design
- Creating API endpoint plan
- Writing SQL database script
- Setting up CI/CD workflow
- Testing and validation fixes

View full commit history: [GitHub Commits](https://github.com/yourusername/RaceDay/commits/main)

---

## References

- W3Schools (2025). *W3Schools.Com*. Available at: https://www.w3schools.com/sql/ [Accessed 28 Aug. 2026].
- Bootstrap (2023). *Get started with Bootstrap*. Available at: https://getbootstrap.com/docs/5.3/getting-started/introduction/ [Accessed 28 Aug. 2026].
- chcomley (2026a). *Azure Boards documentation*. Microsoft Learn. Available at: https://learn.microsoft.com/en-us/azure/devops/boards/ [Accessed 28 Aug. 2026].
- chcomley (2026b). *Azure DevOps documentation*. Microsoft Learn. Available at: https://learn.microsoft.com/en-us/azure/devops/ [Accessed 28 Aug. 2026].
- dimitri-furman (2024). *Monitoring and performance tuning — Azure SQL Database & Azure SQL Managed Instance*. Microsoft Learn. Available at: https://learn.microsoft.com/en-us/azure/azure-sql/database/monitor-tune-overview [Accessed 28 Aug. 2026].
- IBM (2024). *Think topics | IBM*. Available at: https://www.ibm.com/think/topics/agile [Accessed 28 Aug. 2026].
- pauljewellmsft (2023). *Get started with Azure Blob Storage and .NET — Azure Storage*. Microsoft Learn. Available at: https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blob-dotnet-get-started [Accessed 3 Sept. 2026].
- scrumguides (2025). *Home | Scrum Guides*. Available at: https://scrumguides.org/ [Accessed 28 Aug. 2026].

---

## Contact

**Student Name**: [Otlotleng Mabiletsa]  
**Student Number**: [ST10478180]  
**Module**: Programming 2B (PROG6212)  
**Year**: 2026

---

## License

This project is submitted for academic assessment purposes as part of The IIE's Programming 2B module. All rights reserved.

---

*Last Updated: 04 September 2026*
