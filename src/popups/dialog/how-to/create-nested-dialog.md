---
title: "Create Nested Dialog"
component: "Dialog"
description: "Covers customization features such as load content to the dialog from external sources, built-in alert, and confirmation model dialog."
---

# Create Nested Dialog

A Dialog can be nested within another Dialog. The below sample contains parent and child Dialog (inner Dialog).

**Step 1**:

Render two Dialog components in a page.

**Step 2**:

Set the inner Dialog target as `.outerDialog`.

{% tab template="dialog/nested", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { DialogComponent } from '@syncfusion/ej2-react-popups';
import * as React from "react";
import './App.css';

class App extends React.Component<{}, {}> {
  public dialogInstance: DialogComponent;
  public innerDialogInstance: DialogComponent;

  public handleClick() {
      this.dialogInstance.show();
  }

  public nestedbuttonClick = () => {
      this.innerDialogInstance.show();
  }
  
  public render() {
      const effect: any = { effect: 'None' };
    return (
    <div className="App" id='dialog-target'>
      <button className='e-control e-btn' id='targetButton1' role='button' onClick={this.handleClick = this.handleClick.bind(this)}>Open</button>
      <DialogComponent header='Outer Dialog' cssClass="outerDialog" showCloseIcon={true} width='400px' height='300px'
          ref={dialog => this.dialogInstance = dialog!} target='#dialog-target' closeOnEscape={false} animationSettings={effect}>
          <button className="e-control e-btn" id="innerButton" onClick={this.nestedbuttonClick} role="button" >Open InnerDialog</button>
      </DialogComponent>
  
      <DialogComponent id='innerDialog' header='Inner Dialog' showCloseIcon={true} width='250px' height='150px'
      ref={dialog => this.innerDialogInstance = dialog!}
      animationSettings={effect} closeOnEscape={false} target='.outerDialog'> This is a Nested Dialog </DialogComponent>
    </div>);
  }
}
export default App;

```

{% endtab %}