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



## Gulp (& Grunts)

Gulp focus on code 
Grunt focus on configuration

Gulp is speedy!

example (refer code on set up)
gulp style 
to generate new css style created and dropped in the correct folder

THIS SERIES 3 PARTS ARE GOOD
https://www.youtube.com/watch?v=mCW3Q28QXIs
  
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
    
    
## Souce Map

https://docs.google.com/document/d/1U1RGAehQwRypUTovF1KRlpiOFze0b-_2gc6fAH0KY0k/edit

[Plugins with gulp sourcemaps support](https://github.com/gulp-sourcemaps/gulp-sourcemaps/wiki/Plugins-with-gulp-sourcemaps-support)

Setup
Source maps in gulp are easy to setup. It’s a use case where pipes really shine.

Install the gulp-sourcemaps plugin.

Require the gulp-sourcemaps plugin and in your scripts-dist or scripts (or styles) task, 
add a pipe to sourcemaps.init() after you get the source but before you send the source files 
through any pipes that transform them materially. 
After all plugins and pipes have been applied but before you save to the destination, 
pipe through sourcemaps.write() with an optional location parameter if you don't want the source maps to be inlined.

var sourcemaps = require('gulp-sourcemaps');

     gulp.task('scripts-dist', function() {
       gulp.src('js/**/*.js')
        .pipe(sourcemaps.init())
        .pipe(concat('all.js'))
        .pipe(uglify())
        .pipe(sourcemaps.write())
        .pipe(gulp.dest('dist/js'));
    });
  
In the developer console, 
the output of app should automically link errors in the generated code 
to their line numbers in the original source.

### Source map Support for other languages
In addition to things like concatenation and minification, 
source maps also support some languages/extensions that transpile to 
JavaScript like Typescript, CoffeeScript and ES6 / JSX.

You can read more some of the technical aspects of Source Maps on HTML5Rocks.
https://www.html5rocks.com/en/tutorials/developertools/sourcemaps/

This explains well x
https://knpuniversity.com/screencast/gulp/sourcemaps

### Image Optimaisation

check all those courses
https://eu.udacity.com/course/browser-rendering-optimization--ud860
https://eu.udacity.com/course/website-performance-optimization--ud884
https://eu.udacity.com/course/responsive-web-design-fundamentals--ud893
https://eu.udacity.com/course/responsive-images--ud882

## Image Compression
We’re then piping that output into our optimization plugins. 
We can compress images with either `lossless` or `lossy` compression algorithms. 
Lossless compression reduces a file in such a way that the original can be recreated 
from the compressed version. 
You can think of it as reducing the file size but not throwing away any information.

### Imagemin lossless
https://www.npmjs.com/package/gulp-imagemin

gulp-imagemin can losslessly compress JPEGs, GIFS, PNGs and SVGs out of the box. 
Lossless means that even though the file size will end up being smaller, 
special care is taken to not cause any visual changes whatsoever, 
meaning that original visual information stays exactly the same.

After you’ve grabbed the plugin you can simply add a pipe between 
the new crunch-images task and call imagemin() in there. 
There are a few extra options such as generating progressive images, 
but even without any configuration this will take all of your images and do any safe optimizations.

### Lossy Compression

Lossy compression, on the other hand, can only recreate an approximation of the original. 
Lossy compression can give you really small file sizes at the expense of image quality. 
But there are a few lossy optimizations that are truly smart, 
and PNG quantization is one of them. 
PNG quantization takes images with or without `alpha transparency` and converts them to 256 or less colored 8-bit pngs. 
Now if you do this manually and just convert a 16-bit image to a 8-bit image, you won’t like the results. 
It’ll end up...well..like a crappy gif, with unnatural, limited colors.

### PNG Quantization - lossy
PNG quantization benefits from the fact that there are colors that our vision and brain perceives as very similar, 
even though they’re technically completely different. 
The quantization algorithm aims to understand which colors actually matter and remaps them to new, optimized colors.

A cool thing about pngquant, the plugin we’re going to use, 
is that it automatically exits and will not save if a certain quality threshold isn’t passed.

### Set up image optiisation

Let's Try It
Download and require the imagemin-pngquant plugin in addition to gulp-imagemin.
https://www.npmjs.com/package/imagemin-pngquant
Create a config object for imagemin. 
These are the directives that imagemin will use when you pipe images to it. 
The following snippet instructs imagemin to use progressive rendering for JPEG images and PNG quant for well, PNGs.

    gulp.task('default', function() {
        return gulp.src('src/images/*')
            .pipe(imagemin({
                progressive: true,
                use: [pngquant()]
            }))
            .pipe(gulp.dest('dist/images'));
    });
    
Progressive rendering loads an image in layers where each layer makes the image more detailed. 
It can make a page feel faster than typical rendering line by line. 
If you like, you can now configure pngquant as well by adding quality or speed options. 
Read more about these on the plugin homepage.

Now you’ve got automatic image crunching in place and working for you but pro-tip, 
for anything important, take the time to see what will work, 
even if that means putting in a bit of elbow grease and checking things manually.

### Even better compression options
Smaller images can tolerate more aggressive lossy compression. 
You might want to try other things like converting images to SVG where applicable. 
SVG stands for Scalable Vector Graphics and uses a XML-based format 
to describe an image and can in most cases be scaled infinitely without 
any increase in file size or loss of image quality. 
If you’d like to further explore techniques to work with your images, 
head to the notes for a few advanced topics. 
This includes stuff such as automatically resizing your images to become responsive 
and fit retina and non-retina screens, or inlining your images into your CSS 
or into a sprite to save a couple more HTTP requests.

### scafolding
HTML boiler plate
https://html5boilerplate.com/
web starter kit
https://developers.google.com/web/tools/starter-kit/
Yaomen - this is the way
http://yeoman.io/






