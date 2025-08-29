# MySQL + Adminer Course Environment

This repository contains a ready-to-use MySQL + Adminer setup using Docker, to be used in the database-related courses at Iscte-Instituto Universitário de Lisboa.
It allows you to create databases, run SQL scripts, and import/export CSV files without installing MySQL locally.
Works on **Windows** and **macOS** (Intel or Apple Silicon).

---

## 1. Install Prerequisites

1. **Docker Desktop**
   - [Download here](https://www.docker.com/products/docker-desktop/)
   - **Windows**: make sure WSL2 backend is enabled during installation.
   - **macOS**: install as a standard application.

2. **Git**  
   - [Download here](https://git-scm.com/downloads)  
   - Alternatively, you can just download this repo as a ZIP.

---

## 2. Setup

1. **Clone this repository** (or download as ZIP and extract):  
   ```bash
   git clone https://github.com/antoniolopes/docker-compose-db-course.git
   cd docker-compose-db-course
   ```

2. **Create your `.env` file** based on the example:  
   ```bash
   cp .env.example .env
   ```
   Edit `.env` and set your passwords:
   ```bash
   MYSQL_ROOT_PASSWORD=your_root_password
   MYSQL_DATABASE=course_db
   MYSQL_USER=student
   MYSQL_PASSWORD=your_student_password
   ```

3. **Start the containers**:  
   ```bash
   docker compose up -d
   ```
   or 
   ```bash
   docker compose -f docker-compose-adminer.yml up -d
   ```

4. Wait a few seconds for MySQL to initialize.
   Access Adminer at:  
   **http://localhost:8182**  
   - **System:** MySQL  
   - **Server:** mysql  
   - **Username:** student (or root)  
   - **Password:** from `.env`  
   - **Database:** course_db (or any you create)

---

## 3. File Structure

```
.
├── docker-compose.yml          # Docker services definition
├── .env                        # Your passwords (NOT committed to git)
├── mysql-data/                 # MySQL data files (auto-created, persistent)
└── README.md                   # This file
```

- **`mysql-data/`**: Actual MySQL binary data. Persisted between runs. Delete to reset DB.

---

## 4. Stopping and Resetting

- **Stop containers** (keep data):  
  ```bash
  docker compose down
  ```
  or 
  ```bash
  docker compose -f docker-compose-adminer.yml down
  ```

- **Stop containers and delete all data**:  
  ```bash
  docker compose down
  rm -rf mysql-data
  ```

---

## 5. Troubleshooting

- **Port in use**: Change the `ports` mapping in `docker-compose.yml`.
- **MySQL connection refused**: Wait for the container to finish initializing, then retry.
