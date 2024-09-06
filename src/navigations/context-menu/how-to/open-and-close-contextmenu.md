---
title: "Open or Close ContextMenu"
component: "ContextMenu"
description: "This section helps to learn how to open and close a ContextMenu."
---

# Open and close ContextMenu

Open and close the ContextMenu manually whenever required by using open and close methods.

In the following sample, the ContextMenu is opened using the [`open`](../api/context-menu#open) method at the
specified position with `X` and `Y` coordinates and to close the ContextMenu, [`close`](../api/context-menu#close)
method is called internally on ContextMenu item click or document click.

{% tab template="context-menu/how-to", isDefaultActive = "true",  sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { ContextMenuComponent, MenuItemModel } from '@syncfusion/ej2-react-navigations';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

class App extends React.Component<{}, {}> {
    public cMenu: ContextMenuComponent;
    private menuItems: MenuItemModel[] = [
        {
            text: 'Cut'
        },
        {
            text: 'Copy'
        },
        {
            text: 'Paste'
        }
    ];
    constructor(props: any) {
        super(props);
        this.btnClick = this.btnClick.bind(this);
    }
    public btnClick(): void {
        this.cMenu.open(40, 20);
    }

    public render() {
        return (
            <div className="container">
                <ContextMenuComponent id='contextmenu' ref={(scope) => this.cMenu = scope as ContextMenuComponent} items={this.menuItems} />
                <ButtonComponent onClick={this.btnClick}>Open ContextMenu</ButtonComponent>
            </div>
        );
    }
}

ReactDom.render(<App />,document.getElementById('element'));
```

{% endtab %}
