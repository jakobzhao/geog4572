# Color Use and Web Typogrpahy

> Spring 2018 | Geography 4/572 | Geovisualization: Geovisual Analytics
>
> **Instructor:** Bo Zhao  **Location:** WITH 205 | **Time:** TR 1100 - 1150

**Learning Objectives**

- Learn the basic syntax of Bootstrap;
- Learn how to use Bootstrap to set up a web user interface.
- Learn how to set up a google analytics to assess your web site.


## Color

###

## 2\. Web Typography

Difference Between Serif and Sans-serif Fonts

![](assets/serif.gif)

The `font-family` property specifies the font for an element. The font-family property can hold several font names as a ***"fallback"*** system. If the browser does not support the first font, it tries the next font.

There are two types of font family names:

`family-name` - The name of a font-family, like "times", "courier", "arial", etc.
`generic-family` - The name of a generic-family, like "serif", "sans-serif", "monospace".

Start with the font you want, and always end with a generic family, to let the browser pick a similar font in the generic family, if no other fonts are available.


```css
p.a {
    font-family: "Times New Roman", Times, serif;
}

p.b {
    font-family: Arial, Helvetica, sans-serif;
}
```

**Note:** Separate each value with a comma.

**Note:** If a font name contains white-space, it must be quoted. Single quotes must be used when using the "style" attribute in HTML.


### Popular Font Alternatives

In this section, I listed the google web font alternative to the commonly used commerical fonts.

![](img\GoogleFontAlt.png)


| Commonly Used Commercial Fonts | Google Web Fonts |
| ------------------------------ | ---------------- |
| Helvetica                      | Sans Source Pro  |
| Century Gothic                 | Questrial        |
| Calibri                        | Droid Sans       |
| Garamond                       | Merriweather     |
| Avenir Next Rounded            | Nunito           |
| Frutiger                       | Istok Web        |
| Adobe Caslon Pro               | Lusitana         |
| Futura Condensed               | Oswald           |
| Rockwell                       | Arvo             |
| Impact                         | Anton            |


### commonly used font combinations

**Serif Fonts**

- Georgia, serif

- "Palatino Linotype", "Book Antiqua", Palatino, serif

- "Times New Roman", Times, serif


**Sans-Serif Fonts**

- Arial, Helvetica, sans-serif

- "Arial Black", Gadget, sans-serif

- "Comic Sans MS", cursive, sans-serif

- Impact, Charcoal, sans-serif

- "Lucida Sans Unicode", "Lucida Grande", sans-serif

- Tahoma, Geneva, sans-serif

- "Trebuchet MS", Helvetica, sans-serif

- Verdana, Geneva, sans-serif

**Monospace Fonts**

- "Courier New", Courier, monospace

- "Lucida Console", Monaco, monospace

### Use a Google Web Font

To use a google font in your web application, you should include the font link in the head element as shown below:

```html
    <link href='//fonts.googleapis.com/css?family=Sofia' rel='stylesheet'>
```

Apply a google font for a specific div. For example, the code below applies the sofia font to all the texts inside of the body div.

```css
 <style>
        body {
            font-family: 'Sofia';font-size: 22px;
        }
    </style>
```



### Font Template
Look for the font families on [Google Web Fonts](https://fonts.google.com/), and generate the font css for the following html elements, including `html`, `body`, `h1` to `h6`, and other elements you think is necessary.

> **Note:** regarding the header elements, perhaps your project will not use al the six headers, please only list those are important.

```html
<!DOCTYPE html>
<html>
<head>
    <title>Font Template Page</title>
    <link href='//fonts.googleapis.com/css?family=Sofia' rel='stylesheet'>
    <style>
        body {
            font-family: 'Sofia';font-size: 22px;
        }
    </style>
</head>
<body>

<h1>Sofia</h1>
<p>Lorem ipsum dolor sit amet, consectetuer adipiscing elit.</p>
<p>123456790</p>
<p>ABCDEFGHIJKLMNOPQRSTUVWXYZ</p>
<p>abcdefghijklmnopqrstuvwxyz</p>

</body>
</html>
```


## References

[1] https://www.canva.com/font-combinations/gesta/
