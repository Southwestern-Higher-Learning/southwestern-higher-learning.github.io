# Deploying the Backend

There are two main things needed to deploy the backend, a server to host the FastAPI application and a PostgreSQL database. Therefore, you can use any platform or service such as Heroku, Digital Ocean, AWS, GCP, private VPS, Azure, etc. 

There is a GitHub Actions workflow in `.github/workflows/main.yml` that will automate the process of building the production Dockerfile and deploy it to Google Cloud Run. This will be helpful to reference to as there are a series of commands that deploy it to Google Cloud Run. 

This guide will go through deploying the backend to Google Cloud Platform.

## Pushing Docker Imager to GCP

First, we need to push the production docker image to GCP for Cloud Run to use. Download the gcloud CLI tool by following the directions here: [https://cloud.google.com/sdk/docs/quickstart](https://cloud.google.com/sdk/docs/quickstart). Ensure that you selected the project that you used in the Google Setup when setting up Google API. Run the command `gcloud auth configure-docker`. Next, we need to establish where to push the built Docker image to. The URL format will be the following (will be referenced as `<GCR_URL>`):

```
gcr.io/<GCP_PROJECT_ID>/<CUSTOM_NAME>:latest
```

Where `<GCP_PROJECT_ID>` will be your specific project ID and `<CUSTOM_NAME>` can be anything that you want such as "backend". Next, run the following command in the root directory of the backend. 

```
docker build \
  --tag <GCR_URL> \
  --file ./project/Dockerfile.prod \
  "./project"
```

Wait for the Docker image to build and then run:

```
docker push <GCR_URL>
```

Now the production Docker image should be pushed to GCP, where we will see it when we setup Google Cloud Run.

## VPC Setup

Before going into the database and backend setup, we need to create a Virtual Private Cloud network so that the Cloud Run instances can communicate to the database using a standard TCP connection with the database's private address that we will see later on. 

Go to the "VPC network" section (you may have to enable Compute Engine API) and go to the "Serverless VPC access" section (again, enabling the specific API). Once the specific API is enabled, click on the "Create connector" button. Give the VPC a name, set it to a region that is convenient. Select the "Subnet" to "Custom IP range", set the "IP range" to "10.8.0.0" and click on "Create."

## Database Setup

Go to the "SQL" section on GCP and click on "Create instance" (or similar) and choose PostgreSQL. Give the database instance a name, a password you can remember and an appropriate region.

!!! info
    Cloud SQL databases can be costly, you can select a "Lightweight" database by going to "Machine type" under "Customize your instance" under the initial setup page. You can change this later.

Click on "Create" and wait a while for the database instance to be created. Once it is created, go to the "Connections" section. Enable "Private IP" and select "default" as your network and then click "Save". 

Now that we have it all setup, we should take note of the new database URL that you will use later. On the "Overview" page take note of the "Private IP". The database URL will be in the following format:
```
postgres://postgres:<password>@<private_ip>/postgres
```

## Cloud Run Setup

Go to the GCP console and go to the Cloud Run section. Up at the top, click on "Create service". Give the service a name and leave the "Deployment platform" as is, but use the "Region" dropdown to select an ideal region. 

In the next step, select a container image using the "Select" button. You should find that there is a dropdown under the GCR URL you pushed the Docker image to in the previous step. Click on the dropdown and select the latest image. 

Stay in the same step and go into "Advanced settings." Under "Container" > "Capacity", choose an appropriate size of RAM and CPUs, but it will fine if you leave it as it is. Under "Container" > "Autoscaling", leaving the "Minimum" at 0 will cause the server to have a long start up time, change this to 1 if you want to have a server running at all times.

Under the "Variables" tab, you want to add every variable you have in your local `.env` file. Fill out the variable name and its value appropriately. You will want to change your DATABASE_URL to the one above in Cloud SQL setup.

Under the "Connections" tab, under "VPC Connector", select the connector as "default".

In the next step, leave "Ingress" as is and set the "Authentication" to "Allow unauthenticated ..." and click on create.

Once you the service is setup completely, you should see a "URL" near the name of the service. Go to the `/docs` of that URL and see if it is running. 

!!! info
    Remember to add the URL to the Google OAuth API