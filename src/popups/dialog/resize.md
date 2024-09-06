---
title: "React Dialog Resizing"
component: "Dialog"
description: "Explains about the resizeable dialog which allows changing its size dynamically."
---

# Resizing

The Dialog supports resizing feature. To resize the dialog, we have to select and resize it by using its handle (grip) or hovering on any of the edges or borders of the dialog within the sample container.

The resizable dialog can be created by setting the [enableResize](../api/dialog/#enableresize) property to true, which is used to change the size of a dialog dynamically and view its content with expanded mode. The [resizeHandles](../api/dialog/#resizehandles) property can also be configured for all the which directions in which the dialog should be resized. When you configure the target property along with the [enableResize](../api/dialog/#enableresize) property, the dialog can be resized within its specified target container.

{% tab template="dialog/getting-started", sourceFiles="app/App.tsx", compileJsx=true %}

```javascript
import { DialogComponent } from '@syncfusion/ej2-react-popups';
import * as React from "react";

class App extends React.Component<{}, {hideDialog: boolean;}> {  
  public buttons: any = [{
        buttonModel: {
            content: 'OK',
            cssClass: 'e-flat',
            isPrimary: true,
        },
        'click': () => {
            this.setState({ hideDialog: false })
        }
    },
    {
      buttonModel: {
          content: 'Cancel',
          cssClass: 'e-flat'
      },
      'click': () => {
          this.setState({ hideDialog: false })
      }
    }];

  constructor(props: {}) {
      super(props);
      this.state = {
          hideDialog : true
      };
  }
public handleClick() {
    this.setState({ hideDialog: true })
}

public dialogClose = () => {
    this.setState({ hideDialog: false })
}

public render() {
  return (
  <div className="App" id='dialog-target'>
      <button className='e-control e-btn' id='targetButton1' role='button' onClick={this.handleClick = this.handleClick.bind(this)}>Open</button>
      <DialogComponent width='250px' target='#dialog-target' visible = {this.state.hideDialog} close = {this.dialogClose} header='Dialog' enableResize={true} resizeHandles={['All']} allowDragging={true} showCloseIcon={true}  buttons={this.buttons}>
      This is a Dialog with drag enabled </DialogComponent>
  </div>);
}
}
export default App;

```

{% endtab %}
