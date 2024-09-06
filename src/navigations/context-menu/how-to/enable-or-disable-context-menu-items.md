---
title: "Enable or Disable ContextMenu Items"
component: "ContextMenu"
description: "This section helps to learn how to enable or disable items in ContextMenu."
---
# Enable or disable context menu items

You can enable and disable the menu items using the [`enableItems`](../../api/menu#enableitems) method in ContextMenu. To enable menuItems, set the `enable` property in argument to `true` and vice-versa.

In the following example, the **Display Settings** in parent items and **Medium icons** in sub menu items are disabled.

{% tab template= "context-menu/getting-started", sourceFiles="app/**/*.tsx,index.html,index.css", isDefaultActive=true, compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { ContextMenuComponent, MenuItemModel } from '@syncfusion/ej2-react-navigations';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

class App extends React.Component {
    public cMenu: ContextMenuComponent;
    private menuItems: MenuItemModel[] = [
        {
            items: [
                { text: 'Large icons' },
                { text: 'Medium icons' },
                { text: 'Small icons' }
            ],
            text: 'View'
        },
        {
            text: 'Sort By'
        },
        {
            text: 'Refresh'
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
            text: 'Display Settings'
        },
        {
            text: 'Personalize'
        }
    ];
    constructor(props: any) {
        super(props);
        this.created = this.created.bind(this);
        this.beforeOpen = this.beforeOpen.bind(this);
    }
    public render() {
        return (
            <div className="container">
                <div id='target'>Right click / Touch hold to open the ContextMenu</div>
                <ContextMenuComponent id="cmenu" ref={(scope) => this.cMenu = scope as ContextMenuComponent} target='#target' items={this.menuItems} created={this.created} beforeOpen={this.beforeOpen} />
            </div>
        );
    }
    private created() {
        this.cMenu.enableItems(['Display Settings'], false);
    };
    private beforeOpen() {
        this.cMenu.enableItems(['Medium icons'], false);
    };
}

ReactDom.render(<App />,document.getElementById('element'));
```

{% endtab %}

> To disable sub menu items, use the [`beforeOpen`](../../api/menu#beforeopen) event.