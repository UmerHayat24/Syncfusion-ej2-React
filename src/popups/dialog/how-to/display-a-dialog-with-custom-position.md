---
title: "Display a dialog with custom position"
component: "Dialog"
description: "Covers customization features such as load content to the dialog from external sources, built-in alert, and confirmation model dialog."
---

# Display a dialog with custom position

By default, the dialog is displayed in the center of the target container. The dialog position can be set using the position property by providing custom X and Y coordinates.
The dialog can be positioned inside the target based on the given X and Y values.

{% tab template="dialog/dlg-position", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript

import { DialogComponent } from '@syncfusion/ej2-react-popups';
import * as React from "react";
import './App.css';

class App extends React.Component<{}, {}> {
  public render() {
    const firstPosition: any = { X: 160, Y: 14 };
    const secondPosition: any = { X: 160, Y: 240 };
    const effect: any = { effect: 'None' };
  return (
  <div className="App" id='dialog-target'>
      <DialogComponent id='firstDialog' header='Position-01' visible={true}
      width='360px' height='120px' target='#dialog-target'
      closeOnEscape={false} animationSettings={effect} position={firstPosition}
      >
     The dialog is positioned at X: 160, Y: 14 coordinates </DialogComponent>

      <DialogComponent id='secondDialog' header='Position-02' visible={true}
      width='360px' height='120px' target='#dialog-target'
      closeOnEscape={false} animationSettings={effect} position={secondPosition}
      >
     The dialog is positioned at X: 160, Y: 240 coordinates </DialogComponent>
  </div>);
}
}
export default App;

```

{% endtab %}