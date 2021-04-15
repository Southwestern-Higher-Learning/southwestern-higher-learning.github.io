# Using Google

An important aspect of the project is the scheduling of users with tutors, we utilize the Google API in a couple of different ways.

## Authentication

We require users to log in with their Google account in order to get their credentials (API specific credentials, not a password) and get permission to view and update their calendars and events.

## Creating and Getting Schedules

Whenever a user becomes a tutor (specifics in Admin section), the backend creates a calendar for them named "TutorApp Schedule". In this calendar they can setup blocks of time they are available to tutor, along with a location that can be physical or virtual.

Whenever a user wants to schedule, we query the Google Calendar API to get the events of the specific "TutorApp Schedule" calendar. When the user schedules, we use the same API to add them as an attendee to the event they schedule for.