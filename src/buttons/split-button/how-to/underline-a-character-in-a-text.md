---
title: "Underline a character in a text"
component: "SplitButton"
description: "React SplitButton how to section, group popup items using list view component, dialog open on popup item click."
---

# Underline a character in a text

Underline a particular character in a text can be handled in [`beforeItemRender`](../../api/split-button#beforeitemrender)  event by adding `<u>` tag in between the text and given as
innerHTML in `li` rendering.

In the following example, `C` is underlined in the text `Copy`.

{% tab template= "split-button/underline", sourceFiles="app/**/*.tsx,index.html,style.css", compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { SplitButtonComponent, ItemModel, MenuEventArgs } from '@syncfusion/ej2-react-splitbuttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

// To render SplitButton.
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
       <SplitButtonComponent items = {this.items} beforeItemRender={this.itemRender}>Paste</SplitButtonComponent>
      </div>
    );
  }
}
ReactDom.render(<App />,document.getElementById('button'));
```

{% endtab %}