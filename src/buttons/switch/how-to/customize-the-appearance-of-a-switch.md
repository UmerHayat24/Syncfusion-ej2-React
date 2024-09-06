---
title: "Customize the appearance of a Switch"
component: "Switch"
description: "React Switch how to section, customization of Switch bar and handle, change size, name and value in form submit."
---

# Customize the appearance of a Switch

You can customize the appearance of the Switch component using the CSS rules. Define your own CSS rules according to
your requirement and assign the class name to the [`cssClass`](../../api/switch#cssClass) property.

## Customize Switch bar and handle

Switch bar and handle can be customized as per requirement using CSS rules. Switch bar and handle customized using
`cssClass` property. In the following sample, the `border-radius` CSS property for the Switch bar (`e-switch-inner`)
and handle (`e-switch-handle`) elements was changed border radius circle to square shape.

{% tab template="switch/customize", sourceFiles="app/**/*.tsx,index.html,index.css", isDefaultActive=true, compileJsx=true %}

```tsx
import { SwitchComponent } from '@syncfusion/ej2-react-buttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

// To render Switch.
class App extends React.Component<{}, {}> {
  public render() {
    return (
            <div className="switch-control">
                <div>
                    <h3>Customizing Shape</h3>
                </div>
                <div>
                    <label htmlFor="switch1" style={{ padding: "10px 85px 10px 7px" }}> Square Switch </label>
                    <SwitchComponent id="switch1" cssClass="square" />
                </div>
                <div>
                    <label htmlFor='switch2' style= {{ padding: "10px 76px 10px 7px" }}> Bar and handle </label>
                    <SwitchComponent id="switch2" cssClass="custom-switch" checked={true} />
                </div>
                <div>
                    <label htmlFor='switch3' style= {{ padding: "10px 96px 10px 7px" }}> Handle text </label>
                    <SwitchComponent id="switch3" cssClass="handle-text" />
                </div>
            </div>
    );
  }
}
ReactDom.render(<App />, document.getElementById('switch'));
```

{% endtab %}

## Color the Switch

Switch colors can be customized as per the requirement using CSS rules. Switch bar and handle colors customized using
`cssClass` property. In the following sample, the Switch bar (`e-switch-inner`) element background and border colors
were changed from default colors.

{% tab template= "switch/customize-color", sourceFiles="app/**/*.tsx,index.html,index.css", isDefaultActive=true, compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDom from 'react-dom';
import { SwitchComponent } from '@syncfusion/ej2-react-buttons';

// To render Switch.
class App extends React.Component<{}, {}> {
  render() {
    return (
        <div className="switch-control">
            <div>
                <h3>Customizing Color</h3>
            </div>
            <div>
                <label htmlFor="switch1" style={{ padding: "10px 85px 10px 0" }}> Custom color </label>
                <SwitchComponent id="switch1" cssClass='bar-color' />
            </div>
            <div>
                <label htmlFor='switch2' style={{ padding: "10px 90px 10px 0" }}> Handle color </label>
                <SwitchComponent id="switch2" cssClass='handle-color' checked={true} />
            </div>
            <div>
                <label htmlFor='switch3' style={{ padding: "10px 103px 10px 0" }}> iOS Switch </label>
                <SwitchComponent id="switch3" cssClass='custom-iOS' checked={true}  />
            </div>
        </div>
    );
  }
}
ReactDom.render(<App />, document.getElementById('switch'));
```

{% endtab %}