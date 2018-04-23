# Fetch API

- Fetch Is Promise-based

- Might Need A Polyfill 
  http://caniuse.com/#feat=fetch to check if  your browser support fetch API
  If not
  https://github.com/github/fetch
  This is pollyfill, you can add this to your project so you can use Fetch
  

### Cross-Origin Issues?
    Just because Fetch is new and awesome and is replacing the XHR object for making asynchronous network requests 
    doesn't mean it can bypass the rules for making those network requests. 
    Fetch requests still need to obey the cross-origin protocol of how resources are shared.

### How to add header
    https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/fetch
    https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch
    https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API
    
    he Fetch request takes the URL to the requested resource as the first argument,
    but the second argument is a configuration object. 
    One of the options to this config object is a headers property.

### Changing The HTTP Method
    fetch(`https://api.unsplash.com/search/photos?page=1&query=${searchedForText}`, {
        method: 'POST'
    });
    
