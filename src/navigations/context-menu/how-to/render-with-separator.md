---
title: "ContextMenu Items with Separator"
component: "ContextMenu"
description: "This section helps to learn how to render items with separator in ContextMenu."
---
# Rendering items with Separator

The Separators are horizontal lines that are used to separate the menu items. You cannot select the separators. You
can enable separators to group the menu items using the [`separator`](https://ej2.syncfusion.com/react/documentation/api/context-menu/menuItemModel/#separator)
property. Cut, Copy, and Paste menu items are grouped using `separator` property in the following sample.

{% tab template="context-menu/separators",  sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { ContextMenuComponent, MenuItemModel } from '@syncfusion/ej2-react-navigations';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

export default class App extends React.Component<{}, {}> {
  private menuItems: MenuItemModel[] = [
    {
        text: 'Cut'
    },
    {
        text: 'Copy'
    },
    {
        text: 'Paste'
    },
    {
        separator: true
    },
    {
        text: 'Font'
    },
    {
        text: 'Paragraph'
    }];

  public render() {
    return (
            <div className="container">
              <div id='target'>Right click / Touch hold to open the ContextMenu</div>
              <ContextMenuComponent id='contextmenu' target='#target' items={this.menuItems}/>
           </div>
        );
    }
}

ReactDom.render(<App />,document.getElementById('element'));
```

{% endtab %}

> The [`separator`](https://ej2.syncfusion.com/react/documentation/api/context-menu/menuItemModel/#separator) property `should not` be given along with
the other fields in the [`MenuItem`](https://ej2.syncfusion.com/react/documentation/api/context-menu/menuItemModel/).
