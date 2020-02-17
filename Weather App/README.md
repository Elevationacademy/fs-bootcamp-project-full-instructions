#### INTRO

There are a lot of different weather apps on the market. Most of them get their information from some API and display it in a way that looks nice on your phone or desktop.

You're going to be creating your own weather app with the full stack!

In this project you will write a client using OOP and MVC design, create a server, access an external API from your server, and save data to a database with CRUD operations.

Weather you're ready or not, let's go!

* * * * *

#### PACKAGE REQUIREMENTS

You'll need the following packages for this project:

-   body parser
-   express
-   handlebars
-   jQuery
-   mongoose
-   request

You can also use font-awesome and moment.js, though neither are necessary.

* * * * *

#### WHETHER WEATHER

You should work on this project in steps:

1.  Set up the server
2.  Set up your Schemas and DB
3.  Get data from the external API
4.  Set up the routes on your server
5.  Set up your client (MVC & OOP)
6.  Work on your Model
7.  Work on your Renderer (View)
8.  Work on your Controller
9.  Design (for mobile!)

Here we go!

* * * * *

#### SERVER

Your server should have a normal set up with the following:

-   Express
-   body parser setup
-   connection to your DB
-   A server folder with a model and routes folder

-   Your model folder should have a City.js file
-   Your Routes folder should have an api.js file, with an express Router setup

* * * * *

#### DB SCHEMA

Your DB schema in your City.js file should have the following:

-   `name` - a string
-   `temperature` - a number
-   `condition` - a string
-   `conditionPic` - a string

* * * * *

#### EXTERNAL API

There are [a lot ](https://www.programmableweb.com/news/top-10-weather-apis/analysis/2014/11/13)of different weather APIs you can work with. We recommend using [ open weather map](https://openweathermap.org/) as it's free and fairly simple. But you're free to use a different API if you'd like.

Note:* If you choose to use a different API, do not spend more than 30 minutes trying to figure it out, as this is not the point of this project. The rest of the API directions will be tailored for open weather map*.

You'll need to sign up in whichever way you prefer. Once you do, you'll be redirected to a page which provides you with your API key. You'll need to use this to query the API, so save it as a variable in your server somewhere.

Now that you have access to the external API:

-   Read over the documentation, it's really thorough and nice
-   On your server, set up a route that makes a request to the API
-   Query the API for a *city* of your choice, you wan't the current data to start with
-   Use postman to test at this point

* * * * *

#### SERVER ROUTES

You should have the following routes on your server:

-   A get route to `/city`
    -   This route should take a `cityName` parameter
    -   This should be the route that makes a call to your external API

-   A get route to `/cities`
    -   This route should find all of the city data saved in your DB, and send it to the client

-   A post route to `/city`

    -   This route should take some data from the body, and save it as a new City to your DB

-   A delete route to `/city`

    -   This route should take a `cityName` parameter
    -   This route should find the city's data in your DB and remove it from your DB

* * * * *

#### CHECKPOINT

So far you should have:

-   An express server set up
-   Connection to your DB and one mongoose schema
-   One route which communicates with an external weather API
-   Three routes which communicate with your DB

Ready? Let's continue.

* * * * *

#### CLIENT

For your client you'll need to have a dist folder with a separate file for your Model, View, Controller, HTML, and CSS. You can call them what you like, we called ours `TempManager.js`, `Renderer.js`, `main.js`, and `style.css` respectively.

* * * * *

#### YOUR MODEL - TempManager

Here's what should go inside your TempManager class:

-   An array of `cityData`. This will be empty to start with
-   A `getDataFromDB` method, which sends a GET request to the `/cities` route on your server

    -   If any data comes back, set the class' `cityData` array equal to it

-   A `getCityData` method , which sends a GET request to the `/city` route on your server

    -   This should have a parameter of `cityName`
    -   This method needs to be async
-   When the data comes back, add an object to the class' `cityData` array. It should have these properties:
    -   City name
    -   Temperature
    -   Conditions
    -   Condition icon
    -   Any other data you fancy

-   A `saveCity` method, sends a city's data as POST request to the `/city` post route on your server

    -   The method should take a parameter of `cityName`
    -   It should find that city's data object from the class' `cityData` array
    -   Then it should pass it as the body of the post request

-   A `removeCity` method, which sends a DELETE request to the `/city` delete route on your server

    -   The method should take a parameter of `cityName`

* * * * *

#### YOUR VIEW - RENDERER

Here's what should go inside of your Renderer class:

-   A method `renderData` which appends data to the HTML

    -   This mentod should take `allCityData` - an array of all the city data and use Handlebars and jQuery to render it on the HTML

Though it's not explicitly part of your render class, you also need to add in your Handlebars template to your HTML. The template should include:

-   A div for each city
-   The city name
-   The temperature
-   The conditions
-   An image of the conditions
-   Any other data you want

* * * * *

#### YOUR CONTROLLER - MAIN.JS

Your controller should have the following:

-   A `loadPage` function, which should render any saved data

    -   It should call `getDataFromD`B from an instance of your `TempManager`
    -   It should then render the city data from your `TempManager`
    -   This function should run when the page loads

-   A `handleSearch` function, which should call to the server and render new weather data

    -   It should take the `city-input` from your html
    -   It should call the `getCityData` method from an instance of your `TempManager`, and send the `city-input` as the parameter
    -   It should then render the data you get back from the server
    -   This function needs to be `async` to work

-   An on click for your search button, which calls your `handleSearch` function as it's callback function
-   An on click for each of the save buttons that:

    -   Takes the name of the city from the DOM
    -   Calls the `saveCity` method from an instance of the `TempManager`, sending the `cityName` as a parameter

-   An on click for each of the remove buttons that:

    -   Takes the name of the city from the DOM
    -   Calls the `removeCity` method from an instance of the `TempManager`, sending the `cityName` as a parameter

* * * * *

#### DESIGN

You are going to be designing this App for mobile!

Use the mobile icon in the top left corner of your dev tools (if you're using Chrome) pick the mobile device of your liking, and use this display while creating the design. Don't worry too much about Media Queries for now, just make sure it looks good on mobile as the default.

Here's where you can find the button if you've forgotten:

![](https://developers.google.com/web/tools/chrome-devtools/device-mode/imgs/device-mode-initial-view.png)

We recommend using Grid, because it's great.

* * * * *

#### FULL STACK PROJECT COMPLETE! OUTLOOK? SUNNY

That's the project! As long as your client and server are communicating well, you should have a well functioning Weather App. Congrats! If you want to add some more spunk, go on to the extensions below. Good job!

* * * * *

#### EXTENSIONS

So far, our app is static - I cannot refresh the weather unless I remove it, and add it back again. That's just poor functionality, so lets fix it

* * * * *

#### 1\. REFRESH BUTTON

Add a button to each of the city's weather while rendering. This button will need to:

-   Trigger an on click function in your controller that takes takes the name of the city
-   It should then call an `updateCity` method on your `TempManager` and pass it the city name

    -   The `updateCity` function should call a PUT request to the `/city` put route on the server, and pass it the city name
    -   When it gets the data back it should update the class' `cityData` array

-   It should then call the `renderData` method of your `Renderer`
-   On the Server `/city` `put` route

    -   You should take the city name and call to the external API
    -   Then it should send the city data back and update your DB with the new data

-   You'll need async on a couple of these functions to make this work

* * * * *

#### 2\. LAST UPDATED

Now let's display the time that the weather data was last updated.

In order to display the data you'll need to do a few things:

1.  Update your DB Schema to have an `updatedAt` key which is of type `date`.
2.  Extract the last updated time from the weather API. Notice how the API will only return that data if you request data in `XML` format. Read the documentation to see how you can do that. You'll need to understand how to handle data in XML. For a hint head to the end of the page.
3.  Now that you have the `updatedAt` property for every city, you need to add this to your HTML template.

Once we are recording and displaying the "last updated" time of the weather, we need to make our app smart!

On page load you need to do the following:

-   Create a new date either with native JS or moment.js
-   Get the saved data from your DB and check, for each city, the difference in date between the city's `updatedAt` date and time, and the current time
-   If the difference in time is greater than 3 hours, then query the external API for the weather, update your DB with the new results and send your results back to the client.

Your app also now updates on it's own. Dope.

Hint for handling XML:

You can convert XML to JSON in order to work with it in a way that you're already familiar with. You can find an npm package that does that for you - there are many so feel free to do a google search - or you can use [xml2js](https://www.npmjs.com/package/xml2js) which we found can do the trick.