---
title: "Menu Right To Left"
component: "Menu"
description: "This section helps to learn how to Right to Left."
---

# Right-To-Left

Menu component has RTL support. This can be achieved by setting [`enableRtl`](../../api/menu#enablertl) as `true`.

The following example illustrates how to enable right-to-left support in Menu component.

{% tab template= "menu/getting-started", sourceFiles="app/**/*.tsx,index.html,index.css", isDefaultActive=true, compileJsx=true %}

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

    public render() {
        return (
            <MenuComponent items={this.menuItems} enableRtl={true}/>
        );
    }
}

ReactDom.render(<App />,document.getElementById('element'));
```

{% endtab %}