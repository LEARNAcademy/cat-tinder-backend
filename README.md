# Creating Your Own API
We've looked at connecting React apps to an external API, and seen how to use data from an API to build compelling front end applications.  Today we're going to build our own API that will serve the data we create to our front end. 

These sections will cover:
- [App Setup](./01-rails-setup/README.md)
- [Generating Seeds](./02-generating-seeds/README.md)
- [Setting up Cross Origin Resource Sharing (CORS)](./03-cross-origin-resource-sharing/README.md)
- [API Endpoints](./04-api-endpoints/README.md)
- [Validations](./05-validations/README.md)
- [Cat Index](./06-getting-cats-to-the-frontend/README.md)
- [Connecting the New Cat form](./connecting-new-cat-form/README.md)

Creating our own API opens up a new world of possibilities for building engaging, interactive applications.  We can begin to accept user input, store and manipulate that input in the backend, and then provide a personalized experience for our user, perfectly suited to the task he/she is trying to achieve.

As you've seen, the primary tool to collect input from users is an HTML form.  The user fills in form fields with information that allows them to interact with the application.  As a general rule, we always want to process, validate, and store user data on the server where we have more control and processing power to handle it.  To do so, we need to build an API that the React app can both send data to and receive data from.  Ruby on Rails is a fantastic platform to build just such an API, and is what we'll use in class.  There are many other options for building back end APIs.

In the architecture we are building, our front and backend will be two separate applications, giving us more freedom to choose the tools and technologies we want.  Throughout your career as a developer, you'll interact with many other backend platforms.  APIs can be built using Ruby, PHP, Python, Java, and even Javascript, among many others.  That might seem overwhelming, but remember that the concepts are generally the same no matter what technology is used.  The server is where we process data sent by the frontend, clean and store that data, and serve updated data back to the front end app to be consumed by the user.

## Review APIs
![Api](https://s3.amazonaws.com/learn-site/curriculum/React/api.jpeg)


## Building an API for Cat Tinder
We're going to build an application to help our users' cats socialize and be well adjusted members of the feline community.  Our application will allow users to create profiles for their cats, search other cat profiles and setup kitty play dates.  In this module we're focusing on the server side, so let's jump in and start building an application.

## Overview of goals
* Setting up a Ruby on Rails API application
* Creating endpoints to accept and serve data
* Validating user input

First thing's first, let's set up the Rails app.

[Go to App Setup](./01-rails-setup/README.md)