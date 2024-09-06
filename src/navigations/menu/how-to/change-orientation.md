---
title: "Change Orientation in Menu"
component: "Menu"
description: "This section helps to learn how to change orientation in Menu."
---

# Change orientation

Orientation in menu items can be changed horizontally or vertically using the
[`orientation`](../../api/menu#orientation) property.
By default, it is horizontally aligned.

{% tab template="menu/getting-started",  sourceFiles="app/**/*.tsx,index.html", isDefaultActive=true, compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { MenuComponent, MenuItemModel } from '@syncfusion/ej2-react-navigations';
import * as React from 'react';
import * as ReactDom from 'react-dom';
enableRipple(true);

class App extends React.Component<{}, {}> {
    public menuItems: MenuItemModel[] = [
        {
            items: [
                { text: 'Open' },
                { text: 'Save' },
                { text: 'Exit' }
            ],
            text: 'File'
        },
        {
            items: [
                { text: 'Cut' },
                { text: 'Copy' },
                { text: 'Paste' }
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
        { text: 'Help' }
    ];

    public render() {
        return (
            <MenuComponent items={this.menuItems} orientation="Vertical"/>
        );
    }
}

ReactDom.render(<App />,document.getElementById('element'));
```

{% endtab %}
