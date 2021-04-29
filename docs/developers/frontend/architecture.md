## Architecture

The project directory attempts to enforce an architecture of the applications. In the source directory, there is a filed named `app.js`. This file is the root file that acts as the entry point for the application. Another layer deeper and we get to the auxiliary files used to support the view, functionality, and reusability of components of the application.

### Components

One of the benefits of using React and React Native is the compartmentalization of various components. As a result, the folder `/src/components` contains all of the reusable UI components. It's important in developing an application like this to modularize the UI components so that they can be reused and limit the complexity and size of the code base.

### Navigators

Navigators are a necessary component of React Native and what are utilized to make decisions about how the user will flow through the application. As a result, these files have been placed in `/src/navigators` and the contain references to the their children which are screens.

### Screens

A screen is the canvas that contains the UI elements along with presenting a user some functionality. All of the screens are in `/src/screens` and when adding new screens, this is where you would want to place those files. It's important to keep as much of the business of the application out of the screen which is where providers and components come together to flesh out the application

### Providers

Providers are the business logic of the application. In this folder we have the global user provider which deals with the user state and allows different components access to that state. We also have all of the api functionality within the providers folder at `/src/providers/   `. This folder is part of enforcing that we remove as much of the business of the application out of the screens files to avoid the files growing so large in size that they become incomprehensible. 