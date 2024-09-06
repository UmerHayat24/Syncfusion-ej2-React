---
title: "Custom animation for popup mode"
component: "In-place Editor"
description: "Learn how to configure custom animation for popup and customize it dynamically in the Essential JS 2 React In-place Editor component."
---

# Set custom animation for popup mode

In popup mode, the In-place Editor rendered with the Essential JS 2 React `Tooltip` component. You can use tooltip properties and events to customize the popup by configure properties into the [model](../../api/inplace-editor/popupSettings/#model) property inside the [popupSettings](../../api/inplace-editor/popupSettings/) API.

In the following sample, popup animation can be customized by passing animation effect using the `model` property and the dynamic animation effect changes configured from the Essential JS 2 React `DropDownList` component `change` event.

{% tab template="in-place-editor/custom-animation", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ChangeEventArgs, DropDownListComponent } from '@syncfusion/ej2-react-dropdowns';
import { InPlaceEditorComponent } from '@syncfusion/ej2-react-inplace-editor';
import * as React from 'react';
import './App.css';

class App extends React.Component<{},{}> {
  public inplaceEditorObj: InPlaceEditorComponent;
  public dropdownObj: DropDownListComponent;

  public openAnimateData = ['None', 'FadeIn', 'FadeZoomIn', 'ZoomIn'];
  public model = { placeholder: 'Enter some text' };
  public popupSettings = { model: { animation: { open: { effect: 'ZoomIn', duration: 1000, delay: 0 } } } };

  public onChange(e: ChangeEventArgs): void {
    (this.inplaceEditorObj as any).popupSettings.model.animation.open.effect = e.value;
    this.inplaceEditorObj.dataBind();
  }

  public render() {
    return (
    <div id='container'>
        <table className="table-section">
          <tbody>
            <tr>
                <td> Open Animation: </td>
                <td>
                  <DropDownListComponent id='openDropDown' value='ZoomIn' dataSource= {this.openAnimateData} placeholder='Select a animate type' popupHeight='150px' change={ this.onChange=this.onChange.bind(this) } />
                </td>
            </tr>
            <tr>
                <td  className="sample-td"> Enter your name: </td>
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