# Docker
- `docker-compose up --build -d`: rebuild all containers

## Import an SQL file into a Postgres Docker Container
- `docker cp db-to-import.sql postgres-container:/db-to-import.sql`: copy the file to the root of the container
- `docker exec -i postgres-container -U db-user -d db-name -f /db-to-import.sql`: import the sql file into the database (it MUST exist already and be empty)
