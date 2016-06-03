# react-avatar-editor

<a href="http://badge.fury.io/js/react-avatar-editor"><img alt="npm version" src="https://badge.fury.io/js/react-avatar-editor.svg"></a>
<a href="https://npmjs.org/package/react-avatar-editor"><img alt="Downloads" src="http://img.shields.io/npm/dm/react-avatar-editor.svg"></a>

Facebook like, avatar / profile picture component.
Resize and crop your uploaded image using a clear user interface.

# Usage


```javascript

var React = require('react'),
  AvatarEditor = require('react-avatar-editor');

var MyEditor = React.createClass({

  render: function() {
    return (
        <AvatarEditor
          image="http://example.com/initialimage.jpg"
          width={250}
          height={250}
          border={50}
          color={[255, 255, 255, 0.6]} // RGBA
          scale={1.2} />
    );
  }

});

module.exports = MyEditor;
```

## Props
| Prop                   | Type     | Description
| ---------------------- | -------- | ---------------
| width                  | Number   | The total width of the editor
| height                 | Number   | The total width of the editor
| border                 | Number   | The cropping border. Image will be visible through the border, but cut off in the resulting image.
| color                  | Number[] | The color of the cropping border, in the form: [red (0-255), green (0-255), blue (0-255), alpha (0.0-1.0)]
| style                  | Object   | Styles for the canvas element
| scale                  | Number   | The scale of the image. You can use this to add your own resizing slider.
| useDropFile            | bool     | Whether it should accept file drop or not (Will obsolete onDropFile prop).
| onDropFile(event)      | function | Invoked when user drops a file (or more) onto the canvas. Does not perform any further check.
| onLoadSuccess(imgInfo) | function | Invoked when an image (whether passed by props or dropped) load succeeds.
| onLoadFailure(event)   | function | Invoked when an image (whether passed by props or dropped) load fails.
| onMouseUp()            | function | Invoked when the user releases their mouse button after interacting with the editor.

## Accessing the resulting image

The size of the resulting image will have the width and the height of the editor - minus the borders.

```javascript

var React = require('react'),
  AvatarEditor = require('react-avatar-editor');

var MyEditor = React.createClass({
  onClickSave: function() {
    var dataURL = this.refs.editor.getImage();
    // now save it to the state and set it as <img src="…" /> or send it somewhere else
  },
  render: function() {
    return (
        <AvatarEditor
          ref="editor"
          image="http://example.com/initialimage.jpg"
          width={250}
          height={250}
          border={50}
          scale={1.2} />
    );
  }

});

module.exports = MyEditor;
```

## Accessing the cropping rectangle

Sometimes you will need to get the cropping rectangle (the coordinates of the area of the image to keep),
for example in case you intend to perform the actual cropping server-side.

``getCroppingRect()`` returns an object with four properties: ``x``, ``y``, ``width`` and ``height``;
all relative to the image size (that is, comprised between 0 and 1). It is a method of AvatarEditor elements,
like ``getImage()``.


# Development

For development you can use following build tools:

* `npm run build`: Builds a minified dist file: `dist/index.js`
* `npm run build-debug`: Builds an unminified dist file: `dist/index.js`
* `npm run watch`: Watches for file changes and builds unminified into: `dist/index.js`
* `npm run demo`: Builds the demo based on the dist file `dist/index.js`
