---
title: "Template and Multilevel Nesting in ContextMenu Items"
component: "ContextMenu"
description: "This section helps to learn about Template and Multilevel nesting in ContextMenu."
---

# Template and Multilevel nesting

The ContextMenu items can be customized using the
[`beforeItemRender`](../api/context-menu#beforeitemrender) property. The item render
event triggers while rendering each menu item. The event argument will be used to identify the menu
item and customized it based on the requirement. In the following sample, the menu item is rendered with
keycode for specified action in ContextMenu using the template. Here, the keycode is specified for
Save as, View page source, and Inspect in the right side corner of the menu items by adding span
element in the [`beforeItemRender`](../api/context-menu#beforeitemrender) event.

{% tab template="context-menu/template", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```tsx
import { createElement, enableRipple } from '@syncfusion/ej2-base';
import { ContextMenuComponent, MenuEventArgs, MenuItemModel } from '@syncfusion/ej2-react-navigations';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

class App extends React.Component<{}, {}> {
  public menuItems: MenuItemModel[] = [
    {
        text: 'Save as...'
    },
    {
        text: 'View page source'
    },
    {
        text: 'Inspect'
    }];
    public itemBeforeEvent: any = (args: MenuEventArgs) => {
        const shortCutSpan = createElement('span');
        const text = args.item.text;
        const shortCutText = text === 'Save as...' ? 'Ctrl + S' : (text === 'View page source' ? 'Ctrl + U' : 'Ctrl + Shift + I');
        shortCutSpan.textContent = shortCutText;
        args.element.appendChild(shortCutSpan);
        shortCutSpan.setAttribute('class','shortcut');
    }

  public render() {
    return (
            <div class="container">
              <div id='target'>Right click / Touch hold to open the ContextMenu</div>
              <ContextMenuComponent id='contextmenu' target='#target'
              items={this.menuItems} beforeItemRender={this.itemBeforeEvent}/>
           </div>
        );
    }
}
ReactDom.render(<App />,document.getElementById('element'));
```

{% endtab %}

> To create span element, `createElement` util function used from `ej2-base`.

## Multilevel nesting

Multiple level nesting supports in ContextMenu. It can be achieved by mapping the
[`items`](../api/context-menu/menuItemModel#items) property inside the parent
[`menuItems`](../api/context-menu#items). In the below sample,
three level nesting of ContextMenu is provided.

{% tab template="context-menu/getting-started",  sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDom from 'react-dom';
import { ContextMenuComponent, MenuItemModel } from '@syncfusion/ej2-react-navigations';
import { enableRipple } from '@syncfusion/ej2-base';

enableRipple(true);

export default class App extends React.Component {
  private menuItems: MenuItemModel[] = [
    {
        text: 'Show All Bookmarks'
    },
    {
        text: 'Bookmarks Toolbar',
        items: [
            {
                text: 'Most Visited',
                items: [
                    {
                        text: 'Google'
                    },
                    {
                        text: 'Gmail'
                    }
                ]
            },
            {
                text: 'Recently Added'
            }
        ]
    }];

  render() {
    return (
            <div class="container">
              <div id='target'>Right click / Touch hold to open the ContextMenu</div>
              <ContextMenuComponent id='contextmenu' target='#target'
              items={this.menuItems}> </ContextMenuComponent>
           </div>
        );
    }
}

ReactDom.render(<App />,document.getElementById('element'));
```

{% endtab %}

> To open sub menu items only on click, [`showItemOnClick`](../api/context-menu#showitemonclick) property should be set as `true`.

## See Also

* [Populate menu items with data source](./how-to/data-binding)
