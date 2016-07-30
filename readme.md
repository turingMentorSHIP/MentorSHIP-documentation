# MentorSHIP

![mentorship](https://s3.amazonaws.com/f.cl.ly/items/1o2y3w262I2b0A2G1a3B/Screen%20Shot%202016-07-20%20at%209.11.26%20PM.png?v=d5da8526)

The MentorSHIP is an application to connect Turing School students and mentors. Students can browse mentors by skills and interest, and view their contact information.

This project is a ground up rebuild of the previous [mentorSHIP](https://github.com/turingschool-projects/mentorSHIP) app.

The front end is built in Ember.js with Bootstrap 3. And the backend is a Rails 5 API.

## Running the project

To run the project, see the readme for the front end and back end.

* [MentorSHIP-FrontEnd](https://github.com/turingMentorSHIP/MentorSHIP-FrontEnd)
* [MentorSHIP-BackEnd](https://github.com/turingMentorSHIP/MentorSHIP-API)

## Our vision for the project

Our vision for the MVP of the project was as follows

* User can login with github
* Users can create a mentor or student account, and fill out a profile
* Mentors can view index of students
* Students can view index of Mentors
* Students can see contact info of mentors like email or phone number

## What we accomplished

An incredible landing page for the site thanks to [Mark Miranda](https://github.com/notmarkmiranda)

* User can login with github (on the back end only right now)
* Mentors can view index of students
* Students can view index of Mentors
* Students can see contact info of mentors like email or phone number

Authentication and authorization was partially implemented on the back end, and planned for but not implemented on the front end.

## What we didn't accomplish

* User can login with github (on the front end)
* Users can create a mentor or student account, and fill out a profile

## Next steps

* The mentorSHIP is in your hands now, her future destination is up to you.

## Links we found helpful

We are assuming future students working on the project will be familiar with using Ruby on Rails, and new to Ember.js

Ember is a really cool framework that has a lot of similarities to Ruby on Rails. But it also has a lot of differences.

We found the following tutorials on Ember.js to be helpful during development of the project.

* [Modern Bridge Between Ember and Rails 5 with JSON API](http://emberigniter.com/modern-bridge-ember-and-rails-5-with-json-api/)
* [Building an Ember Bookstore App](http://emberigniter.com/building-user-interface-around-ember-data-app/)

## Authentication and Authorizations decisions

Mark and Josh's voyage aboard the MentorSHIP ran aground while trying to implement authentication and authorization between the front end ember app and the back end rails api. Ultimately we ended up with a partially implemented solution. The next salty dogs to captain this fine vessel shall be left with the decision of whether to continue with our implementation or scrap it for a solution you decide on.

In the case of continuing with our solution we are documenting here the path we decided to take, what we implemented in that path, and what the next steps will be.

### It's complicated

There are a lot of methods for implementing authentication and authorization between the front end and the back end, and none of them are perfect answers.

We used the following tutorials/articles as a possible solutions when making our decisions

* [Implementing Authentication with Ember Services](http://emberigniter.com/implementing-authentication-with-ember-services/)
* [Real World Authentication with Ember Simple Auth](http://emberigniter.com/real-world-authentication-with-ember-simple-auth/)
* [GitHub Social Authentication with Ember Simple Auth and Torii](https://disjoint.ca/til/2016/03/21/github-social-authentication-with-ember-simple-auth-and-torii/)

### What we decided on

Ultimately, we decided on a completely different implementation of leaving all of the authorization and authentication to the back end, with the front end using a simple token to authenticate its requests to the api. Our solution was inspired by this Mike Pack's comments on [this](https://github.com/exercism/ember-experiment/issues/4) Pull Request conversation

The basic flow of our envisioned authentication process was this: (I tried diagramming software but I'm too old)
![AuthenticationDiagram](https://s3-us-west-2.amazonaws.com/rails-misc-pictures/diagram.JPG)

Our thought process for this model, was that storing any sensitive data in a front end application is inherently risky, and the back end should handle that for us.

### What we implemented in that process

We implemented the GitHub OAuth on the back end. As the project stands now, when the user clicks the login with GitHub button on the site, it takes them the Rails backend, which redirects them to login with Github. The Github login stores the users information, or retrieves it from the database, and redirects them back to the front end application.

### The next steps

The next steps would be to edit the GitHub callback action. After the user is redirected back to the Rails app, the app should generate an access token for that user, and store it in the database. Then on the redirect back to the front end that token is passed as a param.

```ruby
  redirect_to "MentorSHIP-FrontEnd/login&token=1234"
```

The Ember app would store that token in a session, cookie, or local storage. When the user wants to make an api request that needs authenticating, the app would pass that token along with the request that the api can use to authorize the request to the appropriate user.

When a user clicks Logout, the token would be cleared from the session, cookie, or local storage. And the front end would send an AJAX request to change the users token in the database to be an empty string.


## Contributors

* [Mark Miranda](https://github.com/notmarkmiranda)
* [Joshua Washke](https://github.com/jwashke)
* Add your name to this list

Future contributors should feel free to edit this readme and update it on the current status and future of the HMS mentorSHIP.
