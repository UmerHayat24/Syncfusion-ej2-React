---
title: "Hide Controls in ColorPicker"
component: "ColorPicker"
description: "This section explains, how to hide the controls in ColorPicker"
---

# Hide control buttons

ColorPicker can be rendered without control buttons (Apply/Cancel). In this case, while selecting a color, the
ColorPicker pop-up is closed and selected colors can be applied directly. To hide control buttons, set the [`showButtons`](../../api/color-picker#showbuttons) property to `false`.

{% tab template="colorpicker/how-to", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html,styles.css", compileJsx=true %}

```tsx
import { ColorPickerComponent } from '@syncfusion/ej2-react-inputs';
import * as React from "react";
import * as ReactDOM from "react-dom";

//To hide control buttons.
class App extends React.Component<{}, {}> {
    public render() {
        return (
          <div id='container'>
            <div className='wrap'>
                <h4>Choose Color</h4>
                <ColorPickerComponent showButtons={false} />
            </div>
          </div>
        );
    }
};
ReactDOM.render(<App />, document.getElementById('element'));
```

{% endtab %}
