# TutorConnect Codebase Documentation

TutorConnect is a full-stack web application designed to connect students with tutors. Users can register as either a Student (Học viên) or a Tutor (Gia sư), post learning requests, apply for teaching jobs, and manage classes.

## Tech Stack

- **Backend**:
  - Language: Java 17+
  - Framework: Spring Boot 3.x
  - Build Tool: Maven
  - Security: Spring Security + JWT
  - Database: MySQL (configured via `application.properties`)
  - Integration: REST APIs, Lombok, Hibernate/JPA
- **Frontend**:
  - Framework: React (with Vite)
  - Language: TypeScript
  - Styling: Vanilla CSS + Tailwind CSS (Lucide-react icons)
  - State Management: Zustand (Auth Store)
  - Data Fetching: React Query (@tanstack/react-query)
  - Routing: React Router DOM

---

## Project Structure

### Backend (`/BE`)

The backend follows a standard Spring Boot layered architecture:
- `com.btljava.GiaSu.entity`: JPA Entities representing database tables (`TaiKhoan`, `GiaSu`, `HocVien`, `UngTuyen`, `YeuCauTimGiaSu`, `LopHoc`).
- `com.btljava.GiaSu.repository`: Spring Data JPA repositories for DB access.
- `com.btljava.GiaSu.service`: Business logic layer.
- `com.btljava.GiaSu.controller`: REST Controllers handling API endpoints (prefixed with `/api`).
- `com.btljava.GiaSu.dto`: Data Transfer Objects for request/response bodies.
- `com.btljava.GiaSu.config`: Configuration classes (Security, CORS).

### Frontend (`/FE`)

The frontend is a modern SPA organized by feature:
- `src/api`: API client configuration (`apiClient`).
- `src/components`: Reusable UI components (Modals, Navbars, PrivateRoute).
- `src/hooks`: Custom React Query hooks (`useAuth`, `useTutor`, `useStudent`).
- `src/layouts`: Layout components for different user roles (`StudentLayout`, `TutorLayout`).
- `src/pages`: Main view components organized by role:
  - `auth/`: Login and Register pages.
  - `student/`: Student Dashboard, Search Tutors, Tutor Detail, My Requests.
  - `tutor/`: Tutor Dashboard, Job List, My Applications, Invitations.
- `src/store`: Zustand stores for global state (e.g., `authStore`).
- `src/types`: TypeScript interfaces for the entire app.

---

## Core Workflows

### 1. Authentication
- **Flow**: User logs in -> `AuthService` validates credentials -> Generates JWT -> FE stores JWT and user info in Zustand `authStore`.
- **API**: `POST /api/auth/login`

### 2. Recruitment (Apply for Job)
- **Flow**:
  1. Student posts a request (`YeuCauTimGiaSu`).
  2. Tutor views the job list and clicks "Ứng tuyển".
  3. `useTutor` hook calls the backend `TuyenDungController.ungTuyen` endpoint.
  4. Application record is created (`UngTuyen`) with status `CHỜ HỌC VIÊN XÁC NHẬN`.
  5. Student views candidates and approves/rejects.
- **Key API**: `POST /api/tuyen-dung/ung-tuyen`

### 3. Class Management
- **Flow**: When a student approves an application, a `LopHoc` record is created. Both parties can then view the class in their "My Classes" section.

---

## Key Data Models

| Entity | Description |
| :--- | :--- |
| `TaiKhoan` | Base user account (Email, Password, Role). |
| `GiaSu` | Additional profiles for Tutors (Education, Experience). |
| `HocVien` | Profile for Students. |
| `YeuCauTimGiaSu` | A specific learning request posted by a student. |
| `UngTuyen` | Represents a tutor's application to a job request. |
| `LopHoc` | A confirmed teaching relationship between a tutor and student. |

---

## Environment Variables

- **Frontend (`.env`)**:
  - `VITE_API_BASE_URL`: Base URL for the backend API (e.g., `http://localhost:8080/api`).

- **Backend (`application.properties`)**:
  - Database connection details (URL, Username, Password).
  - JWT Secret and Expiration times.
