---
title: "Change ContextMenu Items Dynamically"
component: "ContextMenu"
description: "This section helps to learn how to change ContextMenu items dynamically."
---
# Change menu items dynamically

The items visible in the ContextMenu can be changed dynamically based on the context you open. To achieve this behavior, initialize
ContextMenu with all items using [`items`](https://ej2.syncfusion.com/react/documentation/api/context-menu/#items) property and then based on the context you open hide/show
required items using [`hideItems`](https://ej2.syncfusion.com/react/documentation/api/context-menu/#hideitems)/[`showItems`](https://ej2.syncfusion.com/react/documentation/api/context-menu/#showitems)
method in [`beforeOpen`](https://ej2.syncfusion.com/react/documentation/api/context-menu/#beforeopen) event.

In the following example, the datasource for Clipboard div is `Cut`, `Copy`, `Paste` and for the Editor div is `Add`,
`Edit`, `Delete` is changed on [`beforeOpen`](https://ej2.syncfusion.com/react/documentation/api/context-menu/#beforeopen) event
using [`hideItems`](https://ej2.syncfusion.com/react/documentation/api/context-menu/#hideitems) and [`showItems`](https://ej2.syncfusion.com/react/documentation/api/context-menu/#showitems) method.

{% tab template="context-menu/dynamic",  sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { BeforeOpenCloseMenuEventArgs } from '@syncfusion/ej2-navigations';
import { ContextMenuComponent, MenuItemModel } from '@syncfusion/ej2-react-navigations';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

class App extends React.Component {
  public cmenuInstance: ContextMenuComponent;
  public menuItems: MenuItemModel[] = [
    {
        text: 'Cut'
    },
    {
        text: 'Copy'
    },
    {
        text: 'Paste'
    },
    {
        text: 'Add'
    },
    {
        text: 'Edit'
    },
    {
        text: 'Delete'
    }];
  constructor(props: any) {
    super(props);
    this.beforeOpen = this.beforeOpen.bind(this);
  }
  public beforeOpen: any = (args: BeforeOpenCloseMenuEventArgs) => {
      if ((args.event.target as HTMLElement).id === 'right') {
        this.cmenuInstance.hideItems(['Cut', 'Copy', 'Paste']);
        this.cmenuInstance.showItems(['Add', 'Edit', 'Delete']);
      } else if ((args.event.target as HTMLElement).id === 'left') {
        this.cmenuInstance.showItems(['Cut', 'Copy', 'Paste']);
        this.cmenuInstance.hideItems(['Add','Edit','Delete']);
      }
  }

  public render() {
    return (
            <div className="container">
              <div id="target">
                 <div id='right' className='e-div'>Editor</div>
                 <div id='left' className='e-div'>Clipboard</div>
              </div>
              <ContextMenuComponent id='contextmenu' target='#target' ref={cmenu => this.cmenuInstance = cmenu as ContextMenuComponent}
              items={this.menuItems} beforeOpen={this.beforeOpen} beforeClose={this.beforeClose}/>
           </div>
        );
    }
}

ReactDom.render(<App />,document.getElementById('element'));
```

{% endtab %}
