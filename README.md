# Week 2 Practical 2 - Positioning

In this practical, you will practice creating page layouts using basic CSS. This is one of the hardest skills to master in CSS as it is quite easy to unintentionally create styles that cancel each other out and you are often fighting against implicit style rules and the many, many quirks of CSS. There are more modern approaches to layout that can make this task _slightly_ easier. We will cover these approaches next week. For now, however, your job is to wrestle with the older approach to layout as it is still useful and widely used and therefore important to know. 

## Stage 1: Adding General Styles
Alongside these instructions, you will have downloaded a folder containing an HTML file and a folder with images. The HTML file represents a webpage for a fictional news organisation, York University Press.

### Exercise 1.1: Examine the HTML
Open the starter code folder in VS Code and read the HTML. Look carefully at the elements used and where IDs and classes are used. If you encounter elements you haven’t seen before, look them up in the reference (MDN or W3 Schools).

Open the page in Chrome, preferably using the Live Server extension.

### Exercise 1.2: Add general styles for text
Create a CSS file and link it to the HTML.

Add the following styles:
- Change the font family for all text to a sans-serif font, using one of the [CSS Web Safe Fonts](http://www.w3schools.com/cssref/css_websafe_fonts.asp) or a combination suggested by VS Code.
- Choose a different font for headings. It should apply to all heading levels (h1 through h6).
- Remove the underlines from all links and change their colour. It is important for usability that links look visually distinct from other text so make sure the colour is different from the rest of the text.
- Set the font size of all h1 elements to 2em.
- …but the main site heading should have a unique font that is different from other headings and the rest of the page text. It should also be bigger than other headings of the same level, and it should be a different colour.
- Optionally, style other text properties such as `line-height` and `font-weight`. For size-related properties such as `line-height` and `font-size`, be sure to use relative units.

## Stage 2: CSS Layouts Exercises

The final objective is to create the layout shown below, but the process has been broken down step by step in different exercises.

![Layout for stage 2 exercises](https://github.com/IM-WADD/Week2Practical2/assets/5978932/d3a942d6-df99-4300-83c8-628fef27ed25)

### Exercise 2.1: Create the content area 
In the image of the final layout, notice that the content is contained in a central area with equal size margins on either side. Create this effect by changing the background colour of the body to a colour of your choosing. 

HTML elements are transparent by default so you will be able to see your background colour behind the text. You will need to set the background colour of your content elements to white. The simplest way to do this is to add a `<div>` as the first child of the `<body>` element then put all the other content elements inside it. We haven’t seen `<div>` much yet because there have been better semantic choices in the examples so far. However, this is an appropriate time to use a `<div>` as the goal is to create a visual grouping without a particular meaning in terms of the content or structure of the page. 

Add CSS to give the `<div>` a white background and equal size left and right margins (use relative units!). It’s a good idea to give the `<div>` a unique ID for styling purposes, just in case you need to use more `<div>` elements elsewhere in the page. 

### Exercise 2.2: Style the header
Get the page title and date to appear side-by-side by setting `display` to `inline-block` on the appropriate elements. 

The date should be right aligned using the `text-align` property. Normally, that is all that is required to set the alignment of a paragraph. However, remember that setting a block element’s `display` property to `inline` or `inline-block` causes its width to shrink from the width of its parent to the width of its content. This means that right aligned text will appear the same as left aligned text. To get around this, you can set the widths of the page title and date elements using relative units that add up to 100%.

You’ve probably just encountered another CSS quirk: the `inline-block` whitespace issue. In lecture, we saw that we can fix misbehaving widths of block elements by setting the `box-sizing` property to `border-box` so that the width calculation includes padding, border, and margin as well as content. Although the current problem looks similar, the box model is not the culprit in this instance. When the browser renders `inline-block` elements, it automatically adds a few pixels of space for any white space it encounters in the HTML file. This includes line breaks between HTML elements. There are two ways to fix this, both are hacky:

1. Delete the line breaks between the page title and date elements in the HTML file. This is simple but prone to accidental breakage should you decide to improve the readability of your code in future.
2. Set the `font-size` of the parent element (`<header>`) to 0. This prevents the whitespace from rendering. However, if you used “em” units to set the size of your page title and date, or you didn’t set their sizes at all, you will find that the text disappears. In the case of em units, this is because the font-size is calculated relative to the parent `font-size`, which is now 0. Simply change “em” to “rem” and your text should reappear. If you did not set the `font-size` of the date, give it a size of 1rem to override the 0 inherited from the parent. 

### Exercise 2.3: Style the main navigation
Style the navigation items using the `inline-block` approach once again. The steps you need to take will be very similar to the example shown in the last lecture.

Notice that, in the final layout, the items stretch across the full width of the line, with each item taking up 25% of the content area width. Your navigation should do the same. Also make your navigation items look more button-like using `background-color` and `padding` in the appropriate places. The button background should change colour when an item link is hovered.

Tip: In lecture, we made the navigation item background change colour on hover by adding a hover effect to the list item, rather than the link. This created the visual effect we wanted but had the drawback of giving users the impression that the item background is clickable when it isn’t. Try this alternative approach:

1. Set the navigation link’s `display` property to `block` (it is `inline` by default). This will cause the link to take up the full width of the list item.
2. Set the navigation link’s `line-height` to be the desired full height of the list item (I used 2rem) and remove any `padding` from the list item. This makes the link take up the full height of the list item.

Now, clicking on the list item background will also activate the link

### Exercise 2.4: Create the middle section
Look at the final layout alongside the HTML. Hopefully you can see how the main layout grid areas map to the semantic HTML elements. Notice that the `<main>` area fills 75% of the content area width. The `<aside>` is 25% of the content area width and sits alongside the `<main>` area.

Write CSS to achieve this layout using any of the approaches covered in lecture. There are a few different ways to approach this task. All have pros and cons!
1. Set `float:left` on `<main>`. You will also need to add styling to `<footer>`.
2. Alternatively, change the display property of `<main>` and `<aside>` to `inline-block`. If you find the `<aside>` is not aligned with the top of `<main>`, try setting the `vertical-align` property of `<aside>`.
3. Another option is to use the `position` property. You will likely need to wrap `<main>` and `<aside>` in another `<div>` with its `position` property set.

### Exercise 2.5: The Main News Story
The main news story consists of the headline, content paragraphs including subheadings and an image with a caption. Make the image and caption float to the right of the story, with the subheading and its content wrapping the image.

Once you have successfully coded this layout, put the figure caption within the image in a semi-transparent box, similar to that shown below. Consider making the caption background a little less transparent than pictured to improve readability.

![Caption readability example](https://github.com/IM-WADD/Week2Practical2/assets/5978932/ec51b4c0-d7ce-492a-b937-49856d4cb61a)

Hint: You will need to think about which positioning method should be used for the caption.

### Exercise 2.6: The Other Headlines content
Using either `float` or `inline-block` position the images and headlines in the Other Headlines section as shown in the final layout.

### Exercise 2.7: The footer
Give the footer a background colour then align the copyright text so it is centred horizontally and vertically.

