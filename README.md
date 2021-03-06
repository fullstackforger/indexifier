# Generate an index for a given directory

[![Build status](https://img.shields.io/travis/joscha/indexifier/master.svg)](https://travis-ci.org/joscha/indexifier)
[![npm](https://img.shields.io/npm/v/indexifier.svg)](https://www.npmjs.com/package/indexifier)
![npm](https://img.shields.io/npm/l/indexifier.svg)
![node](https://img.shields.io/node/v/indexifier.svg)
[![Commitizen friendly](https://img.shields.io/badge/commitizen-friendly-brightgreen.svg)](http://commitizen.github.io/cz-cli/)
[![semantic-release](https://img.shields.io/badge/%20%20%F0%9F%93%A6%F0%9F%9A%80-semantic--release-e10079.svg)](https://github.com/semantic-release/semantic-release)

This module generates a tree view of a given directory.

## Usage

### CLI API

```
Usage: indexifier [options] <dir>

Options:

  -h, --help               output usage information
  -V, --version            output the version number
  -e, --extensions <list>  The extensions to take into account; defaults to .htm,.html
  -h, --html               Enable to generate HTML output
```

#### Install

```console
npm install -g indexifier
```

#### Examples

```console
indexifier ./ --extensions .html,.htm
```
would generate something like this:

```
A
├─┬ B
│ └── c.html
├── d.html
└── e.html
```

There is also an HTML flag that would generate the above output as linked HTML:

```console
indexifier --extensions .html --html .
```

```html
<!-- ... -->
<a href="./">A</a><br/>
├─┬ <a href="./B">B</a><br/>
│ └── <a href="./B/c.html">c.html</a><br/>
├── <a href="./d.html">a.html</a><br/>
└── <a href="./e.html">b.html</a><br/>
<!-- ... -->
```
> The links are always relative to the given directory.

### Node API

```
indexifier(String directory [, opts={
                                     fileTypes: Array.<String>
                                     isHtml: Boolean
                                    }]);
```

#### Install

```console
npm install indexifier --save
```

#### Examples

Tree of files:

```js
const indexifier = require('indexifier');

const treeOfFiles = indexifier(__dirname);
```

Tree of HTML files:

```js
const indexifier = require('indexifier');

const treeOfHtmlFiles = indexifier(__dirname, { fileTypes: ['.html'] });
```

or for HTML output:

```js
const indexifier = require('indexifier');

const treeOfJpegFiles = indexifier(__dirname, {
    fileTypes: ['.jpg', '.jpeg'],
    isHtml: true
});
```
