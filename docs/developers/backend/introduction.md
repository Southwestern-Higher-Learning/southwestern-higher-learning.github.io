# Introduction to the Backend

## Development

There are multiple parts to the backend, mainly the FastAPI server and PostgreSQL database. FastAPI utilizes TortoiseORM to interact with the database. Docker was used to easily develop the application.

### FastAPI
FastAPI is an asynchronous, Python web framework. It provides various tools to develop RESTful APIs in a timely manner. For example, it provides serialization, deserialization, and a specific `/docs` route that lists all of the method and endpoints available for the frontend to refer to.

### TortoiseORM
TortoiseORM queries and manages the PostgreSQL database. It's compatible with MySQL and SQLite as well, but Postgres is just better.

### PostgreSQL
PostgreSQL is not a strict requirement. However, TortoiseORM (paired with aerich) generates migrations files, which are a series of SQL commands, to set up the database. These migration files are specific to PostgreSQL.

### Docker
Docker with Docker Compose was used to ease development of this project. Docker allows the creation of containers which are parts of an application. In this project, there was a Docker container for the FastAPI server and one for Cloud SQL Proxy. There are able to connect with each other through a Docker specific network. While the server and database were in separate containers, they were able to communicate as if they were on the same exact machine.

### Google Calendar API
The Google Calendar API was used to get a tutor's schedule and add attendees to a specific event. To achieve this, we have each user log in with their Google accounts through OAuth2, and ask permission to read and update their calendar.

## Deployment

For this project, we used Google Cloud Platform's Cloud Run and Cloud SQL.

### Cloud Run

Cloud Run allows a Docker image to be deployed. This allows Cloud Run to easily make more instances of an application and balance requests between them. This is cost efficient as you only pay for what you use. We could use other services with GCP such as App Engine, but that stays on 24/7 whereas Cloud Run can shut down instances as the load decreases.


!!! info
    You can use any server that supports Docker to host the backend server. But the instructions here will be specific to Cloud Run.

### Cloud SQL

Since we were using GCP with free credits, we decided to use Cloud SQL for our PostgreSQL server. 