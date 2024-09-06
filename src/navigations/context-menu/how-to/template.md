---
title: "Templates in ContextMenu"
component: "ContextMenu"
description: "This section helps to learn how to use templates in ContextMenu."
---

# Template

## Table in Sub ContextMenu

Menu items of the ContextMenu can be customized according to the requirement. The section explains about how to customize table template
in sub menu item.

This can be achieved by appending table layout while `li` rendering by using `beforeItemRender` event.

{% tab template="context-menu/table",  sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { ContextMenuComponent, MenuEventArgs, MenuItemModel } from '@syncfusion/ej2-react-navigations';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

class App extends React.Component<{}, {}> {
    private menuItems: MenuItemModel[] = [
        {
            iconCss: 'e-cm-icons e-cut',
            text: 'Cut',
        },
        {
            iconCss: 'e-icons e-copy',
            text: 'Copy'
        },
        {
            iconCss: 'e-cm-icons e-paste',
            text: 'Paste'
        },
        {
            separator: true
        },
        {
            iconCss: 'e-icons e-link',
            text: 'Link'
        },
        {
            iconCss: 'e-icons e-table',
            items: [
                {
                    id: 'table'
                }
            ],
            text: 'Table'
        }
    ];
    public createHeader = () => {
        const header = document.createElement('h4');
        header.textContent = 'Insert Table';
        return header;
    }
    public createTable = () => {
        const table = document.createElement('table');
        for (let i: number = 0; i < 5; i++) {
            const row = document.createElement('tr');
            table.appendChild(row);
            for (let j: number = 0; j < 6; j++) {
                const col = document.createElement('td');
                row.appendChild(col);
                col.setAttribute('class', 'data');
            }
        }
        return table;
    }

    public itemBeforeEvent: any = (args: MenuEventArgs) => {
        if (args.item.id === 'table') {
            args.element.classList.add('bg-transparent');
            args.element.appendChild(this.createHeader());
            args.element.appendChild(this.createTable());
        }
    }

    public render() {
        return (
            <div className="container">
                <div id='target'>Right click / Touch hold to open the ContextMenu</div>
                <ContextMenuComponent id='contextmenu' target='#target'
                    items={this.menuItems} beforeItemRender={this.itemBeforeEvent}/>
            </div>
        );
    }
}

ReactDom.render(<App />,document.getElementById('element'));
```

{% endtab %}

### UI Components in ContextMenu

UI components can also be placed inside the each `li` element of ContextMenu.

In the following example, CheckBox component is placed inside each `li` element and this can be achieved by creating
CheckBox component in `beforeItemRender` event and appending it into the `li` element.

{% tab template="context-menu/ui-element",  sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```tsx
import { closest, createElement, enableRipple} from '@syncfusion/ej2-base';
import { createCheckBox } from '@syncfusion/ej2-buttons';
import { BeforeOpenCloseMenuEventArgs, ContextMenuComponent, MenuEventArgs, MenuItemModel } from '@syncfusion/ej2-react-navigations';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

class App extends React.Component<{}, {}> {

    public menuItems: MenuItemModel[] = [
        { text: 'Option 1' },
        { text: 'Option 2' },
        { text: 'Option 3' }
    ];
    public itemBeforeEvent: any = (args: MenuEventArgs) => {
        const check = createCheckBox(createElement, false, {
            checked: (args.item.text === 'Option 1' || args.item.text === 'Option 2') ? true : false,
            label: args.item.text
        });
        args.element.innerHTML = '';
        args.element.appendChild(check);
    }

    public beforeClose: any = (args: BeforeOpenCloseMenuEventArgs) => {
        if (closest((args.event.target as HTMLElement), '.e-menu-item')) {
            args.cancel = true;
            const selectedElem = args.element.querySelectorAll('.e-selected');
            for (const elem of selectedElem as any) {
                const ele = elem as HTMLElement;
                ele.classList.remove('e-selected');
            }
            const checkbox = closest(args.event.target as Element, '.e-checkbox-wrapper') as HTMLElement;
            const frame = checkbox.querySelector('.e-frame');
            if (checkbox && frame.classList.contains('e-check')) {
                frame.classList.remove('e-check');
            } else if (checkbox) {
                frame.classList.add('e-check');
            }
        }
    }
    public render() {
        return (
            <div className="container">
                <div id='target'>Right click / Touch hold to open the ContextMenu</div>
                <ContextMenuComponent id='contextmenu' target='#target' items={this.menuItems} beforeItemRender={this.itemBeforeEvent} beforeClose={this.beforeClose} />
            </div>
        );
    }
}
ReactDom.render(<App />,document.getElementById('element'));
```

{% endtab %}
