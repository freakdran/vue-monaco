# Monaco Editor for Vue

## Description

A short implementation of the monaco-editor for Vue

## Installation

Most dependencies for this module should be already present in your project. If not add the ones from the package.json

## Adding it to your website

Just register it as a component like you do it with every other one. For further instructions see the example.

The editor NEEDS a wrappeing container as it sets it height/width to the size of it.

## Options

`value`: The initial code in the editor - required

`theme`: normal VS themes, e.g. vs-light, vs-dark

`options`: JSON with Monaco-Editor options, e.g. `{ readOnly: true }`. For more options see the [Official Site](https://microsoft.github.io/monaco-editor/api/interfaces/monaco.editor.ieditoroptions.html)

`minimapOptions`: JSON with maximum three values
```/** 
* @param {Boolean} enabled is the minimap enabled 
* @param {Boolean} force is if the minimap is always shown - mandatory if enabled is true 
* @param {Number} lines number of lines when the minimap should not be displayed, e.g. lines:30 -> minimap shown at 31 lines - mandatory if force is false 
*/ 
minimapOptions: { enabled: true, force: false, lines: 40 },
```

`foldOptions`: JSON with maximum two values
```/** 
* @param {Number} foldDepth 
* @param {Number} lines number of lines when fold should happen - only if foldDepth is set 
*/ 
foldOptions: { foldDepth: 2, lines: 50 }
```
