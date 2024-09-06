---
title: "Center the dialog based on current scroll position"
component: "Dialog"
description: "This section explains how to center the dialog based on the current scroll position."
---

# Center the dialog based on the current scroll position

The dialog is always centered based on the target container. If the target is not specified, then the dialog will be rendered based on its body and centered in the position of the current viewpoint.

In the following sample, the model dialog is centered based on its current scroll position of the page.

{% tab template="dialog/center-the-dialog", tab compileJsx=true %}

```typescript

import { DialogComponent } from '@syncfusion/ej2-react-popups';
import * as React from "react";
import './App.css';

class App extends React.Component {
  constructor(props) {
    super(props);
    this.onOverlayClick = () => {
      this.setState({ hideDialog: false });
    };
    this.dialogClose = () => {
      this.setState({ hideDialog: false });
    };
    this.state = {
      hideDialog: true
    };
  }
  handleClick() {
    this.setState({ hideDialog: true });
  }
  render() {
    return (
      <div className="App" >
        <button
          className="e-control e-btn"
          id="targetButton1"
          role="button"
          onClick={(this.handleClick = this.handleClick.bind(this))}
        >
          Open
        </button>

        <DialogComponent
          width="250px"
          isModal={true}
          visible={this.state.hideDialog}
          close={this.dialogClose}
          overlayClick={this.onOverlayClick}
        >
          This is a modal Dialog{" "}
        </DialogComponent>
      </div>
    );
  }
}
export default App;

```

{% endtab %}