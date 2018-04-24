### Debug on the developer's tool

    fetch(`https://api.unsplash.com/search/photos?page=1&query=${searchedForText}`, {
        headers: {
            Authorization: 'Client-ID abc123'
        }
    }).then(function(response) {
        debugger; // work with the returned response
    });

     debugger line inside the .then() function, 
     the code will pause on the debugger line when the response is finally returned.
 
 
 ### The Responce Object
 
    a response object has information about the response itself, 
    it doesn't have the data...yet. To actually get the data, 
    we need to get the "body" of the response.
  
    The .json() method on a Response object returns a Promise, 
    so we need to chain on another .then() to actually get and start using the returned data. 
    This time, let's call addImage to pass it the returned data:

    fetch(`https://api.unsplash.com/search/photos?page=1&query=${searchedForText}`, {
        headers: {
                Authorization: 'Client-ID abc123'
            }
        }).then(function(response) {
            return response.json();
        }).then(addImage);

        function addImage(data) {
            debugger;
        }

    if you wanted to fetch an image
      .blob() will extract the image body from the response.
  
[Making Fetch Request](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch#Making_fetch_requests)
https://davidwalsh.name/fetch

ES6 on Fetch

    // without the arrow function
    }).then(function(response) {
        return response.json();
    })

    // using the arrow function
    }).then(response => response.json())

    ES6 course:
    https://classroom.udacity.com/courses/ud356

Display The Image On The Page
We're making our request to Unsplash, 
it's returning a response that we're then converting to JSON, 
and now we're seeing the actual JSON data. Fantastic! 
All we need to do now is display the image and caption on the page.

Here's the code that I'm using:

    function addImage(data) {
        let htmlContent = '';
        const firstImage = data.results[0];

        if (firstImage) {
            htmlContent = `<figure>
                <img src="${firstImage.urls.small}" alt="${searchedForText}">
                <figcaption>${searchedForText} by ${firstImage.user.name}</figcaption>
            </figure>`;
        } else {
            htmlContent = 'Unfortunately, no image was returned for your search.'
        }

        responseContainer.insertAdjacentHTML('afterbegin', htmlContent);
    }
    This code will:

    get the first image that's returned from Unsplash
    create a <figure> tag with the small image
    creates a <figcaption> that displays the text that was searched for along with the first name of the person that took the image
    if no images were returned, it displays an error message to the user

### Handling Errors

    Issues with the network
    Issues with the fetch request
    Unsplash not having an image for the searched term

    fetch(`https://api.unsplash.com/search/photos?page=1&query=${searchedForText}`, {
        headers: {
            Authorization: 'Client-ID abc123'
        }
    }).then(response => response.json())
    .then(addImage)
    .catch(e => requestError(e, 'image'));

    function addImage(data) {
        debugger;
    }

    function requestError(e, part) {
        console.log(e);
        responseContainer.insertAdjacentHTML('beforeend', `<p class="network-warning">Oh no! There was an error making a request for the ${part}.</p>`);
    }
    
    
 # Ondexdb
 
 wenplat form has hata base valled indexdb
 
    
    
    
    
    
    
    
    
    
    
    
    
# 
