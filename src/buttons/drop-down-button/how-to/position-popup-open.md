---
title: "Position popup open"
component: "DropDownButton"
description: "React DropDownButton how to section, hide drop down arrow, group popup items using list view component, dialog open on popup item click."
---

# Position popup open

Popup open position can be changed according to the requirement. Popup open position can be changed in
[`open`](../../api/drop-down-button#open) event by setting `top` and `left` for the popup element.

In the following example, the `top` position of the popup element is changed in `open` event.

{% tab template= "drop-down-button/position", sourceFiles="app/**/*.tsx,index.html,styles.css",isDefaultActive=true, compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { DropDownButtonComponent, ItemModel, OpenCloseMenuEventArgs } from '@syncfusion/ej2-react-splitbuttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

enableRipple(true);

// To render DropDownButton.
class App extends React.Component<{}, {}> {
    public ddb: DropDownButtonComponent;
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
    constructor(props: any) {
        super(props);
        this.onOpen = this.onOpen.bind(this);
    }
    // To open popup in particular position.
    public onOpen (args: OpenCloseMenuEventArgs) {
      const elem = (args.element.parentElement as HTMLElement);
      elem.style.top = this.ddb.element.getBoundingClientRect().top - elem.offsetHeight +'px';
    }
  
    public render() {
      return (
        <div>
          <DropDownButtonComponent ref= {(scope) => { this.ddb = scope as DropDownButtonComponent; } } items = {this.items} open={this.onOpen} cssClass='e-caret-up'>Clipboard</DropDownButtonComponent>
        </div>
      );
    }
  }
ReactDom.render(<App />,document.getElementById('button'));

```

{% endtab %}