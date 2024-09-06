---
title: "React Toast Action Buttons"
component: "Toast"
description: "Toast control action button section explains how to add button control inside the toast control using button properties."
---

# Action Buttons

You can include action Buttons into toast by adding [`buttons`](../../api/toast#buttons) property. You can bind collections of Essential JS 2 Button Model to `model` property inside buttons property, You can also include  click event callback function, for each button.

{% tab template="toast/toast", sourceFiles="app/App.tsx", compileJsx=true  %}

```typescript
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { ToastComponent  } from '@syncfusion/ej2-react-notifications';
import * as React from "react";

class App extends React.Component<{}, {}> {
  public toastInstance: ToastComponent;
  public position = { X: "Right", Y: "Bottom" };
  private buttons: object[] = [
    { model: { content: "Ignore" } },
    { model: { content: "reply" } }
  ];

  public toastShow() {
    this.toastInstance.show();
  }

  public toastCreated(): void {
    this.toastInstance.show();
  }

  public contentTemplate() {
    return <p><img src='./laura.png'/></p>;
  }

  public render() {
    return (
      <div>
        <ButtonComponent cssClass="e-primary" onClick={this.toastShow = this.toastShow.bind(this)}> Show Toast </ButtonComponent>
        <ToastComponent ref={toast => this.toastInstance = toast!} title="Anjolie Stokes" content={this.contentTemplate} position={this.position} width='230' height='250' buttons={this.buttons} created={this.toastCreated = this.toastCreated.bind(this)} />
      </div>
    );
  }
};
export default App;
```

{% endtab %}

## See Also

* [Configuring options](./config/)