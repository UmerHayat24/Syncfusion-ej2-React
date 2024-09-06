# To set title for Menu

In this sample , the title for menu item  can be achievable by using 'beforeItemRender' client-side event in Menu component.

{% tab template="menu/title-menu", compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { MenuComponent, MenuEventArgs, MenuItemModel } from '@syncfusion/ej2-react-navigations';
import * as React from 'react';
import * as ReactDom from 'react-dom';
enableRipple(true);

class App extends React.Component<{}, {}> {
    public menuItems: MenuItemModel[] = [
        {
            id: 'settingIcon',
            iconCss: 'em-icons e-file',
            items: [
                { text: 'Open',
                  items: [
                      { text: 'Sub Option1' },
                      { text: 'Sub Option2' },
                  ]
                },
                { text: 'Save' },
                { separator: true },
                { text: 'Exit' }
            ]
        }
    ];
    constructor(props: any) {
        super(props);
        this.beforeItemRender = this.beforeItemRender.bind(this);
    }

    public beforeItemRender(args: MenuEventArgs): void {
        if (args.item.id == 'settingIcon') {
        args.element.setAttribute('title', 'Settings');
      }
    }

    public render() {
        return (
            <MenuComponent items={this.menuItems}  beforeItemRender={this.beforeItemRender}/>
        );
    }
}

ReactDom.render(<App />,document.getElementById('element'));
```

{% endtab %}
