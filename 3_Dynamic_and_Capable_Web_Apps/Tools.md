# Tools

### Build-in Command

**Searching**

`CMD + T` to find fuzzy finding the file


**Symbol serch menu**

`@` or `CMD + R`

Locate stuff in a current file

**Find the word**

Higlight the word and hit `CMD + ALT + G` to find next instance of it

**Tab completion**

**Multiple seltction**

ALT and drag - not really use

`Select` by ightlight then press `CMD + D` to go next instance

`CMD + CTRL + G ti selct all the word i the file



### Gulp & Grunts

  Gulp focus on code 
  Grunt focus on configuration

  Gulp is speedy!


### Live editing

1. Every key stroke in Editor
2. Every save via Gulp
3. All in the browser!

Check plug in of live preview for your local editor.

Workspaces enable you to save a change that you make in Devtools to a local copy 
of the same file on your computer.

https://developers.google.com/web/tools/chrome-devtools/workspaces/

browser sync
https://www.browsersync.io/


note: Globally installed so far

  gulp
  browser sync
  

## Prevent disasters

### Linting

- via your editer
- via your build process
- via pre commit hook in version control

https://www.sitepoint.com/comparison-javascript-linting-tools/
https://eslint.org/

it checks 

- Code style and syntax

populer ones are JSHint, JSCS, ESLint

### Unit Test

Phantom JS - it's basically headless version of web kit
gilp jusmine-phantom plugin used that to its advantage 
to actuallu runyour test in a real browser test env
https://www.npmjs.com/package/gulp-jasmine-phantom

### Continuous Intergration in Cloud

Really good need to watch through
https://classroom.udacity.com/courses/ud611

### Development and Production Modes

Split development and production modes













# Set UP of Tools

    Example
        var gulp = require('gulp');
        var sass = require('gulp-sass');
        var autoprefixer = require('gulp-autoprefixer');
        var browserSync = require('browser-sync').create();

        gulp.task('default', ['styles'], function() {
          gulp.watch('sass/**/*.scss', ['styles']);

          browserSync.init({
            server: './'
          });
        });

        gulp.task('styles', function() {
          gulp.src('sass/**/*.scss')
            .pipe(sass().on('error', sass.logError))
            .pipe(autoprefixer({
              browsers: ['last 2 versions']
            }))
            .pipe(gulp.dest('./css'))
            .pipe(browserSync.stream());
        });


### Set up Gulp

Gulp https://github.com/gulpjs/gulp/blob/master/docs/getting-started.md

How to enable the root user on your Mac
https://support.apple.com/en-gb/HT204012



### Set up gulp-sass

npm install gulp-sass
http://sass-lang.com/
create folder called sass
then move all css file to extention .scss


### Set up gulp-autoprefixer
https://www.npmjs.com/package/gulp-autoprefixer

$ npm install gulp-autoprefixer
https://www.npmjs.com/package/gulp-autoprefixer


### Set up browserSync
https://www.browsersync.io/

npm install -g browser-sync


### Set up ES lint

        install 

        npm install eslint

        npm install -g eslint  (may require sudo)


        eslint --init 

https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint


top of the gulp file
you can set * eslin-env node */
this type of special comment works like configlration but it's local to current file

    on gulp file:

    var eslint = require('gulp-eslint');
        gulp.task('lint', function () {
          return gulp.src(['js/**/*.js'])
            // eslint() attaches the lint output to the eslint property
            // of the file object so it can be used by other modules.
            .pipe(eslint())
            // eslint.format() outputs the lint results to the console.
            // Alternatively use eslint.formatEach() (see Docs).
            .pipe(eslint.format())
            // To have the process exit with an error code (1) on
            // lint error, return the stream and pipe to failOnError last.
            .pipe(eslint.failOnError());
        });

        see on https://www.npmjs.com/package/gulp-eslint


### Lint precommit hooks

### Set up Unit Test

fiest install phantom JS
http://phantomjs.org/
then 
install gulp-jasmine-phantom
https://www.npmjs.com/package/gulp-jasmine-phantom







