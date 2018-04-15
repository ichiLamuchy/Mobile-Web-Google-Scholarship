### SW for Restaurant-APP-Project_1

Basic structure & improved fetch
    

const version= '1';
const staticCacheName = "review-v" + version;
const staticFiles = [
    "index.html",
    "restaurant.html",
    "css/styles.css",
    "data/restaurants.json",
    "js/dbhelper.js",
    "js/restaurant_info.js"
];

// install
self.addEventListener("install", (event) => {
    event.waitUntil(
        caches.open(staticCacheName).then((cache) => {
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
        return cacheName != staticCacheName;
        }).map(function (cacheName){
          return cache.delete(cacheName);
        })
      )  
    })
  );
});

//fetch
self.addEventListener('fetch', (event)=>{
    event.respondWith(    
        cache.match(event.request)
            .then((response)=>{
                // cash hit
                if (response) {
                    console.log("hit cache");
                    return response;
                }
                
                // clone request
                const fetchToNetwork = event.request.clone();
                return fetch(request)
                    .then(networkResponse => {
                        console.log(`Fetching ${request.url} from network`);
                        if(!networkResponse || networkResponse !== 200 || networkResponse.type !== 'basic') {
                            return networkResponse;
                            console.log(`Fetched ${request.url} from origin`);
                        }
                        const responseToCache = networkResponse.clone();
                        caches.open(staticCacheName)
                            .then(function(cache) {
                                cache.put(event.request, responseToCache);
                                // .then(() => console.log("Caching from origin succeed"))
                                // .catch(error => console.error("Caching from Network failed", error));
                                // return networkRes;
                            });
                            return response;
                        }
                })
        );
      
};

    
// to do, could use request.url
// add image file on static
// think of using whiteList array to check 


This can be a little help:
https://googlechrome.github.io/samples/service-worker/basic/
this guy made codes based on that
https://github.com/JeremieLitzler/mws-restaurant-stage-1/blob/master/sw.js
Just different way to code for img
https://github.com/FoxyHutch/mws-restaurant-stage-1/blob/master/sw.js


https://developers.google.com/web/fundamentals/primers/service-workers/#handling_responsive_images
some are put together all in once
https://github.com/anyulled/mws-restaurant-stage-1/blob/master/serviceWorker.js
