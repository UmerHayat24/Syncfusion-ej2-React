---
title: "Menu with Images, URL, and Multi level items"
component: "Menu"
description: "React Menu supports submenu, images, and url navigations in menu items"
---

# Icons and Sub menu items

## Icons

The menu item contains an icon/image in it to provide a visual representation of an action. To place the icon on a menu item, set the [`iconCss`](../api/menu/menuItemModel#iconcss) property with the required icon CSS. By default, the icon is positioned at the left of the menu item. In the following sample, the icons of `File` and `Edit` menu items and `Open`, `Save`, `Cut`, `Copy`,and `Paste` sub menu items are added using the `iconCss` property.

{% tab template="menu/item-icons",  sourceFiles="app/**/*.tsx,index.html,index.css", isDefaultActive=true, compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { MenuComponent, MenuItemModel } from '@syncfusion/ej2-react-navigations';
import * as React from 'react';
import * as ReactDom from 'react-dom';
enableRipple(true);

class App extends React.Component<{}, {}> {
    // Menu items definition
    public menuItems: MenuItemModel[] = [
        {
            iconCss: 'em-icons e-file',
            items: [
                { text: 'Open', iconCss: 'em-icons e-open' },
                { text: 'Save', iconCss: 'e-icons e-save' },
                { separator: true },
                { text: 'Exit' }
            ],
            text: 'File'
        },
        {
            iconCss: 'em-icons e-edit',
            items: [
                { text: 'Cut', iconCss: 'em-icons e-cut' },
                { text: 'Copy', iconCss: 'em-icons e-copy' },
                { text: 'Paste', iconCss: 'em-icons e-paste' }
            ],
            text: 'Edit'
        },
        {
            items: [
                { text: 'Toolbar' },
                { text: 'Sidebar' },
                { text: 'Full Screen' }
            ],
            text: 'View'
        },
        {
            items: [
                { text: 'Spelling & Grammar' },
                { text: 'Customize' },
                { text: 'Options' }
            ],
            text: 'Tools'
        },
        { text: 'Go' },
        { text: 'Help' }
    ];

    public render() {
        return (
            <MenuComponent items={this.menuItems}/>
        );
    }
}

ReactDom.render(<App />,document.getElementById('element'));
```

{% endtab %}

## Navigation

Navigation in Menu is used to navigate to the other web page when a menu item is clicked. It can be achieved by providing a link to the menu item using the [`url`](../api/menu/menuItemModel/#url) property. In the following sample, the Navigation URL is added to sub menu items using the url property.

{% tab template="menu/getting-started",  sourceFiles="app/**/*.tsx,index.html", compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { MenuComponent, MenuEventArgs, MenuItemModel } from '@syncfusion/ej2-react-navigations';
import * as React from 'react';
import * as ReactDom from 'react-dom';
enableRipple(true);

class App extends React.Component<{}, {}> {
    // Menu items definition
    public menuItems: MenuItemModel[] = [
        {
            items: [
                { text: 'Washing Machine', url: 'https://www.google.com/search?q=washing+machine' },
                { text: 'Air Conditioners', url: 'https://www.google.com/search?q=air+conditioners' }
            ],
            text: 'Appliances'
        },
        {
            items: [
                { text: 'Headphones', url: 'https://www.google.com/search?q=headphones' },
                { text: 'Memory Cards', url: 'https://www.google.com/search?q=memory+cards' },
                { text: 'Power Banks', url: 'https://www.google.com/search?q=power+banks' }
            ],
            text: 'Mobile'
        },
        {
            items: [
                { text: 'Televisions', url: 'https://www.google.com/search?q=televisions' },
                { text: 'Home Theatres', url: 'https://www.google.com/search?q=home+theatres' },
                { text: 'Gaming Laptops', url: 'https://www.google.com/search?q=gaming+laptops' }
            ],
            text: 'Entertainment'
        },
        { text: 'Fashion', url: 'https://www.google.com/search?q=fashion' },
        { text: 'Offers', url: 'https://www.google.com/search?q=offers' }
    ];

    public beforeItemRender(args: MenuEventArgs): void {
        if (args.item.url) {
            args.element.getElementsByTagName('a')[0].setAttribute('target', '_blank');
        }
    }

    public render() {
        return (
            <MenuComponent items={this.menuItems} beforeItemRender={this.beforeItemRender}/>
        );
    }
}

ReactDom.render(<App />,document.getElementById('element'));
```

{% endtab %}

## Multilevel nesting

The Menu supports multiple level nesting, and it can be achieved by mapping the [`items`](../api/menu/menuItemModel#items) property inside the parent [`menuItems`](../api/menu#items). In the following sample, three-level nesting of menu has been provided.

{% tab template="menu/getting-started",  sourceFiles="app/**/*.tsx,index.html", compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { MenuComponent, MenuItemModel } from '@syncfusion/ej2-react-navigations';
import * as React from 'react';
import * as ReactDom from 'react-dom';
enableRipple(true);

class App extends React.Component<{}, {}> {
    // Menu items definition
    public menuItems: MenuItemModel[] = [
        {
            items: [
                {
                    items: [
                        {
                            items: [
                                { text: 'Trimmers' },
                                { text: 'Shavers' }
                            ],
                            text: 'Personal Care'
                        },
                        {
                            items: [
                                { text: 'Shirts' },
                                { text: 'Jackets' },
                                { text: 'Track Suits' }
                            ],
                            text: 'Clothing'
                        },
                        { text: 'Footwear' }
                    ],
                    text: 'Men Fashion'
                },
                {
                    items: [
                        {
                            items: [
                                { text: 'Kurtas' },
                                { text: 'Salwars' },
                                { text: 'Sarees' }
                            ],
                            text: 'Clothing'
                        },
                        {
                            items: [
                                { text: 'Nosepins' },
                                { text: 'Anklets' }
                            ],
                            text: 'Jewellery'
                        }
                    ],
                    text: 'Women Fashion'
                }
            ],
            text: 'Fashion'
        },
        {
            items: [
                {
                    items: [
                        { text: 'Fully Automatic' },
                        { text: 'Semi Automatic' }
                    ],
                    text: 'Washing Machine'
                },
                {
                    items: [
                        { text: 'Inverter ACs' },
                        { text: 'Split ACs' }
                    ],
                    text: 'Air Conditioners'
                }
            ],
            text: 'Home & Living'
        },
        { text: 'Accessories' },
        { text: 'Sports' },
        { text: 'Gaming' }
    ];

    public render() {
        return (
            <MenuComponent items={this.menuItems} />
        );
    }
}

ReactDom.render(<App />,document.getElementById('element'));
```

{% endtab %}

> You can achieve multi level nesting with data source by mapping `name` of the child items to the [`children`](../api/menu/fieldSettingsModel#children) sub-property of [`fields`](../api/menu/fieldSettingsModel) property. Also, we can specify [`id`](../api/menu/menuItemModel/#id) property for menu items. For more information, refer to the [`data source binding`](./data-source-binding-and-custom-menu-items#data-binding) section. To open sub menu items only on item click, [`showItemOnClick`](../api/menu#showitemonclick) should be set as `true`.

## See Also

* [Customize menu items](./how-to/customize-menu-items)
* [Group menu items with separator](./getting-started#group-menu-items-with-separator)