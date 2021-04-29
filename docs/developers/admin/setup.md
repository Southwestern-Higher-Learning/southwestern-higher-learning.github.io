# Setup

## Local Setup

To setup the admin interface locally, you need to have Node.js installed. Look within the frontend developer guide to see how to do this. Next, clone the repository and run `npm install` in the root folder. This will install all of the necessary dependencies. Next, rename `.env.example` to `.env.`. This assumes that you have already setup the backend accordingly. 

!!! info
    You will need to add `http://localhost:3000/login` to the Google API account you setup in the backend developers guide.

Start the backend, then run `npm start` in the root directory of the admin interface. Once it's started, navigate to `http://localhost:3000` and try logging in with a valid Google account. 

## Deployment

For deployment, it is recommended to use Netlify as it handles redirects from Google that React Admin can understand. Before starting, you should fork the admin interface repository on GitHub. Then follow this guide on deploying a site from a GitHub repository and pause when you get to Step 5: [https://www.netlify.com/blog/2016/09/29/a-step-by-step-guide-deploying-on-netlify/](https://www.netlify.com/blog/2016/09/29/a-step-by-step-guide-deploying-on-netlify/). 

The admin interface's configuration is a bit different, under "basic build settings" ensure that the "Build command" is `npm run build` and the "Publish directory" is `build`. Click "Show advanced" and under "Advanced build settings" and two new variables: `REACT_APP_BASE_URL` and `REACT_APP_REDIRECT_FULL_URL`. The `REACT_APP_BASE_URL` should be the URL of your backend and `REACT_APP_REDIRECT_FULL_URL` will be the URL of your admin interface and then `/login`. You can edit these environment variables anytime in the "Site Settings" > "Build & deploy" > "Environment" section.


!!! info
    Ensure that the `REACT_APP_REDIRECT_FULL_URL` is an Authorized Redirect URI in your Google API setup.