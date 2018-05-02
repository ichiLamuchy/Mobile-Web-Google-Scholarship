
### project 2 steps

    Basic Steps to complete
    1: Fork and clone the server repository. 
    You’ll use this development server to develop your project code.
    
            --->see https://github.com/ichiLamuchy/mws-restaurant-stage-2

    2: Change the data source for your restaurant requests to pull JSON from the server, 
    parse the response and use the response to generate the site UI.
    

    3: Cache the JSON responses for offline use by using the IndexedDB API.

    4: Follow the recommendations provided by Lighthouse to achieve 
    the required performance targets.

    4: Submit your project code for review.

So two main things

  1: Change to Use server data instead of local memory 
  by use fetch API.
  2: Use IndexedDB to cache JSON responses
  3: accessability retained as it is
  4: check performance using lighthouse
  
  rubricks:
  https://review.udacity.com/#!/rubrics/1131/view



You can audit your site's performance with Lighthouse by 
using the Audit tab of Chrome Dev Tools.

#### Lighthouse:
    You can audit your site's performance with Lighthouse by 
    using the Audit tab of Chrome Dev Tools.

    Lighthouse measures performance in four areas, but your review will focus on three:

    Progressive Web App score should be at 90 or better.
    Performance score should be at 70 or better.
    Accessibility score should be at 90 or better.


#### Tip
    When you wanna see json data in formated
    go to developer's tool, go to console, then write such as
    json = <then paste the json data> then you see it in the formated way
    
    manifest
    for app - manifest fil will be read when it opens in the browser
    if it opens a couple - a few times, the browser ask for if you woul like to down load app
    https://app-manifest.firebaseapp.com/
    
    console on developer's tool
    use such as fetch(http://localhotst:1337/restaurants")
    .then (res=>res.json())
    .then (json=>json)    
    so you can see the result 
    
    on the fetch on sw
    check if I can break down more
    
### `npm i -g serve` to install server 
Now I can use `serve -p 8000 -o` to listen to port 8000

At the moment web application is using port 8000 / getting Json data from port 1337

    


