---
title: "Rounded Corner in Menu"
component: "Menu"
description: "This section helps to learn about how to achieve rounded corner in Menu."
---

# Menu with rounded corner

The rounded corner can be achieved by using the [`cssClass`](../../api/menu/#cssclass) property. Add a custom class to the menu component and customize it using the `border-radius` CSS property. For more information, refer to the `style.css` file mapped under the source tab.

{% tab template="menu/rounded",  sourceFiles="app/**/*.tsx,index.html,index.css", isDefaultActive=true, compileJsx=true %}

```tsx
import { MenuComponent, MenuItemModel } from '@syncfusion/ej2-react-navigations';
import * as React from 'react';
import * as ReactDom from 'react-dom';

class App extends React.Component<{}, {}> {
    // Menu items definition
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
                { text: 'Sidebar' }
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

    render() {
        return (
            <MenuComponent items={this.menuItems} cssClass='e-rounded-menu'/>
        );
    }
}

ReactDom.render(<App />,document.getElementById('element'));
```

{% endtab %}
