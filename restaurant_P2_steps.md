
### project 2 steps

    Basic Steps to complete
    1: Fork and clone the server repository. 
    You’ll use this development server to develop your project code.
    
            --->see https://github.com/ichiLamuchy/mws-restaurant-stage-2

    2: Change the data source for your restaurant requests to pull JSON from the server, 
    parse the response and use the response to generate the site UI.
    
            ? helper js onto html page ?

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


## Gulp Hollow this to pull all plug in and make gulp.file

--save 
adds the package to your dependency list ("dependencies" in package.json). 
This is a list of only the dependencies that your package needs to run. 
These are the dependencies that need to be installed when a user installs 
your package from npm with the intent of using it.

--save-dev 
adds the package to your developer dependency list ("devDependencies" in package.json). 
This is a list of dependencies that you need only for developing the package. Examples would be like babel, gulp, a testing framework, etc.

#### npm install --global gulp-cli
start gulp
https://github.com/gulpjs/gulp/blob/master/docs/getting-started.md

#### npm init
initialise so packahe.json will be created

#### npm install --save-dev gulp@next
? (just first gulp set up)

#### npm install gulp-sass --save-dev
Set up gulp-sass
http://sass-lang.com/
https://www.npmjs.com/package/gulp-sass

#### $ npm install --save-dev gulp-autoprefixer
https://www.npmjs.com/package/gulp-autoprefixer

#### npm install -g browser-sync
Live editing
https://www.browsersync.io/

#### npm install gulp-eslint
Linting
https://www.npmjs.com/package/gulp-eslint

#### $ npm install --save-dev gulp-jasmine-phantom
Unit test


## Development and Production Mode
check if any can be imlay to project 2

## sass minification and concat
check code and need @import

#### npm install gulp-concat
JS concat - check through
gulp styles to generate new css style created and dropped in the correct folder dist/css/
Code for browser-sync to listen to change in index.html
- dont really know what it means


