---
title: "Underline a character in the item text"
component: "DropDownButton"
description: "React DropDownButton how to section, hide drop down arrow, group popup items using list view component, dialog open on popup item click."
---

# Underline a character in the item text

Underline a particular character in a text can be handled in
[`beforeItemRender`](../../api/drop-down-button#beforeitemrender)event by
adding `<u>` tag in between the text and given as innerHTML in `li` rendering.

In the following example, `C` is underlined in the text `Copy`.

{% tab template= "drop-down-button/default", sourceFiles="app/**/*.tsx,index.html,styles.css",isDefaultActive=true, compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { DropDownButtonComponent, ItemModel, MenuEventArgs } from '@syncfusion/ej2-react-splitbuttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

// To render DropDownButton.
class App extends React.Component<{}, {}> {

  public items: ItemModel[] = [
    {
        text: 'Cut'
    },
    {
        text: 'Copy'
    },
    {
        text: 'Paste'
    }];

  public itemRender(args: MenuEventArgs) {
    if (args.item.text === 'Copy') {
        // To underline a particular text.
        args.element.innerHTML = '<u>C</u>opy';
    }
  }
  public render() {
    return (
      <div>
        <DropDownButtonComponent items = {this.items} beforeItemRender={this.itemRender}>Clipboard</DropDownButtonComponent>
      </div>
    );
  }
}
ReactDom.render(<App />,document.getElementById('button'));

```

{% endtab %}