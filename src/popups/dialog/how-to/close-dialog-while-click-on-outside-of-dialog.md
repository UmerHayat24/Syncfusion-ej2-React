---
title: "Close the React dialog while click on outside of dialog"
component: "Dialog"
description: "Covers customization features such as load content to the dialog from external sources, built-in alert, and confirmation model dialog."
---

# Close dialog while click on outside of dialog

By default, dialog can be closed by pressing Esc key and clicking the close icon on the right of dialog header. It can also be closed by clicking outside of the dialog using hide method.
Set the [CloseOnEscape](../../api/dialog/#closeonescape) property value to false to prevent closing of the dialog when pressing Esc key.

In the following sample, dialog is closed when clicking outside the dialog area using [hide](../../api/dialog/#hide) method.

{% tab template="dialog/dlg-close", tab compileJsx=true %}

```typescript
import { DialogComponent } from '@syncfusion/ej2-react-popups';
import * as React from "react";
import './App.css';

class App extends React.Component<{}, {}> {
  public settings: any = { effect: 'Zoom', duration: 400, delay: 0 };
  public dialogInstance: DialogComponent;
  public buttons: any = [{
      buttonModel: {
          content: 'Close',
          cssClass: 'e-flat',
          isPrimary: true,
      },
      'click': () => {
          this.dialogInstance.hide();
      }
  }];
  
  public handleClick() {
      this.dialogInstance.show();
  }
  
  public componentDidMount() {
      document.onclick = (args: any) : void => {
          if(args.target.id === 'dialog-target') {
              this.dialogInstance.hide();
          }
      }
  }
  
  public render() {
    return (
    <div className="App" id='dialog-target'>
    <button className='e-control e-btn' id='targetButton1' role='button' onClick={this.handleClick = this.handleClick.bind(this)}>Open</button>
    <DialogComponent header='Delete Multiple Items' showCloseIcon={true} visible={true} animationSettings={this.settings}
      width='300px' buttons={this.buttons} closeOnEscape={true}
      content='Are you sure you want to permanently delete all of these items?' ref={dialog => this.dialogInstance = dialog!}
      target='#dialog-target'/>
    </div>);
  }
}
export default App;

```

{% endtab %}
