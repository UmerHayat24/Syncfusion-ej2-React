---
title: "Submit name and value in form"
component: "Switch"
description: "React Switch how to section, customization of Switch bar and handle, change size, name and value in form submit."
---

# Submit name and value in form

The name attribute of the Switch is used to group Switches. When the Switches are grouped in form, the checked items
value attribute will post to the server on form submit. The disabled and unchecked Switch values will not be sent to
the server on form submit.

In the following code snippet, USB and Wi-Fi in the checked state, and Bluetooth is in disabled state.
Values that are in checked state only be sent on form submit.

{% tab template= "switch/form", sourceFiles="app/**/*.tsx,index.html", isDefaultActive=true, compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { ButtonComponent, SwitchComponent } from '@syncfusion/ej2-react-buttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

// To render Switch.
class App extends React.Component<{}, {}> {
  public render() {
    return (
        <form>
            <div className="switch-control">
                <div>
                    <h3>Form Submit</h3>
                </div>
                <div>
                    <label htmlFor="switch1" style={{ padding: "10px 85px 10px 0" }}> USB </label>
                    <SwitchComponent id="switch1" name='Tethering' value='USB' checked={true} />
                </div>
                <div>
                    <label htmlFor='switch2' style={{ padding: "10px 80px 10px 0" }}> Wi-Fi </label>
                    <SwitchComponent id="switch2" name='Hotspot' value='Wi-Fi' checked={true} />
                </div>
                <div>
                    <label htmlFor='switch3' style={{ padding: "10px 53px 10px 0" }}> Bluetooth </label>
                    <SwitchComponent id="switch3" name='Tethering' value='Bluetooth' disabled={true} />
                </div>
                <div>
                    <ButtonComponent isPrimary={true}>Submit</ButtonComponent>
                </div>
            </div>
        </form>
    );
  }
}
ReactDom.render(<App />, document.getElementById('switch'));
```

{% endtab %}