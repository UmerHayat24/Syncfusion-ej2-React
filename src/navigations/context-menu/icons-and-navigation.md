---
title: "Icons or Navigations in ContextMenu Items"
component: "ContextMenu"
description: "This section helps to learn about icons and navigations in ContextMenu."
---

# Icons and Navigation

## Icons

The ContextMenu item have an icon / image in it to provide visual representation of the
action. To place the icon on a menu item, set the [`iconCss`](../api/context-menu/menuItemModel#iconcss)
property to e-icons with the required icon CSS. By default, the icon is positioned to the left
side of the menu item. In the following sample, the icons for Cut, Copy and Paste menu items
are added using `iconCss` property.

{% tab template= "context-menu/icons", sourceFiles="app/**/*.tsx,index.html,index.css", isDefaultActive=true, compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { ContextMenuComponent, MenuItemModel } from '@syncfusion/ej2-react-navigations';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

class App extends React.Component<{}, {}> {
  private menuItems: MenuItemModel[] = [
    {
        iconCss: 'e-cm-icons e-cut',
        text: 'Cut'
    },
    {
        iconCss: 'e-icons e-copy',
        text: 'Copy'
    },
    {
        iconCss: 'e-cm-icons e-paste',
        text: 'Paste'
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

## Navigation URL

Navigation URL in ContextMenu is used for navigating to other web page when menu item is
clicked. This can be achieved by providing link to the menu item using the
[`url`](../api/context-menu/menuItemModel#url) property.
In the following sample, Navigation URL for Flipkart, Amazon, and Snapdeal menu items
are added using the `url` property.

{% tab template= "context-menu/navigation", sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { ContextMenuComponent, MenuEventArgs, MenuItemModel } from '@syncfusion/ej2-react-navigations';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

class App extends React.Component<{}, {}> {
  private menuItems: MenuItemModel[] = [
    {
        iconCss: 'e-cart-icon e-link',
        text: 'Flipkart',
        url: 'https://www.google.co.in/search?q=flipkart'
    },
    {
        iconCss: 'e-cart-icon e-link',
        text: 'Amazon',
        url: 'https://www.google.co.in/search?q=amazon'
    },
    {
        iconCss: 'e-cart-icon e-link',
        text: 'Snapdeal',
        url: 'https://www.google.co.in/search?q=snapdeal'
    }];

  public itemBeforeEvent: any = (args: MenuEventArgs) => {
      args.element.getElementsByTagName('a')[0].setAttribute('target', '_blank');
  }

  public render() {
    return (
            <div className="container">
              <div id='target'>Right click / Touch hold to open the ContextMenu</div>
              <ContextMenuComponent id='contextmenu' target='#target' items={this.menuItems}
              beforeItemRender={this.itemBeforeEvent}/>
           </div>
        );
    }
  }

ReactDom.render(<App />,document.getElementById('element'));
```

{% endtab %}

> To open the links in new tab, set 'target' attribute with the value '_blank' in the
[`beforeItemRender`](../api/context-menu#beforeitemrender) event.

## See Also

* [How to change menu items dynamically](./how-to/change-menu-items-dynamically)
