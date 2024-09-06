---
title: "Menu Customizations"
component: "Menu"
description: "This section helps to learn how to customize Menu Items."
---

# Customize menu items

## Add or remove menu items

Menu items can be added or removed using the [`insertAfter`](../api/menu#insertafter),
[`insertBefore`](../api/menu#insertbefore) and [`removeItems`](../api/menu#removeitems) methods.

In the following example, the **Europe** menu items are added before the **Oceania** item,
the **Africa** menu items are added after the **Asia**, and the **South America**
and **Mexico** items are removed from menu.

{% tab template="menu/getting-started",  sourceFiles="app/**/*.tsx,index.html", compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { FieldSettingsModel, MenuComponent } from '@syncfusion/ej2-react-navigations';
import * as React from 'react';
import * as ReactDom from 'react-dom';
enableRipple(true);

class App extends React.Component<{}, {}> {
    public menuObj: MenuComponent;

    // Menu data source
    public data: Array<{ [key: string]: any }> = [
        {
            continent: 'Asia',
            countries: [
                { country: 'China' },
                { country: 'India' },
                { country: 'Japan' }
            ]
        },
        {
            continent: 'North America',
            countries: [
                { country: 'Canada' },
                { country: 'Mexico' },
                { country: 'USA' }
            ]
        },
        {
            continent: 'South America',
            countries: [
                { country: 'Brazil' },
                { country: 'Colombia' },
                { country: 'Argentina' }
            ]
        },
        {
            continent: 'Oceania',
            countries: [
                { country: 'Australia' },
                { country: 'New Zealand' },
                { country: 'Samoa' },
            ]
        },
        { continent: 'Antarctica' }
    ];

    // Menu fields definition
    public menuFields: FieldSettingsModel = {
        children: ['countries'],
        text: ['continent', 'country'],
    };
    constructor(props: any) {
        super(props);
        this.created = this.created.bind(this);
    }
    public created(): void {
        let insertItem: Array<{ [key: string]: any }> = [
            {
                continent: 'Europe',
                countries: [
                    { country: 'Finland' },
                    { country: 'Austria' }
                ]
            }
        ];
        // Add items before to 'Oceania'
        this.menuObj.insertBefore(insertItem, 'Oceania', false);

        insertItem = [
            {
                continent: 'Africa',
                countries: [
                    { country: 'Nigeria' }
                ]
            }
        ];

        // Add items after to 'Asia'
        this.menuObj.insertAfter(insertItem, 'Asia', false);

        // Remove items
        this.menuObj.removeItems(['South America', 'Mexico'], false);
    }

    public render() {
        return (
            <MenuComponent ref={scope => this.menuObj = scope} items={this.data} fields={this.menuFields} created={this.created}/>
        );
    }
}

ReactDom.render(<App />,document.getElementById('element'));
```

{% endtab %}

> To process items with `ID` values, set `isUnique` to `true`.

## Enable or disable menu items

You can enable and disable the menu items using the [`enableItems`](../api/menu#enableitems)
method in Menu. To enable menuItems, set the `enable` property in argument to `true` and vice-versa.

In the following example, the **Directory** header item, **Conferences**, and **Music** sub menu items are disabled.

{% tab template="menu/enable-disable",  sourceFiles="app/**/*.tsx,index.html", compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { BeforeOpenCloseMenuEventArgs, MenuComponent, MenuItemModel } from '@syncfusion/ej2-react-navigations';
import * as React from 'react';
import * as ReactDom from 'react-dom';
enableRipple(true);

class App extends React.Component<{}, {}> {
    public menuObj: MenuComponent;
    // Menu items definition
    public menuItems: MenuItemModel[] = [
        {
            items: [
                { text: 'Conferences' },
                { text: 'Music' },
                { text: 'Workshops' }
            ],
            text: 'Events'
        },
        {
            items: [
                { text: 'Now Showing' },
                { text: 'Coming Soon' }
            ],
            text: 'Movies'
        },
        {
            items: [
                { text: 'Media Gallery' },
                { text: 'Newsletters' }
            ],
            text: 'Directory'
        },
        {
            items: [
                { text: 'Our Policy' },
                { text: 'Site Map' }
            ],
            text: 'Queries'
        },
        { text: 'Services' }
    ];

    public disableItems: string[] = ['Conferences', 'Music', 'Directory'];
    constructor(props: any) {
        super(props);
        this.created = this.created.bind(this);
        this.beforeOpen = this.beforeOpen.bind(this);
        this.btnClick = this.btnClick.bind(this);
    }
    public beforeOpen(args: BeforeOpenCloseMenuEventArgs): void {
        // Handling sub menu items
        for (const item of args.items) {
            if (this.disableItems.indexOf(item.text) > -1) {
                this.menuObj.enableItems([item.text], false, false);
            }
        }
    }

    public created(): void {
        // Disable items
        this.menuObj.enableItems(this.disableItems, false, false);
    }

    public btnClick(): void {
        // Enable items
        this.menuObj.enableItems(this.disableItems, true, false);
        this.disableItems = [];
    }

    public render() {
        return (
            <div className="control-section">
                <ButtonComponent id='enable' content='Enable all items' onClick={this.btnClick}/>
                <div className="menu-section">
                    <MenuComponent ref={scope => this.menuObj = scope} items={this.menuItems} beforeOpen={this.beforeOpen} created={this.created}/>
                </div>
            </div>
        );
    }
}

ReactDom.render(<App />,document.getElementById('element'));
```

{% endtab %}

> To disable sub menu items, use the [`beforeOpen`](../api/menu#beforeopen) event.

## Hide or show menu items

You can show or hide the menu items using the [`showItems`](../api/menu#showitems)
and [`hideItems`](../api/menu#hideitems) methods.

In the following example, the **Movies** header item, **Workshops**, and **Music** sub menu items
are hidden in menu.

{% tab template="menu/enable-disable",  sourceFiles="app/**/*.tsx,index.html", compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { BeforeOpenCloseMenuEventArgs, MenuComponent, MenuItemModel } from '@syncfusion/ej2-react-navigations';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

class App extends React.Component<{}, {}> {
    public menuObj: MenuComponent;

    public menuItems: MenuItemModel[] = [
        {
            items: [
                { text: 'Conferences' },
                { text: 'Music' },
                { text: 'Workshops' }
            ],
            text: 'Events'
        },
        {
            items: [
                { text: 'Now Showing' },
                { text: 'Coming Soon' }
            ],
            text: 'Movies'
        },
        {
            items: [
                { text: 'Media Gallery' },
                { text: 'Newsletters' }
            ],
            text: 'Directory'
        },
        {
            items: [
                { text: 'Our Policy' },
                { text: 'Site Map' }
            ],
            text: 'Queries'
        },
        { text: 'Services' }
    ];

    public hiddenItems: string[] = ['Workshops', 'Music', 'Movies'];
    constructor(props: any) {
        super(props);
        this.created = this.created.bind(this);
        this.beforeOpen = this.beforeOpen.bind(this);
        this.btnClick = this.btnClick.bind(this);
    }
    public beforeOpen(args: BeforeOpenCloseMenuEventArgs): void {
        // Handling sub menu items
        for (const item of args.items) {
            if (this.hiddenItems.indexOf(item.text) > -1) {
                this.menuObj.hideItems([item.text], false);
            }
        }
    }

    public created(): void {
        // Disable items
        this.menuObj.hideItems(this.hiddenItems, false);
    }

    public btnClick(): void {
        // show items
        this.menuObj.showItems(this.hiddenItems, false);
        this.hiddenItems = [];
    }

    public render() {
        return (
            <div className="control-section">
                <ButtonComponent content='Show all items' onClick={this.btnClick}/>
                <div className="menu-section">
                    <MenuComponent ref={scope => this.menuObj = scope} items={this.menuItems} beforeOpen={this.beforeOpen} created={this.created}/>
                </div>
            </div>
        );
    }
}

ReactDom.render(<App />,document.getElementById('element'));
```

{% endtab %}

> Using the [`beforeOpen`](../api/menu#beforeopen) event, you can hide the sub menu items as in the above example since the menu supports to hide items only for headers initially.
