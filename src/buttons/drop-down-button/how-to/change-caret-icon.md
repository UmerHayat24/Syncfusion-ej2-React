---
title: "Change caret icon"
component: "DropDownButton"
description: "React DropDownButton how to section, hide drop down arrow, group popup items using list view component, dialog open on popup item click."
---

# Change caret icon

Dropdown arrow can be customized on popup open and close. It can be handled in
[`beforeOpen`](../../api/drop-down-button#beforeopen) and
[`beforeClose`](../../api/drop-down-button#beforeclose) event.

In the following example, the up arrow is updated on popup close and down arrow is updated
on popup open using `beforeOpen` and `beforeClose` event by adding and removing
`e-caret-up` class.

{% tab template= "drop-down-button/updown", sourceFiles="app/**/*.tsx,index.html,styles.css",isDefaultActive=true, compileJsx=true %}

```tsx
import { enableRipple } from '@syncfusion/ej2-base';
import { DropDownButtonComponent, ItemModel } from '@syncfusion/ej2-react-splitbuttons';
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
      this.beforeOpen = this.beforeOpen.bind(this);
      this.beforeClose = this.beforeClose.bind(this);
    }
    // To update up arrow with `e-caret-up` class.
    public beforeOpen () {
        this.ddb.cssClass = 'e-caret-up';
    }
    // To remove `e-caret-up` class.
    public beforeClose () {
        this.ddb.cssClass = '';
    }
  
    public render() {
      return (
      <div>
        <DropDownButtonComponent ref={(scope) => { this.ddb = scope as DropDownButtonComponent; }} items = {this.items} beforeOpen={this.beforeOpen} beforeClose={this.beforeClose}> Clipboard</DropDownButtonComponent>
        </div>
      );
    }
  }
ReactDom.render(<App />,document.getElementById('button'));

```

{% endtab %}