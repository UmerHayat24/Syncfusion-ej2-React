---
title: "Render Palette alone in ColorPicker"
component: "ColorPicker"
description: "This section explains, how to render ColorPicker with only Palette."
---

# Render palette alone

To render the `Palette` alone in ColorPicker, specify the [`mode`](../../api/color-picker#mode) property as `Palette`, and set the [`modeSwitcher`](../../api/color-picker#modeswitcher) property to `false`.

In the following sample, the [`showButtons`](../../api/color-picker#showbuttons) property is disabled to hide the control buttons and it renders only the `Palette` area.

{% tab template="colorpicker/how-to", sourceFiles="app/**/*.tsx,index.html,styles.css", compileJsx=true %}

```tsx
import { ColorPickerComponent } from '@syncfusion/ej2-react-inputs';
import * as React from "react";
import * as ReactDOM from "react-dom";

class App extends React.Component<{}, {}> {
    render() {
        return (
          <div id='container'>
            <div className='wrap'>
                <h4>Choose Color</h4>
                <ColorPickerComponent mode = "Palette" modeSwitcher={false} showButtons ={false}></ColorPickerComponent>
            </div>
          </div>
        );
    }
};
ReactDOM.render(<App />, document.getElementById('element'));
```

{% endtab %}

>> To render `Picker` alone specify the [`mode`](../../api/color-picker#mode) property as 'Picker'.
