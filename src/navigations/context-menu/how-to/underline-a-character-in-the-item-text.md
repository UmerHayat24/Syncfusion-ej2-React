---
title: "Mnemonics in ContextMenu Items"
component: "ContextMenu"
description: "This section helps to add Mnemonics in ContextMenu items."
---

# Underline a character in the item text

To underline a particular character in a text, it can be handled in `beforeItemRender` event by
adding `<u>` tag in between the text and given as innerHTML in `li` rendering.

{% tab template= "context-menu/getting-started", sourceFiles="app/**/*.tsx,index.html,index.css", isDefaultActive=true, compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { ContextMenuComponent, MenuEventArgs, MenuItemModel } from '@syncfusion/ej2-react-navigations';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

class App extends React.Component {
  private menuItems: MenuItemModel[] = [
    {
        text: 'Cut'
    },
    {
        text: 'Copy'
    },
    {
        text: 'Paste'
    }];

  public itemBeforeEvent: any = (args: MenuEventArgs) => {
      if (args.item.text === 'Copy') {
        args.element.innerHTML = '<u>C</u>opy';
      }
  }

  public render() {
    return (
            <div className="container">
              <div id='target'>Right click / Touch hold to open the ContextMenu</div>
              <ContextMenuComponent id='contextmenu' target='#target' items={this.menuItems} beforeItemRender={this.itemBeforeEvent}/>
           </div>
        );
    }
}

ReactDom.render(<App />,document.getElementById('element'));

```

{% endtab %}
