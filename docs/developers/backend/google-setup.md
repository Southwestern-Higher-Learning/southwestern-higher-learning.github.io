# Google Setup

Before going in-depth about setting up the backend project, we need to setup the Google API service and get specific credentials that will be added to an `.env` file. 

## Initial Setup

You can use an existing project, or a new project, on Google Cloud Platform. Take note of the "Project ID" on the Dashboard page. 

## Setting Up OAuth2

Under APIs & Services, go to the OAuth consent screen section and follow the steps to create an "External" application.

## Getting Credentials

Go to the "Credentials" section. Near the top, click on "Create Credentials" and then on "OAuth Client ID". 

In the form, select the "Application Type" as "Web application" and then give it a nice name. For "Authorized JavaScript Origins", you don't need to add anything here. Under "Authorized redirect URIs", add the URI `http://localhost:8080/auth/callback` and `http://localhost:8080/auth/swap`. You can add to these later on.

Once you click "Create", there will be a pop up with the Client ID and Secret, take note of both.

## Adding API Libraries

We need to add specific APIs so we can access them. Go to the "Library" section and search for "Google Calendar API", click on the one that matches and click "ENABLE".


## Next Steps

This is the minimal setup for Google Cloud Platform, we will touch on Cloud Run and Cloud SQL later on. By now, you should have the following information:

 - Your Google project ID
 - Google Client ID
 - Google Client Secret
 - List of Redirect URIs
 - List of JavaScript origins (which is empty)