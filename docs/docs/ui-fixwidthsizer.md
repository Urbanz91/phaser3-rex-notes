## Introduction

Layout children game objects into lines.

- Author: Rex
- Game object

## Source code

[Plugin](https://github.com/rexrainbow/phaser3-rex-notes/blob/master/templates/ui/ui-plugin.js), [minify](https://github.com/rexrainbow/phaser3-rex-notes/blob/master/plugins/dist/rexuiplugin.min.js)

[Class](https://github.com/rexrainbow/phaser3-rex-notes/blob/master/templates/ui/fixwidthsizer/FixWidthSizer.js)

## Usage

[Sample code](https://github.com/rexrainbow/phaser3-rex-notes/tree/master/examples/ui-fixwidthsizer)

### Install plugin

Install plugin in [configuration of game](game.md#configuration)

```javascript
import UIPlugin from 'rexTemplates/ui/ui-plugin.js';

var config = {
    // ...
    plugins: {
        scene: [{
            key: 'rexUI',
            plugin: UIPlugin,
            mapping: 'rexUI'
        },
        // ...
        ]
    }
    // ...
};
var game = new Phaser.Game(config);
```

### Add sizer object

```javascript
var sizer = scene.rexUI.add.fixWidthSizer({
    x: 0,
    y: 0,
    width: 2,
    height: 2
    orientation: 0,
    space: {
        left: 0,
        right: 0,
        top: 0,
        bottom: 0,
        item: 0,
        line: 0
    }
});
```

or

```javascript
var sizer = scene.rexUI.add.fixWidthSizer(x, y, {
    width: 2,
    height: 2
    orientation: 0,
    space: {
        left: 0,
        right: 0,
        top: 0,
        bottom: 0,
        item: 0,
        line: 0
    }
});
```

or

```javascript
var sizer = scene.rexUI.add.fixWidthSizer(x, y, width, height, {
    orientation: 0,
    space: {
        left: 0,
        right: 0,
        top: 0,
        bottom: 0,
        item: 0,
        line: 0
    }
});
```

or

```javascript
var sizer = scene.rexUI.add.fixWidthSizer(x, y, width, height, orientation,
    {
        left: 0,
        right: 0,
        top: 0,
        bottom: 0,
        item: 0,
        line: 0
    }
);
```

- `x`, `y` : Position of this dialog object, it is valid when this dialog is the top object.
    - Number : World position in pixels.
    - String (`'p%+n'`) : Position based on visible window. See [anchor](anchor.md#create-instance).
- `width`, `height` : Minimum width, minimum height.
- `orientation` : Main orientation of the sizer.
    - `'left-to-right'`, `'horizontal'`,`'h'`, `'x'`, or `0` : Arrange game objects from left ot right.
    - `'top-to-bottom'`, `'vertical'`,`'v'`, `'y'`, or `1` : Arrange game objects from top to bottom.
- `space` : Pads spaces
    - `space.left`, `space.right`, `space.top`, `space.bottom` : Space of bounds.
    - `space.item` : Space betwen each child of a line.
    - `space.line` : Space between each line.

### Custom class

- Define class
    ```javascript
    class MySizer extends RexPlugins.UI.FixWidthSizer {
        constructor(scene, x, y, minWidth, minHeight, orientation) {
            super(scene, x, y, minWidth, minHeight, orientation);
            // ...
        }
        // ...
    }
    ```
- Create instance
    ```javascript
    var sizer = new MySizer(scene, x, y, minWidth, minHeight, orientation);
    ```

### Add background

```javascript
sizer.addBackground(child, paddingConfig);
```

### Add child

Add a game obejct to sizer

```javascript
sizer.add(child);
```

or

```javascript
sizer.add(child, paddingConfig);
```

- `child` : A game object
- `paddingConfig` : Add space between bounds. Default is 0.
    - A number for left/right/top/bottom bounds
    - Or a plain object
        ```javascript
        {
            left: 0,
            right: 0,
            top: 0,
            bottom: 0
        }
        ```

### Layout children

Arrange position of all children.

```javascript
sizer.layout();
```

### Other properties

See [base-sizer object](ui-basesizer.md).