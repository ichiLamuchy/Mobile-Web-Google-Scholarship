#### Server usage
    on mws-restaurant-stage-2 (use bash)
    # node server
    on mws-restaurant-stage-1 (use terminal on vs code)
    serve -p 8000 -o
    





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

    


### Steps for index db in this project

use inport idb from 'idb'; idb pollyfield  
Task: Cache the JSON responses for offline use by using the IndexedDB API.

The json is details for the restaurants 

openDataBase Function
1 creating promise for database by opening the data base
2 create object store 
3 detaermine what to store (restaurant details)
4 define key (id) and define indexed by if necessary

openSocket Function
5 Parse the Json received then store in object sore, 
it shoud happen fetchRestaurant function
indexController._onsocketMessage on witter.
is where JASON.parse

showRestaurant function
6 call openSocket function within to show the restaurant
7 get restaurant details from the object store then possibly send to another function 
such as show post restrantinfo.js and mainjs?


Logic, 
browser get the skelton static from cache through service worker.
But updated dynamic contents from indexed db
Open websocket to get updated contents from network (by pass http cache and sw)
Browser update the contents to indexed db when the contents arrived

(you need indexController.js for all the display this incluse 
regesterServiceWorker, event listeniner such as listening to websocket, pass it to json)

#### Tip

method indexdDB.deleteDatabase('database name')
on the colsole dev tools to delete the indexedDB

force update on reload check on dev tools - easier to develop



  Basic steps:
  1.Get data from ide.open                  - step 1
  2.Open transaction on database            - step 2
  3.Open object store on transaction        - step 2
  4.Optionally open index on object store
  5.Perform operation on object store or index
