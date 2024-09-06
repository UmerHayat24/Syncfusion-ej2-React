---
title: "Prevent the focus on the first element"
component: "Dialog"
description: "Covers customization features such as load content to the dialog from external sources, built-in alert, and confirmation model dialog."
---

# Prevent the focus on the first element

By default, the dialog focuses on the first elements of the content area which can be active and focusable. You can prevent this default focusing behavior using the [open](../../api/dialog/#open) event and by enabling the `preventFocus` argument.

Bind the open event and enable the preventFocus argument within an event like the below sample.

{% tab template="dialog/dlg-focus", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript

import { DialogComponent } from '@syncfusion/ej2-react-popups';
import * as React from "react";
import './App.css';

class App extends React.Component<{}, {}> {
  public dialogInstance: DialogComponent;
  public buttons: any = [{
    buttonModel: {
        content: 'Ok',
        isPrimary: true,
    },
    'click': () => {
        this.dialogInstance.hide();
    }
  }, {
    buttonModel: {
        content: 'Cancel'
    },
    'click': () => {
        this.dialogInstance.hide();
    }
  }];

  public dialogContent(): JSX.Element {
    return (
        <div class='form-group'><label for='email'>Email:</label>
            <input type='email' class='form-control' id='email'>
        </div>
        <div class='form-group'>
            <label for='comment'>Password:</label>
            <input type='password' class='form-control' id='password'>
        </div>
    )
  }
  
  public onOpen = (args: any): void =>{
      args.preventFocus = true;
  }
  
  public render() {
    return (
    <div className="App" id='container'>  
        <DialogComponent id="dlg-focus" width='300px' isModal={true} target='#container' header='Sign In' open={this.onOpen} buttons={this.buttons} ref={dialog => this.dialogInstance = dialog!}>
         <div>{this.dialogContent()}</div>
         </DialogComponent>
    </div>);
  }
}
export default App;

```

{% endtab %}