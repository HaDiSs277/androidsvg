# AndroidSVG

AndroidSVG is a SVG parser and renderer for Android.  It has almost complete support for the static
visual elements of the SVG 1.1 and SVG 1.2 Tiny specifications (except for filters).  AndroidSVG
correctly renders the [SVG Acid Test](http://www.codedread.com/acid/acid1.html).

*AndroidSVG is licensed under the [Apache License v2.0](http://www.apache.org/licenses/LICENSE-2.0)*.

<a href="https://twitter.com/AndroidSVG"><img src="http://i.imgur.com/gSGIbYP.png"/></a>

## Downloads

The [current release (v1.2.1)](https://bitbucket.org/paullebeau/androidsvg/downloads) is hosted at Bitbucket.

Check the [Release Notes](https://code.google.com/p/androidsvg/wiki/ReleaseNotes) to find out what's in the latest release.

Older releases can be found on this site's [ downloads page](https://code.google.com/p/androidsvg/downloads/list?can=1&q=&colspec=Filename+Summary+Uploaded+ReleaseDate+Size+DownloadCount).

## Editor support

A design goal of this project is to correctly render SVG files that have been exported from the
most popular vector editors. AndroidSVG has been tested with files generated by Adobe Illustrator,
Inkscape, Xara and Corel Draw.

![SVG Acid Test](http://i.imgur.com/ZaOi6rO.png)
![Xara Blue car](http://i.imgur.com/og8xnr6.png)

## How do I use AndroidSVG?

Download the latest release from the [download page](https://bitbucket.org/paullebeau/androidsvg/downloads)
and add it to your project.  If you are using Eclipse, you can drag the library to the `libs` folder for
your project in the Package Explorer.

For those building with Maven, AndroidSVG releases are also avaliable in the [Maven Central Repository](http://search.maven.org/#search|gav|1|g%3A%22com.caverock%22%20AND%20a%3A%22androidsvg%22).
To include AndroidSVG in your project, add the following dependency to your POM file.

```
<dependency>
  <groupId>com.caverock</groupId>
  <artifactId>androidsvg</artifactId>
  <version>1.2.1</version>
</dependency>
```

## API Introduction

All interaction with AndroidSVG is via the `SVG` class.

Typically, you will call one of the SVG loading and parsing classes then call the renderer, passing it a canvas to draw upon.
 
* Use one of the static `SVG.getFromX()` methods to read and parse the SVG file.  They will return an instance
  of the `SVG` class.
* Then to render, you can either call `renderToPicture()` to get an Android `Picture` instance, or call
  `renderToCanvas()` to render directly to a Canvas.

For more information, see the [Documentation](https://code.google.com/p/androidsvg/wiki/Documentation) or
read the [Javadoc](https://androidsvg.googlecode.com/hg/doc/index.html).

## Usage example

[Download the latest version](https://bitbucket.org/paullebeau/androidsvg/downloads) and copy it to your `libs` folder
in Eclipse.  Then in your app, you can do something like the following.

```java
  // Read an SVG from the assets folder
  SVG  svg = SVG.getFromAsset(getContext().getAssets(), filename);
  // Create a canvas to draw onto
  if (svg.getDocumentWidth() != -1) {
     Bitmap  newBM = Bitmap.createBitmap(Math.ceil(svg.getDocumentWidth()),
                                         Math.ceil(svg.getDocumentHeight()),
                                         Bitmap.Config.ARGB_8888);
     Canvas  bmcanvas = new Canvas(newBM);
     // Clear background to white
     bmcanvas.drawRGB(255, 255, 255);
     // Render our document onto our canvas
     svg.renderToCanvas(bmcanvas);
  }
```

If you just want to use an SVG icon in your layout, you can use the supplied
[SVGImageView](https://code.google.com/p/androidsvg/wiki/SVGImageView) custom view class.

## What features of SVG are supported?

AndroidSVG supports the following SVG elements:

### Fully supported

`<circle> <clipPath> <defs> <desc> <ellipse> <g> <line> <linearGradient> <marker> <mask> <path> <polygon> <polyline> <rect> <solidColor> <stop> <svg> <switch> <symbol> <title> <use> <view>`.

### Supported with some limitations

`<image> <text> <textPath> <tref> <tspan> <pattern> <radialGradient> <style>`

### Not supported at all

* Animation is not supported.
* Filters are not supported.

For more information on what elements, attributes and properties are supported, see the
[https://code.google.com/p/androidsvg/wiki/SVGImplementationDetails](SVGImplementationDetails SVG Implementations Details) page.

### Find a bug?

Please file an [bug report](https://github.com/BigBadaboom/androidsvg/issues) and include as much detail as you can.
If possible, please include a sample SVG file showing the error.

If you wish to contact the author with feedback on this project, you can email me at
[androidsvgfeedback@gmail.com](mailto:androidsvgfeedback@gmail.com).

If you have found AndroidSVG useful and use it in your project, please let me know. I'd love to hear about it!