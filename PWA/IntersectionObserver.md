https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API
https://developers.google.com/web/fundamentals/performance/lazy-loading-guidance/images-and-video/



#LAZY-LOADING 

regarding to the goole doc
lazy lloading is easy to do using Intersect observer before writing the `jS`
let's see the set up

create JS page then call on the both htmls

the img tag will be made on the each JS page 


### on the main.js write bsome code on line 143

img class="" src="placeholder-image.jpg" data-src="image-to-lazy-load-1x.jpg" data-srcset="image-to-lazy-load-2x.jpg 2x, image-to-lazy-load-1x.jpg 1x" alt="I'm an image!">
There are three relevant pieces of this markup we should focus on:

The class attribute, which is what we'll select the element with in JavaScript.
The src attribute, which references a placeholder image that will appear when the page first loads.
The data-src and data-srcset attributes, which are placeholder attributes containing the URL for the image we'll load once the element is in the viewport.


        document.addEventListener("DOMContentLoaded", function() {
          var lazyImages = [].slice.call(document.querySelectorAll("img.lazy"));

          if ("IntersectionObserver" in window) {
            let lazyImageObserver = new IntersectionObserver(function(entries, observer) {
              entries.forEach(function(entry) {
                if (entry.isIntersecting) {
                  let lazyImage = entry.target;
                  lazyImage.src = lazyImage.dataset.src;
                  lazyImage.srcset = lazyImage.dataset.srcset;
                  lazyImage.classList.remove("lazy");
                  lazyImageObserver.unobserve(lazyImage);
                }
              });
            });

            lazyImages.forEach(function(lazyImage) {
              lazyImageObserver.observe(lazyImage);
            });
          } else {
            // Possibly fall back to a more compatible method here
          }
        });




