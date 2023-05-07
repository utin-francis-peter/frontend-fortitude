---
title: "How the CSS Absolute and Relative Units Work Behind the Scenes"
datePublished: Mon Mar 06 2023 19:35:21 GMT+0000 (Coordinated Universal Time)
cuid: clex826h5000109lcc0sogety
slug: how-the-css-absolute-and-relative-units-work-behind-the-scenes
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/Q3t49sVquH0/upload/0033079816323b2f0d7cd54faae49594.jpeg
tags: css, html5, frontend-development, responsive-web-design

---

CSS units are essential in web development, allowing developers to specify distances, sizes, and other measurements for elements on a web page. Absolute and relative units are two of the most common types of units used in CSS, each with its unique properties and use cases.

In this article, we'll explore how CSS absolute and relative units work behind the scenes, including:

* Their definitions.
    
* How they differ.
    
* The processes they undergo to render on a web page.
    

By the end of this article, you'll have a solid understanding of these fundamental CSS concepts and be able to use them more effectively in your web development projects.

# **Prerequisites**

* Web browser.
    
* Code Editor.
    
* Basic HTML and CSS knowledge.
    

# **An Overview of Absolute and Relative Units**

**Absolute units** are fixed measurements that are not dependent on any other factor; absolute units are fixed and independent CSS units.

Examples of absolute units include:

* pixels (px)
    
* inches (in)
    
* centimetres (cm)
    
* millimetres (mm)
    

With pixels (px) being the most widely used absolute unit, these units are typically used for elements that need to have a fixed size or position across screens, such as logos, icons, or other graphical elements. Absolute units can sometimes lead to issues with responsive design and may require additional CSS code to adapt to different screen sizes.

**Relative units**, on the other hand, are dependent on other factors, such as:

* The size of the viewport.
    
* The size of the parent element.
    
* The font size.
    

Examples of relative units include percent (%), em, root em (rem), viewport height (vh), viewport width (vw), and others. These units are often used for elements that need to be flexible and adapt to different screen sizes or content.

Relative units are useful when there's a need to specify a size or position that should adjust proportionally to other elements on the page or the viewport size. They are ideal for responsive designs because they can adapt to different screen sizes and orientations automatically. However, relative units can sometimes lead to inconsistencies across different browsers or devices, and it may require additional CSS code to ensure that the design remains consistent.

# **How Absolute Units Work Behind the Scenes**

When an absolute unit is used in CSS to specify the size or position of an element, the browser uses the pixel density of the user's device to calculate the final size or position.

Pixel density refers to the number of tiny dots called "pixels" that make up the pictures we see on screens like on your tablet or phone. The more pixels there are, the clearer and sharper the pictures look! So just like how joining more puzzle pieces together can make a picture clearer, more pixels can make a picture on a screen clearer too.

For example, if an element is specified to be `100px` wide and the user is viewing the page on a device with a pixel density of 2, the browser will render the element as 200 physical pixels wide.

To define an absolute unit in CSS, simply add the unit abbreviation after the numerical value. For example, to specify a `width` of 100 pixels for an element—in this case, a `div`, you would use the following CSS code:

```css
div {
  width: 100px;
}
```

To specify a `position` for the `div` using absolute units, you would use the `position` property along with the `top`, `bottom`, `left`, or `right` properties. For example:

```css
div {
  position: absolute;
  top: 50px;
  left: 100px;
}
```

Let's take a look at the behaviour of the `div` element in a browser when it is sized and positioned using an absolute CSS unit.

%[https://codepen.io/utin-francis-peter/pen/LYJyXjp?editors=1100] 

Have you noticed that when you toggle between 1x, 0.5x, and 0.25x on CodePen, the element doesn't adjust in size or position? This is because it was sized and positioned using an absolute unit.

# **How Relative Units Work Behind the Scenes**

When a relative unit is used in CSS to specify the size or position of an element, the browser first calculates the size or position of the parent element and then multiplies or divides that value by the value specified using the relative unit. Results from the calculation would solely depend on the relative unit used—%, em, rem, vw, and vh.

## **Percentage (%) Relative Unit**

In simple mathematics, we get asked to calculate a certain percentage of a number. For example, you can be asked to calculate 20% of 100.

How would you calculate this?

Remember, in mathematics, **of** interprets as **multiplication**. Hence, the solution would become **20/100 \* 100 =** **20**.

In CSS, when a percentage (%) relative unit is attached to an element's size, such as a `width` of `80%`, the browser references the direct parent of the element. It calculates a percentage of the direct parent's current size and assigns the resulting value as the size of the element. It's important to note the following:

* Reference is given to the direct parent and not to indirect parents or ancestral elements.
    
* Block-level elements like `div` and `p,` take up 100% of their parent element's width by default unless their width is explicitly specified in CSS.
    

You may ask yourself how attaching a percentage unit to an element gives it the superpower of adapting to whatever screen a user is viewing on. Let's take a look at a CodePen example for further clarification:

%[https://codepen.io/utin-francis-peter/pen/eYLRmzm] 

## **REM and EM Relative Unit**

These units are relative to the font size of the element they are applied to, making them a flexible option for responsive design. When we say that REM and EM units are "relative to the font size of the element they are applied to," we mean that the size we specify using these units will be based on the font size of the element we're styling. However, even though REM and EM units are both relative to the font size of the element they're applied to, there are some important differences between them. These differences have to do with how the units are calculated and how they interact with the parent elements on the web page. In subsequent paragraphs, we'll explore these differences in more detail!

**REM units** are calculated based on the root element's font size, which is usually set to the font size of the HTML element. The default font size of the HTML element is 16px, but can be increased or reduced using inline, internal, or external CSS styling. The REM unit stands for "root em," and it is relative to the font size of the root element.

When a REM unit is applied to an element's size, such as `font-size: 1.5rem;` the browser calculates the size based on the root element's font size, regardless of its position in the DOM hierarchy. If the root element's font size is set to the default value of `16px`, then `1rem` would be equal to `16px`.

To calculate the px unit equivalent of a value that is set in rem unit, use the guide below:

* Let 1(rem) = 16(px)
    
* Let known(rem) = ?
    

To calculate the rem unit equivalent of a value that is set in px unit, use the guide below:

* Let 1(rem) = 16(px)
    
* Let ? = known(px)
    

**Examples:**

1\. Let’s convert 1.3rem to px, assuming the HTML root element’s font size is 16px:

Let 1rem = 16px

Let 1.3rem = ?

Cross-multiplying would result in:

1(rem) *? = 1.3(rem)* 16(px)

?(rem) = 20.8(rem)(px)

Similar units on the LHS and RHS cancel out:

? = 20.8px

*Therefore, 1.3rem is equivalent to 20.8px when the HTML element font size is 16px.*

> Now try converting 1.3rem to px, assuming the HTML root element’s font size is set to 14px.

2\. Let’s convert 20px to rem, using the default HTML root element font size:

Let 1rem = 16px

Let ? = 20px

Cross-multiplying would result in:

1(rem) *20(px) = 16(px)* ?

20(rem)(px) = ?.16(px)

Make **?** the subject of the formula by dividing both sides by 16px

20(rem)(px) / 16(px) = ?

? = 1.25rem

*Therefore, 20px is equivalent to 1.25rem when the HTML element font size is 16px.*

> Now try converting 32px to rem, assuming the HTML root element’s font size is set to 20px.

Here are two CodePen examples, one with the default font size of the HTML root element (`16px`) and the other without. Both examples set the same `font-size` of `2rem`. Let's take a closer look:

%[https://codepen.io/utin-francis-peter/pen/rNZwVNm] 

%[https://codepen.io/utin-francis-peter/pen/YzOQXWd] 

**EM units** are another relative unit of measurement in CSS, which is based on the font size of the parent element. The EM unit is relative to the font size of the parent element, meaning that any element's font size, margin, padding, or other properties set in EM units will be calculated based on the font size of its immediate parent.

For example, if the parent element's font size is set to `14px`, and an element's font-size property is set to `1.5em`, the computed font size of the element will be 1.5 times the parent element's font size, which is `21px`.

Consider this other example, if a p element has a font size of `16px` and a child `span` element has a font size of `1.5em`, then the font size of the `span` element will be `24px` (1.5 times the font size of the parent p element).

However, if there is a grandparent element with a different font size, it will not affect the size of the child `span` element. The em unit only takes into account the immediate parent element's font size and not any ancestral parent element.

Let's take a look at a CodePen example for further clarification. Consider reading through the comments in the CSS for a better understanding.

%[https://codepen.io/utin-francis-peter/pen/MWqowqO] 

To calculate the equivalent px value of a value set in EM units, you would need to know the computed font size of the parent element. Let's assume the parent element's font size is `14px` and you want to convert a value of `1.5em` to pixels. You can use the formula below:

1em = parent element's font size in pixels

1.5em = ?

Cross-multiplying results in:

1em *? = 1.5em* 14px

? = 21px

*Therefore, 1.5em is equivalent to 21px when the parent element's font size is 14px.*

Similarly, to convert a value in pixels to EM units, you would need to know the computed font size of the parent element. Let's assume the parent element's font size is `16px` and you want to convert a value of `32px` to EM units. You can use the formula below:

1em = parent element's font size in pixels

32px = ?

Cross-multiplying results in:

1em *? = 32px* 1

? = 32px / 16px

? = 2em

*Therefore, 32px is equivalent to 2em when the parent element's font size is 16px.*

> Now try converting 5em to px, assuming: 
> 
> * The parent element’s font size is set to 2rem.
>     
> * The HTML root element’s font size is set to 20px.
>     

## **Browser Viewport’s Relative Units (VW and VH)**

Viewport relative units are CSS units that are relative to the size of the viewport, which is the visible area of the browser window. The two most commonly used viewport relative units are vw and vh. The "vw" unit represents 1% of the viewport's width, while the "vh" unit represents 1% of the viewport's height.

Understanding viewport relative units is important because they allow web developers to create responsive layouts that adapt to different screen sizes. By using these units, developers can ensure that their designs scale proportionally, regardless of the device or screen size being used. This is particularly important in today's world, where people access the web from a wide range of devices, including desktop computers, laptops, tablets, and smartphones.

For example, if a developer wants to create a full-width banner image that spans the entire width of the viewport, they could set the image's width to `100vw`. Similarly, if a developer wants to create a button that is always centred vertically and horizontally in the viewport, they could set the button's `position` to "`absolute`" and use the "`top: 50vh`" and "`left: 50vw`" properties to centre it. Overall, understanding viewport relative units is an important skill for web developers who want to create responsive and flexible web designs.

When vw and vh units are used to size or position an element, they are relative to the browser viewport rather than the element's parent. Due to this, a nested child element whose `width` is set to `80vw` would take `80%` of the viewport’s `width`, and not `80%` of the direct parent `width`.

Let's see what happens when a nested child element is being sized, using the browser viewport's relative unit.

%[https://codepen.io/utin-francis-peter/pen/poOwbPK] 

# **Conclusion**

CSS provides several units for sizing and positioning elements on a webpage.

The rendering process of absolute units is straightforward and does not depend on the context or parent elements. They include units like pixels (px), points (pt), inches (in), and centimetres (cm), among others.

On the other hand, relative units depend on the context of the parent element and the viewport. They include units like percentages (%), ems (em), rems (rem), viewport width (vw) and viewport height (vh).

It is best to use relative units in situations where elements should respond to changes in the browser's viewport or parent elements. However, in cases where absolute sizes are required, it is best to use absolute units.

It is essential to have a good understanding of CSS units to create responsive and accessible web pages. Some good references for further reading on CSS units include [Mozilla Developer Network (MDN)](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Values_and_units), [W3Schools](https://www.w3schools.com/cssref/css_units.php), and [CSS-Tricks](https://css-tricks.com/the-lengths-of-css/).

That's all folks! I hope this was helpful. Please do well to leave some feedback as this is my first technical article.