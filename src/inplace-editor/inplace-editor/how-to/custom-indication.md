---
title: "Custom indication for unsaved value"
component: "In-place Editor"
description: "Learn how to add a custom indication to the unsaved value of the Essential JS2 React In-place Editor component."
---

# Add custom indication to unsaved value

You can add custom indication to unsaved input value by using the [actionSuccess](../../api/inplace-editor/#actionsuccess) event, when data not submitted to the server.

In this sample, the `actionSuccess` event configured and the [URL](../../api/inplace-editor/#url) property not included. Then submit button clicked, the current editor value saved into input and data sending to server action prevented due to the `URL` property not configured.

But `actionSuccess` event will trigger the handler function with `null` argument values. In handler function data property [primaryKey](../../api/inplace-editor/#primarykey) value checked, whether it empty or not. If it is empty custom class, added in the `e-value-wrapper` element to customize its styles.

> To send input value to local, set the `URL` property as empty.

{% tab template="in-place-editor/custom-indication", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { isNullOrUndefined as isNOU } from '@syncfusion/ej2-base';
import { ActionEventArgs, InPlaceEditorComponent } from '@syncfusion/ej2-react-inplace-editor';
import * as React from 'react';
import './App.css';

class App extends React.Component<{},{}> {
  public inplaceEditorObj: InPlaceEditorComponent;

  public model = { placeholder: 'Enter some text' };

  public actionSuccess(e: ActionEventArgs): void {
    const keyVal = 'PrimaryKey';
    const primeKey: string = e.data[keyVal];
    if (isNOU(primeKey) || primeKey === '') {
      ((document.querySelector('.e-editable-value') as any)).classList.add('e-send-error');
    }
  }

  public render() {
    return (
    <div id='container'>
        <span className="content-title"> Enter your name: </span>
        <InPlaceEditorComponent id='customtextbox' mode='Inline' value='Andrew' model={this.model} actionSuccess={ this.actionSuccess = this.actionSuccess.bind(this) } />
     </div>
    );
  }
}

export default App;
```

{% endtab %}