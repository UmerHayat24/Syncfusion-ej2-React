---
title: "Position the Dialog on center of the page on scrolling"
component: "Dialog"
description: "Covers customization features such as load content to the dialog from external sources, built-in alert, and confirmation model dialog."
---

# Position the Dialog on center of the page on scrolling

By default, when scroll the page/container Dialog also scrolled along with the page/container.
When a user expects to display the Dialog in the same position without scrolling achieving this in
sample level as like below. Here added 'e-fixed' class to Dialog element and prevent the scrolling.

{% tab template="dialog/scrollposition", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript

import { DialogComponent } from '@syncfusion/ej2-react-popups';
import * as React from "react";
import './App.css';

class App extends React.Component<{}, {}> {
  public dialogInstance: DialogComponent;
  public handleClick = () => {
      this.dialogInstance.cssClass = 'e-fixed';
  }

  public render() {
    return (
    <div className="App" id='dialog-target'>
    <DialogComponent header='Dialog' width='250px' ref={dialog => this.dialogInstance = dialog!}
    target='#dialog-target' closeOnEscape={false}>
      <button className="e-control e-btn" id="targetButton" role="button" onClick={this.handleClick = this.handleClick}>Prevent Dialog Scroll</button>
    </DialogComponent>
    </div>
    );
  }
}
export default App;

```

{% endtab %}