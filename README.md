clone this repository

install and setup docker

run docker compose up -d to run the app


you can access services at(ensure these ports are not pre-occupied)-

Frontend:localhost:3000
Backend:localhost:8080
Database:localhost:5432


check the logs to troubleshoot using

overall:
docker-compose logs

indiviual services:
docker-compose logs frontend
docker-compose logs backend
docker-compose logs db
