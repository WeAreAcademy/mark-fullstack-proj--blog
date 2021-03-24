---
module: Full-Stack

level: 1

methods:
  - team
  - pair
  - solo

tags:
  - full-stack
---

# Academy Project: Blog

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

This recommended setup is not different than the earlier full-stack apps, except we recomment you use [the github integration](https://devcenter.heroku.com/articles/github-integration) to deploy to heroku instead of the heroku cli.

- Create the starting app by using this template repo: https://github.com/WeAreAcademy/mark-fullstack-proj--starter-1
- Create a local database
- Create a `.env` file, locally, based on `.env.example`. This will be used to configure a `DATABASE_URL` environment variable when running locally which will tell your code where the database is that it should connect to, and what username and password it should use.
- In the terminal, run `yarn` to install the required packages.
- In the terminal, run `yarn start:dev` and resolve any errors before proceeding.
- Publish the project repo to github, call it `blog-backend`.
- Set up deployment of your project to heroku from github:
  - https://devcenter.heroku.com/articles/github-integration
- Provision Heroku Postgres DB service for your app:
  - In the heroku dashboard for your newly added app, go to Resources, and search for and add the "add-on" called "Heroku Postgres". (You'll want to choose the free version, if offered)
  - Once the service appears as an add-on, click on it. It should take you to the database administration part of the dashboard. (Also accessible from https://data.heroku.com/ )
  - Choose Settings: View Credentials and copy the long `URI` value. This includes your database username and password so do not store it in source control.
  - from your laptop, ensure you can connect to the remote database from Postico or psql using the URI found in the credentials in the previous step.  
  - Run SQL commands to create the tables you need for you app
  - When your app runs on heroku, it will automatically be given an environment variable, DATABASE_URL with the necessary location and credentials for connection to your database.
- Write the code for your blog API.

### Setup front-end

- Create a new React app on your machine called `blog-react`. Make sure you set up with TypeScript not the JavaScript default.  See [guide to React project initial creation (with TypeScript)](https://www.notion.so/weareacademy/How-to-create-a-React-app-with-TypeScript-76643f84db564a69a04db9a0b6a2f2e7).

- Publish the project repo to github. Call it `blog-react`.

- Set up continuous deployment of your app to [Netlify](https://netlify.app/) as `academy-yourgithubusername-blog`.netlify.app where `yourgithubusername` is your github username.  See [Netlify deployment guide for React apps](https://www.notion.so/weareacademy/How-to-deploy-a-React-app-to-free-Netlify-hosting-9e6ebd4dcb814cb483c34eb0f05ea96e).

- Follow [this guide on how to configure an API base-URL in a React app for production AND development](https://www.notion.so/weareacademy/How-to-configure-an-API-base-URL-in-a-React-app-for-production-AND-development-d74af8551cb9430ba95a976f32dae360)

## Level 1

As a user, via the front-end app:

- I should be able to create a blog post with title, and main text. (Date of creation should be automatically recorded for me.)
  - A post's title should be able to store at least 250 characters.
  - A post's main text should be able to store at least 10,000 characters.
- I should be able to view a list of all created blog posts (title, creation date, and a (maximum 300-character) excerpt of the main text), in reverse chronological order.
- I should be able to click on a blog post from the summary view and be presented with a single-record view, including the full main text.
- I should be able to return to the list view from the single-record view
- I should be able to delete any blog post
- I should be able to edit the title or main text of any post
- I should not be able to edit the creation time of any post

To avoid confusion around multiple meanings of the word `post` in your code, we suggest you call your blog posts `articles` (and your database, `blog`)

## Level 2 - filtering

As a user, via the front-end app:

- I should be able to filter the list view entries by text. Only those who have matching text in their title or main text should be shown. Case should be ignored.

## Level 3 - comments
**Overview:** Add support to allow users to add, view and delete comments on a specific paste.

- I should be able to add a number of comments to a blog post. My comment text and my offered name should be recorded.
- I should be able to see all comments under a given blog post, in the single-record view for that post.
- I should be able to delete a comment.
- When I delete a blog post, all related comments should be deleted automatically.

**API**: On the API side, we suggest you enable this functionality by providing the following routes:

*  POST 'articles/:articleId/comments' to create a new comment specific to a given article.
*  GET 'articles/:articleId/comments' to get all comments corresponding to a specific article.
*  DELETE 'articles/:articleId/comments/:commentId' to delete a comment of a given id that belongs on a given article.

These are conventional RESTful routes for "nested" resources.   You don't *have* to adhere to these conventions.  The priority is that the new functionality is made available to the user.

**Database**: In the database:

- Ensure that all comments always each relate to an existing article.  You should strive to make it impossible to have an 'orphaned' comment in the database, regardless of any programming mistakes that might be made in your express code.
- Ensure that if you delete an article, all related comments are automatically deleted
- Ensure that if you delete a comment, the related article is NOT deleted automatically!
