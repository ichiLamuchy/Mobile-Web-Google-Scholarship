# Ajax with JQuery

Making an Ajax call

      $.ajax({
          url: 'https://swapi.co/api/people/1/'
      });


Responce : e can chain on to .ajax() with a .done() method.

    function handleResponse(data) {
        console.log('the ajax request has finished!');
        console.log(data);
    }

    $.ajax({
        url: 'https://swapi.co/api/people/1/'
    }).done(handleResponse);

    - we do not need to create an XHR object

    adding header code below unser url
    
    headers:{
        Authorization: "ClietID 11122asd34'
    }


#### Is it JSON?

    Content isn't getting added to the page jQuery detects the response 
    and if it's JSON, it will automatically convert it to JavaScript for us.
    
    //function addImage() {
        //const data = JSON.parse(this.responseText);
        //const firstImage = data.results[0];
    *** instead ****
    
    function addImage(images) {
        const firstImage = images.results[0];
    
        responseContainer.insertAdjacentHTML('afterbegin', `<figure>
                <img src="${firstImage.urls.small}" alt="${searchedForText}">
                <figcaption>${searchedForText} by ${firstImage.user.name}</figcaption>
            </figure>`
        );
    }
    
    What changed
        * the function now has one parameter images
        * this parameter has already been converted from JSON to a JavaScript object, 
            so * the line that had JSON.parse() is no longer needed.
        *the firstImage variable is set to the images.results first item

### DEvelopers tool
#### jQuery debugger

[Pause Your Code With Breakpoints](https://developers.google.com/web/tools/chrome-devtools/javascript/breakpoints)

[JavaScript Debugging Reference](https://developers.google.com/web/tools/chrome-devtools/javascript/reference)

    DevTools provides is the JavaScript Call Stack. -> sources tag
    This displays the order of function calls that are in progress. 
    The function at the bottom of the stack is the first one to run. 
    It calls the second one on the stack...the second calls the third, the third

