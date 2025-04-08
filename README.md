# 🐘 PostgREST + PostgreSQL + pgAdmin (Docker Compose Setup)

This project runs a local development environment with:

- **PostgreSQL** – database server
- **PostgREST** – instant REST API over your Postgres tables
- **pgAdmin** – web-based database admin panel

---

## 🚀 How to Run

```bash
docker-compose up
```

### Access the services:


PostgREST: http://localhost:3000

pgAdmin: http://localhost:5050

```bash
Email: nahid@example.com
Password: admin123
```

## 🧑‍💻 Add PostgreSQL Server to pgAdmin

Once logged into **pgAdmin**:

1. Click **"Add New Server"**  
   *(Right-click on "Servers" in the left sidebar ➜ Create ➜ Server)*

2. In the **"General"** tab:
   - **Name**: `Local DB`

3. In the **"Connection"** tab:
   - **Host name/address**: `db`
   - **Port**: `5432`
   - **Username**: `postgres`
   - **Password**: `postgres`
   - ✅ **Save Password**

4. Click **Save**

You’ll now see your PostgreSQL instance listed in the left sidebar under *"Servers"*.

## 📬 Test the PostgREST API

Once you’ve created the `todos` table and granted permissions, you can test the API using Postman, `curl`, or your browser.

### Example Table

```sql
CREATE TABLE todos (
  id SERIAL PRIMARY KEY,
  task TEXT NOT NULL,
  done BOOLEAN DEFAULT false
);

GRANT USAGE ON SCHEMA public TO postgres;
GRANT SELECT, INSERT, UPDATE, DELETE ON todos TO postgres;
```


## 📡 API Endpoints

You can interact with the `todos` table using the following PostgREST API endpoints.

---

### `GET /todos` – List all tasks

```bash
curl http://localhost:3000/todos
```

### `POST /todos` – Create a new task

```bash
curl -X POST http://localhost:3000/todos \
     -H "Content-Type: application/json" \
     -d '{"task": "Buy milk", "done": false}'
```

### `PATCH /todos?id=eq.1` – Update task with ID 1

```bash
curl -X PATCH "http://localhost:3000/todos?id=eq.1" \
     -H "Content-Type: application/json" \
     -d '{"done": true}'
```

### `DELETE /todos?id=eq.1` – Delete task with ID 1
```bash
curl -X DELETE "http://localhost:3000/todos?id=eq.1"
```