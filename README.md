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

- This is the application entry point where all the request land and are routed to their specific API depending on the type of request.

- Map of application architecture is detailed in this component. 

- `Passport`, `Express-Session` and `Express` packages are invoked and configured.

- `Sequelize` models are required from file, invoked and synced to DB.

- Server `PORT` is also defined with either `.env` or a static predifened value for localhost application access, later active application listening PORT is displayed in terminal.

- `Session` component is initialized.

- `Body Parser` for API requests and `Static` content folder is also defined.

- `Passport` is required from file and initialized.

- `API` routes for CRUD operations, `HTML` static routes are invoqued from file and initialized.

### PackageJson

Lists all the npm packages needed for the application to have working functionality.

For this particular app project the following depenencies are needed:

- bcryptjs 2.4.3

- express 4.17.0

- express-session 1.16.1

- mysql2 1.6.5

- passport 0.4.0

- passport-local 1.0.0

- sequelize 5.8.6

They can all be installed by running  `npm i` command in terminal.

************ In the `scripts` section of the JSON file we have the `watch` script specifyng `nodemon`. Since there is no `DevDependencies` section specified this could be a problem. Install `nodemon` by submitting in terminal the following command `npm i -D nodemon` and that will install the package as a `DevDependency`. Also suggest thst we change the `watch` section to `dev` in order for us to use file monitoring during our development process.

### Routes-ApiRoutesJs

- `Sequelize` models and `Passport` functionality are references by file.

- `POST /api/login` route is invoked using passport authentication middleware, username is sent back as a JSON.

- `POST /api/signup`. route registers a new user using the post method and referenciing the 

- `POST /logout`. Invokes logout function and redirects to `/`.

- `GET /api/user_data`. route that returns user's email and ID if the user is already logged in if not it returns an empty object.

*********** `logout` API method is not referencing `/api/` route and that could bring inconsistencies. `login` and `logout` could be implemented as static routes or separate routes.

### Routes-HtmlRoutesJs

- `Sequelize` models and `Passport` functionality are references by file.

- Authentication middleware is invoked in order to confirm if user has the right credentials.

- `GET /` brings up the signup form as a landing page.

- `GET /login` submits the user credentials in case he is already registered.

- Both API's redirect to `GET /members` page after user is succesffuly logged in. 

********** Express `Router` method is not used in order to generate the API routes. Implementation would be much cleaner if this component wold be used. Also directory structure could be used for implementation and we could forgo specifying `/api/` sectiong of the API url.

*********** `logout` API method is not referencing `/api/` route and that could bring inconsistencies. `login` and `logout` could be implemented as static routes or separate routes.

### Public

Folder that allocates static resources.

#### JS-LoginJs

- front end functionality for `login.HTML`.

- HTML component references are created for `loginForm`, `emailInput` and `passwordInput`.

- During form submission we vaklidate that theres user input for email and password.

- If email and password are present we kic off the loginUser function and clear form.

- if login route does a successfull post it redirects us to the main page.

#### JS-Members

- File imeplments GET route to query which userID is currently logged in and updated the HTML page.

#### JS-SignUp

- `form signup`, `email input`, `password input` 

- `signupForm` is deployed in order to validate user input and make sure that theres an username and password when submitted. If everything is correct we run invoque the signup function.

- we do a post to `api/signup` passing email and password value. If error is encountered we show an alert.

#### Stylesheet-StyleCss.

- css customizations and declarations.

#### LoginHtml

- HTML that enabled pre-registered users to sign in.

#### MembersHtml

- HTML that displays main functionality page. It displays a personalized Welcome message priting the curren user logged in and the `Logout` control button.

#### SignupHtml

- HTML landing page where user registers using email and password.

### Models-IndexJs

- Helper file that inspects all models available in models folder 

### Models-UserJs

-

### Config

-

#### ConfigJSON

-

#### PassportJS

-

#### Middleware-IsAuthenticatedJS

-

## Improvements

## DocumentLink

