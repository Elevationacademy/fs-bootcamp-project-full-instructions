#### INTRO

Time to bring our new-found knowledge to a bit of practice.

In this mini-project, we're going to use a couple of APIs, host everything on a server, and of course throw in some OOP, Handlebars, and Grid.

Basically, you're going to build something like this:

![](https://s3-us-west-2.amazonaws.com/learn-app/lesson-images/ejn-roster-mini-project.PNG)

The user will be able to type in a team name in the input, and when they hit the Get Roster button, they'll get some information and images about players from that team.

You're mostly on your own for this one (even the CSS!) but these are your priorities:

1.  Get the server running and serving your client side
2.  Make the external API request inside the server (to the NBA API) work
3.  Make the API request from your client to your server work (hard-code it at first)
4.  Display the data from the client-server request on the page
5.  Make things pretty

To understand the overall architecture, look at this flow of events:

![](https://s3-us-west-2.amazonaws.com/learn-app/lesson-images/ejn-roster-architecture-flow.PNG)

Click [here](https://s3-us-west-2.amazonaws.com/learn-app/lesson-images/ejn-roster-architecture-flow.PNG) to embiggen.

Of course, your server will also server the entire client files using app.use(express.static...), but in terms of the flow of data, we have a client-server request, then server-externalAPI request, and then of course the data has to flow back: from the NBA API to our server, and from our server back to our client.

Keep referencing this image as you work on this project - it will be your north star.

* * * * *

#### PROJECT SPECS

This project has three parts: the client, your server, and an external NBA server.

Let's start with your server.

Server Specs

To get data about NBA players, you should use this API: http://data.nba.net/10s/prod/v1/2018/players.json. Make sure you [explore this API's data](http://data.nba.net/10s/prod/v1/2018/players.json) before trying to use it.

You should make this request inside a route on your server. Specifically, create a /teams/:teamName route. We'll explain the teamName parameter soon. Inside the callback of this route, make your request to the NBA API using the request module. In terms of the [flow](https://s3-us-west-2.amazonaws.com/learn-app/lesson-images/ejn-roster-architecture-flow.PNG), this is part 2.

Notice that when you make a request to this API *from the server*, you're going to receive a very big string with some data in it.

You will need to JSON.parse this string (remember, you need to first extract it from the body of the API's response). The actual data you're interested is an array that is inside .league.standard - this holds several objects, each of which has a lot of data about each player in the NBA. In terms of the [flow](https://s3-us-west-2.amazonaws.com/learn-app/lesson-images/ejn-roster-architecture-flow.PNG), this is the end of part 3.

You'll need to filter this data to match a certain teamId. For now, you can use this object to map between team names and team IDs:

const teamToIDs = {
    "lakers": "1610612747",
    "warriors": "1610612744",
    "heat": "1610612748",
    "suns": "1610612756"
}\
This object should be defined outside of your route. Now you can use the :teamName parameter to get the relevant teamId, and filter the data from the API accordingly.

Note that there are two filter conditions:

1.  You're only interested in players with a matching teamId
2.  You're only interested in players whose isActive status is true

For example, if someone accesses the route localhost:3000/teams/heat, you should filter that data such that you're only left with players whose teamId is 1610612748, and whose isActive is true.

Once you're done with the filter, you'll want to return an array with only the following properties for each player: firstName, lastName, jersey, pos - there are many other pieces of data for each player, but make sure you're only returning these fields (and their values, of course).

Ultimately, the teams/:teamName route should send a response with an array that looks something like this (assuming they went to /teams/heat) :

```
[
    { firstName: "Lebron", lastName: "James",  jersey: 23, pos: "F" },
    { firstName: "Alex", lastName: "Caruso",    jersey: 4, pos: "G" },
    //...
]
```

In terms of the [flow](https://s3-us-west-2.amazonaws.com/learn-app/lesson-images/ejn-roster-architecture-flow.PNG), this is part 4.

* * * * *

That's pretty much it for the server. Make sure you test your route with the other teams (warriors, lakers, suns) to make sure you're getting the correct array in return.

Remember, you can test simple GET requests directly in the browser! Just run your server and go to http://localhost:3000/teams/warriors, for example, and make sure you're seeing the array you expect on the page.

* * * * *

Client Specs

Most of this part should be straightforward.

You should have an input and a button on your page. In the input, the user can type a team name such as heat or warriors

When the user presses the button, it should invoke a function that grabs the team name from the input, and makes a GET request to your server - specifically, the request should be to your /teams/:teamName route. In terms of the [flow](https://s3-us-west-2.amazonaws.com/learn-app/lesson-images/ejn-roster-architecture-flow.PNG), this is part 1.

When the data comes back (i.e, in the callback) - invoke a separate function that renders the data.

For starters, only render the name, jersey number, and position (pos) of each player.

At this point, when you go to localhost:3000/, your page should look something like this:

![](https://s3-us-west-2.amazonaws.com/learn-app/lesson-images/ejn-roster-mini-project-partial.PNG)

Not very pretty yet, but it works! That's your client making a request to your server which is making a request to an external NBA API!

And at this point, you've completed the [entire architecture](https://s3-us-west-2.amazonaws.com/learn-app/lesson-images/ejn-roster-architecture-flow.PNG)! Now we just need to add some finishing touches.

* * * * *

Once that is set up, check out [this resource](https://nba-players.herokuapp.com/).

It shows us that we can get headshots for any NBA player if we provide a lastName/firstName, like this:

https://nba-players.herokuapp.com/players/{lastName}/{firstName}

Note that this link *returns an image!* As such, you should insert it directly into your img tag's src attribute. Remember, the only data you need to make this work is the first and last name of the player, which you already have from your previous request to the teams route.

Make sure this is all set up properly using handlebars - don't forget that you can have handelbars directly in the src!

* * * * *

Finally, once you're displaying images and data - go ahead and prettify everything. Add some grid in there. Make it look at least like this, if not nicer:

![](https://s3-us-west-2.amazonaws.com/learn-app/lesson-images/ejn-roster-mini-project.PNG)

* * * * *

#### EXTENSIONS

OOP

If you didn't use OOP as much as possible (at least in the client side) - do so! There are at least two separate concerns here: fetching data from your server, and rendering it.

More Data (non-trivial)

The resource we used for images also has some references for getting [player stats](https://nba-players.herokuapp.com/).

Figure out how that works, and add another route in your server called /playerStats/:player.

When you click on any player's image, it should display the player's stats over the image.

* * * * *

#### SWISH ≈ 

Well done. You've completed your first fancy server project ~ feel good.