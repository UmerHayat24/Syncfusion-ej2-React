---
title: "Change Size"
component: "Switch"
description: "React Switch how to section, customization of Switch bar and handle, change size, name and value in form submit."
---

# Change Size

The different Switch sizes available are default and small. To reduce the size of default Switch to small,
set the [`cssClass`](../../api/switch#cssclass) property to `e-small`.

{% tab template= "switch/size", sourceFiles="app/**/*.tsx,index.html", isDefaultActive=true, compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { SwitchComponent } from '@syncfusion/ej2-react-buttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

// To render Switch.
class App extends React.Component<{}, {}> {
  public render() {
    return (
         <table className='size'>
            <tr>
                <td className='lSize'>Small</td>
                <td>
                    <SwitchComponent cssClass="e-small" />
                </td>
            </tr>
            <tr>
                <td className='lSize'>Default</td>
                <td>
                   <SwitchComponent />
                </td>
            </tr>
        </table>
    );
  }
}
ReactDom.render(<App />, document.getElementById('switch'));
```

{% endtab %}