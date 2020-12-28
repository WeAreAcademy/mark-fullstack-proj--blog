---
module: Full-Stack

level: 1

methods:
  - team
  - pair
  - solo

tags:
  - wip
---

# Academy Project: Favourite Places

<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-nd/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/">Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International License</a>.

## Overview

You will make and deploy a full-stack blog app which will allow you to write and read blog entries and comments.

## Technology stack

- The front-end will be written in TypeScript using the React library, and hosted on Netlify.
- The back-end will be written in TypeScript, using the express and node-postgres(pg) libraries, and hosted on Heroku. Data will be stored in PostgreSQL.

## Intentional limitations

- The system will not include any authentication or authorisation. As a result, anyone who accesses the app will be able to create, edit or delete blog posts as though they were the author.

## Setup

### Setup back-end

- Clone the starting app from this url: TODO: create and link back-end API starter app.
- Create a local database: TODO: link local database setup instructions
- Create a `.env` file, locally, based on `.env.example`. This will be used to configure a `DATABASE_URL` environment variable when running locally which will tell your code where the database is that it should connect to, and what username and password it should use.
- Run `yarn start:dev` and resolve any errors before proceeding.
- Publish the project repo to github. Call it `blog-backend`. TODO: add link to instructions: "publishing new project repo to github".
- Set up deployment of your project to heroku from github:
  - https://devcenter.heroku.com/articles/github-integration
- Provision Heroku Postgres service for your app:
  - In the heroku dashboard for your newly added app, go to Resources, and search for and add the "add-on" called "Heroku Postgres". (You'll want to choose the free version, if offered)
  - Once the service appears as an add-on, click on it. It should take you to the database administration part of the dashboard. (Also accessible from https://data.heroku.com/ )
  - Choose Settings: View Credentials and copy the long `URI` value. This includes your database username and password so do not store it in source control.
  - from your laptop, ensure you can connect to the remote database by running the psql command with the URI found in the credentials in the previous step. E.g. here's how your command might look (though I have replaced the credentials):
    `psql postgres://thisIsMyUsername:thisIsMyPassword@machinename.eu-west-1.compute.amazonaws.com:5432/databasename`
  - you can run commands in this way to create the tables you need for you app
  - When your app runs on heroku, it will automatically be given an environment variable, DATABASE_URL with the necessary location and credentials for connection to your database.
- Write the code for your blog API, starting in server.ts

### Setup front-end

- Create a new React app on your machine called `blog-react`. Make sure you set up with TypeScript not the JavaScript default. TODO: add link to instructions: "React project creation setup (w typescript)".

- Publish the project repo to github. Call it `blog-react`. TODO: add link to instructions: "publishing new project repo to github".

- Set up continuous deployment of your app to [Netlify](https://netlify.app/) as `academy-yourgithubusername-blog`.netlify.app where `yourgithubusername` is your github username. TODO: add link to Netlify deploy instructions.

- Follow the given instructions on configuring the API base URL for local development and for production. TODO: make and link API config instructions for react app on netlify and local.

## Level 1

As a user, via the front-end app:

- I should be able to create a blog post with title, and main text. (Date of creation should be automatically recorded for me.)
- I should be able to view a list of all created blog posts (title, creation date, and a (maximum 300-character) excerpt of the main text), in reverse chronological order.
- I should be able to click on a blog post from the summary view and be presented with a single-record view, including the full main text.
- I should be able to return to the list view from the single-record view
- I should be able to delete any blog post
- I should be able to edit the title or main text of any post
- I should not be able to edit the creation time of any post

## Level 2

As a user, via the front-end app:

- I should be able to filter the list view entries by text. Only those who have matching text in their title or main text should be shown. Case should be ignored.
- I should be able to add a number of comments to a blog post. My comment text and my offered name should be recorded.
- I should be able to see all comments under a given blog post, in the single-record view for that post.
- I should be able to delete a comment.

# Ideas for more work
