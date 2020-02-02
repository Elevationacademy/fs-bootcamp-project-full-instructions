#### INTRO

This extension of the My Roster project should comes as no surprise to you, following what we've learned about CRUD, Router, and Middleware.

You can probably entirely guess what we're going to do here, but just to be clear...

* * * * *

#### CLEANING UP YOUR SERVER

For starters, **separate your `server.js` to the proper setup that takes advantage of `express.Router` in a separate file** - make sure everything is still working.

* * * * *

#### ADDING A TEAM

In our `server.js` we have a `teamToIDs` object which currently only has 4 teams.

Your next task is to **add a `put` route called `/team`** - you should send an object to this route - **not** a query string or parameters, but an actual object - that looks like this: `{teamName: {name}, teamId: {id}}` - use this object to update the `teamToIDs` object.

**Don't forget**, data you send to the server comes in as JSON.

Use the following data to test your route:

```
wizards - "1610612764"
raptors - "1610612761"
spurs - "1610612759"
rockets - "1610612745"
```

This is an "admin-only" operation, so there should be **no UI** for this. Test it using Postman.

* * * * *

#### MY ROSTER

Now you're going to make this an actual roster-building application.

For reference (if you're not big on sports), some fans like to fantasize about the Ideal Roster, i.e. the perfect team that would be undefeatable.

Generally they'll pick one or two players from a number of different teams to create this Ultimate Team.

Your task is to **implement this roster generation feature**. Here are your guidelines:

-   Start by creating a `get` route called `/dreamTeam`

  -   This route should return an array of 5 players
  -   You'll have to create this array, of course: call it `dreamTeam`

-   Next, you'll need a `post` route called `/roster` which accepts a single player

  -   This route accepts a player (with first name, last name, jersey number, and position)
  -   Of course, this data should come as an object - not as a query string or parameter
  -   You should add this object to your `dreamTeam` array

That's it for the **backend**, next you'll need to complete the **client** code:

-   Start by adding a button called `Dream Team`

  -   When you click this button, it should make a GET request to `/dreamTeam`
  -   Use the data that returned from the server and display the Dream Team on the page

-   Next, either add a button or just an `onclick` to each `.player`

  -   Clicking this button should send a POST request to `/roster` with the info about the clicked player

And there you have it: your own roster generator.

* * * * *

#### EXTENSIONS

Hungry for more challenges? No problem. You should be able to do all of these:

-   Prevent the user from adding the same player to the `dreamTeam` array
-   Allow users to remove players from the `dreamTeam` array (make sure you use the `delete` route)
-   Make sure your code is entirely OOP, MVC compliant
-   Let users save a roster with a name (like "East Coast Roster" or "Cali Team") - use Local Storage for now

Once you've done all that, certainly congratulate yourself.\
You the [real MVP](https://www.youtube.com/watch?v=NmRJgKbibB8).