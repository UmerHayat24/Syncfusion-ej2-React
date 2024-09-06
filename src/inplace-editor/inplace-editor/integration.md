---
title: "Integrate HTML5 components"
component: "In-place Editor"
description: "Learn how to configure template and integrate HTML5 components, get and pass a modified value to the server in the Essential JS2 React In-place Editor component."
---

# Integrate HTML5 components (Template)

The In-place Editor supports adding HTML5 input components using the [template](../api/inplace-editor/#template) property. The Template property can be given as either a `string` or a `query selector`.

## As a string

The HTML element tag can be given as a string for the template property. Here, the input is rendered as an HTML template.

```typescript
template: "<div><input type='text' id='name'></input></div>"

```

## As a selector

The template property also allows getting template content through query `selector`. Here, the input wrapper element 'ID' attribute is specified in the template.

```typescript
template: "#date"

```

Template mode, the `value` property not handled by the In-place Editor component. So, before sending a value to the server, you need to modify at [actionBegin](../api/inplace-editor/#actionbegin) event, otherwise, an empty string will pass. In the following template sample, before submitting a data to the server, event argument and [value](../api/inplace-editor/#value) property content updated in the `actionBegin` event handler.

{% tab template="in-place-editor/html-template", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ActionBeginEventArgs, InPlaceEditorComponent } from '@syncfusion/ej2-react-inplace-editor';
import * as React from 'react';
import './App.css';

class App extends React.Component<{},{}> {
  public inVal: string = '2018-05-23';
  public inplaceEditorObj: InPlaceEditorComponent;
  public actionBegin(e: ActionBeginEventArgs): void {
    const value: string = (this.inplaceEditorObj.element.querySelector('#date') as any).value;
    this.inplaceEditorObj.value = value;
    (e as any).value = value;
  }
  public render() {
    return (
      <div>
        <div id='container'>
            <span className="content-title"> Select date: </span>
            <InPlaceEditorComponent ref={(text) => { this.inplaceEditorObj = text! }} id='datepicker' mode='Inline' template='#date' value='2018-05-23' actionBegin={ this.actionBegin = this.actionBegin.bind(this) } />
        </div>
        <div id='html-template' style={ { display: "none" } }>
            <input id="date" defaultValue= { this.inVal } type="date" />
        </div>
     </div>
    );
  }
}

export default App;
```

{% endtab %}