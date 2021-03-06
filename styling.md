
## Style 

After accessibility applied - make it look good but not confict with accessibility

### Use relative unit

    width:50%;
    font-size: 1.2em;
    font-size: 2rem;
    
    http://pxtoem.com/
    https://stackoverflow.com/questions/14238799/css-base-font-size-set-in-browser-and-responsive-design

    48dp minimum touch target size
    (dp is device independant pixels)
    you can add additional padding to make up to 48 pixels
    it also should 32 pixels apart
    so set 32 pixels marging around

        WebAIM checklist items:

        1.4.4: http://webaim.org/standards/wcag/checklist#sc1.4.4
        https://webaim.org/standards/wcag/checklist#sc1.4.4

        Udacity course on Responsive Web Design Fundamentals
        https://eu.udacity.com/course/responsive-web-design-fundamentals--ud893

        Material Design Accessibility recommendations for touch targets
        https://material.io/guidelines/usability/accessibility.html#accessibility-layout

    Author's Note: On older browsers (particularly Mobile Safari) 
    developers would add user-scaleable=no because it would disable the 350ms click delay 
    in that browser.
    As of Safari 9.1 this is no longer the case, and using width=device-width 
    in your viewport will handle removing that click delay.
    
### Focus
    
    Check default seting such as focus
    Checklist 2.4.7: http://webaim.org/standards/wcag/checklist#sc2.4.7
    i.e. blue focus on blue back ground is not so good

        :focus{
          outline:
        }
        button:focus.
        button:hover {
            background: #E91£63;
            color: #FFFFFF;
            text-decoration: underline;
        }

    Set outline 0 -get rid of default set then instead use box-shadow with different color
            
        outline displayed in various way depends on the browsers.
        box-shadow is consistant

    button:focus.{
        outline: 0;
        box-shadow: 0 0 8px 3px
        rgba(255, 255, 255, 0.8);
    }

    this set gives you much better visibility.
    default one the focus will go both radio button and actua written and looks ugly and confusing
        
        .radio:focus{
            outline:0;
        }

        .radio:focus::before{
            box-shadow: 0 0 1px 2px #5B9DD9
        }


    .nav > li > a:hover,
    .nav > li > a:focus,
    .jumbotron .mdl-button:hover,
    .jumbotron .mdl-button:focus,
    .mdl-button.raised:hover,
    .mdl-button.raised:focus,{
        background: #C2185B;
        color: #FFFFFF;
        text-decoration: underline;
        box-shadow: 0 2px 2px 0 rgba(0, 0, 0, .14),
                    0 3px 1px -2px rgba(0, 0, 0, .2),
                    0 1px 5px 0 rgba(0, 0, 0, .12);
     }

    :focus pseudo-class
    https://developer.mozilla.org/en-US/docs/Web/CSS/:focus

    outline CSS property
    https://developer.mozilla.org/en-US/docs/Web/CSS/outline

    :hover pseudo-class
    https://developer.mozilla.org/en-US/docs/Web/CSS/:hover

    ::before pseudo-element
    https://developer.mozilla.org/en-US/docs/Web/CSS/::before

### Keyboad focus vs Tab focus

    :moz-focusring pseudo-class
    https://developer.mozilla.org/en-US/docs/Web/CSS/:-moz-focusring

    Proposing CSS input modality article
    https://www.oreilly.com/ideas/proposing-css-input-modality

    Input modality shim
    https://github.com/alice/modality


### Style with Aria

    css atribute selector

    .toggle[aria-pressed = "true"]{
        // transition to
        // pressed stated
    }
    content and expand can be written like below

    .disclosure-button[aria-expanded="false"] .icon::after {
      content: '▶';
    }

    .disclosure-button[aria-expanded="true"] .icon::after {
      content: '▼';
    }

    .disclosure-content[aria-hidden="true"] {
      visibility: hidden;
      opacity: 0;
    }

    .disclosure-content[aria-hidden="false"] {
      visibility: visible;
      opacity: 1;


### Respoisive design 

    i.e. when zoom in it will go design for mobile

    resize text!

    always use viewport tag!
    do not use user-scalable=no on content it's anti-pattern

    use responsive grid

        1.4.4: http://webaim.org/standards/wcag/checklist#sc1.4.4
        https://webaim.org/standards/wcag/checklist#sc1.4.4

        Udacity course on Responsive Web Design Fundamentals
        https://eu.udacity.com/course/responsive-web-design-fundamentals--ud893

        Material Design Accessibility recommendations for touch targets
        https://material.io/guidelines/usability/accessibility.html#accessibility-layout




### Setting accessability on iphone
    
    go to general setting
    tap accessability
    turn voice over on


### Color contrast

    contrast ration higher is better. minimum 4.5:1 is recommended

    WebAIM checklist items:

    1.4.3: http://webaim.org/standards/wcag/checklist#sc1.4.3
    https://webaim.org/standards/wcag/checklist#sc1.4.3

    1.4.6: http://webaim.org/standards/wcag/checklist#sc1.4.6
    https://webaim.org/standards/wcag/checklist#sc1.4.6

    Chrome Accessibility Developer Tools

### Don't convey info with color alone

    Using things like message or underline
    than just change the color for warning or focused

    WebAIM checklist items:

    1.4.1: http://webaim.org/standards/wcag/checklist#sc1.4.1
    https://webaim.org/standards/wcag/checklist#sc1.4.1

    NoCoffee Chrome extension
    https://chrome.google.com/webstore/detail/nocoffee/jjeeggmbnhckmgdhmgdckeigabjfbddl?hl=en-US

    http://www.colourblindawareness.org/colour-blindness/
    color blind awearness site

### High contrast

    High contrast extention
    https://chrome.google.com/webstore/detail/high-contrast/djcfdncoelnlbldjfhinnjlhdjlikmph?hl=en

    Mac OSX has accessability setting

    check your web using high contrast extention, still the user can experience your website


=========NEXT PROJECT================

need focus
SEmentiv mark up
with styiling keyed off of sementic property - we can insure the experience for all users
minimum color contrast
responsive design - mobile users


