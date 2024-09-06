---
title: "Change Animation Settings in Menu"
component: "Menu"
description: "This section helps to learn how to change animation settings in Menu."
---

# Change animation settings

To change the animation of the Menu, [`animationSettings`](https://ej2.syncfusion.com/react/documentation/api/menu/menuAnimationSettingsModel/) property is used. The supported effects for Menu are,

| Effect | Functionality |
| ------------ | ----------------------- |
| None | Specifies the sub menu transform with no animation effect. |
| SlideDown | Specifies the sub menu transform with slide down effect. |
| ZoomIn | Specifies the sub menu transform with zoom in effect. |
| FadeIn | Specifies the sub menu transform with fade in effect. |

The following sample illustrates how to open Menu with `FadeIn` [`effect`](https://ej2.syncfusion.com/react/documentation/api/menu/menuAnimationSettingsModel/#effect) with the [`duration`](https://ej2.syncfusion.com/react/documentation/api/menu/menuAnimationSettingsModel/#duration) of `800ms`. Also we can set [`easing`](https://ej2.syncfusion.com/react/documentation/api/menu/menuAnimationSettingsModel/#easing) for menu items.

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

    private animationSettings: any = {
        duration: 800,
        effect: 'FadeIn'
    }

    public render() {
        return (
            <MenuComponent items={this.menuItems} animationSettings={this.animationSettings}/>
        );
    }
}

ReactDom.render(<App />,document.getElementById('element'));
```

{% endtab %}
