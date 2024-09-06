---
title: "Configuration"
component: "In-place Editor"
description: "Learn how to configure various renders, display modes, and configure the focus out actions in the Essential JS 2 React In-place Editor component."
---

# Configuration

## Rendering modes

This section explains the rendering modes supported by the In-place Editor. Possible rendering modes are given in below.

* Popup
* Inline

> By default, component will be rendered with `Popup` mode, when opening an editor.

* For `Popup` mode, editable container displays as like tooltip or popover above the element.

* For `Inline` mode, editable container will be displayed instead of the popup element. To render `Inline` mode while opening the editor, specify `mode` as `Inline`.

In the following sample, the In-place Editor renders with `Inline` mode. You can dynamically switch to another mode by changing the drop-down item value.

{% tab template="in-place-editor/modes", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { InPlaceEditorComponent, RenderMode } from '@syncfusion/ej2-react-inplace-editor';
import { DropDownListComponent , ChangeEventArgs } from '@syncfusion/ej2-react-dropdowns';
import * as React from 'react';import { ChangeEventArgs, DropDownListComponent } from '@syncfusion/ej2-react-dropdowns';
import { InPlaceEditorComponent, RenderMode } from '@syncfusion/ej2-react-inplace-editor';
import * as React from 'react';
import './App.css';

class App extends React.Component {
  public inplaceEditorObj: InPlaceEditorComponent;
  public dropdownObj: DropDownListComponent;

  public modeData = ['Inline', 'Popup'];
  public model = { placeholder: 'Enter some text' };

  public onChange(e: ChangeEventArgs): void {
    const mode: RenderMode = e.itemData.value as RenderMode;
    this.inplaceEditorObj.mode = mode;
    this.inplaceEditorObj.dataBind();
  }

  public render() {
    return (
    <div id='container'>
         <table className="table-section">
         <tbody>
             <tr>
                <td> Mode: </td>
                <td>
                    <DropDownListComponent id='dropDown' dataSource= {this.modeData} width='auto' change={ this.onChange = this.onChange.bind(this) } value='Inline' placeholder='Select Mode'/>
                </td>
             </tr>
             <tr>
                 <td  className="sample-td"> Enter your name: </td>
                 <td  className="sample-td">
                    <InPlaceEditorComponent ref={(text) => { this.inplaceEditorObj = text! }} id='element' mode='Inline' value='Andrew' model={this.model} />
                 </td>
              </tr>
              </tbody>
           </table>
     </div>
    );
  }
}
export default App;
```

{% endtab %}

### Pop-up customization

In-place Editor popup mode can be customized by using the [title](../api/inplace-editor/popupSettings/#title) and [model](../api/inplace-editor/popupSettings/#model) properties in [popupSettings](../api/inplace-editor/popupSettings/) API.

Popup mode rendered by using the Essential JS2 React Tooltip component, so you can use tooltip properties and events to customize the behavior of popup via the [model](../api/inplace-editor/popupSettings/#model) property of [popupSettings](../api/inplace-editor/popupSettings/) API.

> For more details, refer the tooltip documentation [section](../tooltip/).

In the following sample, popup [title](../api/inplace-editor/popupSettings/#title) and [position](../api/tooltip/#position) customized using the [popupSettings](../api/inplace-editor/popupSettings/) property. All possible tooltip position data configured in the drop-down, if we change drop down item, selected value bound to [model](../api/inplace-editor/popupSettings/#model) property and applied it to [Tooltip](../tooltip/) component. `Tooltip` have following position options.

* TopLeft
* TopCenter
* TopRight
* BottomLeft
* BottomCenter
* BottomRight
* LeftTop
* LeftCenter
* LeftBottom
* RightTop
* RightCenter
* RightBottom

{% tab template="in-place-editor/popup", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ChangeEventArgs, DropDownListComponent } from '@syncfusion/ej2-react-dropdowns';
import { InPlaceEditorComponent } from '@syncfusion/ej2-react-inplace-editor';
import * as React from 'react';
import './App.css';

class App extends React.Component {
  public inplaceEditorObj: InPlaceEditorComponent;
  public dropdownObj: DropDownListComponent;

  public positionData = ['TopLeft', 'TopCenter', 'TopRight', 'BottomLeft', 'BottomCenter', 'BottomRight', 'LeftTop', 'LeftCenter', 'LeftBottom', 'RightTop', 'RightCenter', 'RightBottom'];
  public model = { placeholder: 'Enter some text' };
  public popupSettings = { title: 'Enter name', model: { position: 'BottomCenter' } }

  public onChange(e: ChangeEventArgs): void {
    (this.inplaceEditorObj as any).popupSettings.model.position = e.value;
    this.inplaceEditorObj.dataBind();
  }

  public render() {
    return (
    <div id='container'>
         <table className="table-section">
          <tbody>
              <tr>
                <td> Position: </td>
                <td>
                  <DropDownListComponent id='dropDown' value='BottomCenter' dataSource= {this.positionData} placeholder='Select a position' popupHeight='150px' change={ this.onChange = this.onChange.bind(this) } />
                </td>
              </tr>
              <tr>
                  <td  className="edit-heading sample-td"> Enter your name: </td>
                  <td  className="sample-td">
                    <InPlaceEditorComponent ref={(text) => { this.inplaceEditorObj = text! }} id='element' mode='Popup' value='Andrew' model={this.model} popupSettings={this.popupSettings} />
                  </td>
              </tr>
            </tbody>
           </table>
     </div>
    );
  }
}
export default App;
```

{% endtab %}

## Event actions for editing

The event action of the editor that enable in the edit mode based on the [editableOn](../api/inplace-editor/#editableon) property, by default `Click` is assigned, the following options are also supported.

* **[Click](../api/inplace-editor/editableType/)**:  The editor will be opened as single click actions.
* **[DblClick](../api/inplace-editor/editableType/)**: The editor will be opened as double-click actions and it is not applicable for edit icon.
* **[EditIconClick](../api/inplace-editor/editableType/)**: Disables the editing of event action of input and allows user to edit only through edit icon.

> In-place Editor get focus by pressing the `tab` key from previous focusable DOM element and then by pressing `enter` key, the editor will be opened.

In the following sample, when switching drop-down item, the selected value assigned to the `editableOn` property. If you changed to `DblClick`, the editor will open when making a double click on the input.

{% tab template="in-place-editor/editable-on", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ChangeEventArgs, DropDownListComponent } from '@syncfusion/ej2-react-dropdowns';
import { EditableType, InPlaceEditorComponent } from '@syncfusion/ej2-react-inplace-editor';
import * as React from 'react';
import './App.css';

class App extends React.Component {
  public inplaceEditorObj: InPlaceEditorComponent;
  public dropdownObj: DropDownListComponent;

  public editableOnData = ['Click', 'DblClick', 'EditIconClick'];
  public model = { placeholder: 'Enter some text' };

  public onChange(e: ChangeEventArgs): void {
    const editType: EditableType = e.itemData.value as EditableType;
    this.inplaceEditorObj.editableOn = editType;
    this.inplaceEditorObj.dataBind();
  }

  public render() {
    return (
    <div id='container'>
         <table className="table-section">
          <tbody>
            <tr>
                <td> EditableOn: </td>
                <td>
                    <DropDownListComponent id='dropDown' dataSource= {this.editableOnData} width='auto' value='Click' change={ this.onChange = this.onChange.bind(this) } placeholder='Select edit type'/>
                </td>
            </tr>
            <tr>
                <td  className="sample-td"> Enter your name: </td>
                <td  className="sample-td">
                    <InPlaceEditorComponent ref={(text) => { this.inplaceEditorObj = text! }} id='element' mode='Inline' value='Andrew' model={this.model} />
                </td>
              </tr>
            </tbody>
           </table>
     </div>
    );
  }
}
export default App;
```

{% endtab %}

## Action on focus out

Action to be performed when the user clicks outside the container, that means focusing out of editable content and it can be handled by the [actionOnBlur](../api/inplace-editor/#actiononblur) property, by default `Submit` assigned. It also has the following options.

* **[Cancel](../api/inplace-editor/actionBlur/)**: Cancels the editing and resets the old content.
* **[Submit](../api/inplace-editor/actionBlur/)**: Submits the edited content to the server.
* **[Ignore](../api/inplace-editor/actionBlur/)**: No action is performed with this type and allows to edit multiple editors.

In the following sample, when switching drop-down item, the selected value assigned to the `actionOnBlur` property.

{% tab template="in-place-editor/action-on-blur", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ChangeEventArgs, DropDownListComponent } from '@syncfusion/ej2-react-dropdowns';
import { ActionBlur, InPlaceEditorComponent } from '@syncfusion/ej2-react-inplace-editor';
import * as React from 'react';
import './App.css';

class App extends React.Component {
  public inplaceEditorObj: InPlaceEditorComponent;
  public dropdownObj: DropDownListComponent;

  public blurActionData = ['Submit', 'Cancel', 'Ignore'];
  public model = { placeholder: 'Enter some text' };

  public onChange(e: ChangeEventArgs): void {
    const editType: ActionBlur = e.itemData.value as ActionBlur;
    this.inplaceEditorObj.actionOnBlur = editType;
    this.inplaceEditorObj.dataBind();
  }

  public render() {
    return (
    <div id='container'>
         <table className="table-section">
            <tbody>
             <tr>
                <td> ActionOnBlur: </td>
                <td>
                    <DropDownListComponent id='dropDown' dataSource= {this.blurActionData} width='auto' value='Submit' change={ this.onChange = this.onChange.bind(this) } placeholder='Select blur action'/>
                </td>
             </tr>
             <tr>
                 <td  className="sample-td"> Enter your name: </td>
                 <td  className="sample-td">
                    <InPlaceEditorComponent ref={(text) => { this.inplaceEditorObj = text! }} id='element' mode='Inline' value='Andrew' model={this.model} />
                 </td>
              </tr>
            </tbody>
           </table>
     </div>
    );
  }
}
export default App;
```

{% endtab %}

## Display modes

By default, In-place Editor input element highlighted with a dotted underline. To remove dotted underline from input element, add `data-underline="false"` attribute at In-place Editor root element.

In the following sample shows intractable and normal display modes with different samples.

{% tab template="in-place-editor/under-line", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { InPlaceEditorComponent } from '@syncfusion/ej2-react-inplace-editor';
import * as React from 'react';
import './App.css';

class App extends React.Component {
  public model = { placeholder: 'Enter some text' };

  public render() {
    return (
    <div id='container'>
         <h4>Example of data-underline attribute</h4>
         <table className="table-section">
            <tbody>
             <tr>
                <td className="col-lg-6 col-md-6 col-sm-6 col-xs-6 control-title"> Intractable UI </td>
                <td className="col-lg-6 col-md-6 col-sm-6 col-xs-6">
                    <InPlaceEditorComponent id='default' mode='Inline' value='Andrew' model={this.model} />
                </td>
             </tr>
             <tr>
                 <td className="col-lg-6 col-md-6 col-sm-6 col-xs-6 control-title"> Normal UI </td>
                 <td className="col-lg-6 col-md-6 col-sm-6 col-xs-6">
                    <InPlaceEditorComponent id='element' data-underline='false' mode='Inline' value='Andrew' model={this.model} />
                 </td>
              </tr>
              </tbody>
           </table>
     </div>
    );
  }
}
export default App;
```

{% endtab %}

## See Also

* [Disable the editor](./how-to/disable-edit-mode/)
* [Animate the editor during popup mode](./how-to/custom-animation/)