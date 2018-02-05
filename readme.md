## **Why the library war born？**
The freelance project of the design draft usually with random pixel. Designer
 does not care about those pixel are integer or not.

It is means you can not find any regularization lead to build component hardly. 
Especially with inexperienced designer or you have no authority to correct 
this mess. 

This library will generate some class to help you to overcome this 
situation.

## **How easy it is?**
```html
    <div class="df-sm">
      <div>Foo</div>
      <div>Bar/div>
    </div>
    
    It will make this div display: flex; when tablet and above.
    In other words display: block; when mobile.

    <div class="tal-sm tac-md mt30-sm mt50-md">
      <h3>Foo</h3>
      <h3>Bar/h3>
    </div>
    
    It will make this div text-align: left; when tablet and above
                          text-align: center; when normal screen and above
                          margin-top: 30px; when tablet and above
                          margin-top: 50px; when normal screen and above 
    
         Imagine how much code you need to write if you are not using 
    behavioral binding media? !
```


## **Who need this?**
* Have a new project
* Freelancer
* No authority to correct design draft
* Clean coder

<b>Import library folder if you want to use. In addition tool.scss method for 
your own reference or self-increase.</b>


Recommend you read the concept even you do not use it.

## **How to use?**
##### The usage of library currently contains margin, padding, text-align, display
```
    Usage explanation * indicates that the number can be 0px, 5px, 15px, 20px
     ~~ 150px in 5 intervals
    -------------------------------------------------------
            xs(320up) | sm(768up) | md(992up) | lg(1200up)
    -------------------------------------------------------
    mt*-xs     Yes    |    Yes    |    Yes    |    Yes
    mt         Yes    |    Yes    |    Yes    |    Yes
    -------------------------------------------------------
    mt*-sm     No     |    Yes    |    Yes    |    Yes
    -------------------------------------------------------
    mt*-md     No     |    No     |    Yes    |    Yes
    -------------------------------------------------------
    mt*-lg     No     |    No     |    No     |    Yes
    -------------------------------------------------------
    Yes means work / No means not work
    
            xs(320up) | sm(768up) | md(992up) | lg(1200up)
    -------------------------------------------------------
    tal-xs     Yes    |    Yes    |    Yes    |    Yes
    tal        Yes    |    Yes    |    Yes    |    Yes
    -------------------------------------------------------
    tal-sm     No     |    Yes    |    Yes    |    Yes
    -------------------------------------------------------
    tal-md     No     |    No     |    Yes    |    Yes
    -------------------------------------------------------
    tal-lg     No     |    No     |    No     |    Yes
    -------------------------------------------------------    
    Yes means work / No means not work
``` 

The following is an example
``` 
     mt10 = mt10-xs = mobile (all media) margin-top: 10px
     ml20-sm = tablet and above margin-left: 20px
     mb35-md = normal screen and above margin-bottom: 35px
     mr100-lg = large screen and above margin-right: 100px
     
     mtn = mtn-xs = mobile and above (all media) margin-top: 0px
     mrl100-sm = tablet and above margin-right: 100px; margin-left: 100px
     mtb100-sm = tablet and above margin-top: 100px; margin-bottom: 100px
     mta100-sm = tablet and above margin-top: auto; margin-bottom: auto
``` 
``` 
     tac-sm = tablet and above text-align: center
     tal-md = normal screen and above text-align: center
     tar-lg = large screen and above text-align: center
     tan = tan-xs = mobile and above (all media) text-align: inherit
``` 
``` 
     df-sm = tablet and above display:flex
     dib-md = normal screen and above display:inline-block
     di-lg = large screen and above display:inline
     db = db-xs = mobile and above (all media)  display:block
```

## **What is behavior？ What is bind media？**

「Behavior」is means a element align left, right, top or bottom. 

If a div position needs to vertically centered and down 30 pixel, you 
will define a class like this below.  

```scss
.flex-vertical-center{
    display: flex;
    align-items: center;
}
.mt30{
    margin-top: 30px !improtant;
}
```

Why I use `!important?` here? Everybody says do not use `!important`. 

Do you really understand why?  

Most of reasons are the element will be very hard to change anymore.

But！ It is precisely because this is a behavioral naming style, you may
 named "align-left" but the css syntax is `taxt-align: right;
`? Or do you want to move down 20px but the css syntax is `margin-lift: 
100px;`? Based on this situation, there is no reason to change!


```html
<div class="flex-vertical-center mt30">
    <h3>Foo</h3>
    <h3>Bar/h3>
</div>
```
So Foo and Bar will be vertically centered and down 30px

The class as following If works tablet and above (meaning that does not contain 
mobile).
```scss
@media (min-width: $screen-sm-min) {
    .flex-vertical-center-sm{
        display: flex;
        align-items: center;
    }
    .mt30-sm{
        margin-top: 30px !improtant;
    }
}
```
## **Why we need to do that？ What the benefit**

You must have encountered this situation! ! Assume login and registration of 
the block class are `.Auth_wrapper`, after the designer came a new design, in 
the user's edit page also use the same template, then you want to change class 
name?
If you user `.user_edit_wrapper` to wrap user's page and change `
.Auth_wrapper {code}` to`.auth_wrapper, .user_edit_wrapper {code} `?
In practice, it will not be as simple as this. There must be a few places to 
be modified, and engineers always struggle is in such a dilemma.

2. If you already define a `. Banner` class in home page, but next design is 
banner need to down 30px? What you gonna do?
Most people choose to add one more class that's available for this, but the 
idea I'm trying to convey is directly to use the `.flex-vertical-center` class.

    * When using `.banner` in more than one place, you're absolutely afraid 
to change a little place to all the scenes, but class behavior is not.
    * If you have a lot of places to be centered vertically, you must have a 
class or name, and you have to write a vertically-aligned syntax in the CSS 
file, then it's time to change it to behavior class to reuse.

3. In general, front-end engineers will be trouble in CSS-specificity. LESS, 
SCSS are good tool to write, but do not use too much nested. The problem will
 bring about specificity too heavy to overwrite.

    ```scss
    @media (max-width: 480px){
      .modal{
        .grouped.fields{
          .field{
            width: 50%;
            padding-left: 25px;
          }
        }
      }
    }
    ```
   
    ```html
    
    tal  = taxt-align:left;
    tac  = taxt-align:center;
    mt30 = margin-top:30px;
    
    <div class="tal-sm tac-md mt30-sm mt50-md">
      <h3>Foo</h3>
      <h3>Bar/h3>
    </div>
        
        It will make this div text-align: left; when tablet and above
                              text-align: center; when normal screen and above
                              margin-top: 30px; when tablet and above
                              margin-top: 50px; when normal screen and above 
        
             Imagine how much code you need to write if you are not using 
        behavioral binding media? !
    ```

4. Can cope with the designer's design flaws, most of the designers are 
"graphic designer" not "website designer" in Taiwan, the concept of RWD and 
component concept are week. Often designers do not have component concept lead to every 
version are not the same, we can not find a rule to build.

5. In my case the concept of an average page can save about 300 lines of 
CSS code.

6. Maintenance become simple, because everything will happen are directly 
expressed in the class.

## **A few simple SCSS files are enough to cope with all layout？**
Need to load additional Boostrap following three components
* [bootstrap/variables](https://github.com/twbs/bootstrap/blob/v4-dev/scss/_variables.scss)
* [bootstrap/utilities](https://github.com/twbs/bootstrap/tree/v4-dev/scss/utilities)
* [bootstrap/responsive-utilities](http://getbootstrap.com/css/#responsive-utilities)

And recommend using Bootstrap Grid
* [bootstrap/grid](https://github.com/twbs/bootstrap/blob/v4-dev/scss/bootstrap-grid.scss)

Not exactly, these libraries that have been able to cope with 80% of the 
front-end complex RWD layout.

[tool.scss](https://github.com/lustan3216/Behavior-Bind-Media/blob/master
/tool.scss) contain out of practical methods, can be applied to the project.

The other 20% still need to rely on engineers to find ways to define the most basic (frame, background color, color, etc.) template and then use this Library to do extension.      

## **Someone asked how the size of the fonts on the RWD how to solve it？**
This is the basis for the design of web pages, which should be defined in the
 Style Guide Line which is also a prerequisite for the site to be developed.
