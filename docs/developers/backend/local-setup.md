# Local Setup

Now on to actually setting up the backend project for local development.

## Docker

Docker with Docker Compose is used to easily develop as we can launch our services with one command. 

Follow the instructions to download Docker here: <a href="https://docs.docker.com/get-docker/">https://docs.docker.com/get-docker/</a>

Verify you have Docker and Docker Compose installed by running:

```sh
docker --version

docker-compose --version
```

## Configuration

Before starting the services, we need to configure environment variables and our database.

### Database Setup
There are a couple of options that you could personally use to setup a database. Two ways implemented in this project are Cloud SQL Proxy and a standard PostgreSQL database, both described in the `docker-compose.yml` file. 

#### Cloud SQL
To setup Cloud SQL, you first need to setup a database on GCP and create service credentials that access it. 

Follow instructions to setup the database here: <a href="https://cloud.google.com/sql/docs/postgres/quickstart" target="_blank">https://cloud.google.com/sql/docs/postgres/quickstart</a>

Create a database called `tutorappdev`

Next create a service account by following these instructions: <a href="https://cloud.google.com/sql/docs/mysql/connect-admin-proxy#create-service-account" target="_blank">https://cloud.google.com/sql/docs/mysql/connect-admin-proxy#create-service-account</a>

!!! info
    You can just follow the "Create a Service Account" instructions

Move the private key file to the root directory of the project, at the same level as the `docker-compose.yml` file, and rename it to `tutorappcreds.json`.

In `docker-compose.yml`, go to the `cloud-sql-proxy` section and look at the command. Change the `-instances...` to the following format based on your project ID, database ID and database location: `-instances=<project ID>:<location>:<database ID>=tcp:0.0.0.0:5432`.

#### Local Database
If you would like to run the database as a normal PostgreSQL database, you can easily switch from the proxy to local. In `docker-compose.yml`, you can comment out the `cloud-sql-proxy` by putting `#` at the beginning of each line. Then uncomment the `web-db` section, ensuring that each section is aligned appropriately. 

### Environment Variables

To configure the project, we need `.env` file in the same directory as the `docker-compose.yml` file. So create a new file and paste in the following:

```
GOOGLE_CLIENT_ID=
GOOGLE_PROJECT_ID=
GOOGLE_CLIENT_SECRET=
GOOGLE_REDIRECT_URIS=
GOOGLE_JS_ORIGINS=
TOP_DOMAIN="southwestern.edu"
DATABASE_URL=
```

Fill out each variable appropriately, with most of the information obtained from the Google setup. The URIs are expected to be an array so fill out the URIs and Origins like so:

```
GOOGLE_REDIRECT_URIS=["http://localhost:8080/auth/callback","http://localhost:8080/auth/swap"]
GOOGLE_JS_ORIGINS=[]
```

The `TOP_DOMAIN` variable only allows users of that domain to access Tutor App. For instance, if we had the email: `john@southwestern.edu` then that email will be allowed to log in with Google.

The `DATABASE_URL` varies based on the database process you followed, however it has the general format:

```
postgres://<username>:<password>@<ip address>:5432/<database>
```

If you followed the Cloud SQL Proxy fill it out like so:
```
postgres://<username>:<password>@cloud-sql-proxy:5432/tutorappdev
```

Otherwise with the Local Setup:
```
postgres://postgres:postgres@web-db:5432/postgres
```

## Starting the Project

To run the project use the following command:

```
docker-compose up --build
```

This will build the containers by downloading necessary components and start the FastAPI and database container.

Once you build once, you don't have to build again so you can instead run:

```
docker-compose up
```
