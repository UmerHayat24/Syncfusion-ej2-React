---
title: "ColorPicker Disabled Property"
component: "ColorPicker"
description: "This section explains, how to disable the ColorPicker"
---

# Disabled

To achieve disabled state in ColorPicker, set the [`disabled`](../../api/color-picker#disabled) property to `true`. The ColorPicker pop-up cannot be accessed in disabled state.

The following example shows the `disabled` state of ColorPicker component.

{% tab template="colorpicker/how-to", sourceFiles="app/**/*.tsx,index.html,styles.css", compileJsx=true %}

```tsx
import { ColorPickerComponent } from '@syncfusion/ej2-react-inputs';
import * as React from "react";
import * as ReactDOM from "react-dom";

class App extends React.Component<{}, {}> {
    public render() {
        return (
          <div id='container'>
            <div className='wrap'>
                <h4>Choose Color</h4>
                <ColorPickerComponent disabled={true}/>
            </div>
          </div>
        );
    }
};
ReactDOM.render(<App />, document.getElementById('element'));
```

{% endtab %}