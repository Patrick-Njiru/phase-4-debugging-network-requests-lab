# Putting it All Together: Client-Server Communication

## Learning Goals

- Understand how to communicate between client and server using fetch, and how
  the server will process the request based on the URL, HTTP verb, and request
  body
- Debug common problems that occur as part of the request-response cycle

## Introduction

Just like the last lesson, we've got code for a React frontend and Rails API
backend set up. This time though, it's up to you to use your debugging skills to
find and fix the errors!

To get the backend set up, run:

```console
$ bundle install
$ rails db:migrate db:seed
$ rails s
```

Then, in a new terminal, run the frontend:

```console
$ npm install --prefix client
$ npm start --prefix client
```

Confirm both applications are up and running by visiting
[`localhost:4000`](http://localhost:4000) and viewing the list of toys in your
React application.

## Deliverables

In this application, we have the following features:

- Display a list of all the toys
- Add a new toy when the toy form is submitted
- Update the number of likes for a toy
- Donate a toy to Goodwill (and delete it from our database)

The code is in place for all these features on our frontend, but there are some
problems with our API! We're able to display all the toys, but the other three
features are broken.

Use your debugging tools to find and fix these issues.

There are no tests for this lesson, so you'll need to do your debugging in the
browser and using the Rails server logs and `byebug`.

**Note**: You shouldn't need to modify any of the React code to get the
application working. You should only need to change the code for the Rails API.

As you work on debugging these issues, use the space in this README file to take
notes about your debugging process. Being a strong debugger is all about
developing a process, and it's helpful to document your steps as part of
developing your own process.

## Your Notes Here

- Add a new toy when the toy form is submitted

  - How I debugged:
    - I read the error that was appearing in the terminal of the running rails server when I tried to add a toy. It has a NameError that appeared in toy_controller.rb line 10. So I went to this file and found a typo, toy = Toys.create(toy_params) instead of toy = Toy.create(toy_params), so I fixed it.

- Update the number of likes for a toy

  - How I debugged:
    - When I clicked the update button, the page was displaying an error on the frontend, ToyCard.js, but I knew the problem was on the backend. So I navigated to the code editor and read the error from the rails server terminal. I found the error to be in the update method in the toys_controller. 
    - At first I struggled to understand what the problem was since all the code was written well. I tried changing the params so that only `likes` param was being updated but to no avail. It was after a while that I decided to take a step back and look at the whole method that I realized someting was missing. The toy was being updated successfully but not being rendered at all. So I added the code to render it in json format in toys_controller.rb line 17 and fixed the bug.

- Donate a toy to Goodwill (and delete it from our database)

  - How I debugged:
    - On pressing the `Donate to GoodWill` button, the error that was appearing on the rails server terminal indicated that there was no `route` matching `DELETE` for any of the toys. So I navigated to the routes.rb file and found that the route for the destroy method had not been added. So I added it and fixed the bug.
