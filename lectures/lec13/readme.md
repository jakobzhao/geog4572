# Icons, Illustrator and Scalable Vector Graphics (SVG)

> Spring 2018 | Geography 4/572 | Geovisualization: Geovisual Analytics
>
> **Instructor:** Bo Zhao  **Location:** WITH 205 | **Time:** TR 1100 - 1150

**Learning Objectives**

- Apply icons for interactive web geovisualization;

- Use gravit (or illustrator) for basic design needs;

- Generate Vector graphics through raster images; and

- Create a Favicon for web pages.


## 1\. Icons for Web Uses

Icon is an important feature for geovisualization. It is simple, concrete and informative. Sometimes, a  icon is more than thousands of words or a well-designed map. In this section, we will talk about how to include icons in web pages.

There are several major icon libraries for web use. To name a few, such as [font awesome icons](https://fontawesome.com/icons?d=gallery), [Google material icons](https://material.io/icons/), [open icons](https://useiconic.com/open) and etc. To insert an icon to a web page, you will first include the icon library to the `<head>` tag, and then insert the `icon class` of the specific icon, sometimes associated with text, to the html elment you would like to visualize. The <i> and <span> elements are widely used to add icons. Here, Font Awesome Icons and Google Material Icons are introduced as follow.

### 1\.1 Font Awesome Icons

Font Awesome is a font and icon toolkit based on CSS and LESS. It was made by Dave Gandy for use with Twitter Bootstrap, and later was incorporated into the BootstrapCDN. Font Awesome has a 20% market share among those websites which use third-party Font Scripts on their platform, ranking it second place after Google Fonts.

Font Awesome 5 was released on December 7, 2017 with 1,278 icons. Version 5 comes in two packages: Font Awesome Free and the proprietary Font Awesome Pro (available for a fee). The free versions (all releases up to 4 and the free version for 5) are available under SIL Open Font License 1.1, Creative Commons Attribution 4.0, and MIT License.

![](img/fa.png)

To use the Font Awesome icons, add the following line inside the <head> section of your HTML page:

```html
 <link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.0.12/css/all.css">
```

Below shows some examples on using font awesome icons in web page.

```html
<p><i class="fas fa-user"></i>
    <i class="far fa-user"></i>
    <!--brand icon-->
    <i class="fab fa-github-square"></i>
</p>
<p>
    <i class="fab fa-github fa-xs"></i>
    <i class="fab fa-github fa-sm"></i>
    <i class="fab fa-github fa-lg"></i>
    <i class="fab fa-github fa-2x"></i>
    <i class="fab fa-github fa-3x"></i>
    <i class="fab fa-github fa-5x"></i>
    <i class="fab fa-github fa-7x"></i>
    <i class="fab fa-github fa-10x"></i>
</p>
```

### 1\.2 Google Material Icons

In a bid to create a new "visual language" for users, Google is taking the design of its Android, Chrome OS and web properties back to basics with its new "Material Design." According to Google, Material Design is intended to make better use of available space, and bring a consistent user experience whether viewed on a smartphone, tablet or desktop. Google's apps will be updated to reflect this change, as you may have seen in early Gmail and Calendar app leaks and in the latest version of the Google+ app on Android.

```html
<link rel="stylesheet" href="https://fonts.googleapis.com/icon?family=Material+Icons">
```

Below shows some examples on using material icons in web page. above all, you will need to define the styles in a `<style>` tag.

```css
<style>
    .red {
        color: red;
    }

    .large {
        font-size: 5vw;

    }

    .extra-large {
        font-size: 8vw;
    }
</style>
```

And then you can apply the styles to the icons. As you might notice, you need to insert a short text to indicate the specific icon to use. It is a little different from font awesome icons.

```html
<p>
    <span> <i class="material-icons">info</i></span>
    <span> <i class="material-icons red">face</i></span>
    <span> <i class="material-icons large">room</i></span>
    <span> <i class="material-icons extra-large">favorite</i></span>

</p>
```

![](img/material.png)

## Scalable Vector Graphics (SVG)

### Creating a vector using Gravit


### Vectorizing a raster image using Illustrator

With the introduction of the improved Image Trace function in Adobe Illustrator CS6 and later upgrades, a whole world of possibility opened up to users of graphics software who want the ability to trace line art and photos and turn them into vector images. Now users can turn bitmap to vectors and PNG files into SVG files using Illustrator with relative ease.

#### 1\. Getting Started

This process works best with an image with a subject that stands out clearly against its background, such as the cow in the image above.

To add an image to trace, select `File > Place` and locate the image to be added to the document. When you see the “Place Gun,” click the mouse and the image drops into place.

To start the tracing process, click once on the image to select it.

When converting an image to vectors, the areas of contiguous colors are converted to shapes. The more shapes and vector points, such as in the village image above, the larger the file size and the greater CPU resources required as the computer works to map all of those shapes, points, and colors to the screen.

#### 2\. Types of Tracing

With the image in place, the most obvious starting point is the Image Trace dropdown in the Illustrator Control Panel. There are a lot of choices that are aimed at specific tasks; you may wish to try each one to see the result. You can always return to your starting point by pressing Control-Z (PC) or Command-Z (Mac) or, if you really messed up, by selecting `File > Revert`.

When you choose a Trace method, you will see a progress bar showing you what is going on. When it finishes, the image is converted to a series of vector paths.


#### 3\. View and Edit

If you select the tracing result with either the Selection Tool or the Direct Selection Tool, the entire image is selected. To see the paths themselves, click the `Expand` button in the Control Panel. The tracing object is converted to a series of paths.

In the case of the above image, we can select the sky and grass areas and delete them.

To further simplify the image, we can select `Object > Path > Simplify` and use the sliders in the Simplify panel to reduce the number of points and curves in the traced image.

#### 4\. Edit a Traced Image

With the trace completed, you may want to remove portions of it. In this example, we wanted just the cow without the sky or the grass.

To edit any traced object, click the `Expand` button in the Control Panel. This will turn the image into a series of editable paths. Switch to the `Direct Selection` tool and click on the paths to be edited.

#### 5\. Export as a SVG file



## Favicons for web pages

A favicon (short for favorite icon), also known as a shortcut icon, website icon, tab icon, URL icon, or bookmark icon, is a file containing one or more small icons,associated with a particular website or web page. A web designer can create such an icon and upload it to a website (or web page) by several means, and graphical web browsers will then make use of it. Browsers that provide favicon support typically display a page's favicon in the browser's address bar (sometimes in the history as well) and next to the page's name in a list of bookmarks. Browsers that support a tabbed document interface typically show a page's favicon next to the page's title on the tab, and site-specific browsers use the favicon as a desktop icon.

To add a favicon, you need to creat one using an image editor, such as illustrator or photoshop. Or, you can find an open source one from google image search. Regarding the images found from the Internet, please refer to or credit the author's efforts in your web map application.

For example, I search "oregon icon" on [Google Images](https://images.google.com/)

![](img/google-image.png)

I find an png image, and then convert the image to ico from http://convertico.com/.

![](img/convertico.png)

I downloaded the converted file, named it as **favicon.ico**, and then put it in the `img` folder.

To properly show the favicon, I added one line in the `head` tag of the `index.html` file.

```html
<!--add favicon for the web page-->
<link rel="shortcut icon" href="img/favicon.ico" type="image/x-icon">
```

Regarding the code, I declare that I added the favicon for the web page, and include from the right place. If everything works correctly, you will see an icon showing on the web page tab on your Google Chrome browser.

![](img/favicon-web-page-tab.png)



## References

[1] https://www.flaticon.com/

[2] https://mangomap.com/blog/3-more-free-map-icon-packs/

[3] https://fontawesome.com/how-to-use/web-fonts-with-css

[4] https://www.lifewire.com/use-image-trace-in-adobe-illustrator-cc-2017-4125254