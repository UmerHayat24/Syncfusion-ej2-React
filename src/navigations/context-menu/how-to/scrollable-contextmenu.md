---
title: "Scrollable ContextMenu Items"
component: "ContextMenu"
description: "This section helps to learn how to achieve scrollable ContextMenu."
---

# Scrollable ContextMenu

Scrollable ContextMenu can be achieved by restricting the height of the `ul` element.

In the following example, the `height` of the ContextMenu is set as `150px` and `overflow` property is set
as `auto`.

{% tab template="context-menu/scrollable",  sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { ContextMenuComponent, MenuItemModel } from '@syncfusion/ej2-react-navigations';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

class App extends React.Component<{}, {}> {
    public menuItems: MenuItemModel[] = [
        { text: 'ABS' },
        { text: 'ACOS' },
        { text: 'ACOSH' },
        { text: 'ACOT' },
        { text: 'ACOTH' },
        { text: 'AGGREGATE' },
        { text: 'COS' },
        { text: 'COSH' },
        { text: 'COT' },
        { text: 'COTH' }
    ];

    public render() {
        return (
            <div className="container">
                <div id='target'>Right click / Touch hold to open the ContextMenu</div>
                <ContextMenuComponent id='contextmenu' target='#target' cssClass='e-custom' items={this.menuItems} />
            </div>
        );
    }
}

ReactDom.render(<App />,document.getElementById('element'));
```

{% endtab %}
