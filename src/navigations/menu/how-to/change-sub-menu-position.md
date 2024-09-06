---
title: "Change position of Sub menu in Menu"
component: "Menu"
description: "This section helps to learn how to change the position of a sub menu in Menu."
---

# Change sub menu position

The submenu position can be changed by using the [`beforeOpen`](../../api/menu/#beforeopen) event. Assign the top and left position where you want to open the submenu to the [`beforeOpen`](../../api/menu/#beforeopen) event arguments `args.top` and `args.left` respectively.

In the below sample, the sub menu opens above the parent menu item.

{% tab template="menu/position",  sourceFiles="app/**/*.tsx,index.html", isDefaultActive=true, compileJsx=true %}

```tsx
import { closest, enableRipple} from '@syncfusion/ej2-base';
import { BeforeOpenCloseMenuEventArgs, MenuComponent, MenuItemModel } from '@syncfusion/ej2-react-navigations';
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

    public onBeforeOpen(args: BeforeOpenCloseMenuEventArgs) {
        // Getting parent menu item element offset
        const relativeOffset = closest(args.event.target as Element, '.e-menu-item').getBoundingClientRect();
        // Getting sub menu wrapper element using closest method
        const subMenuEle = closest(args.element, '.e-menu-wrapper') as HTMLElement;
        subMenuEle.style.display = 'block';
        args.top = (relativeOffset.top - subMenuEle.getBoundingClientRect().height) + pageYOffset;
        args.left = relativeOffset.left + pageXOffset;
        subMenuEle.style.display = '';
    }

    public render() {
        return (
            <MenuComponent items={this.menuItems} beforeOpen={this.onBeforeOpen}/>
        );
    }
}

ReactDom.render(<App />,document.getElementById('element'));
```

{% endtab %}

>> For custom positioning, set both `top` and `left` position in the [`beforeOpen`](../../api/menu/#beforeopen) event.