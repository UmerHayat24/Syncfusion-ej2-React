---
title: "Add or Remove ContextMenu Items"
component: "ContextMenu"
description: "This section helps to learn how to add or remove items in ContextMenu."
---
# Add or remove context menu items

ContextMenu items can be added or removed using the [`insertAfter`](../../api/menu#insertafter), [`insertBefore`](../../api/menu#insertbefore) and [`removeItems`](../../api/menu#removeitems) methods.

In the following example, the **Display Settings** menu items are added before the **Personalize** item, the **Sort By** menu items are added after the **Refresh**, and the **Paste** item is removed from context menu.

{% tab template= "context-menu/getting-started", sourceFiles="app/**/*.tsx,index.html,index.css", isDefaultActive=true, compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { ContextMenuComponent, MenuItemModel } from '@syncfusion/ej2-react-navigations';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

class App extends React.Component {
  public cMenu: ContextMenuComponent;
  public menuItems: MenuItemModel[] = [
    {
        items: [
          {
            text: 'Large icons'
          },
          {
            text: 'Medium icons'
          },
          {
            text: 'Small icons'
          }
        ],
        text: 'View'
    },
    {
        text: 'Refresh'
    },
    {
        text: 'Paste'
    },
    {
        separator: true
    },
    {
        text: 'New'
    },
    {
        separator: true
    },
    {
        text: 'Personalize'
    }];
  constructor(props: any) {
    super(props);
    this.created = this.created.bind(this);
  }
  public created(): void {
    this.cMenu.insertAfter([{text: 'Sort By'}] , 'Refresh');
    this.cMenu.insertBefore([{text: 'Display Settings'}] , 'Personalize');
    this.cMenu.removeItems(['Paste']);
  };
  public render() {
    return (
            <div className="container">
              <div id='target'>Right click / Touch hold to open the ContextMenu</div>
               <ContextMenuComponent id="cmenu" ref={(scope) => this.cMenu = scope as ContextMenuComponent} target='#target' items={this.menuItems} created={this.created}/>
           </div>
        );
    }
}

ReactDom.render(<App />,document.getElementById('element'));
```

{% endtab %}
