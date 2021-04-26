# Using the Docs

One of the many benefits of FastAPI is that it generates documentation based on the added routes. Once you have your local docker containers running, you can go to `http://localhost:8080/docs` to view the documentation.

![Docs](/assets/be/docs-intro.png)

## Testing Google

To test your Google setup. Go to `http://localhost:8080/auth/code/client` in your browser. A familiar Google sign-in page will appear, select a valid Google account (one ending in the same `TOP_DOMAIN` variable configured earlier). Accept the permissions and you should be taken to a screen where your specific user information should be. If there is very little information, such as `{"details": "<info here>"}` that means something is not correct and you may need to double-check your Google credentials.

## Example Use of Docs

To test any of the routes, click on the route you would like to test. For instance, click on the `/ping` route and a drop down will appear with more information about that route. The documentation will let you know if there are any query parameters needed or if the request expects a body. Clicking on `Try it out` will allow you to fill out the necessary information. Once you filled out any information click on `Execute` and the website will let you know the server's response.

![Docs](/assets/be/docs-example.png)

## Authorizing the Docs

You might notice locks around certain routes. These locks indicate that the route is protected and needs authorization information to be used. To use the protected routes in the documentation, go back to `http://localhost:8080/auth/code/client` in your browser. Once you log in, take note of the `access_token` that is a part of the JSON response. 

This access token is used in the headers of your request, where you can set the `Authorize` header to `Bearer <access_token>`. The documentation website takes care of this. Near the top of the page, there is a green `Authorize` button. Click on that and fill out the `Value` box with the access token from `http://localhost:8080/auth/code/client`. Click on `Authorize` and then `Close` will let you access the protected routes. To verify that your access token is correct, go to the `/user/me` route try it out. The response should be your specific user information.

## Wrapping Up

Now that you have your docs authorized, you're now able to use any of the routes (except ones requiring a superuser permission).

