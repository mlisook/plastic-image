# \<plastic-image\>

A Polymer 2.0 element which adds extra plasticity to `iron-image` with support for **srcset**,
**lazy loading** and **webp**.

`plastic-image` extends `iron-image` by adding a `srcset` attribute for client side image
size selection. It adds a `lazy-load` attribute for deferring the image load until
the element is showing in the viewport. Finally, it allows you to serve (typically smaller) 
`webp` images to browsers that support webp.

Please review the api docs for `iron-image` as this element is a subclass of `iron-image`.

## plastic-image srcset 

The `srcset` attribute is a string consisting of one or more image selection strings separated by commas. 
Each image selection string is composed of:

1. A url to an image
2. One or more spaces as a separator
3. One or _more_ descriptors separated by spaces
  - width descriptor: a positive integer directly followed by 'w'. e.g. `700w`
  - height descriptor: a positive integer directly followed by 'h'. e.g. `345h`
  - pixel density descriptor: a positive floating point number directly followed by 'x'. e.g. `2.0x`

`plastic-image` extends the `<img srcset="...">` feature by allowing multiple descriptors for an image
and mixed descriptors in a single srcset.

`plastic-image` also extends srcset use by optionally allowing image selection to be based on the render size of
the `plastic-image` element instead of the viewport, which is the standard.  To use this optional function 
include the `use-element-dim` attribute.

### Example srcset

`srcset="foo-s.jpg 150w, foo-sh.jpg 150w 2.0x, foo-m.jpg 405w, foo-mh 2.0x 405w, foo-l 1024w, foo-t 500w 750h"`

### Automatic Density

If _none_ of the image selection strings includes a pixel density descriptor ('x' e.g. `4.0x`), then the image
selection process will automatically compensate for the viewport's pixel density.

## Lazy ... wait for it ... Loading

Lazy loading delays loading the image (but not the placeholder image) until the element is at least 1px inside the viewport. 
This can improve the perceived performance of the page by removing below the fold images from first paint. 

`plastic-image` uses an `IntersectionObserver` to trigger image loads when `lazy-load` is selected. IntersectionObserver is automatically polyfilled if a feature test shows the browser does not include native support. 

To use lazy loading simply add the `lazy-load` attribute to the element.

```HtML
<plastic-image preload fade lazy-load srcset="..." ... ></plastic-image>
```

## Webp Support

You can include `webp` format images alongside images of other formats (e.g. JPG, GiF, PNG) in the `srcset`
attribute.  If you include one or more webp images and the browser supports webp, the control will select
the best fit webp image.  If the browser does not support webp, the control will select  the best fit non webp image.

Webp images are typically significantly smaller than JPG or PNG so it can represent a decrease in network traffic.

There are no flags or attributes to enable this support.  Just include webp along with non webp images in the srcset to take advantage.  

### Example Webp

```HTML
<plastic-image id="wp01" lazy-load preload fade use-element-dim sizing="contain" style="height: 200px; width: 300px;"
          srcset="images/20160827_055746-150x150.jpg 150w,images/20160827-055746-150x150.webp 150w,images/20160827_055746-300x169.jpg 300w,images/20160827-055746-300x169.webp 300w,images/20160827_055746-768x432.jpg 768w,images/20160827-055746-768x432.webp 768w"
          placeholder="data: image/jpeg;base64,/9j/4AAQSkZJRgABAQAAAQABAAD//gA7Q1JFQVRPUjogZ2QtanBlZyB2MS4wICh1c2luZyBJSkcgSlBFRyB2OTApLCBxdWFsaXR5ID0gODIK/9sAQwAGBAQFBAQGBQUFBgYGBwkOCQkICAkSDQ0KDhUSFhYVEhQUFxohHBcYHxkUFB0nHR8iIyUlJRYcKSwoJCshJCUk/9sAQwEGBgYJCAkRCQkRJBgUGCQkJCQkJCQkJCQkJCQkJCQkJCQkJCQkJCQkJCQkJCQkJCQkJCQkJCQkJCQkJCQkJCQk/8AAEQgACAAOAwEiAAIRAQMRAf/EAB8AAAEFAQEBAQEBAAAAAAAAAAABAgMEBQYHCAkKC//EALUQAAIBAwMCBAMFBQQEAAABfQECAwAEEQUSITFBBhNRYQcicRQygZGhCCNCscEVUtHwJDNicoIJChYXGBkaJSYnKCkqNDU2Nzg5OkNERUZHSElKU1RVVldYWVpjZGVmZ2hpanN0dXZ3eHl6g4SFhoeIiYqSk5SVlpeYmZqio6Slpqeoqaqys7S1tre4ubrCw8TFxsfIycrS09TV1tfY2drh4uPk5ebn6Onq8fLz9PX29/j5+v/EAB8BAAMBAQEBAQEBAQEAAAAAAAABAgMEBQYHCAkKC//EALURAAIBAgQEAwQHBQQEAAECdwABAgMRBAUhMQYSQVEHYXETIjKBCBRCkaGxwQkjM1LwFWJy0QoWJDThJfEXGBkaJicoKSo1Njc4OTpDREVGR0hJSlNUVVZXWFlaY2RlZmdoaWpzdHV2d3h5eoKDhIWGh4iJipKTlJWWl5iZmqKjpKWmp6ipqrKztLW2t7i5usLDxMXGx8jJytLT1NXW19jZ2uLj5OXm5+jp6vLz9PX29/j5+v/aAAwDAQACEQMRAD8A8p8A/EK70MfZbvVJ0tAuF8qJGcHju3br611Go/EPS7pkY+K7tMDBV7ZevrxHRRXdSzKtTVt/W/8AmeRUwVOc3fr6f5H/2Q==" >
        </plastic-image>
``` 

## Install the Component

`bower install --save plastic-image`

## Basic Use Examples
Use the control as you would an `iron-image` but with the srcset.

```HTML
<plastic-image preload fade sizing="contain"
  srcset="images/foo-s.jpg 150w, images/foo-sh.jpg 150w 2.0x, images/foo-m.jpg 405w, 
  images/foo-mh 2.0x 405w, images/foo-l 1024w, images/foo-t 500w 750h"
  placeholder="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAYAAAAGCAYAAADgzO9IAAAAmElEQVQImWNmYGBgSExMzBATE7dSVFT8eO/evTcMDAwMjIFe5iYSIjybL136cunNW56FulIaEoJcfBdY5GWjvJ4/+SJhIcUhwavI5SbIxR+YvzRqH8unx7/Osf8VYpAVEWLgZuO8ljrfbwMDAwMD07u/j/ZYun5f9JfjSfGnHx9dGaCAJcBimwXjZ4Z+HllGn0XbXr+ASQAAi5UxQq88/fsAAAAASUVORK5CYII="></plastic-image>
```

To base image selection on the rendered size of the control, instead of the viewport (default), add the `use-element-dim` attribute.

```HTML
<plastic-image preload fade sizing="contain" use-element-dim
  srcset="images/foo-s.jpg 150w, images/foo-sh.jpg 150w 2.0x, images/foo-m.jpg 405w, 
  images/foo-mh 2.0x 405w, images/foo-l 1024w, images/foo-t 500w 750h"
  placeholder="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAYAAAAGCAYAAADgzO9IAAAAmElEQVQImWNmYGBgSExMzBATE7dSVFT8eO/evTcMDAwMjIFe5iYSIjybL136cunNW56FulIaEoJcfBdY5GWjvJ4/+SJhIcUhwavI5SbIxR+YvzRqH8unx7/Osf8VYpAVEWLgZuO8ljrfbwMDAwMD07u/j/ZYun5f9JfjSfGnHx9dGaCAJcBimwXjZ4Z+HllGn0XbXr+ASQAAi5UxQq88/fsAAAAASUVORK5CYII="></plastic-image>
```

To automatically compensate for pixel density do not supply _any_ pixel density descriptors in the srcset.

```HTML
<plastic-image preload fade sizing="contain" use-element-dim
  srcset="images/foo-s.jpg 150w, images/foo-sh.jpg 300w, images/foo-m.jpg 405w, 
  images/foo-mh 810w, images/foo-l 1024w, images/foo-t 500w 750h"
  placeholder="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAYAAAAGCAYAAADgzO9IAAAAmElEQVQImWNmYGBgSExMzBATE7dSVFT8eO/evTcMDAwMjIFe5iYSIjybL136cunNW56FulIaEoJcfBdY5GWjvJ4/+SJhIcUhwavI5SbIxR+YvzRqH8unx7/Osf8VYpAVEWLgZuO8ljrfbwMDAwMD07u/j/ZYun5f9JfjSfGnHx9dGaCAJcBimwXjZ4Z+HllGn0XbXr+ASQAAi5UxQq88/fsAAAAASUVORK5CYII="></plastic-image>
```

To defer loading until the image is in (well, at least peaking into) the viewport add the `lazy-load` attribute.

```HTML
<plastic-image lazy-load preload fade sizing="contain"
  srcset="images/foo-s.jpg 150w, images/foo-sh.jpg 150w 2.0x, images/foo-m.jpg 405w, 
  images/foo-mh 2.0x 405w, images/foo-l 1024w, images/foo-t 500w 750h"
  placeholder="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAYAAAAGCAYAAADgzO9IAAAAmElEQVQImWNmYGBgSExMzBATE7dSVFT8eO/evTcMDAwMjIFe5iYSIjybL136cunNW56FulIaEoJcfBdY5GWjvJ4/+SJhIcUhwavI5SbIxR+YvzRqH8unx7/Osf8VYpAVEWLgZuO8ljrfbwMDAwMD07u/j/ZYun5f9JfjSfGnHx9dGaCAJcBimwXjZ4Z+HllGn0XbXr+ASQAAi5UxQq88/fsAAAAASUVORK5CYII="></plastic-image>
```

To serve webp images to browsers that support webp and jpg to browsers that do not, simply include
the alternate webp images in the srcset.  You can mix in width, height and density selectors also.

```HTML
<plastic-image lazy-load preload fade sizing="contain"
  srcset="images/foo-s.jpg 150w, images/foo-s.webp 150w, 
    images/foo-m.jpg 405w, images/foo-m.webp 405w, 
    images/foo-mh.jpg 2.0x 405w, images/foo-mh.webp 2.0x 405w"
  placeholder="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAYAAAAGCAYAAADgzO9IAAAAmElEQVQImWNmYGBgSExMzBATE7dSVFT8eO/evTcMDAwMjIFe5iYSIjybL136cunNW56FulIaEoJcfBdY5GWjvJ4/+SJhIcUhwavI5SbIxR+YvzRqH8unx7/Osf8VYpAVEWLgZuO8ljrfbwMDAwMD07u/j/ZYun5f9JfjSfGnHx9dGaCAJcBimwXjZ4Z+HllGn0XbXr+ASQAAi5UxQq88/fsAAAAASUVORK5CYII="></plastic-image>
```

If you need to control when to load (perhaps you are waiting for an ajax response) use the `delay-load` attribute and then set `delayLoad` to false once your data is ready.

```HTML
<plastic-image id="foo" delay-load lazy-load preload fade sizing="contain"
  srcset="[[myImageSelector]]"
  placeholder="[[myMicroB64]]"></plastic-image>
```

```Javascript
fetch('imageDetail/47561').then((response) => {
  return response.json();
}).then((imgData) => {
  this.myImageSelector = imgData.srcset;
  this.myMicroB64 = imgData.mt;
  this.$.foo.delayLoad = false;
});
```

## Polymer Build / polymer.json
The element may automaticall loads 2 polyfill scripts to support IntersectionObserver on browsers where native support is not available. These are not detected by the Polymer build analyzer. If you are using `polymer build` you should modify the `polymer.json` file to include these scripts in your build by adding them to the `extraDependencies` array:
```Javascript
"extraDependencies": [
    "bower_components/plastic-image/intersection-observer.js",
    "bower_components/ua-parser-js/dist/ua-parser.min.js",
    ...
  ]
  ```

## Standard iron-image properties that should not be used
Do not use `preventLoad` / `prevent-load`.  This is used internally by `plastic-image` to allow the srcset processing step.
To achieve that function use `delayLoad` / `delay-load` instead.

Do not use `src`.  That will be overwritten by the srcset evaluation.  To specify a fallback image use
the `fallbackSrc` / `fallback-src` attribute instead.
 
## License

MIT

