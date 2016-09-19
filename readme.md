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

## What has been accomplished

An incredible landing page for the site thanks to [Mark Miranda](https://github.com/notmarkmiranda)

* User can login with github
* Mentors can view index of students
* Students can view index of Mentors
* Students can see contact info of mentors like email or phone number

The front end makes an API call that triggers the backend to initiate the OmniAuth process and then returns to the front end.

## What we didn't accomplish

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

The Authentication is accomplished using the OmniAuth gem and a fairly simple interaction between the front and back ends. The front end has a link that goes directly to the backend controller to start the process. Consequently, that link has to have the path to the backend. And the backend needs a path to redirect control to the front end when OmniAuth completes. We tried using an ENV variable in the ember front end to change the path depending on the current, but we ran aground on that. The branch 'localhost_version' has the links hard coded to the local servers for testing and development.

These are articles the previous team found useful on authentication.

* [Implementing Authentication with Ember Services](http://emberigniter.com/implementing-authentication-with-ember-services/)
* [Real World Authentication with Ember Simple Auth](http://emberigniter.com/real-world-authentication-with-ember-simple-auth/)
* [GitHub Social Authentication with Ember Simple Auth and Torii](https://disjoint.ca/til/2016/03/21/github-social-authentication-with-ember-simple-auth-and-torii/)

Ultimately, they went with a simpler implementation using OmniAuth.

### Current Progress

Once the front end triggers the Auth process it hands over control to the backend. This allows us to keep our client ID and client Secret on the server without ever exposing it to the possibility of a user reading it from the browser. Once Github returns the user's info, the Rails server either retrieves them from the database, or creates a new entry. Information is passed to the front end using cookies. The session id, user's email, and user's token are saved in a cookie that the front end can then access. A boolean value of `authenticated=true` is also set in a cookie. The 'logout' path causes the backend to delete these cookies when it clears the session. The cookie is a session cookie, so it should be deleted automatically if the user closes the browser without signing out.

On the front end we created a "Welcome" view and a helper method that enables the views to retrieve data from the cookies.

### The next steps

The next step is to get the ENV variable to work, or find some other solution to avoid hard coding different versions of the links between test/development and production. After that, we can begin to implement the MVP functionality:

* Mentors can view index of students
* Students can view index of Mentors
* Students can see contact info of mentors like email or phone number
* Create a dashboard/account management page for the user


## Contributors

* [Mark Miranda](https://github.com/notmarkmiranda)
* [Joshua Washke](https://github.com/jwashke)
* [Christopher Soden](https://github.com/seeker105)
* [Parker Phillips](https://github.com/Parker-CP)
* Add your name to this list

Future contributors should feel free to edit this readme and update it on the current status and future of the HMS mentorSHIP.
