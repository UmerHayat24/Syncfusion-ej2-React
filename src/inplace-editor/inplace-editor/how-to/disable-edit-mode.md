---
title: "Disable the edit mode specifically"
component: "In-place Editor"
description: "Learn how to disable the edit mode in the Essential JS 2 React In-place Editor component."
---

# Disable the edit mode specifically

The edit mode of In-place Editor can be disabled by setting the [disabled](../../api/inplace-editor/#disabled) property value to `true`. In the following sample, when check or uncheck the checkbox, In-place Editor component will disable or enable the edit mode.

{% tab template="in-place-editor/disable-edit", sourceFiles="app/App.tsx", compileJsx=true %}

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
    (this.inplaceEditorObj as any).disabled = e.checked;
    this.inplaceEditorObj.dataBind();
  }

  public render() {
    return (
    <div id='container'>
        <table className="table-section">
            <tr>
                <td> Disabled: </td>
                <td>
                  <CheckBoxComponent id='enable' label='Disable' checked={false} change={ this.onChange=this.onChange.bind(this) }/>
                </td>
            </tr>
            <tr>
                <td className="sample-td"> Enter your name: </td>
                <td className="sample-td">
                  <InPlaceEditorComponent ref={(text) => { this.inplaceEditorObj = text! }} id='disableEdit' mode='Inline' value='Andrew' model={this.model} />
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