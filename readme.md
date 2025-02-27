# pdf2pic

Forked from: https://github.com/yakovmeister/pdf2image

A utility for converting pdf to image, base64 or buffer format.

> IMPORTANT NOTE: Please support this library by donating to the owner via [PayPal](https://www.paypal.com/paypalme/yakovmeister), your help is much appreciated. Contributors are also welcome!

## Prerequisites

* node >= 14.x 
* graphicsmagick
* ghostscript

### Don't have graphicsmagick and ghostscript yet?

Follow [this](docs/gm-installation.md) guide to install the required dependencies.

## Installation

```
npm install --save pdf2pic
```

## Usage

### Converting specific page of PDF from path, then saving as image file

```javascript
import { fromPath } from "pdf2pic";

const options = {
  density: 100,
  saveFilename: "untitled",
  savePath: "./images",
  format: "png",
  width: 600,
  height: 600,
  ignoreAspectRatio: false
};
const convert = fromPath("/path/to/pdf/sample.pdf", options);
const pageToConvertAsImage = 1;

convert(pageToConvertAsImage, { responseType: "image" })
  .then((resolve) => {
    console.log("Page 1 is now converted as image");

    return resolve;
  });
```

## pdf2pic API

- [fromPath(filePath, options)](#frompathfilepath-options)
- [fromBuffer(buffer, options)](#frombufferbuffer-options)
- [fromBase64(b64string, options)](#frombase64b64string-options)

### fromPath(filePath, options)

Initialize PDF to image conversion by supplying a file path

#### Functions

Convert a specific page of the PDF to Image/Base64/Buffer by supplying a file path

```javascript
fromPath(filePath, options)(page, convertOptions)
```
* filePath - pdf file's path
* options - see [options](#options).
* page - page number to convert to an image
* convertOptions - see [convertOptions](#convertoptions).

---

Converts PDF to Image/Base64/Buffer by supplying a file path
```javascript
fromPath(filePath, options).bulk(pages, convertOptions)
```
* filePath - pdf file's path
* options - see [options](#options).
* pages - page numbers to convert to image
  * set `pages` to `-1` to convert all pages
  * `pages` also accepts an array indicating the page number e.g. `[1,2,3]`
  * also accepts number e.g. `1`
* convertOptions - see [convertOptions](#convertoptions)

---

Set GraphicsMagick's subclass or path
```javascript
fromPath(filePath, options).setGMClass(subClass)
```
NOTE: should be called before calling `convert()` or `bulk()`.
* filePath - pdf file's path
* options - see [options](#options).
* subClass - path to gm binary or set to true to use imagemagick
  * set `subClass` to true to use imagemagick
  * supply a valid path as `subClass` to locate gm path specified

---

### fromBuffer(buffer, options)
 
Initialize PDF to image conversion by supplying a PDF buffer

#### Functions

Convert a specific page of the PDF to Image/Base64/Buffer by supplying a buffer
```javascript
fromBuffer(buffer, options)(page, convertOptions)
```

Functions same as `fromPath(filePath, options)(page, convertOptions)` only input is changed

---
Converts PDF to Image/Base64/Buffer by supplying a buffer:

```javascript
fromBuffer(buffer, options).bulk(pages, convertOptions)
```

Functions same as `fromPath(filePath, options).bulk(pages, convertOptions)` only input is changed

---
Set GraphicsMagick's subclass or path:
```javascript
fromBuffer(buffer, options).setGMClass(subClass)
```

Functions same as `fromPath(filePath, options).setGMClass(subClass)` only input is changed

---

### fromBase64(b64string, options)
Initialize PDF to image conversion by supplying a PDF base64 string.

#### Functions
Convert a specific page of the PDF to Image/Base64/Buffer by supplying a base64 string:
```javascript
fromBase64(b64string, options)(page, convertOptions)
```

Functions same as `fromPath(filePath, options)(page, convertOptions)` only input is changed.

---
Converts PDF to Image/Base64/Buffer by supplying a base64 string:

```javascript
fromBase64(b64string, options).bulk(pages, convertOptions)
```

Functions same as `fromPath(filePath, options).bulk(pages, convertOptions)` only input is changed.

---
Set GraphicsMagick's subclass or path:
```javascript
fromBase64(b64string, options).setGMClass(subClass)
```

Functions same as `fromPath(filePath, options).setGMClass(subClass)` only input is changed.
---
### options
Following are the options that can be passed on the pdf2pic api:

| option       | default value | description                  |
|--------------|--------------- |------------------------------|
| quality      | `0`            | Image compression level. Value depends on `format`, usually from `0` to `100` ([more info](http://www.graphicsmagick.org/GraphicsMagick.html#details-quality))                        |
| format       | `'png'`        | Formatted image characteristics / image format ([image characteristics](http://www.graphicsmagick.org/GraphicsMagick.html#details-format), [image format](http://www.graphicsmagick.org/formats.html)) |
| width        | `768`            | Output width                 |
| height       | `512`            | Output height                |
| density      | `72`             | Output DPI (dots per inch) ([more info](http://www.graphicsmagick.org/GraphicsMagick.html#details-density)) |
| savePath     | `'./'`         | Path where to save the output |
| saveFilename | `'untitled'`   | Output filename              |
| ignoreAspectRatio | `false`   | If gm should ignore output aspect ratio |
| compression  | `'jpeg'`       | Compression method ([more info](http://www.graphicsmagick.org/GraphicsMagick.html#details-compress)) |

### convertOptions

| option       | default value | description |
|--------------|---------------|-------------|
| responseType | `image`       | Response type of the output. Accepts: `image`, `base64` or `buffer` |

The parameter can also be a boolean, if `true` then the response type will be `base64` and if `false` then the response type will be `image`. 
This is deprecated and will be removed in the next major version.

## License
pdf2pic is [MIT licensed](LICENSE).