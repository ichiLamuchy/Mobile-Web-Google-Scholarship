
# Responsive image



>#### Setup
>[VS Code: set up local web server local host](https://blogs.msdn.microsoft.com/cdndevs/2016/01/24/visual-studio-code-and-local-web-server/#comment-111475)

#### Developer's tool 
    * Check the Image Size 
    disable cache then reload, you can see the size on image under network tab

    * Natural size check
    go to element, click one of image you wanna check
    then click console and type $0 to see what it is
    type $0.naturalWidth to check natural width
    you could also just click the image on the element


    Total bits = pixels x bits per pixel
    Less pixel x better compressionn = less bytes


#### To put image side by side

    You can put margin between the images 
    suchu as 
        margin-right: 10px;
        width:calc((100% - 10px)/2);

    just type selecter to not put margin after the last image
        img:last-of-type {
        margin:0 ; 
        }

### CSS UNIT

    1 unit corresponds to 1 % of VP
    
    ** vh & vw **
    vh - view port height
    vw - view port width
        
        (i.e)
        width: 100vw;
        height: 100vh
        
    ** vmin - view port minimum **
    fit to smaller height or width of viewport
    If you set it to both, it will get the effect
        
        width: 100vmin;
        height: 100vmin;

    **vmax - viewport max**
    cover whole vieport without stretching or squosh.
    it corresponding to whichever greater of viewport
    but it will chane img to square 
        
        width: 100vmax;
        height: 100vmax;
  

#### Raster vs Vecter

    Vecter is better, browser can render a vecter image at any size
    SVG is ideal, very small.

    jpg for photograph
    
    webp is widely supported - alpha transparency and animaton
    
    png if svg not available 
        use png over gif
  
    
#### Optimize images    
    Natural imagesize:
        Obviously image need to be only as large as it's display
      

    Optimize images
        grunt-page speed

    remember 1em is 16px
    reasonable width is 50em
    
### Img optinazation 


#### page speed 
    Page speed Insights 
    https://developers.google.com/speed/pagespeed/insights/
    Grunt PageSpeed plugin
    https://www.npmjs.com/package/grunt-pagespeed
        
#### How to use Grunt
    1. install grunt cli in your root.
    2. npm install to install dependancies on your project on VS code
    3. installed imagemagics
    Run grunt on command prompt to run grunt 
        "grunt" alone creates a new, completed images directory
        "grunt clean" removes the images directory
        "grunt responsive_images" re-processes images without removing the old ones
    then it create new folder with separate folder with new image files (as you set) to use for your web

###### vs code and dependancies 
    npm install to use package.json file to download dependancies
    npm run to run on localhost
    otherwise the udacity front end extension won't recognise how fast the speed could be

     
>Every 100ms delay drops amazon sales of 1%
>Requset only can as fast as the half the speed of light,
>simply from San Francisco to London takes 100ms 


#### Simply reduce number of images and reduce the request make it all quick       
    image sprites in CSS for HTTP1
        Rather than include each image as a separate image file, it is much more memory- and bandwidth-friendly to send them as a single image, so the number of HTTP requests is reduced.
    https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Images/Implementing_image_sprites_in_CSS

    However when you use HTTP2, you don't need to use these hacks

#### Text As Text
    Using text as text when it's on over image,
    Do not use it as graphics, 


### Think if you really need image 

#### CSS effect
        such as "shadow" and all that cost time to response

#### pure css (library)
        for web and it is really powerful and small
    
#### Background
        CSS to add a background pattern to an element or page itself
        You can convine taht with gradients and other CSS effect
        http://lea.verou.me/css3patterns/

#### backgound-size cover property 
        if you dont know the size of VP, it would be very handy
        part of image will be lost but you can add transition to make the change smooth

###### background-size:
    cover - image kept as small as possible, it matched to containers smallest dimention (x or y)
    completely filled the container though the one of dimention is hidden, not visible
    or contain i- is completely filled is with largest dimention which means shorter dimention may not be filled

#### use unicode
        https://unicode-table.com/en/
        https://developer.mozilla.org/en-US/docs/Web/HTML/Element/meta
        need charset=uft-8 on meta tag

        It's actualy recommended to copy and paste the actual unicode charactor on html
        it's easier to read and maintain

        1: use html code such as &#128522; directly in html
        2: see if work then copy the actual calacter then paste it on where &#128522; is

#### Icon Font 
        http://zocial.smcllns.com/
        http://fontello.com/
        https://fontawesome.com/
        http://weloveiconfonts.com/
        https://css-tricks.com/examples/IconFont/
        https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA

        how to
        https://classroom.udacity.com/nanodegrees/nd024/parts/0bf842e9-7269-42de-b68b-812ca7823517/modules/c1af53e5-7b6f-4bdf-be4a-24a7a865de18/lessons/3483659506/concepts/34791494350923

    Inline SVG & DataURL 
        https://www.lynda.com/CSS-tutorials/Adding-SVG-file-svg-your-page/374186/384066-4.html

        reduce number of request
        can be written a background on CSS - reduce http request
        https://css-tricks.com/lodge/svg/09-svg-data-uris/

        Inline SVG on tag and data srl on image tag
        inline looks like this src = "data:image/ping;base65.....




### srcset 

#### x to differentiate between device pixel ratios (DPR)

    <img src+"wallaby_1x.jpg" srcset="wallaby_1x.jpg 1x, wallaby_2x.jpg 2x" alt="wallaby">
    
    Browser should choose higher resolution for high DPI display
    The 1x 2x syntax is called a Pixel Density Descripter

    Go to developer's tool then go console, type
    window.devicePixelRatio
    to check the divice pixed ratio for your display

    if the device doesn't support the srcset attribute, 
    it will be ignored and the img loaded in the usual way
    src attribute as a fallback.

#### w to describe the image's width

    Set srcset equal to a comma separated string of filename widthDescriptor pairs.
    widthDescriptor gives the natural width of each image file
    
    tells the browser the width of each img
    <img src="small.jpg" srcset="small.jpg 500w, medium.jpg 1000w, large.jpg 1500w" alt="wallaby">
    Enable the browser to choose right size image depends on the screen pixed density
    and the view port size
    ***example*** 
    browser window size 500 pixels wide on a 2x display 1000 is adequate
    Some conside H size 
    see this Working with h units
        https://github.com/ResponsiveImagesCG/picture-element/issues/86



[A fun article on srcset (Warning: A little bit of NSFW language)]
        (http://ericportis.com/posts/2014/srcset-sizes/)

[Pixel Density List]
        (http://pixensity.com/list/phone/)

[High DPI Image for Variable Pixel Densities]
        (https://www.html5rocks.com/en/mobile/high-dpi/)

#### Sizes attribute

    sizes consists of comma separated mediaQuery width pairs.
    Browser parses html and down load img before css is parsed. 
    So it knows nothing about image display size.

    sizes tells the browser early in the load process that the image will be displayed 
    at some width when the mediaQuery is hit.

    <img src="small.jpg" srcset="small.jpg 500w, medium.jpg 1000w, large.jpg 1500w" sizes="50vw" alt="wallaby">
    
    50vw meands it will be always display as 50%
    if the width changes depens on vp
    sizes= "(max-width: 250px) 100vw, 50vw" alt="Wallaby"
    this means that up till width of 250px, VP With is 100%, above that it will be 50%

        <img  src="images/great_pic_800.jpg"
              sizes="(max-width: 400px) 100vw, (min-width: 401px) 50vw"
              srcset="images/great_pic_400.jpg 400w, images/great_pic_800.jpg 800w"
              alt="great picture">
    
    
    
### <picture> element

    source set - it goes down from top to see if it is available
    picture element is great way to provide alternative source for image files.
    So browser can choose depends on device capabilities

    <picture>
        <source srcset="kittens.webp" type="image/webp">
        <source srcset="kittens.jpg" type="image/jpeg">
        <img src="kittens.jpg" alt="Two grey tabby kittens">
    </picture>
    
    More information about WebP
    https://developers.google.com/speed/webp/?csw=1
<source> can also have media query with medis attribute. see example below    
    <picture>
          <source media="(min-width: 1000px)" srcset="kookaburra_large_1x.jpg 1x, kookaburra_large_2x.jpg 2x">
          <source media="(min-width: 500px)" srcset="kookaburra_medium_1x.jpg 1x, kookaburra_medium_2x.jpg 2x">
          <img src="kookaburra_small.jpg" alt="The kookaburra: a terrestrial tree kingfisher native to Australia and New Guinea">
    </picture>
    
picturefill for browser not supported <source>
http://scottjehl.github.io/picturefill/

article about picture element
https://www.html5rocks.com/en/tutorials/responsive/picture-element/
    
Lots of other <picture> use cases, examples and code snippets
https://dev.opera.com/articles/responsive-images/
    
[element queries](https://github.com/marcj/css-element-queries)
    
[Responsive Images Community Group](http://responsiveimages.org/)




use vector when it's possible. 
inline is good
external is good for using frequently as you can pick it up from cache

1. make the wrapper max-width 600-1200px
2. each image width 100%
3. use grunt to change the size of image and compressor
4. think if you need the image use icon font or css pure back ground when possible
5. choose background-size: cover (or contain);
6. use unicoe
7. use iconfont
8. use svg inline data
9. use srcset and sizes
10. Picture tags








