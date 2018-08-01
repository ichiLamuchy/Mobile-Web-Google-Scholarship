
### Summary

#### How To Make Responsive

    1:  Set the device as small as possible on Developer's Tool
    2:  Set viewport on Headder on index.html
    3:  Make all width 100% if they are less than 100% fixed 
        Tap area at least 48px
        Check them on developer tool
    4:  Make media quaries style sheet and link it on index file
    5:  Find break point and see what it can be done
    6:  Apply responsive pattens 
    7:  Deal with table if you ahve one
    8:  check font size, too









### 1: Start Small

>Testing Web
>http://udacity.github.io/RWDF-samples/quizzes/viewport-quiz/

>Check list on your frontend tool
>https://developers.google.com/web/tools/lighthouse/



### 2: Set viewport

    <meta name="viewport" content="with=device-width, initial-scale=1">

     initial-scale=1 means 1:1 
     so it will keep as it is on CSS

     CSS allow content to overflow it's container
     (Such as img overflow the size of div)
     To prevent this set 

     img, embed, object, video{
       max-width: 100%;
     }



    






### 4: Useing media queries (@media screen)

#### Adding basic media queries
https://developer.mozilla.org/en-US/docs/Web/CSS/@media#Media_types

    <link rel="stylesheet" media="screen and (min-width: 500px)" href="responsive500.css">
    then straight add body{background-color: green;} on responsive500.css
    
    or
    
    <link rel="stylesheet" type="text/css" href="responsive.css">
    then add below on responsive.css
    @media screen and (min-width: 500px){
        body{background-color: green;}
    }    
       
    don't do it with @import tag - expensive / too many http requests
    use max-width, min-width (according to blowser window)


### 5: Breakpoint 
    
    break point to change the size of written font and appearnce:

    example:
    725 minor break point
    800 minor break point - nav menu will show up, hamburger will disappeared
    960 break point - layout change
    1024 ads show up

    Where to put breakpoints:
    Look at contents!

    Step1: Make it small as I get
        Slowly size up and see the layout that where the content likes to have a breakpoint
    add link on head on each breakpoint
    
    
#### Grid fluid system 
    Boot strap, 960 pixel grid layout system and etc
    
##### Flexbox

    on <div> container add
    
    display:flex;       // defalt fit on the single line
    flex-wrap: wrap;    // can go next row, only re-seize when really need to do.
    
    css "order" attribute to change order
        @media screen and (min-width: 500px){
            header {width:100%; order:1;}
            .blue{width:10%; order:4;}
            .pink{width:90%; order:3;}
            .green{width:40%; order:2;}
            .orange{width:20%; order:5;}
         }
    
    
### 6 Responsive patterns
    
    ***** Mostly fluid *****
    
    below code can be on 1 sheet. Everything is just added onto original css file. 
    all @media screen can be on the page
    Only what you want to change (overwrite or add) from the original CSS will be on @media screen
    (Alternatively you can make separate CSS style sheet)
         
     Examples:

        .container{
            disolay: flex;
            flew-wrap: wrap;
        }
        .box{
            width: 100%;
        }

        @media screen and (min-width: 450px){
            .dark_blue, .green {width:50%;}
        }
        @media screen and (min-width: 550px){
            .dark_blue, .light_blue {width:25%;}
            .green, .red, .orange {width:33.3333%;}
        }

        *** the way to keep the margin after 800px width ***
        @media screen and (min-width: 700px){
            .container {width700px;
            margin-left: auto;
            margin-right: auto;
         }


    ***** Column drop *****

    Vertically until first break point hits

    then next breakpoint hits to change the shape

    Generally once the view port hits a maximum width, 
    the columns hit a maximun size, and instead of getting wider,
    margins are added to the left and right

        .container{
            disolay: flex;
            flew-wrap: wrap;
        }
        .box{
            width: 100%;
        }

        // if the vp changed >= 450px
        @media screen and (min-width: 450px){
            .dark_blue {width:25%;}
            .light_blue {width:75%;}
        }

        @media screen and (min-width: 550px){
            .dark_blue, .green {width:25%;}
            .light_blue {width:75%;}
        }

    ***** Layout shifter *****

        using order attribute. moving the place around.
        set 
            width: and order:
        you can set negative number too
        default start from 0

    Off canvas:
    for NAV

        https://classroom.udacity.com/nanodegrees/nd024/parts/0bf842e9-7269-42de-b68b-812ca7823517/modules/e08f25bf-f172-4fb8-9812-b09ca908ae37/lessons/3561069759/concepts/35307193050923
        off screan content is only comes in when width is big enough

        example of side nav :
        https://www.w3schools.com/howto/howto_js_sidenav.asp
            // JS
            menu.addEventListener('click', function(e) {
                drawer.classList.toggle('open');
                e.stopPropagation();
            });
            // CSS
            nav {
              width: 300px;
              position: absolute;
              /* This trasform moves the drawer off canvas. */
              -webkit-transform: translate(-300px, 0);
              transform: translate(-300px, 0);
              /* Optionally, we animate the drawer. */
              transition: transform 0.3s ease;
            }
            nav.open {
              -webkit-transform: translate(0, 0);
              transform: translate(0, 0);
            }


### The way it works (for me) on Responsive Pattern
  
  
#### 6-1: to CSS main
  
      1. Look the website
      2. Find any segment can be moved together - normally where wrapped in <section> tag
        give is flow-glow attribute to main css (smallest width first)
      3. Make sure to set width 100% to all section (hopefully separately) 
      4. Add some padding if necessary
  
#### 6-2: to index.html
      1. this is hamburger menu svg
        <a id="menu" class="header__menu">
          <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24">
            <path d="M2 6h20v3H2zm0 5h20v3H2zm0 5h20v3H2z"/>
          </svg>
        </a>
        
#### 6-3: to response CSS file
       1. on the top

            .content {
              display: flex;
              flex-wrap: wrap;
            }

            .header__menu {
              display: none;
            }

            .hero, .top-news, .scores, .weather, .recent-news {
              order: 10;
            }

        2: first media query is tidy up header bit - logo, title, nav
            
            This is the example
            .nav {
                z-index: 10;
                background-color: #fff;
                width: 300px;
                position: absolute;
                /* This trasform moves the drawer off canvas. */
                -webkit-transform: translate(-300px, 0);
                transform: translate(-300px, 0);
                /* Optionally, we animate the drawer. */
                transition: transform 0.3s ease;
              }
              .nav.open {
                -webkit-transform: translate(0, 0);
                transform: translate(0, 0);
              }
              .nav__item {
                display: list-item;
                border-bottom: 1px solid #E0E0E0;
                width: 100%;
                text-align: left;
              }
              .header__menu {
                display: inline-block;
                position: absolute;
                right: 0;
                padding: 1em;
              }
              .header__menu svg {
                width: 32px;
                fill: #E0E0E0;
              }
            }

        3: to the each breakpoint add "order" attribute and "width" on the each section
        where flow-glow attribute presented

            <script>
            /*
            * Open the drawer when the menu ison is clicked.
            script for burger menu
            */
            var menu = document.querySelector('#menu');
            var main = document.querySelector('main');
            var drawer = document.querySelector('.nav');

            menu.addEventListener('click', function(e) {
            drawer.classList.toggle('open');
            e.stopPropagation();
            });
            main.addEventListener('click', function() {
            drawer.classList.remove('open');
            });

            </script>

        4: @media screen on each break point
            mostly change     
                order: 1;
                width: 40%;

        5: set @media screen width as 

            @media screen and (min-width: 850px) {
              main, .header__inner, .nav, .content {
                width: 850px;
                margin-left: auto;
                margin-right: auto;
              }


#### Resauce
    get image Responsive

check out:
https://classroom.udacity.com/courses/ud882

tables:
https://www.thoughtco.com/display-none-vs-visibility-hidden-3466884

Table Dable Tricks:
https://css-tricks.com/responsive-data-table-roundup/



### 7: What to do with tables - 3 ways

    1. hiden columns
           check what is the most important ones to show
           put display: none for all others


    2. no more tables 
            1: 
                table, thread, tbody, th, td, tr{
                    display: block;
                }
            2: hide table header instead of display none, just keep it way off screen
                thread tr {
                    position: absolute;
                    top: 9999px;
                    left: -9999px
                }
            3: just add padding and set the position relative to td
            4: 
            td:before{
                    position: absolute;
                    left: 6px;
                    content: attr(data-th);// pull the data element of each of td elements
                    front-weight bold;
                }
            }

    3. contained tables

        wrap in the div "contained_table"
        div>contained_table{
            width: 100%
            overflow-x: auto;
        }


### 8: Font reading

 
    ideal measure is 45-90cpl
    pretty solid consensus around 65 cpl for web
 
    set at least 
    font-size:18 px
    line height: 1.25em
 
    minor break point 
    adding padding 
    make font size bigger for easier to read
 
 
 

      

    
    
    
    
    
