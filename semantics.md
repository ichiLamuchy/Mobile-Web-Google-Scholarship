
### Semantics


Technologies rely on programmatically expressed semantics to create an accessible user experience

#### Assistive technology 
    is an umbrella term for devices, software, and tools that help any person with a disability complete a task

#### An affordance 
    is any object that offers, or affords, its user the opportunity to perform an action. 
    The better the affordance is designed, the more obvious or intuitive its use.

  Web AIM WCAG 2.0 Checklist 4.1.2

  Name (Label), Role, Value: makup is used in a way that facilitates accessability

### How:

Screen reader says:
    Element Role - what type of element it is   
    sometimes screen reader simply states element role
        i.e. edit text 
    Elements name 
        i.e. your email address
 
 State
    
    I could look like this if you only need screen  reader but no UI ----------

        main
            form
                radio button
                    name: round trip
                    state: selected
                edit text
                    name: full name
                combo box
                    value: no preference
                    name: seat type
                    state collapsed
                button
                    name: search
                    
Screen reader take HTML DOM then modify it

    Link, button automatically handled

++++++++ do 12-12 on with udacity extention


### Two type of labels 
https://webaim.org/techniques/alttext/

    - visible labels
        form <input> have text content but it will not be picked for audiolabel>
        wrap with <label> then it will be picked 
        or separate <input> with for attribute (which matched with id attribute of input
            <input type="checkbox" checked name="jLetter" id="letter">
            <label for="letter">Promotional offers?</label>


    - text alternatives (like img alt)
      https://webaim.org/techniques/alttext/

        <button> normally have text content - act as text alternative
        <img> alt is alternative when the img is not available, 
        title for the image is rather extra texts
        if the alt is redundant such as repeating previous item, then empty it (alt="")

### Good way to check if what you do is correct is that
### imagine if it would makes sence if the web site was only made by text no image.

    link is already provide the description


#### Voice Over (screen reader) on Mac (since OSX 10)
        https://webaim.org/articles/nvda/
        https://webaim.org/articles/voiceover/
 
 
 
 
### Heading h1 h2 h3 h4 h5 h6

    1.3.2: http://webaim.org/standards/wcag/checklist#sc1.3.2
    2.4.10: http://webaim.org/standards/wcag/checklist#sc2.4.10
    1.3.1: http://webaim.org/standards/wcag/checklist#sc1.3.1
    2.4.1: http://webaim.org/standards/wcag/checklist#sc2.4.1
    2.4.6: http://webaim.org/standards/wcag/checklist#sc2.4.6
     
     Heading level
     
         how prominent they are
         Think about section and subsection
     
         people use heading to navigate the contents within the page
         Heading is following DOM order not the visual 
     
         DOM > Accessibility tree > Screen reader  
         
             Example:

                CMD+F5 to turn on VoiceOver on OS X
                Normal keyboard operation (TAB, Shift+TAB, arrow keys etc.) work as normal with VoiceOver running
                CMD+L to jump to address bar
                CTRL+Option+U to open Web Rotor
                Type search term with Web Rotor open to search within Web Rotor
                CTRL + Option + ← ↑ ↓ → to explore content
                CTRL + Option + CMD + H to move forward by heading
                CTRL + Option + CMD + Shift + H to move backward by heading
           
     
     write this on console in developer's tool to check what headings are in the page
        
        for (var i = 0, headings = $$('h1,h2,h3,h4,h5,h6');
             i < headings.length; i++) {
           console.log(headings[i].textContent.trim() + " " +  
                       headings[i].tagName,
                       headings[i]);
        }   
           

### Other navigational options
    
    Shortcuts mentioned:

        CTRL+Option+U to open Web Rotor
        ← and → to change panes within Web Rotor
        Type search term with Web Rotor open to search within Web Rotor
        Enter to move VoiceOver focus to item from Web Rotor
        CTRL + Option + Spacebar to activate link/button/other element
        CTRL + Option + ← ↑ ↓ → to explore content
        CTRL + Option + CMD + H to move forward by heading
        CTRL + Option + CMD + Shift + H to move backward by heading
        CTRL + Option + W to have a word spelled out

    WebAIM's article on accesskey: http://webaim.org/techniques/keyboard/accesskey

    WebAIM's articles on VoiceOver and NVDA:

    http://webaim.org/articles/voiceover/
    http://webaim.org/articles/nvda
        
### Link Text 
    
    <a> tag with href attribute!!
    it meansshow up on the link list - available to work on key board
    can be book marked

    Let the screenreader find the links:
    http://webaim.org/standards/wcag/checklist#sc2.4.9

        if you use things like 
        <a href='#' onclick="dosomething()">
        this is more like button so use <button>
        <button class='link' onclick="dosomething()">click me</button>

        this style works too, just make sure you put alt
        <a href="/">
            <img alt="Udacity" src="logo_wordmark.svg">
        </a>
        
### Learn more 

    often use as the end of article, you can change to

    "learn more about apple"
    or make heading as "about apple"

    use more semantic elemets such as header, nav, main, section, article
    
    
    
    
    
    
    
