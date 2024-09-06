---
title: "Enable ripple for Switch label"
component: "Switch"
description: "React Switch how to section, customization of Switch bar and handle, change size, name and value in form submit."
---

# Enable ripple for Switch label

By default, label with ripple effect is not available in Switch. You can achieve this by using `rippleMouseHandler`
method.

The following example illustrates how to enable ripple effect for labels in Switch component.

{% tab template= "switch/ripple", sourceFiles="app/**/*.tsx,index.html", isDefaultActive=true, compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { rippleMouseHandler } from '@syncfusion/ej2-buttons';
import { SwitchComponent } from '@syncfusion/ej2-react-buttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

// To render Switch with checked state.
class App extends React.Component<{}, {}> {
    public onCreated(): void {
        // Function to handle ripple effect for Switch with label.
        (document.querySelector('.lSize label') as HTMLElement).addEventListener('mouseup', rippleHandler);
        (document.querySelector('.lSize label') as HTMLElement).addEventListener('mousedown', rippleHandler);
        function rippleHandler(e: MouseEvent): void  {
            const rippleSpan = (e.target as HTMLElement).parentElement.nextElementSibling.querySelector('.e-ripple-container');
            if (rippleSpan) {
                rippleMouseHandler(e, rippleSpan);
            }
        }
    }
  public render() {
    return (
        <table className='size'>
            <tr>
                <td className='lSize'>
                    <label htmlFor='switch1'>USB Tethering</label>
                </td>
                <td>
                    <SwitchComponent id="switch1" created={this.onCreated} checked={true} />
                </td>
            </tr>
        </table>
    );
  }
}
ReactDom.render(<App />, document.getElementById('switch'));
```

{% endtab %}

> While accessing HTML Elements we got the exception 'object is possibly null' due to 'strictNullChecks' option. So you can disable it in 'tsconfig.json' file.