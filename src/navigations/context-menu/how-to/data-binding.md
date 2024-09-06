---
title: "Databinding in ContextMenu Items"
component: "ContextMenu"
description: "This section helps to learn Databinding in ContextMenu."
---
# Data Binding

In the following example, menu items are populated from data source and mapped to
[`items`](https://ej2.syncfusion.com/react/documentation/api/context-menu/menuItemModel/#items) property.

{% tab template="context-menu/data-binding",isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html,index.css,datasource.tsx",compileJsx=true %}

```tsx
import { ContextMenuComponent, MenuEventArgs, MenuItemModel } from '@syncfusion/ej2-react-navigations';
import * as React from 'react';
import * as ReactDom from 'react-dom';
// @ts-ignore
import { data, IRecord } from '../datasource.tsx';


class App extends React.Component<{}, {}> {

    public getMenuItems = () => {
        let record: IRecord;
        const menuItems: MenuItemModel[] = [];
        for (const d of data) {
            record = d as IRecord;
            if (record.parentId) {
                if (!menuItems[record.parentId - 1].items) {
                    menuItems[record.parentId - 1].items = [];
                }
                menuItems[record.parentId - 1].items.push({ text: record.text });
            } else {
                menuItems.push({ text: record.text });
            }
        }
        return menuItems;
    }

    public itemBeforeEvent: any = (args: MenuEventArgs) => {
        if (!args.item.text) {
            args.element.classList.add('e-separator');
        }
    }

    public render() {
        return (
            <div className="container">
                <div id='target'>Right click / Touch hold to open the ContextMenu</div>
                <ContextMenuComponent id='contextmenu' target='#target'
                    items={this.getMenuItems()} beforeItemRender = {this.itemBeforeEvent} />
            </div>
        );
    }
}

ReactDom.render(<App />,document.getElementById('element'));
```

{% endtab %}

> While accessing Array we got the exception 'object is possibly undefined' due to 'strictNullChecks' option. So you can disable it in 'tsconfig.json' file.