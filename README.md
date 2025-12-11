

## Description  
This project is a complete solution for managing employees within **TalensPlus**, replacing the manual Excel process used previously by the HR department.

The system is composed of:

### ✔ Web Application (HR Administrator)  
The HR administrator can:

- Manage employees (create, edit, list, delete).  
- Associate employees with departments and job roles.  
- Import employees directly from an Excel file:
  - Validate structure and data.
  - Insert or update employee records.
- Generate Employee Resume (Hoja de Vida) as **PDF**, including:
  - Personal data  
  - Job information (position, salary, hire date, status)  
  - Education level  
  - Professional profile  
  - Department  
  - Contact data  

### ✔ Dashboard with AI Assistant  
The system includes a dashboard containing:

- Total number of employees  
- Number of employees on vacation  
- Additional metrics (e.g., active employees, employees by department, etc.)  
- Natural Language Assistant powered by **AI (Gemini / GPT / Groq / Claude, etc.)**  
  - Interprets natural language questions such as:  
    - “¿Cuántos empleados están inactivos?”  
    - “¿Cuántos auxiliares hay?”  
    - “¿Cuántos empleados hay en Tecnología?”  
  - The AI helps interpret the question, and **the system executes the real query against PostgreSQL.**  
  - No invented or hallucinated values.

### ✔ REST API (Employee Portal)  
Allows employees to access and manage their own info.

#### Public Endpoints  
- List departments  
- Employee self-registration (includes **real SMTP welcome email**)  
- Login → returns **JWT**

#### Protected Endpoints  
- Get employee data (based on JWT, no document in URL)  
- Download personal Resume (PDF)

---

## Technologies Used

- **C# / .NET 8**
- **ASP.NET Core MVC**
- **ASP.NET Core Identity** (admin + employee auth)
- **Entity Framework Core**
- **PostgreSQL**
- **JWT Authentication**
- **AI Integration** (Gemini / GPT / Claude / HuggingFace / Groq)
- **EPPlus / ClosedXML (Excel processing)**
- **iTextSharp / QuestPDF / PDFSharp (PDF Generation)**
- **Docker & Docker Compose**
- **Repository Pattern / Clean Architecture**

---

## Prerequisites

- [.NET 8 SDK](https://dotnet.microsoft.com/download/dotnet/8.0)  
- PostgreSQL 14+  
- Docker & Docker Compose  
- Any IDE (VS 2022 / Rider / VS Code)  
- SMTP provider (Gmail App Passwords recommended)

---

## Installation

1. Clone the repository:

```bash
git clone <https://github.com/TuUsuario/TalentoPlus-EmployeeSystem.git>
cd TalentoPlus-EmployeeSystem
```

2. Restore NuGet packages:

```bash
dotnet restore
```

---

## Configure Environment Variables  
Create a `.env` file in the root or set the variables in your system:

```env
# Database
POSTGRES_HOST=localhost
POSTGRES_DB=talentoplusdb
POSTGRES_USER=postgres
POSTGRES_PASSWORD=yourPassword

# Connection String
CONNECTION_STRING=Host=localhost;Database=talentoplusdb;Username=postgres;Password=yourPassword;

# JWT
JWT_SECRET=YourSuperSecretKey
JWT_ISSUER=TalentoPlus
JWT_AUDIENCE=TalentoPlusUsers

# SMTP
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_EMAIL=yourEmail@gmail.com
SMTP_PASSWORD=yourAppPassword
```

---

## Configure Connection String in `appsettings.json` (optional)

```json
{
  "ConnectionStrings": {
    "DefaultConnection": "${CONNECTION_STRING}"
  },
  "JWT": {
    "Secret": "${JWT_SECRET}",
    "Issuer": "${JWT_ISSUER}",
    "Audience": "${JWT_AUDIENCE}"
  },
  "SMTP": {
    "Host": "${SMTP_HOST}",
    "Port": 587,
    "Email": "${SMTP_EMAIL}",
    "Password": "${SMTP_PASSWORD}"
  }
}
```

---

## Database Migration

```bash
dotnet ef database update
```

---

## Run the Solution (Without Docker)

### Web App
```bash
cd WebApp
dotnet run
```

### API
```bash
cd EmployeeAPI
dotnet run
```

---

## Run Entire System With Docker Compose

```bash
docker compose up --build
```

This will start:

- PostgreSQL  
- Web Application  
- API REST  

---

## Access the Applications

### Web Application (Admin)
```
http://localhost:5100
```

### REST API Documentation (Swagger)
```
http://localhost:5200/swagger
```

---

## Default Credentials  
(Replace with final testing credentials)

```
Admin Email: admin@talentoplus.com
Password: Admin123*
```

---

## Usage Overview

### ✔ As Administrator  
- Manage employees (CRUD)  
- Upload Excel and sync database  
- Generate employee resumes (PDF)  
- View dashboard with metrics and AI chat  
- Ask natural-language questions to filter or search employee data  

### ✔ As Employee (via API)  
- Self-register  
- Login to obtain JWT  
- View own information  
- Download personal PDF resume  

---

## Tests

The solution includes:

- **2+ unit tests** (domain & validation logic)  
- **2+ integration tests**  
  - API endpoints  
  - Database operations  

Run tests:

```bash
dotnet test
```

---

## Features Summary

- Centralized employee data  
- Excel import with validation  
- Secure authentication (Identity + JWT)  
- Real email notifications  
- PDF generation  
- AI-driven natural language queries  
- Scalable architecture (Repository / Clean Architecture)

---

## Repository Link
👉 **https://github.com/TuUsuario/TalentoPlus-EmployeeSystem**
