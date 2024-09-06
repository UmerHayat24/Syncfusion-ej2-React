---
title: "Dynamically move input to edit mode"
component: "In-place Editor"
description: "Learn how to dynamically move input to edit mode in the Essential JS 2 React In-place Editor component."
---

# Dynamically move input to edit mode

At component initial load, if you want to open editor state without interacting In-place Editor input element, it can be achieved by configuring the [enableEditMode](../../api/inplace-editor/#enableeditmode) property to `true`.

In the following sample, editor opened at initial load and when toggling a checkbox, it will remove or open the editor.

{% tab template="in-place-editor/dynamic-edit", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ChangeEventArgs, CheckBoxComponent } from '@syncfusion/ej2-react-buttons';
import { InPlaceEditorComponent } from '@syncfusion/ej2-react-inplace-editor';
import * as React from 'react';
import './App.css';

class App extends React.Component<{},{}> {
  public inplaceEditorObj: InPlaceEditorComponent;
  public checkboxObj: CheckBoxComponent;

  public model = { placeholder: 'Enter some text' };

  public onChange(e: ChangeEventArgs): void {
    (this.inplaceEditorObj as any).enableEditMode = e.checked;
    this.inplaceEditorObj.dataBind();
  }

  public render() {
    return (
    <div id='container'>
        <table className="table-section">
            <tr>
                <td> EnableEditMode: </td>
                <td>
                  <CheckBoxComponent id='enable' label='Enable' checked={true} change={ this.onChange = this.onChange.bind(this) }/>
                </td>
            </tr>
            <tr>
                <td className="sample-td"> Enter your name: </td>
                <td className="sample-td">
                  <InPlaceEditorComponent ref={(text) => { this.inplaceEditorObj = text! }} id='dynamicEdit' mode='Inline' value='Andrew' enableEditMode={true} actionOnBlur='Ignore' model={this.model} />
                </td>
            </tr>
        </table>
     </div>
    );
  }
}

export default App;
```

{% endtab %}