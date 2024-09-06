---
title: "Buttons"
component: "In-place Editor"
description: "Learn how to show or hide buttons, customize its behavior and the appearance in the Essential JS2 React In-place Editor component."
---

# Buttons

The In-place Editor has an action for save and cancel using buttons. The [saveButton](../api/inplace-editor/#savebutton) and [cancelButton](../api/inplace-editor/#cancelbutton) properties accepts the [ButtonModel](../api/button/buttonModel/) objects for customizing the save and cancel button properties.

Buttons can be show or hide by setting a boolean value to the [showButtons](../api/inplace-editor/#showbuttons) property.

> Without buttons value actions will be performed by the following way.

* **[actionOnBlur](../api/inplace-editor/#actiononblur)**: By clicking out-side of the editor component it will get focus out and perform action based on this property value.
* **[submitOnEnter](../api/inplace-editor/#submitonenter)**: Pressing `Enter` key it performs the submit action, when this property set to `true`.

In the following sample, the [content](../api/button#content) and [cssClass](../api/button#cssclass) properties of `Button` value assigned to the [saveButton](../api/inplace-editor/#savebutton) and [cancelButton](../api/inplace-editor/#cancelbutton) properties to customize its appearance. Also check or uncheck a checkbox buttons render or removed from the editor.

To restrict either save or cancel button rendering into a DOM, simply pass empty object `{}` in the  `saveButton` or `cancelButton` properties.

> For more details about buttons, refer this documentation [section](../button/).

{% tab template="in-place-editor/show-buttons", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ChangeEventArgs, CheckBoxComponent  } from '@syncfusion/ej2-react-buttons';
import { InPlaceEditorComponent } from '@syncfusion/ej2-react-inplace-editor';
import * as React from "react";
import './App.css';

class App extends React.Component<{}, {}> {
  public inplaceEditorObj: InPlaceEditorComponent;
  public checkboxObj: CheckBoxComponent;

  public model = { placeholder: 'Enter some text' };
  public saveButton = { content: 'Ok', cssClass: 'e-outline' };
  public cancelButton = { content: 'Cancel', cssClass: 'e-outline' };

  public onChange(e: ChangeEventArgs): void {
    (this.inplaceEditorObj as any).showButtons = e.checked;
    this.inplaceEditorObj.dataBind();
  }

  public render() {
    return (
    <div id='container'>
         <table className="table-section">
         <tbody>
             <tr>
                <td> ShowButtons: </td>
                <td>
                    <CheckBoxComponent id='enableBtn' checked={true} label='Show' change={ this.onChange = this.onChange.bind(this)  } />
                </td>
             </tr>
             <tr>
                 <td  className="sample-td"> Enter your name: </td>
                 <td  className="sample-td">
                    <InPlaceEditorComponent ref={(text) => { this.inplaceEditorObj = text! }} id='element' mode='Inline' value='Andrew' model={this.model} saveButton={this.saveButton} cancelButton={this.cancelButton}/>
                 </td>
              </tr>
            </tbody>
           </table>
     </div>
    );
  }
};
export default App;
```

{% endtab %}

## See Also

* [In-place editor buttons](./how-to/dynamic-edit-mode/)