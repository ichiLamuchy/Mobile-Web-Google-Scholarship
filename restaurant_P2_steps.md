#### Server usage
    on mws-restaurant-stage-2 (use bash)
    # node server
    on mws-restaurant-stage-1 (use terminal on vs code)
    serve -p 8000 -o
    
### RESTAURANT APP analysis

    INDEX.JS
        when it loaded 
        fetchNeigberhood() is called which originally come from DBHelper
        fetchCuisins() is called which originally come from DBHelper
        Both functions use fetchRestaurants() in DBHelper
        which fetch the text from server 1337, purse the text (restaurants) to object by using .json()

    All the functions in restaurant_info.js are also reading datas from fetchRestaurants




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

    So main things

      1: Change to Use server data instead of local memory 
      by use fetch API.
      2: Use IndexedDB to cache JSON responses
      3: accessability retained as it is
      4: check performance using lighthouse

      rubricks:
      https://review.udacity.com/#!/rubrics/1131/view



#### Lighthouse:
    You can audit your site's performance with Lighthouse by 
    using the Audit tab of Chrome Dev Tools.

    Lighthouse measures performance in four areas, but your review will focus on three:

    Progressive Web App score should be at 90 or better.
    Performance score should be at 70 or better.
    Accessibility score should be at 90 or better.


#### Tip !
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
https://developers.google.com/web/ilt/pwa/working-with-indexeddb
        
        // make a function called newFetchR for indexed db
        
        
        var dbPromise = idb.open('restaurant_app', 4, function(upgradeDb) {
          switch(upgradeDb.oldVersion) {
            case 0:
              var keyValStore = upgradeDb.createObjectStore('keyval');
              keyValStore.put("world", "hello");
            case 1:
              upgradeDb.createObjectStore('people', { keyPath: 'name' });
       
       return dbPromise;
              
        // if sw not exist, don't bother and error out
        // if it does
        // open indexed db restaurant_app
        // callback with parameter (upgradeDB) to create object store called restaurants
        // it would throw error if the name of the object store exists
        
       
            if (!upgradeDb.objectStoreNames.contains('restaurants')) {
                upgradeDb.createObjectStore('restaurants');
            }
        
        // make keypath : id
        
        // make db.transacton to transactonable for read write
        // get the restaurants object store from the db. transaction
        // add or pu t  write onto the db.
        
        // when the network requests happen, the browser try to read it form indexed.db 
        for the contents of restaurants which are all handked in the js
       
       

        // this would be called if sw is not existed or any of fetch fall back
        static fetchRestaurants(callback) {
            fetch("http://localhost:1337/restaurants")
              .then(resp => resp.json())
              .then(json => callback(null, json))
              .catch(err => callback(err, null))
          }
          
        // use inport idb from 'idb'; idb pollyfield 
        // open db Promise the indexed .db

        var dbPromise = idb.open('restaurant-app', 1, function (upgradeDb){
            if (!upgradeDb.objectStoreNames.contains('restaurants')) {
                upgradeDb.createObjectStore('restraurants', {keyPath: 'id'});
            }
        }

        // make transaction write

        dbPromise.then(function(db){
            var tx = db.transaction ('restaurants', 'readwrite');
            var restaurantsStore = tx.objectStore('restaurants');

            // add data from network 
            resstaurantsStore.put(function(data){
            return  fetch(http://localhotst:1337/restaurants")
                .then (res=>res.json())
                .then (json=>json);
        }

        // if it is there make transaction to read when request happens
        // how do i do ?





### How to use indexed DB
Browser can get the Skelton static from cache through service worker.
But updated dynamic contents from indexed db
Open websocket to get updated contents from network (by pass http cache and sw)
Browser update the contents to indexed db when the contents arrived

### Fetch When do you use it

fetch is use for making network request similar to http request.
it use promise.

promise 
synchronise behavior of request / response

So simply when you use it is some thing need to be updated while it has been
 chached in between origin and browser
 
 or need to display something 


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

#### Use of Localforage
Enter localForage, a JavaScript library that provides the ease of use of localStorage with all the advanced features of IndexedDB.

http://blog.teamtreehouse.com/using-localforage-offline-data-storage

Just simple getter and setter

localforage.getItem('key', callbackFunction);
localforage.setItem('key', 'value', callbackFunction);

JS to write one from network
one from indexed DB

(from nicolas)
http://podcast.freecodecamp.org/ep-33-code-dependencies-are-the-devil
