# CSS Grid

## Challenges

1. [Basic Grid](#basic-grid)
2. [Special Properties](#special)
3. [Standard Webpage](#standard-webpage)
4. [Image Grid](#image-grid)

## Basic Grid

Goals:
* grid-template-columns
* grid-template-rows
* Units of measurement
  * px
  * %
  * fr
  * auto
* repeat(number, measurement) (optional)




1. Before adding anything, run basic.html. As you can see, each element fills the entire width of the screen.
2. In basic.css, add the following two lines to your code below `grid-gap: 2px;` and see what happens. Try changing the width of the window. 

``` css
grid-template-columns: 100px auto 100px;
grid-template-rows: 100px 100px;
```
3. `auto` forces a column to fill up any empty space in a row. If there are multiple columns set to `auto`, they will split the empty space. Now, try changing the value of `grid-template-columns` to `20% auto 20%` and now see what happens as you change the width of the window.
4. Now, change the value of `grid-template-columns` to `1fr 1fr 1fr`. Then try changing it to `1fr 3fr 1fr`. `fr` is shorthand for fractional unit, and can be used to divide up a grid into any amount of units of equal size.
4. If you are making columns or rows of equal sizes, the `repeat(number, measurement)` function can come in handy. the `number` argument is the amount of columns you would like to have, and `measurement` is the width of each column. Setting `measurement` to auto will make columns of equal size and make the grid cover the full width of the container. Try changing the value of `grid-template rows` to `repeat(2, 100px)`.


#### Challenges

1. Make a 3x4 grid by adding a row and a column to your grid (hint: you will need to go to basic.html to add more divs).
2. Make a 2x10 grid with columns of equal size filling the entire width of the screen utilizing the `repeat(number, measurement)` function.


## Special

Goals:
* auto-fit
* minmax(min, max)



1. Paste the code below into special.css and run special.html in your browser. Take note of the `repeat(auto-fit, 150px)` function.

``` css
.container{
    display: grid;
    grid-gap: 2px;  
    grid-template-columns: repeat(auto-fit, 150px);
    grid-template-rows: 100px 100px;
    
}
```

As you can see, whenehever you change the width of the window to allow another 150px of room, another column fills the empty space. 
2. Although `auto-fit` is a pretty cool feature by itself, until there are exactly 150px of free space there is a pretty large amount of open space that is not used on the side of the container. We can fix this issue using the `minmax(min, max)` function. Replace your `grid-template-columns` line with the following code: 
``` css
grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
```
Your `minmax()` function gives each a column a minimum width of 150px, and if there is more space in the container, it makes the width of each column a fractional unit of the entire container, hence the `fr`. 

## Standard Webpage

Goals:
* grid-column
* grid-row
* span



Below is the standard layout for a webpage:
    ![](https://ci.apache.org/projects/wicket/guide/6.x/img/layout.png)

In this section, we will learn how to display these elements in a grid.
1. First, take a look at standard.html. you will see that there are four elements with unique ids. Now, take a look at standard.css. You will find code for a 2x2 container and four places to put your unique code for the individual elements. Try running standard.html. You will see the four elements in two rows. This isn't quite yet what we're looking for. 
2. One way to format each individual element is to use the `grid-column` attribute. `grid-column` allows you to specify the width of an individual column. We can modify `grid-column` according to the gridlines. For example, in the image below, the line to the left of the 1 is gridline 1, the line between the 1 and the 2 is gridline 2, etc. 
![](https://i.imgur.com/GozZlb7.png?1)

    You can specify the last gridline in the screen with a simple -1. In the code for `#header{}`, add `grid-column: 1/-1;` within the curly brackets. You can also achieve the same effect using `span`. `span` allows you to specify the aount of columns or rows an element should occupy. Go ahead and change the `grid-column: ` code for `#header{}` to `span 2` instead of `1/-1`.
    
    For example, if you wanted to make an element span across the first two columns of a grid, you could either use `grid-column: 1/3` or `grid-column: span 2`. Both the `start / end` method and the `span` method can be implemented in `grid-column` or `grid-row` within the specific code for an element.
3. Since we want our menu to take up about 1/5 of the width of the grid, have to add three more columns to our grid. Next, we can change our code for `grid-column:` of the header to `span 5` so it fills the entire container. We won't have to change the code for the menu because it by default spans 1 column out of the five we have created. We will now need to add `grid-column: span 4;` to the content section to make the content fill the rest of the second row. Now try and make the footer span across the full third row.

#### Challenges

* Make the content fill 2/3 of the second row instead of 4/5
* Make the menu go down all the way to the bottom of the third row. (Hint: `grid-row` works exactly the same as `grid-column` does.)

    
## Image Grid

* classes
* grid-auto-flow

Classes in html and css allow you to style multiple elements based on their given class. In css, you can add code for a class by adding a `.` and then the class name. We will be using classes in this section to program a grid of 18 images with classes which will determine each photo's size and layout (horizontal or vertical). 
1. Take a look at imagegrid.html. There, you will find many divs, each containing an image. If you look closely, you will see that some of the images have classes assigned to them. The three different classes are big, horizontal, and vertical. Now, go to imagegrid.css, and you will see code for a grid with  `minmax(auto-fit, 100px)`, which will make the grid behave similarly to the grid we made in the last section. Open imagegrid.html in your web browser to see what you have so far. 
2. Now, what we want to do in this lesson is to resize the images based on class. We can do this using `span`. For the big images, we want the images to take up two rows and two columns. For the horizontal images, we want the images to take up two columns and one row, and for the vertical images, we want the images to take up two rows and 1 column. On your own, add code to each class to resize the images. (Hint: for reference, take a look at the paragraph before step 3 of [Standard Webpage](#standard-webpage).)
3. As you can see, the normal images do not fill all of the gaps in the grid. This is because the way that the images are distributed is row by row, column by column. Since the vertical and big images occupy multiple rows, the two rows filled are not fully occupied by smaller images. This can be fixed using the grid's `grid-auto-flow:` property. This property determines the order in which the grid is filled by its elements. The default property for `grid-auto-flow:` is row, which explains why our grid is filled by the row. Try adding `grid-auto-flow: dense` to the code for the grid container as a new line. This should properly fill our image grid!

Click <a href="https://scrimba.com/p/pWqLHa/" target="_blank">here</a> for an awesome css grid tutorial that is a bit more in-depth than this one is.

