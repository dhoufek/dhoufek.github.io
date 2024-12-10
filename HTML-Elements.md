Web browsers provide default styles for HTML elements. Some elements in the framework retain those browser defaults, but most have a minimal amount of opinionated styling applied to them.

# Browser Defaults
Use the `<del>` tag for text that is meant to be treated as deleted text.

Use the `<s>` tag for text that is meant to be treated as no longer accurate or no longer relevant.

Use the `<ins>` tag for text that is meant to be treated as an addition to the document.

Use the `<u>` tag for underlined text.

Use the `<strong>` tag for text with strong importance.

Use the `<b>` tag or the `.dcf-bold` class for bold text without conveying any extra importance.

Use the `<em>` tag to stress text of linguistic import, the way you would emphasize pronunciation if the same text was spoken.

Use the `<i>` tag or the `.dcf-italic` class to italicize text without conveying any extra importance.

Use the `<time>` tag along with the `datetime` content attribute to display dates and time.

# Abbreviations
`<abbr>`

Abbreviations should be spelled out on first occurrence, then abbreviated using the <abbr> element on subsequent occurrences.

# Addresses
`<address>`

The address element should be used for physical or digital contact information for a person, people or an organization.

# Anchors
`<a>`

Use to link to other content. If the link goes to an external site and does not contain an image or SVG as a child, an icon will be appended to the link to indicate external content to users.

# Blockquotes
`<blockquote>`

The blockquote element mostly retains browser default styling, but its measure is restricted to prevent unnecessarily long lines, aiding readability.

# Buttons
`<button>` `<input type="button">` `<input type="submit">`

Baseline button styles to reset display, padding, font-size, line-height, and text alignment.

# Code
`<code>`

Wrap inline snippets of code with `<code>`. Be sure to escape HTML angle brackets.

`<pre>`

Wrap multiple lines of code with `<pre>`. Use the `.dcf-pre` component class to retain code styling.

`<var>`

Variable content

`<kbd>`

User input

`<samp>`

Sample output

# Details & Summary
`<details>` `<summary>`

Combine these elements to build a [native accordion](https://css-tricks.com/quick-reminder-that-details-summary-is-the-easiest-way-ever-to-make-an-accordion/) (i.e., content that can be expanded and contracted).

# Figures
`<figure>` `<figcaption>`

The browser default margins have been removed from the figures.

# Forms
`<form>` `<fieldset>` `<legend>` `<label>` `<input>` `<select>` `<option>` `<textarea>`

Styles applied directly to form elements are intentionally kept to a minimum.

# Headings
`<h1>` `<h2>` `<h3>` `<h4>` `<h5>` `<h6>`

Headings should be selected to accurately convey content hierarchy, not to resize text for the aesthetic needs of the page layout. Instead, use utility classes to increase or decrease a heading’s font-size.

# Horiztonal Rules
`<hr>`

The horizontal rule marks a thematic division of content on the page.

# Images
`<img>`

Ensure that accurate descriptions of the image content are included in the `alt` attribute of each image for accessibility.

# Lists
## Description Lists
`<dl>` `<dt>` `<dd>`

The description list (once known as the definition list) is used to mark up groups of terms and descriptions.

## Ordered Lists
`<ol>` `<li>`

The ordered list prepends each list item with a sequential number.

## Unordered Lists
`<ul>` `<li>`

The unordered list prepends each list item with a bullet.

# Marks
`<mark>`

Use the mark element to highlight text.

# Paragraphs
`<p>`

Use the paragraph element to mark up—you guessed it—paragraphs.

# Progress
`<progress>`

Display the completion progress of a task. Remember to use a `<label>` that includes a `for` attribute that matches the unique `id` attribute in the `<progress>`.

# Quotes
`<q>`

“Smart” or “curly” quotes are applied to inline quotes—no need to add your own.

# Small
`<small>`

The small element is [intended for inline text](https://www.w3.org/wiki/HTML/Elements/small) meant to be treated as fine print. It does not change the `font-size`. Add a `font-size` utility class (like `.dcf-txt-xs`) to the small element to reduce its `font-size`.

# Subscripts & Superscripts
`<sub>`

Subscripts reduce the font-size and place copy slightly below the baseline.

`<sup>`

Superscripts reduce the font-size and elevate the copy slightly above the cap line.

# Tables
`<table>` `<caption>` `<thead>` `<tbody>` `<tfoot>` `<tr>` `<th>` `<td>`

Table borders are collapsed and the background is made transparent.