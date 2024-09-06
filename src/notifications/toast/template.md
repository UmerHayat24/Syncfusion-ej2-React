---
title: "React Toast Template"
component: "Toast"
description: "The Essential JS 2 Toast control template section explains how to customize the toast control as needed."
---

# Template

Template property can be given as the `HTML element` that is either a `string`  or a `query selector`.

The HTML element tag can be given as a string for the template property.

```typescript
template: "<div>Toast Content</div>"

```

The template property also allows getting template content through query `selector`. Here, element 'ID' attribute is specified in the template.

```typescript
template: "#Template"

```

{% tab template="toast/toast", sourceFiles="app/App.tsx", compileJsx=true  %}

```typescript
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
// import { DropDownListComponent } from '@syncfusion/ej2-react-dropdowns';
import { ToastComponent  } from '@syncfusion/ej2-react-notifications';
import * as React from "react";

class App extends React.Component<{}, {position: any, target: any, width: any}> {
  public toastInstance: ToastComponent;
  public position = { X: 'Right', Y: 'Bottom' };
  public template = (document.getElementById("template_toast_ele") as HTMLElement).innerHTML;

  public toastCreated(): void {
    this.toastInstance.show();
  }

  public toastShow() {
    this.toastInstance.show();
  }

  public render() {
    return (
      <div>
        <ButtonComponent cssClass="e-primary" id='template_toast' onClick={this.toastShow = this.toastShow.bind(this)}> Show Toast </ButtonComponent>
        <ToastComponent id='template_toast' ref={toast => this.toastInstance = toast!} template={this.template} position={this.position} extendedTimeout={0} timeOut='120000' created={this.toastCreated = this.toastCreated.bind(this)} />
      </div>
    );
  }
};
export default App;
```

{% endtab %}

## See Also

* [Add template dynamically](./how-to/add-dynamic-template/)