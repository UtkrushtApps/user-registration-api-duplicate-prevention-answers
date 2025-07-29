# Solution Steps

1. Initialize a FastAPI project with an 'app' folder containing main.py, models.py, schemas.py, and database.py.

2. Set up SQLAlchemy database connection in app/database.py and configure it to read the DATABASE_URL from environment variables (defaulting to the PostgreSQL Docker service).

3. Define a User model in app/models.py with an integer primary key 'id' and a string 'email', setting both unique and nullable constraints on email.

4. Create corresponding Pydantic schemas in app/schemas.py for user input (UserCreate) and output (User).

5. Configure Alembic to use the SQLAlchemy Base and generate an initial migration script (alembic/versions/0001_create_users_table.py) to create the 'users' table with a unique constraint on email.

6. Implement the /register endpoint in app/main.py: accept a UserCreate, attempt to insert it, and on IntegrityError (duplicate email), return status 400 with a suitable error message.

7. Write a Dockerfile to build and run the FastAPI app along with requirements.txt.

8. Create a docker-compose.yml file to set up both the 'db' (PostgreSQL) and 'web' (FastAPI app) services, wiring DATABASE_URL, ports, and volumes.

9. Make sure the FastAPI app's CMD will run Alembic migrations at container start, ensuring the database schema is ready.

10. Test the API by running 'docker compose up', making a POST to /register with an email, and verifying duplicate emails are rejected with a clear error.

