
## ARIA


https://github.com/udacity/ud891
for exercise


  For accesibility:
     
        DOM order
        Focus
        Keyboad
        Semantics
        Labeling
        Heading
        Landmaeks
        Links
      
      

How to express semantics HTML cannot express
Aria works by allowing you to specify attributes on elements
which modify the way that element is translated into the accessibility tree

        ARIA 1.0 spec: https://www.w3.org/TR/wai-aria/
        ARIA 1.1 spec: https://www.w3.org/TR/wai-aria-1.1/

    Example: 
    role = "checkbox" aria-checked="true"
    aria attribute always need explicit value
     
    you can set 
        funtion Checkbox(el){
            this.elsetAttributs('role', 'checkbox');
            if (this.el.hasAttribute('checked')){
                this.el.setAttribute('aria-checked', 'true');           
            } else {
                this.el.setAttribute('area-checked', 'false');
            }
        }
        Checkbox.prototype.toggle = function (){
            if (this.el.hasAttribute('checked'))
                this.el.removeAttribute('checked');

                this.el.setAtribute('area-checked', 'false');
            }else {
                this.el.setAttribute('checked', '');
                this.el.setAttribute('area-checked', 'true');
            }
       }
     
#### Roles 
    
    you can modify the sementic meaning by using role
    <button role="switch"

    area can express sementic patterns do not exist in html even!
    such as role = "tree"  / role = "treeitem"

    ARIA allows us to create accessible widgets - not possible in plain html

    ARIA can add extra description text and label, 
    which is only exposed to assisted technology APIs.

    <role = "alart"> Attention!</div> 
        immidiately will voice over

      
    * important - role attribute set the same tag as tabindex attribute is in
        
Aria spec - Taxonomy pof possible value
https://www.w3.org/TR/wai-aria-1.1/#namefromcontent

Practice guide: gives you example of how to do
https://www.w3.org/TR/wai-aria-practices-1.1/
        
        abstruct role means common to several role but may not used as value for the role attribute

#### eample of JS:
        useing setAttribute to set such as ('role', 'radiogroup') to each el
        removeAttribute and setAttribute to switch around
        
#### adding labels
        
    aria-label
        <button aria-label="menu" class = "hamburger"> (some pic)</button>
        there is no text only visual indication
        in this case it would be 
                button 
                name:"menu"
        if the button has x mark with text. And the function is for close the window 
        you can set it as aria-label="close"

#### aria-labelledby
        specify another id to any element
        <div role ="radiogroup" aria-labelledby = "id1">
        then tag where id="id1" has Drink Option then "Drink Option" become the name
                radiogroup
                name:"Drink Option" 

        it is works similar to label element but the relation is oppositway around.
        <label> elemets refers to the thing it labels (<input>)
        labledeby refers to the things labels it

        aria-labelledby can take multiple elements 
        The label will be concatenated in the order of the ID refs are given
        It overrides all other name sources for an element.
            even if there are area-label or class attribute there, 
            aria-labelledby will always take precedence.
            
     
        HTML sementics (area in HTML)
        
        If HTML sementics have been set do not re-define
        <input type="checkbox" role="checkbox">
        this role need to go
        
        https://www.w3.org/TR/html-aria/
        
        aria role can be
        
        role = "banner"
        role = "navigation"
        role = "main"
        role = "serch"
        role = "dialogue"
        role = "complementaty"
        role = "contentinfo"
 
### ARIA RELATIONSHIPS
https://www.w3.org/TR/wai-aria-1.1/#attrs_relationships
#### aria-owns for menu
        
        <div role = 'menu" aria-owns="mi1 
       
        
![aria-owns](https://github.com/ichiLamuchy/Mobile-Web-Google-Scholarship/blob/master/img/area-owns.png)

aria-activedescendent attribute used for elements focused

![aria-activedescendant](https://github.com/ichiLamuchy/Mobile-Web-Google-Scholarship/blob/master/img/aria-activedescendant.png)

#### aria-describedby
        Exactly the same as labelled by allows you toprovide a label
        this is useful if there is nany explanatory text
        supplimentary not essenially 
        
![aria-describedby](https://github.com/ichiLamuchy/Mobile-Web-Google-Scholarship/blob/master/img/aria-describedby.png)

#### aria-posinset and aria-setsize
![aria-posinset](https://github.com/ichiLamuchy/Mobile-Web-Google-Scholarship/blob/master/img/aria-posinset.png)

!!! do quiz 12
