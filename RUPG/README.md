#### INTRO

Now that you know how to request data from APIs and use Handlebars.js to render data on a page really easily - it's time to put your skills to work!

You'll be making a Random-User-Page-Generator. What exactly is a Random-User-Page-Generator (or RUPG for short, pronounced *ruh-pa-geh*)? It's essentially a Facebook profile page, filled with content taken from APIs and generated with different data at the click of a button.

You'll be using APIs, jQuery, Handlebars, and of course creating it all in OOP. Are you Excited? Great, because RUPG is a multi-million-dollar-application just waiting for you to create it!

* * * * *

#### INSTRUCTIONS

Ultimately, your page will end up looking more or less like this:

![](https://s3-us-west-2.amazonaws.com/learn-app/lesson-images/rupg_screenshot.png)

Click [here](https://s3-us-west-2.amazonaws.com/learn-app/lesson-images/rupg_screenshot.png) to embiggen.

Plain and simple, but all the data comes from APIs - you will be writing virtually no text!

There are four APIs you'll need to use in order to accomplish this project:

-   [Random User Generator API](https://randomuser.me/documentation#format)
    -   This API returns an array of User objects which a bunch of data on each user
    -   You'll need to request 7 random people from this API
    -   The first will be your main user (the top section on the page), the next 6 will go in your "Friends" section

    -   From your main user you'll need a picture, a first name & last name, the city and state.
    -   From your other 6 users, you'll just the need first and last name
    -   Reference the image above to see how you should properly render this data

-   [Random Kanye Quote Generator API](https://kanye.rest/)
    -   This API returns a random quote from Kanye West
    -   You'll need the quote (the author is always Kanye)
-   [PokeAPI](https://pokeapi.co/docs/v2.html)
    -   This API is for querying all things pokemon - from cities in the poke-verse, to different berries, and the pokemon themselves
    -   You'll need to query for a random Pokemon from this API.

    -   From the pokemon object you'll need an image of the pokemon, and the name of the pokemon.

    -   *Hint/Fun Fact: there are currently 949 Pokemon recorded (but we know who the cool ones are...)*
    -   *Another Hint: Sprites are commonly known as images or computer graphics*
-   [Bacon Ipsum API](https://baconipsum.com/json-api/)
    -   This API returns random text, like a [Lorem Ipsum](https://www.lipsum.com/) text generator, but it's text about Meat. Mmm. Tasty.
    -   This is the text you will use for the "About Me" section at the bottom

* * * * *

Get started by forking [this repo](https://github.com/Elevationacademy/userPage-API-Project-Student). It contains the starter template of what needs to be done in the project.

Let's go through each part of the project and outline your requirements:

Renderer

-   Your Renderer is a *class* which contains each of the methods to render each section of the user page through Handlebars
-   We've set up some empty methods for you to fill out - their names should suggest what needs to happen in each one
-   You also have a "main" render method which should invoke all the "inner" methods with the relevant parameters

-   This method will receive the data object with all the data from the APIs

HTML

-   Each of your Renderer methods should have a corresponding Handlebars template script filled in here
-   Note that we are using separate scripts for each section - hence you will have to run the whole source-template-compile code for each script

APIManager

-   Your API Manager is a *class* with one loadData method - this should make all the API requests
-   The callbacks of your requests should update the data object in the constructor

main.js (your controller)

-   Here you should:
    -   Create the instances of the classes you'll be using
    -   Define the loadData and renderData functions
    -   Use the instances with MVC principles

    -   In particular, when the user clicks the Load User Data button, you should use your apiManager instance to get all the data
    -   When the user clicks the Display User button, you should invoke your render method and give it the data from the apiManager

    -   The way this works means your page will start empty, and only get populated once you load and display the data via the buttons - this is a limitation we will be able to overcome when we learn about Promises

We've filled in all the CSS for you, so need need to bother with that - but it's worth checking to see that you're using the same classes and IDs!

Alternatively, if you would like a design-challenge, get rid of the whole CSS and do it on your own ;)

* * * * *

#### WORKING WITH NEW APIS

Part of your work as a developer is to explore and understand new APIs - so if you can't figure out how to get what you want out of an API - read the documentation! Remember, when you make a request to an API you're playing by their rules and each API is different!

Strong suggestion: these are all pretty straightforward APIs, so you can test them out using Google (or any browser) - just paste the API link as a URL and you'll be able to see exactly what data returns, which keys it has, etc. Great starting point.

* * * * *

#### YOU'RE DONE!

#### EXTENSIONS

1\. Render every Name on your page in "Proper Case" ("My Name" instead of "my name")\
Create your own Handlebars Helper to do this - you can read on how to make one [here](https://handlebarsjs.com/block_helpers.html)

2. Add in two more buttons - a "Save User Page" button and a "Load User Page".

-   Your "Save User Page" button should save a snapshot of your current user to local storage
-   Your "Load User Page" button should load the user that you saved and render the exact user page back on the page - that means the same user, the quote, pokemon, meatText and friends they came with.

2.1 Save multiple users

-   Edit the object you're saving in Local Storage to be a users object. Every time you save a user, you should save the user's name as a key to your users object (yes, nested objects), and the snapshot of their page as the value.
-   Add a drop-down menu with the list of saved users (taken from local storage). Now, when you click on the "Load User Page" button, it should load the saved user you select from the drop-down menu

-   Hint: Object.keys() *might be useful here*

#### DONE FOR REAL NOW