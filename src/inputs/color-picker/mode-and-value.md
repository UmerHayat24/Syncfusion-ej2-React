---
title: "ColorPicker Mode and Value option"
component: "ColorPicker"
description: "This section helps to learn how to create the color picker in React application with mode and value option"
---

# Mode and Value

## Inline

By default, the ColorPicker will be rendered using SplitButton and open the pop-up to access the ColorPicker. To
render the ColorPicker container alone and to access it directly, render it as inline. It can be achieved by setting the [`inline`](../api/color-picker#inline) property to `true`.

The following sample shows the inline type rendering of ColorPicker.

{% tab template="colorpicker/getting-started", sourceFiles="app/**/*.tsx,index.html",styles.css", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { ColorPickerComponent } from '@syncfusion/ej2-react-inputs';

//To render component as inline.
class App extends React.Component<{}, {}> {
    render() {
        return (
          <div id='container'>
            <div className='wrap'>
                <h4>Choose Color</h4>
                <ColorPickerComponent inline={true} showButtons={false}></ColorPickerComponent>
            </div>
          </div>
        );
    }
};
ReactDOM.render(<App />, document.getElementById('element'));
```

{% endtab %}

>> The `showButtons` property is disabled in this sample because the control buttons are not needed for inline type. To know about the control buttons functionality, refer to the [`showButtons`](./how-to/hide-control-buttons) sample.

## Rendering palette at initial load

By default, the `Picker` area will be rendered at initial load. To render the Palette area while opening the ColorPicker pop-up, and specify the [`mode`](../api/color-picker#mode) property as `Palette`.

In the following sample, it will render the `Palette` at initial load.

{% tab template="colorpicker/getting-started", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html,styles.css", compileJsx=true %}

```tsx
import { ColorPickerComponent } from '@syncfusion/ej2-react-inputs';
import * as React from "react";
import * as ReactDOM from "react-dom";

//To render palette at initial load.
class App extends React.Component<{}, {}> {
  public render() {
        return (
          <div id='container'>
            <div className='wrap'>
                <h4>Choose Color</h4>
                <ColorPickerComponent mode="Palette"/>
            </div>
          </div>
        );
    }
};
ReactDOM.render(<App />, document.getElementById('element'));
```

{% endtab %}

## Color value

The [`value`](../api/color-picker#value) property can be used to specify the color value to the
ColorPicker. It supports either `three` or `six` digit hex codes. To include `opacity`, set the color value as `four` or `eight` digit hex code.

In the following sample, the color value sets as `four` digit hex code, the last digit represents the `opacity` value.

{% tab template="colorpicker/mode-and-value", sourceFiles="app/**/*.tsx,index.html,styles.css", compileJsx=true %}

```tsx
import { ColorPickerComponent } from '@syncfusion/ej2-react-inputs';
import * as React from "react";
import * as ReactDOM from "react-dom";

//To set color value.
class App extends React.Component<{}, {}> {
    public render() {
        return (
          <div id='container'>
            <div className='wrap'>
                <h4>Choose Color</h4>
                <ColorPickerComponent value="035a"/>
            </div>
          </div>
        );
    }
};
ReactDOM.render(<App />, document.getElementById('element'));
```

{% endtab %}

>> The [`value`](../api/color-picker#value) property supports hex code with or without `#` prefix.

## See Also

* [How to render palette alone](./how-to/render-palette-alone)
* [Custom palette](./how-to/customize-colorpicker#custom-palette)
* [No color support in palette](./how-to/handle-no-color-support)
