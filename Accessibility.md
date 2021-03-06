
 ## Accessibility
 repo: https://github.com/udacity/ud891


    Easier to read,
    It makes sense
    Good contrast for read

    Visual impairment:
        Need - Sound, navigate through key boad, large print, color contrast, screen reader

    Minor or dexterity impairments
         They use only key boad, eye tracking software, twitches, voice dictation

    Hearing impairments:
        i.e, messenger app could provide flash alart as well as sound nortification

    Cognitive impairment : ADD Dyslecxia, autism
        Zoom in to easier to read, minimul design


#### Tools to check accessibility
    ChromeVox Lite
        munimal functional screen reader
  
#### WACAG
    https://www.w3.org/TR/WCAG20/
    
    * Checklist for WACAG
    https://webaim.org/standards/wcag/checklist
    
    POUR:
    Percivable
    operable
    Understandable
    Robust


#### Focus on Key board
    Sementics
    Styling

    Should alays accesable by keyboard

#### tab order
    https://www.w3.org/TR/html5/editing.html#sequential-focus-navigation-and-the-tabindex-attribute
    
    Be careful with CSS
        Form tag can be used key board based on the posion on the DOM
        So even using css to float: right; on the first item which visually shows the last visually on brower
        1st tab will be associate with the first DOM element.
        https://webaim.org/standards/wcag/checklist#sc1.3.2

    tabindex atribute
        can be used as tabindex = "0"
        negative number like -1 not in the natural tab order
        can be programatically focused with focus()method
            document.querySelecter("#model").focus()
    "0"
        is in the natural tab order
        and can be programmatically focused
    "5"
        is in the natural tab order
        jumped to the front of the tab order
        anti-pattern
        confusing to screen reader

    tab is for something user will be interactive
    
        The tabindex global attribute indicates if its element can be focused, 
        and if/where it participates in sequential keyboard navigation (usually with the Tab key, hence the name). 
        It accepts an integer as a value, with different results depending on the integer's value:
    
    managing focus
    
        things like menu items on single page website where it takes you to the
        right part of the page when you clicked, 
        you can add taborder = "-1" on place such as a link on writing page. it doesn't appear on the natural taborder
        but call its focus method after the user has taken their action which is tabbed on the menu 
        
        How to do it:
        
        1:  give tabindex+"-1" to heading
                <h2 tabindex="-1">What is Life</h2>
        2:  listen for anchor tag of the menu click
        3:  call focus() method of the header
            then user can go down in the written article to navigate by using tab
            
            JS example ------------------------------------------
            var isFirstPage = true;

            page('/', function() {
              page.redirect('/what-is-vegemite');
            });

            page('/:slug', function(context) {
              // This will match any value after the first / in the url. For example, if
              // the url was /foo, the value of slug would be "foo".
              var slug = context.params.slug;

              // Remove is-active class from previous menu item and section
              var oldMenuItem = document.querySelector('#menu .is-active');
              var oldPage = document.querySelector('main .is-active');
              oldMenuItem.classList.remove('is-active');
              oldPage.classList.remove('is-active');

              // Add is-active class to new menu item and section using the URL slug
              var newMenuItem = document.querySelector('#menu [data-page='+slug+']');
              var newPage = document.querySelector('main [data-page='+slug+']');
              newMenuItem.classList.add('is-active');
              newPage.classList.add('is-active');

              // If this is the first time someone is visiting the site, don't move focus
              // around. Wait until they have clicked a menu item
              if (isFirstPage) {
                isFirstPage = false;
                return;
              }

              // Move focus to a heading in the new page
              newPage.querySelector('h2').focus();

            });

            page({
              hashbang: true
            });
       
       
        The actual contents is not the first things on DOM
        tab goes throug nav and side bar first and it is frastrating eith motor imperiment.

        Skip links
        https://developers.google.com/web/updates/2016/03/focus-start-point?hl=en
                
            when you tab first, it will give you an option if you wanna skip to the content
            press enter, you move down to content area. bypassing all the navigation.

            HTML
                <a href="#maincontent" class="skip-link">Skip to main content</a>
                <nav>
                ...
                </nav>
                <main id="maincontent" tabindex="-1">
                // you don't need tabindex for newer version of browser

            CSS
                .skip-link{
                    position: absolute; // need to be
                    top: -40px // initially set for off screen
                    left:0;
                    Background: #BF1722;
                    color: white;
                    padding: 8px;
                    z-index: 100;
                }

                // focus pseudo class
                .skip-link: focus {
                    top: 0;
                }


        * Focus on comprex contents -------

            AREA design pattern stock
            https://www.w3.org/TR/wai-aria-practices-1.1/

            i.e. radio buttons
            https://www.w3.org/TR/wai-aria-practices-1.1/examples/radio/radio-1/radio-1.html

         * Roving focus ------------------------------------------------
            <li tabindex="0" checked
            <li tabindex="-1">
            <li tabindex="-1">
            <li tabindex="-1"> 
            <li tabindex="-1">

            0 on the currently active item
            keyboad event listner to determine which key user has pressed
            it will set tabindex to 0, the previous one to -1
            attach focus method()
            move checked attribute to the new list
            this change the looks of the (radio button) on browser
            https://github.com/udacity/ud891/blob/gh-pages/lesson2-focus/05-radio-group/solution/radiogroup.js

        RadioGroup.prototype.handleKeyDown = function(e) {
            switch(e.keyCode) {
                case VK_UP:
                case VK_LEFT: }
                 e.preventDefault();

                if (this.focusedIdx === 0) {
                    this.focusedIdx = this.buttons.length - 1;
                } else {
                    this.focusedIdx--;
                }
                break;
                }

              case VK_DOWN:
              case VK_RIGHT: {

                e.preventDefault();
                if (this.focusedIdx === this.buttons.length - 1) {
                  this.focusedIdx = 0;
                } else {
                  this.focusedIdx++;
                }
                break;
              }
            }
            this.changeFocus(this.focusedIdx);
          };


        * Off screen content -----

            if the focus disappeared, write
            document.activeElement on colsole on console
            gives you apparet focus element
            https://developer.mozilla.org/en-US/docs/Web/API/DocumentOrShadowRoot/activeElement

        * Accessibility Developer Tools -----

            https://chrome.google.com/webstore/detail/accessibility-developer-t/fpkknkljclfencbdbgkenhalefipecmb?hl=en

                Audit tab on the tool  
                click accessibitity and Audit present state
                then it will produce number of errors
                including items are focusable but either invisible or obscured by another emements
                as well as the off screen menu like hidde under burger
                How to fix it:
                    visibility: hidden
                    or
                    display: none
                    if anything not showing yet, just use the css above

               Keyboard Trap ----------------------------------------------
               
               https://webaim.org/standards/wcag/checklist#sc2.1.2
                                
                    motal window - 
                    if you use overlay, it will travel the focus out side motal window.
                    Use temporary keyboad trap so the focus doesn't go anywhere else
                    
                    There is trap key boad function 
                    https://github.com/udacity/ud891/tree/gh-pages/lesson2-focus/07-modals-and-keyboard-traps
                    
                    
                 
                    


