---
title: "Render a dialog without header"
component: "Dialog"
description: "Covers customization features such as load content to the dialog from external sources, built-in alert, and confirmation model dialog."
---

# Render a dialog without header

The dialog can be rendered without header by setting the header property value as empty string or null.  By default, dialog is rendered without header.

{% tab template="dialog/dlg-header", sourceFiles="app/App.tsx", tab compileJsx=true %}

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
      this.dialogInstance.show();
  }
  
  public render() {
    return (
    <div className="App" id='dialog-target'>
        <button className='e-control e-btn' id='targetButton1' role='button' onClick={this.handleClick = this.handleClick.bind(this)}>Open</button>
        <DialogComponent width='250px' target='#dialog-target' buttons={this.buttons} ref={dialog => this.dialogInstance = dialog!}>
        This is a dialog without header </DialogComponent>
    </div>);
  }
}
export default App;

```

{% endtab %}