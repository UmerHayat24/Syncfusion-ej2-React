---
title: "Render a React Dialog using utility functions"
component: "Dialog"
description: "Covers customization features such as load content to the dialog from external sources, built-in alert, and confirmation model dialog."
---

# Render a dialog using utility functions

The dialog component provides built-in utility functions to render the alert and confirm dialogs with the minimal code.
The following options are used as an argument on calling the utility functions:

| Options   | Description |
|-----------|-------------|
| title | Specifies the title of dialog like the [`header`](../../api/dialog/#header) property.|
| content | Specifies the value that can be displayed in dialog's content area like the [`content`](../../api/dialog/#content) property. |
| isModal | Specifies the Boolean value whether the dialog can be displayed as modal or non-modal. For more details, refer to the [`isModal`](../../api/dialog/#ismodal) property.|
| position | Specifies the value where the alert or confirm dialog is positioned within the document. For more details, refer to the [`position`](../../api/dialog/#position) property { X: ‘center’, Y: ‘center’}|
| okButton | Configures the `OK button` that contains button properties with the click events. `okButton:{ icon:'prefix icon to the button', cssClass:'custom class to the button', click: 'action for OK button click', text: 'Yes' // <-- Default value is 'OK' }`|
| cancelButton | Configures the `Cancel button` that contains button properties with the click events. `cancelButton:{ icon:'prefix icon to the button', cssClass:'custom class to the button', click: 'action for ‘Cancel’ button click', text: 'No' // <-- Default value is 'Cancel'}`|
|isDraggable|Specifies the value whether the alert or confirm dialog can be dragged by the user.|
| showCloseIcon | When set to true, the close icon is shown in the dialog component. |
|closeOnEscape|When set to true, you can close the dialog by pressing ESC key.|
| animationSettings |Specifies the animation settings of the dialog component. |
| cssClass |Specifies the CSS class name that can be appended to the dialog. |
| zIndex |Specifies the order of the dialog, that is displayed in front or behind of another component. |
| open |Event which is triggered after the dialog is opened. |
| Close |Event which is triggered after the dialog is closed. |

## Alert dialog

An alert dialog box is used to display warning like messages to the users. Use the following code to render a simple alert dialog in an application.

{% tab template="dialog/dialog-utility-alert", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { DialogUtility } from '@syncfusion/ej2-popups';
import * as React from "react";
import './App.css';

class App extends React.Component<{}, {}> {
  public buttonClick(): void {
    DialogUtility.alert('This is an Alert Dialog!');
}
public render() {
return (
  <button className="e-control e-btn" onClick={this.buttonClick} id="targetButton" role="button">Open Alert Dialog</button>);
}
}
export default App;

```

{% endtab %}

### Render an alert dialog with options

{% tab template="dialog/dialog-utility-alert1", compileJsx=true %}

```typescript
import { DialogUtility } from '@syncfusion/ej2-popups';
import * as React from "react";
import './App.css';

class App extends React.Component<{}, {}> {
  public buttonClick(): void {
    DialogUtility.alert({
        animationSettings: { effect: 'Zoom' },
        closeOnEscape: true,
        content: "This is an Alert Dialog!",
        okButton: {  text: 'OK', click: this.okClick.bind(this) },
        showCloseIcon: true,
        title: 'Alert Dialog'
    });
}
public okClick(): void {
    alert('you clicked OK button');
}
public render() {
    return (
    <button className="e-control e-btn" onClick={this.buttonClick = this.buttonClick.bind(this)} id="targetButton" role="button">Open Alert Dialog</button>);
}
}
export default App;

```

{% endtab %}

## Confirm dialog

A confirm dialog displays a specified message along with ‘OK’ and ‘Cancel’ button.

{% tab template="dialog/dialog-utility-confirm", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { DialogUtility } from '@syncfusion/ej2-popups';
import * as React from "react";
import './App.css';

class App extends React.Component<{}, {}> {
  public buttonClick(): void {
    DialogUtility.confirm('This is a Confirmation Dialog!');
}
  public render() {
    return (
    <button className="e-control e-btn" onClick={this.buttonClick = this.buttonClick.bind(this)} id="targetButton" role="button">Open Confirm Dialog</button>
    );
  }
}
export default App;

```

{% endtab %}

### Render a confirmation dialog with options

{% tab template="dialog/dialog-utility-confirm1", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { DialogUtility } from '@syncfusion/ej2-popups';
import * as React from "react";
import './App.css';

class App extends React.Component<{}, {}> {
  public buttonClick(): void {
    DialogUtility.confirm({
      animationSettings: { effect: 'Zoom' },
      cancelButton: {  text: 'Cancel', click: this.cancelClick.bind(this) },
      closeOnEscape: true,
      content: "This is a Confirmation Dialog!",
      okButton: {  text: 'OK', click: this.okClick.bind(this) },
      showCloseIcon: true,
      title: ' Confirmation Dialog',
    });
  }

  public okClick(): void {
    alert('you clicked OK button');
  }

  public cancelClick(): void {
    alert('you clicked Cancel button');
  }
  public render() {
  return (
    <button className="e-control e-btn" onClick={this.buttonClick = this.buttonClick.bind(this)} id="targetButton" role="button">Open Confirm Dialog</button>
  );
  }
  }
export default App;

```

{% endtab %}