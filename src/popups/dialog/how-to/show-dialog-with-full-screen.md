---
title: "Show React Dialog with full screen"
component: "Dialog"
description: "Covers customization features such as load content to the dialog from external sources, built-in alert, and confirmation model dialog."
---

# Show dialog with full screen

You can show the dialog in fullscreen by passing `true` as argument to the dialog [show](../../api/dialog/#show) method.

{% tab template="dialog/dlg-fullscreen", sourceFiles="app/App.tsx", tab compileJsx=true %}

```typescript

import { DialogComponent } from '@syncfusion/ej2-react-popups';
import * as React from "react";
import './App.css';

class App extends React.Component<{}, {}> {
  public dialogInstance: DialogComponent;

public buttons: any = [{
    buttonModel: {
        content: 'OK',
        cssClass: 'e-flat',
        isPrimary: true,
    },
    'click': () => {
        this.dialogInstance.hide();
    }
},
{
    buttonModel: {
        content: 'Cancel',
        cssClass: 'e-flat'
    },
    'click': () => {
        this.dialogInstance.hide();
    }
}];

public handleClick() {
    this.dialogInstance.show(true);
}

public render() {
  return (
  <div className="App" id='dialog-target'>
      <button className='e-control e-btn' id='targetButton1' role='button' onClick={this.handleClick = this.handleClick.bind(this)}>Open</button>

      <DialogComponent header='Dialog' showCloseIcon={true} visible={false} width='250px' target='#dialog-target' buttons={this.buttons} ref={dialog => this.dialogInstance = dialog!}>
      This is a Dialog with fullscreen display </DialogComponent>
  </div>);
}
}
export default App;

```

{% endtab %}