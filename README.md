# \<plastic-image\>

A Polymer 2.0 element which adds extra plasticity to `iron-image` with support for **srcset** and 
**lazy loading**.

`plastic-image` extends `iron-image` by adding a `srcset` attribute for client side image
size selection. It also adds a `lazy-load` attribute for deferring the image load until
the element is showing in the viewport.

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

To base image selection on the rendered size of the control add the `use-element-dim` attribute.

```HTML
<plastic-image preload fade sizing="contain" use-element-dim
  srcset="images/foo-s.jpg 150w, images/foo-sh.jpg 150w 2.0x, images/foo-m.jpg 405w, 
  images/foo-mh 2.0x 405w, images/foo-l 1024w, images/foo-t 500w 750h"
  placeholder="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAYAAAAGCAYAAADgzO9IAAAAmElEQVQImWNmYGBgSExMzBATE7dSVFT8eO/evTcMDAwMjIFe5iYSIjybL136cunNW56FulIaEoJcfBdY5GWjvJ4/+SJhIcUhwavI5SbIxR+YvzRqH8unx7/Osf8VYpAVEWLgZuO8ljrfbwMDAwMD07u/j/ZYun5f9JfjSfGnHx9dGaCAJcBimwXjZ4Z+HllGn0XbXr+ASQAAi5UxQq88/fsAAAAASUVORK5CYII="></plastic-image>
```

To defer loading until the image is in (well, at least peaking into) the viewport add the `lazy-load` attribute.

```HTML
<plastic-image lazy-load preload fade sizing="contain"
  srcset="images/foo-s.jpg 150w, images/foo-sh.jpg 150w 2.0x, images/foo-m.jpg 405w, 
  images/foo-mh 2.0x 405w, images/foo-l 1024w, images/foo-t 500w 750h"
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

## Standard iron-image properties that should not be used
Do not use `preventLoad` / `prevent-load`.  This is used internally by `plastic-image` to allow the srcset processing step.
To achieve that function use `delayLoad` / `delay-load` instead.

Do not use `src`.  That will be overwritten by the srcset evaluation.  To specify a fallback image use
the `fallbackSrc` / `fallback-src` attribute instead.
 
## License

MIT

