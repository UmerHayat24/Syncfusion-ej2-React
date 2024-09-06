---
title: "Customize the dialog appearance"
component: "Dialog"
description: "Covers customization features such as load content to the dialog from external sources, built-in alert, and confirmation model dialog."
---

# Customize the dialog appearance

You can customize the dialog appearance by providing dialog template as string or HTML element to the [content](../../api/dialog/#content) property. In the following sample, dialog is customized as error window appearance.

{% tab template="dialog/dlg-appearance", sourceFiles="app/App.tsx", compileJsx=true %}

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

public render() {
  return (
  <div className="App" id='dialog-target'>
      <button className='e-control e-btn' id='targetButton1' role='button' onClick={this.handleClick = this.handleClick.bind(this)}>Open</button>

      <DialogComponent id="dlg-button"
        header='File and Folder Rename' showCloseIcon={true}
        width='400px' buttons={this.buttons} animationSettings={this.settings}
        closeOnEscape={true}  ref={dialog => this.dialogInstance = dialog!}
        target='#dialog-target'>
        <div>
          <div className = 'dialog-content'>
          <div className='msg-wrapper  col-lg-12'>
              <span className='e-icons close-icon col-lg-2'/>
              <span  className='error-msg col-lg-10'>Can not rename 'pictures' because a file or folder with that name already exists </span>
              </div>
              <div className='error-detail col-lg-8'>
              <span>Specify a different name</span>
              </div>
          </div>
          </div>
      </DialogComponent>
  </div>);
}
}
export default App;

```

{% endtab %}