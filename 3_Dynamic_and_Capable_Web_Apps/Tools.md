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
  
  example (refer code on set up)
  gulp style 
  to generate new css style created and dropped in the correct folder


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
        /*eslint-env node */

        var gulp = require('gulp');
        var sass = require('gulp-sass');
        var autoprefixer = require('gulp-autoprefixer');
        var browserSync = require('browser-sync').create();
        var eslint = require('gulp-eslint');
        var jasmine = require('gulp-jasmine-phantom');

        gulp.task('default', ['styles', 'lint'], function() {
            gulp.watch('sass/**/*.scss', ['styles']);
            gulp.watch('js/**/*.js', ['lint']);

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

        gulp.task('tests', function () {
            gulp.src('tests/spec/extraSpec.js')
                .pipe(jasmine({
                    integration: true,
                    vendor: 'js/**/*.js'
                }));
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

        see on https://www.npmjs.com/package/gulp-eslint


### Lint precommit hooks

### Set up Unit Test

fiest install phantom JS
http://phantomjs.org/
then 
install gulp-jasmine-phantom
https://www.npmjs.com/package/gulp-jasmine-phantom


# Awsome optimisation

        Example
            /*eslint-env node */

            var gulp = require('gulp');
            var sass = require('gulp-sass');
            var autoprefixer = require('gulp-autoprefixer');
            var browserSync = require('browser-sync').create();
            var eslint = require('gulp-eslint');
            var jasmine = require('gulp-jasmine-phantom');
            var concat = require('gulp-concat');
            var uglify = require('gulp-uglify');

            gulp.task('default', ['copy-html', 'copy-images', 'styles', 'lint', 'scripts'], function() {
                gulp.watch('sass/**/*.scss', ['styles']);
                gulp.watch('js/**/*.js', ['lint']);
                gulp.watch('/index.html', ['copy-html']);
                gulp.watch('./dist/index.html').on('change', browserSync.reload);

                browserSync.init({
                    server: './dist'
                });
            });

            gulp.task('dist', [
                'copy-html',
                'copy-images',
                'styles',
                'lint',
                'scripts-dist'
            ]);

            gulp.task('scripts', function() {
                gulp.src('js/**/*.js')
                    .pipe(concat('all.js'))
                    .pipe(gulp.dest('dist/js'));
            });

            gulp.task('scripts-dist', function() {
                gulp.src('js/**/*.js')
                    .pipe(concat('all.js'))
                    .pipe(uglify())
                    .pipe(gulp.dest('dist/js'));
            });

            gulp.task('copy-html', function() {
                gulp.src('./index.html')
                    .pipe(gulp.dest('./dist'));
            });

            gulp.task('copy-images', function() {
                gulp.src('img/*')
                    .pipe(gulp.dest('dist/img'));
            });

            gulp.task('styles', function() {
                gulp.src('sass/**/*.scss')
                    .pipe(sass({
                        outputStyle: 'compressed'
                    }).on('error', sass.logError))
                    .pipe(autoprefixer({
                        browsers: ['last 2 versions']
                    }))
                    .pipe(gulp.dest('dist/css'))
                    .pipe(browserSync.stream());
            });

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

            gulp.task('tests', function () {
                gulp.src('tests/spec/extraSpec.js')
                    .pipe(jasmine({
                        integration: true,
                        vendor: 'js/**/*.js'
                    }));
            });

### Development and Production Mode

    separate them but check production mode time to time

    make dist file so separate from sauce file
    Structiure 

        - Dist
            - css/
            - js/
            - index.html


    so if you do (refer to code above)
    gult styles
    to generate new css style created and dropped in the correct folder dist/css/

    Code for browser-sync to listen to change in index.html

        gulp.watch('./build/index.html')
        .on('change', browserSync.reload)

#### Sass concatination
    Sass doe sboth concatination and minification for you 
    manual concatination is not nesessary
    you can include sinfle sass file isn html
    then use inport directive in your Sass to input other files
    @import
    
    
    minification
    .pipe(sass({utputStyle: 'compressed'}))
    
#### JS concatination

    you need to plug in 
    npm install gulp-concat
    
    +++ gothrough again from 14-7
    
    








