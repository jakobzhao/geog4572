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



Typography is the art and technique of arranging type to make written language legible, readable, and appealing when displayed. The arrangement of type involves selecting typefaces, point sizes, line lengths, line-spacing (leading), and letter-spacing (tracking), and adjusting the space between pairs of letters (kerning). The term typography is also applied to the style, arrangement, and appearance of the letters, numbers, and symbols created by the process. Type design is a closely related craft, sometimes considered part of typography; most typographers do not design typefaces, and some type designers do not consider themselves typographers. Typography also may be used as a decorative device, unrelated to communication of information.



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


### Difference Between Serif and Sans-serif Fonts

![](assets/serif.gif)

`Serif` -  Serif fonts have small lines at the ends on some characters, like "Times New Roman", "Georgia".

`Sans-serif` - "Sans" means without - these fonts do not have the lines at the ends of characters, like "Arial", "Verdana". **On computer screens, sans-serif fonts are considered easier to read than serif fonts.**

`Mobospace`  - All monospace characters have the same width, like "Courier New", "Lucida Console".

### Font Style, Size and Weight

The **font-style** property is mostly used to specify italic text.

This property has three values:

normal - The text is shown normally
italic - The text is shown in italics
oblique - The text is "leaning" (oblique is very similar to italic, but less supported)

```css
p.normal {
    font-style: normal;
}

p.italic {
    font-style: italic;
}

p.oblique {
    font-style: oblique;
}
```


The **font-size** property sets the size of the text.

Being able to manage the text size is important in web design. However, you should not use font size adjustments to make paragraphs look like headings, or headings look like paragraphs.

Always use the proper HTML tags, like <h1> - <h6> for headings and <p> for paragraphs.

The font-size value can be an absolute, or relative size.

```css

body {
    font-size: 100%;
}

h1 {
    font-size: 40px;
}

h2 {
    font-size: 30px;
}

p {
    font-size: 14px;
}
```

The **font-weight** property specifies the weight of a font:

```css
p.normal {
    font-weight: normal;
}

p.thick {
    font-weight: bold;
}
```

```html
<h1 style="font-size:10vw">Hello World</h1>
```


### Responsive Font Size

The text size can be set with a vw unit, which means the "viewport width".

That way the text size will follow the size of the browser window:

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


Google Fonts (previously called Google Web Fonts) is a library of over 800 libre licensed fonts, an interactive web directory for browsing the library, and APIs for conveniently using the fonts via CSS and Android.

The Google Fonts directory is intended to enable font discovery and exploration, and the service is used extensively with over 17 trillion font served, which means that each of its 877 fonts has been downloaded over 19 billion times, which means that each person on Earth has, on average, downloaded each font at least 2 or 3 times. Popular fonts include `Open Sans`, `Roboto`, `Lato`, `Slabo 27px`, `Oswald` and `Lobster`.


To use google font, Looking up the font families on [Google Web Fonts](https://fonts.google.com/), and generate the font css for the following html elements, including `html`, `body`, `h1` to `h6`, and other elements you think is necessary.

The library is maintained through Google Fonts' GitHub repository at [github.com/google/fonts](github.com/google/fonts), where all font files can be obtained directly. Source files for many of the fonts are available from git repositories within the github.com/googlefonts Github organization, along with libre software tools used by the Google Fonts community.

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

[2] https://developers.google.com/fonts/docs/getting_started
