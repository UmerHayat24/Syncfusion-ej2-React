---
title: "List of components"
component: "In-place Editor"
description: "Learn supported built-in, injectable components, and its model configuration for the Essential JS 2 React In-place Editor component."
---

# List of components

In-place Editor renders, various components based on [type](../api/inplace-editor/#type) property and it have built-in, injectable components. To use injectable components need to inject required modules into `In-place Editor`. By default `type` property set as `Text` and render the `TextBox`.

Below table explains Injectable components module name and Built-in components and  their types.

| **Injectable Components** | **Built in Components** |
|-----------------------|---------------------|
| [AutoComplete](../auto-complete/)  (`AutoComplete`)        | [TextBox](../textbox/)  (`Text`)             |
| [ComboBox](../combo-box/)  (`ComboBox`)              | [DatePicker](../datepicker/)  (`Date`)        |
| [MultiSelect](../multi-select/)   (`MultiSelect`)        | [DateTimePicker](../datetimepicker/)   (`DateTime`)     |
| [TimePicker](../timepicker/)   (`Time`)         | [DropDownList](../drop-down-list/)  (`DropDownList`)      |
| [DateRangePicker](../daterangepicker/)   (`DateRange`)       | [MaskedTextBox](../maskedtextbox/)   (`Mask`)      |
| [Slider](../slider/)   (`Slider`)             | [NumericTextBox](../numerictextbox/)   (`Numeric`)    |
| [Rte](../rich-text-editor/)     (`RTE`)              |                     |
| [ColorPicker](../color-picker/)    (`Color`)       |                     |

In the below sample, built-in and injectable based In-place Editor components are rendered.

{% tab template="in-place-editor/components", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { AutoComplete, ColorPicker, ComboBox, Inject, InPlaceEditorComponent } from '@syncfusion/ej2-react-inplace-editor';
import { DateRangePicker, MultiSelect, Rte, Slider, TimePicker } from '@syncfusion/ej2-react-inplace-editor';
import * as React from 'react';
import './App.css';

class App extends React.Component<{}, {}> {
  public frameWorkList = ['Android', 'JavaScript', 'jQuery', 'TypeScript', 'Angular', 'React', 'Vue', 'Ionic'];
  public dateModel = { placeholder: 'Select date' };
  public dateValue = new Date('11/23/2018');
  public dateTimeValue = new Date('11/23/2018 12:30 PM');
  public dropdownModel = { dataSource: this.frameWorkList, placeholder: 'Select frameworks' };
  public maskModel = { mask: '000-000-000' };
  public numericModel = { placeholder: 'Enter number' };
  public textboxModel = { placeholder: 'Enter some text' };
  public dateRangePickerValue = [new Date('11/12/2018'), new Date('11/15/2018')];
  public rteModel = { placeholder: 'Enter your content here' };

  public render() {
    return (
    <div id='container'>
        <h3> Built-in components </h3>
        <table className="table-section">
        <tbody>
            <tr>
                <td className="col-lg-6 col-md-6 col-sm-6 col-xs-6 control-title"> DatePicker </td>
                <td className="col-lg-6 col-md-6 col-sm-6 col-xs-6">
                    <InPlaceEditorComponent id='date' mode='Inline' type='Date' value={this.dateValue} model={this.dateModel}/>
                </td>
            </tr>
            <tr>
                <td className="col-lg-6 col-md-6 col-sm-6 col-xs-6 control-title"> DateTimePicker </td>
                <td className="col-lg-6 col-md-6 col-sm-6 col-xs-6">
                    <InPlaceEditorComponent id='dateTime' mode='Inline' type='DateTime' value={this.dateTimeValue} model={this.dateModel}/>
                </td>
            </tr>
            <tr>
                <td className="col-lg-6 col-md-6 col-sm-6 col-xs-6 control-title"> DropDownList </td>
                <td className="col-lg-6 col-md-6 col-sm-6 col-xs-6">
                    <InPlaceEditorComponent id='dropDowns' mode='Inline' type='DropDownList' value='Android' model={this.dropdownModel}/>
                </td>
            </tr>
            <tr>
                <td className="col-lg-6 col-md-6 col-sm-6 col-xs-6 control-title"> MaskedTextBox </td>
                <td className="col-lg-6 col-md-6 col-sm-6 col-xs-6">
                    <InPlaceEditorComponent id='masked' mode='Inline' type='Mask' value='123-345-678' model={this.maskModel}/>
                </td>
            </tr>
            <tr>
                <td className="col-lg-6 col-md-6 col-sm-6 col-xs-6 control-title"> NumericTextBox </td>
                <td className="col-lg-6 col-md-6 col-sm-6 col-xs-6">
                    <InPlaceEditorComponent id='numeric' mode='Inline' type='Numeric' value={10} model={this.numericModel}/>
                </td>
            </tr>
            <tr>
                <td className="col-lg-6 col-md-6 col-sm-6 col-xs-6 control-title"> TextBox </td>
                <td className="col-lg-6 col-md-6 col-sm-6 col-xs-6">
                    <InPlaceEditorComponent id='textbox' mode='Inline' type='Text' value='Andrew' model={this.textboxModel}/>
                </td>
            </tr>
            </tbody>
        </table>
        <h3> Injectable Components </h3>
        <table className="table-section">
          <tbody>
            <tr>
                <td className="col-lg-6 col-md-6 col-sm-6 col-xs-6 control-title"> AutoComplete </td>
                <td className="col-lg-6 col-md-6 col-sm-6 col-xs-6">
                    <InPlaceEditorComponent id='autoComplete' mode='Inline' type='AutoComplete' value='Android' model={this.dropdownModel} >
                    <Inject services={[AutoComplete]} />
                    </InPlaceEditorComponent>
                </td>
            </tr>
            <tr>
                <td className="col-lg-6 col-md-6 col-sm-6 col-xs-6 control-title"> ColorPicker </td>
                <td className="col-lg-6 col-md-6 col-sm-6 col-xs-6">
                    <InPlaceEditorComponent id='color' mode='Inline' type='Color' value='#81aefd'>
                    <Inject services={[ColorPicker]} />
                    </InPlaceEditorComponent>
                </td>
            </tr>
            <tr>
                <td className="col-lg-6 col-md-6 col-sm-6 col-xs-6 control-title"> ComboBox </td>
                <td className="col-lg-6 col-md-6 col-sm-6 col-xs-6">
                    <InPlaceEditorComponent id='comboBox' mode='Inline' type='ComboBox' value='Android' model={this.dropdownModel} >
                    <Inject services={[ComboBox]} />
                    </InPlaceEditorComponent>
                </td>
            </tr>
            <tr>
                <td className="col-lg-6 col-md-6 col-sm-6 col-xs-6 control-title"> DateRangePicker </td>
                <td className="col-lg-6 col-md-6 col-sm-6 col-xs-6">
                    <InPlaceEditorComponent id='dateRange' mode='Inline' type='DateRange' value={this.dateRangePickerValue} model={this.dateModel} >
                    <Inject services={[DateRangePicker]} />
                    </InPlaceEditorComponent>
                </td>
            </tr>
            <tr>
                <td className="col-lg-6 col-md-6 col-sm-6 col-xs-6 control-title"> MultiSelect </td>
                <td className="col-lg-6 col-md-6 col-sm-6 col-xs-6">
                    <InPlaceEditorComponent id='multiSelect' mode='Inline' type='MultiSelect' value='Android' model={this.dropdownModel} >
                    <Inject services={[MultiSelect]} />
                    </InPlaceEditorComponent>
                </td>
            </tr>
            <tr>
                <td className="col-lg-6 col-md-6 col-sm-6 col-xs-6 control-title"> RTE </td>
                <td className="col-lg-6 col-md-6 col-sm-6 col-xs-6">
                    <InPlaceEditorComponent id='rte' mode='Inline' type='RTE' value='<p>Enter your content here</p>' model={this.rteModel} >
                    <Inject services={[Rte]} />
                    </InPlaceEditorComponent>
                </td>
            </tr>
            <tr>
                <td className="col-lg-6 col-md-6 col-sm-6 col-xs-6 control-title"> Slider </td>
                <td className="col-lg-6 col-md-6 col-sm-6 col-xs-6">
                    <InPlaceEditorComponent id='slider' mode='Inline' type='Slider' value={20}>
                    <Inject services={[Slider]} />
                    </InPlaceEditorComponent>
                </td>
            </tr>
            <tr>
                <td className="col-lg-6 col-md-6 col-sm-6 col-xs-6 control-title"> TimePicker </td>
                <td className="col-lg-6 col-md-6 col-sm-6 col-xs-6">
                    <InPlaceEditorComponent id='time' mode='Inline' type='Time' value={this.dateValue} model={this.dateModel} >
                    <Inject services={[TimePicker]} />
                    </InPlaceEditorComponent>
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

## Model configuration

Component properties and events can be customized through In-place Editor [model](../api/inplace-editor/#model) property.

In the below code, [type](../api/inplace-editor/#type) defined as `Date` and `DatePicker` properties are configured through [model](../api/inplace-editor/#model) property to customize the [DatePicker](../api/datepicker) component at In-place Editor.

```typescript
    public model = { showTodayButton: true, placeholder: 'Select Date' };
```

`[src/app/app.ts]`

{compileJsx=true %}

```typescript

import { InPlaceEditorComponent } from '@syncfusion/ej2-react-inplace-editor';
import * as React from 'react';
import './App.css';

class App extends React.Component {
  public model = { showTodayButton: true, placeholder: 'Select Date' };
  public value = new Date('04/12/2018');
  public render() {
    return (
     <InPlaceEditorComponent id='element' model={this.model} type='Date' value={this.value}/>
    );
  }
}

export default App;

```

{% endtab %}

## See Also

* [Built-in Components](./components/#list-of-components)