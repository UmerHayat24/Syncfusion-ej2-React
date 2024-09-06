---
title: "Mnemonics in Menu"
component: "Menu"
description: "This section helps to learn how to apply Mnemonics in Menu Items."
---

# Create mnemonic UI in menu item

A particular character in a text can be underlined in the [`beforeItemRender`](https://ej2.syncfusion.com/react/documentation/api/menu/#beforeitemrender) event by
adding `<u>` tag in between the text and assign the innerHTML to the `li` element.

In the following example, the first character in `File`, `Open`, and `Save` menu items are underlined.

{% tab template="menu/item-icons",  sourceFiles="app/**/*.tsx,index.html", compileJsx=true %}

```tsx

import { enableRipple } from '@syncfusion/ej2-base';
import { MenuComponent, MenuEventArgs, MenuItemModel } from '@syncfusion/ej2-react-navigations';
import * as React from 'react';
import * as ReactDom from 'react-dom';
enableRipple(true);

class App extends React.Component<{}, {}> {
    public menuObj: MenuComponent;

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
        { text: 'Format' },
        { text: 'View' },
        { text: 'Bookmarks' },
        { text: 'Tools' },
        { separator: true },
        { text: 'Help' }
    ];
    constructor(props: any) {
        super(props);
        this.beforeItemRender = this.beforeItemRender.bind(this);
    }
    public beforeItemRender(args: MenuEventArgs): void {
        if (['File', 'Open', 'Save'].indexOf(args.item.text) > -1) {
            // To underline a First character.
            const underlinedText = '<u>' + args.item.text.slice(0, 1) + '</u>' + args.item.text.slice(1);
            args.element.innerHTML = args.element.innerHTML.replace(args.item.text, underlinedText);
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
