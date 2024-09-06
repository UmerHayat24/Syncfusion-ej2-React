---
title: "Globalization"
component: "In-place Editor"
description: "Learn how to apply localization (l10n), internationalization (i18n), and right-to-left (RTL) format in the Essential JS2 React In-place Editor component."
---

# Globalization

## Localization

Localization library allows you to localize the default text content of the In-place Editor for different cultures using the [locale](../api/inplace-editor/#locale) property. In  In-place Editor following keys will be localize based on culture.

| Locale key | en-US (default) |
|------|------|
| save | Close |
| cancel | Cancel |
| loadingText | Loading... |
| editIcon | Click to edit |
| editAreaClick | Click to edit |
| editAreaDoubleClick | Double click to edit |

To load translation object in an application use `load` function of `L10n` class. In the following sample, `French` culture is set to In-place Editor and change the tooltip text.

{% tab template="in-place-editor/editable-on", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { L10n } from '@syncfusion/ej2-base';
import { ChangeEventArgs, DropDownListComponent } from '@syncfusion/ej2-react-dropdowns';
import { EditableType, InPlaceEditorComponent } from '@syncfusion/ej2-react-inplace-editor';
import * as React from 'react';
import './App.css';

class App extends React.Component<{},{}> {
  public inplaceEditorObj: InPlaceEditorComponent;
  public dropdownObj: DropDownListComponent;

  public editableOnData = ['Click', 'DblClick', 'EditIconClick'];
  public model = { placeholder: 'Enter some text' };

  public onChange(e: ChangeEventArgs): void {
    const editType: EditableType = e.itemData.value as EditableType;
    this.inplaceEditorObj.editableOn = editType;
    this.inplaceEditorObj.dataBind();
  }

  // set locale culture to In-place Editor
    public componentWillMount() {
        L10n.load({
            'fr-BE': {
                'inplace-editor': {
                  'save': 'enregistrer',
                  'cancel': 'Annuler',
                  'loadingText': 'Chargement...',
                  'editIcon': 'Cliquez pour éditer',
                  'editAreaClick': 'Cliquez pour éditer',
                  'editAreaDoubleClick': 'Double-cliquez pour éditer'
                }
            }
        });
    }

  public render() {
    return (
        <div id='container'>
            <table className="table-section">
              <tbody>
                <tr>
                    <td> EditableOn: </td>
                    <td>
                        <DropDownListComponent id='dropDown' dataSource= {this.editableOnData} width='auto' value='Click' change={ this.onChange=this.onChange.bind(this) } placeholder='Select edit type' />
                    </td>
                </tr>
                <tr>
                    <td  className="sample-td"> Enter your name: </td>
                    <td  className="sample-td">
                        <InPlaceEditorComponent ref={(text) => { this.inplaceEditorObj = text! }} id='element' mode='Inline' value='Andrew' locale='fr-BE' model={this.model} />
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

## Right to left

Specifies the direction of the In-place Editor component using the enableRtl property. For writing systems that require it like Arabic, Hebrew, etc., the direction can be switched to right-to-left.

> It will not change based on the locale property.

{% tab template="in-place-editor/default", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { InPlaceEditorComponent } from '@syncfusion/ej2-react-inplace-editor';
import * as React from 'react';
import './App.css';

class App extends React.Component<{},{}> {
  public render() {
    return (
        <div id='container'>
            <span className="content-title"> Enter your name: </span>
            <InPlaceEditorComponent id='rtlelement' mode='Inline' value='Andrew' enableRtl={true} />
        </div>
    );
  }
}

export default App;
```

{% endtab %}

## Format

Formatting is a way of representing the value in different format. You can format the following mentioned controls with its `format` property, when it passed through the In-place Editor [model](../api/inplace-editor/#model) property.

* [DatePicker](../datepicker/date-format/)
* [DateRangePicker](../daterangepicker/globalization/#customize-the-date-format)
* [DateTimePicker](../api/datetimepicker/#format)
* [NumericTextBox](../numerictextbox/formats/#custom-formats)
* [Slider](../slider/format/)
* [TimePicker](../api/timepicker#format)

{% tab template="in-place-editor/format", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { InPlaceEditorComponent } from '@syncfusion/ej2-react-inplace-editor';
import * as React from 'react';
import './App.css';

class App extends React.Component<{},{}> {
  public value = new Date('11/23/2018');
  public model = { placeholder: 'Select date', format: 'yyyy-MM-dd' };
  public render() {
    return (
        <div id='container'>
            <span className="content-title"> Select date: </span>
            <InPlaceEditorComponent id='element' type='Date' value={this.value} model={this.model} />
        </div>
    );
  }
}

export default App;
```

{% endtab %}