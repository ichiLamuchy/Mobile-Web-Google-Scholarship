### SW for Restaurant-APP-Project_1
    https://developers.google.com/web/fundamentals/primers/service-workers/lifecycle (read read read)
    
SW is a script which your browser runs in the backend. 
To use SW you need to register first in your JS, then it goes to installing state,
where you cache.open and tipically started caching static contents. When it gets activate, 
you check if any contents can be deleted by checking against white list of array (using map and index of)
Last stage (event) is fetch, you get responce from cache if the name of the contents mached to the event.request.
If not you need to fetch it from netwowk (you need to clone the request) whitin the fetch, 
you open another cache to store the responce from the network.
    
    

    const version= '7';
    const reviewCacheName = "restaurant-v" + version;
    const dynamicCacheName = "d-restaurant-v" + version;
    const staticFiles = [
        "/",
        "index.html",
        "restaurant.html",
        "css/styles.css",
        "data/restaurants.json",
        "js/dbhelper.js",
        "js/restaurant_info.js",    
    ];

    // install
    self.addEventListener("install", (event) => {
        event.waitUntil(
            caches.open(reviewCacheName).then((cache) => {
                return cache.addAll(staticFiles);
            })
        );
    });

 
    // activate 
    self.addEventListener('activate', function(event) {
        event.waitUntil(
          caches.keys().then ((cacheNames)=>{
            return Promise.all (
              cacheNames.filter((cacheName)=>{
              return cacheName != reviewCacheName;
              }).map(function (cacheName){
                return caches.delete(cacheName);
              })
            )  
          })
        );
      });


    self.addEventListener('fetch', function(event) {
    event.respondWith(
      caches.match(event.request)
        .then(function(response) {
          // Cache hit - return response
          if (response) {
            return response;
          }
          // to clone the response.
          var fetchRequest = event.request.clone();
  
          return fetch(fetchRequest).then(
            function(response) {
              // Check if we received a valid response
              if(!response || response.status !== 200 || response.type !== 'basic') {
                return response;
              }

              // to clone it so we have two streams.
              var responseToCache = response.clone();
  
              caches.open(dynamicCacheName)
                .then(function(cache) {
                  cache.put(event.request, responseToCache);
                });
  
              return response;
            }
          );
        })
      );
  });

    
// to do, could use request.url
// add image file on static
// think of using whiteList array if I have more than 1 chache


    This can be a little help:
    https://googlechrome.github.io/samples/service-worker/basic/
    this guy made codes based on that
    https://github.com/JeremieLitzler/mws-restaurant-stage-1/blob/master/sw.js
    Just different way to code for img
    https://github.com/FoxyHutch/mws-restaurant-stage-1/blob/master/sw.js


    https://developers.google.com/web/fundamentals/primers/service-workers/#handling_responsive_images
    similar to one above but not sending straight from browser from origin instead put in cache
    https://github.com/anyulled/mws-restaurant-stage-1/blob/master/serviceWorker.js
