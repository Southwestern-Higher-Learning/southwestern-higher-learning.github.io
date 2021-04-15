# Local Setup

Now on to actually setting up the backend project for local development.

## Docker

Docker with Docker Compose is used to easily develop as we can launch our services with one command. 

Follow the instructions to download Docker here: https://docs.docker.com/get-docker/

Verify you have Docker and Docker Compose installed by running:

```sh
docker --version

docker-compose --version
```

## Configuration

Before starting the services, we need to configure environment variables and our database.

### Database Setup
There are a couple of options that you could personally use to setup a database. Two ways implemented in this project is Cloud SQL and a standard PostgreSQL database, both described in the `docker-compose.yml` file. 

#### Cloud SQL
To setup Cloud SQL, you first need to setup a database on GCP and create service credentials that access it. 

Follow instructions to setup the database here: https://cloud.google.com/sql/docs/postgres/quickstart

Create a database called `tutorappdev`

Next create a service account by following these instructions: https://cloud.google.com/sql/docs/mysql/connect-admin-proxy#create-service-account

!!! info
    You can just follow the "Create a Service Account" instructions

Move the private key file to the root directory of the project, at the same level as the `docker-compose.yml` file and rename it to `tutorappcreds.json`.

In `docker-compose.yml`, go to the `cloud-sql-proxy` section and look at the command. Change the `-instances...` to the following format based on your project ID, database ID and database location: `-instances=s<project ID>:<location>:<database ID>=tcp:0.0.0.0:5432`.

#### Local Database
If you would like to run the d
