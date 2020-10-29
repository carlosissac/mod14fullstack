# 14 Sequelize: Reverse Engineering.

![GitHub last commit](https://img.shields.io/github/last-commit/carlosissac/mod14hwfullstack) ![Twitter Follow](https://img.shields.io/twitter/follow/zzzakk_cccrlss?style=social) ![GitHub code size in bytes](https://img.shields.io/github/languages/code-size/carlosissac/mod14hwfullstack) ![GitHub followers](https://img.shields.io/github/followers/carlosissac?style=social)

## Description

Reverse engineer provided starter code and create a tutorial document for the code.

## TableOfContents

* [Description](#Description)
* [TableOfContents](#TableOfContents)
* [UserStory](#UserStory)
* [AcceptanceChecklist](#AcceptanceChecklist)
  * [HighLevelRequirements](#HighLevelRequirements)
  * [ApplicationRequirements](#ApplicationRequirements)
* [AppConfig](#AppConfig)
  * [DatabaseConfig](#DatabaseConfig)
  * [ExpressConfig](#ExpressConfig)
  * [HandlebarsConfig](#HandlebarsConfig)
  * [DirectoryStructure](#DirectoryStructure)
* [AppUsage](#AppUsage)
  * [Installation](#Installation)
  * [Configuration](#Configuration)
  * [Operation](#Operation)
  * [Output](#Output)
* [URLS](#URLS)

## UserStory

AS A developer

I WANT a walk-through of the codebase

SO THAT I can use it as a starting point for a new project

## BusinessContext

* When joining a new team, you will be expected to inspect a lot of code that you have never seen before.

* Rather than having a team member explain every line for you, you will dissect the code by yourself, saving any questions for a member of your team.

## HighLevelRequirements

GIVEN a Node.js application using Sequelize and Passport

WHEN I follow the walkthrough

THEN I understand the codebase

## CodeWalkthorugh

Listed below is a file by file walkthorugh of the application code.

### ServerJs

- This is the application entry point where all the requests land and are routed to their specific API depending on their specific type.

- Map of application architecture is detailed in this component. 

- `Passport`, `Express-Session` and `Express` packages are invoked and configured in this file.

- `Passport` description (from npm site). It's sole purpose is to authenticate requests, which it does through an extensible set of plugins known as strategies. Passport does not mount routes or assume any particular database schema, which maximizes flexibility and allows application-level decisions to be made by the developer. The API is simple: you provide Passport a request to authenticate, and Passport provides hooks for controlling what occurs when authentication succeeds or fails.

- `Express-Session` description (from https://tilomitra.com/how-do-nodejs-sessions-work/). A module like express-session will provide you with a nice API to work with sessions (letting you get & set data to the session), but under the hood, it will save and retrieve this data using a cookie. Express-session also offers ways to secure your cookies.

- `Sequelize` models are required from file, invoked and synced to DB.

- Server `PORT` is also defined with either `.env` or a static predifened value for localhost application access, later (after DB is inistialized) the active application listening PORT is displayed in terminal.

- `Session` component is initialized.

- `Body Parser` for API requests and `Static` content folder is also defined.

- `Passport` is required from file and initialized.

- `API` routes for CRUD operations, `HTML` static routes are invoqued from file and initialized.

### PackageJson

- Lists all the npm packages needed for the application to have working functionality.

- For this particular app project the following depenencies are required:

- bcryptjs 2.4.3.

- express 4.17.0.

- express-session 1.16.1.

- mysql2 1.6.5.

- passport 0.4.0.

- passport-local 1.0.0.

- sequelize 5.8.6.

- They can all be installed by running  `npm i` command in terminal.

************ In the `scripts` section of the JSON file we have the `watch` script specifyng `nodemon`. Since there is no `DevDependencies` section specified this could be a problem. Install `nodemon` by submitting in terminal the following command `npm i -D nodemon` and that will install the package as a `DevDependency`. Also suggest thst we change the `watch` section to `dev` in order for us to use file monitoring during our development process.

### Routes-ApiRoutesJs

- Lists all the API routes for the required CRUD operations.

- `Sequelize` models and `Passport` functionality are references by file.

- `POST /api/login` route is invoked using passport authentication middleware, username is sent back as a JSON. If user is logged in successfully with valid credentials then its redirected to the members page if not user will be shown an error.

- `POST /api/signup` route registers a new user using the post method and invoquiquing a sequelize call to the database. We save in the User table the email and password attributes. If everything is registered successfully we send a 307 status message (temporrary redirect) and redirect to login page using `POST /api/login`. If there's an error we display a 401 status (Unauthorized) and show an error message. 

- `POST /logout`. Invokes logout function and redirects to main landing page.

- `GET /api/user_data`. route that returns user's email and ID if the user is already logged in if not it returns an empty JSON object.

*********** `logout` API method is not referencing `/api/` route and that could bring inconsistencies. `login` and `logout` could be implemented as static routes or separate routes.

### Routes-HtmlRoutesJs

- Lists all the static pages invocations.

- `Sequelize` models and `Passport` functionality are references by file.

- Authentication middleware is invoked in order to confirm if user has the right credentials.

- `GET /` brings up the signup form as a landing page. If succesfully logs in, we redirect to `/members`.

- `GET /login` submits the user credentials in case he is already registered.

- Both API's redirect to `GET /members` page after user is succesffuly logged in. By adding `isAutheticated` method any user who is not logged in and tries to access this route will be redirected to the user signup page. 

********** Express `Router` method is not used in order to generate the API routes. Implementation would be much cleaner if this component wold be used. Also directory structure could be used for implementation and we could forgo specifying `/api/` sectiong of the API url.code .

*********** `logout` API method is not referencing `/api/` route and that could bring inconsistencies. `login` and `logout` could be implemented as static routes or separate routes.

********** `module.exports = function(app) { ....` can be replaced by `module.exports = app;` 

### Public

Folder for allocation of static resources.

#### JS-LoginJs

- Front end functionality for `login.HTML`.

- HTML component references are created for `loginForm`, `emailInput` and `passwordInput`.

- During form submission we validate that there's user input for email and password.

- If email and password are present we kick off the loginUser function and clear form afterwards.

- `loginUser` function invokes `POST /api/login` while submitting users email and password as parameters. If login route does a successfull post it redirects us to the main members page.

#### JS-Members

- This file invokes `GET /api/user_data` to query which userID is currently logged in and updates the HTML page with member's name info.

#### JS-SignUp

- front end functionality for `signup.html`.

- we reference the following components `form signup`, `email input`, `password input` 

- `signupForm.on` is deployed in order to validate user input and make sure that there's an username and password when submitted. If everything is correct we run invoque the `signUpUser` function.

- `signUpUser` does a post to `POST api/signup` passing email and password value. If error is encountered we show an alert we invoque `handleLoginErr` function.

- `handleLoginErr` shows a text error and displays an fade-in aler showing a 500 error.

#### Stylesheet-StyleCss.

- File for detailing HTML customzations and styling.

- `form.signup` and `form.login` have a top margin value of 50px.

#### LoginHtml

- HTML that enabled pre-registered users to sign in. 

- Form uses Bootstrap CDN.

- Form has 2 input boxes one for email address and a second one for inputting a password, has a button control for signing in 

- Form also has a link to redirect to signup page.

- HTML references JQUERY CDN link and `js/login.js`.

#### MembersHtml

- HTML that shows the main functionality page. 

- Form uses Bootstrap CDN.

- It also displays a personalized welcome message printing the current logged-in users info and the `Logout` control button in the navbar brand button.

- HTML references JQUERY CDN link and `js/members.js`.

#### SignupHtml

- HTML landing page where user registers using email and password.

### Models-IndexJs

- Helper file that inspects all models available in models folder, and stages them for it to be deployed as db schemas thorugh sequelize. 

### Models-UserJs

- Sequelize schema file that specifies DB schema to be pushed into mysql.

- File requires `bcryptjs` module for pasword encryption, in order to hash user credentials.

- Email attribute cannot be null, must be unique and its proper email format is validated.

- Password attribute should be a string and cant be null.

- password is hashed thorugh Hook methods.

- password attribute is hashed through and then stored in DB.

### Config

- Folder that contains system authentication settings.

#### ConfigJSON

- JSON file that hast the DB connection credentials attributes.

#### PassportJS

- This Passport component implements an authentication prcedure called `LocalStrategy` which consist of using `username` and `password`.

- we require passport as a dependency and implement.

- When user attempts to log in we do a GET request to try to find the user's email.

- If email its not found we return `incorrect email`.

- Afterwards we confirm if password is correct, in case we have an error `incorrect password` message is sent.

#### Middleware-IsAuthenticatedJS

- 

## Improvements

- 

## DocumentLink

