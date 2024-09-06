---
title: "How To"
component: "DatePicker"
description: "Miscellaneous aspects of customizing the date picker"
---

# Customize the datepicker day header

You can change the format of the day that to be displayed in header using [`dayHeaderFormat`](../../api/datepicker#dayheaderformat) property. By default, the format is `Short`.

You can find the possible formats on below.

| **Name** | **Description** |
|------|---------------------|
| `Short` | Sets the short format of day name (like Su ) in day header. |
| `Narrow` | Sets the single character of day name (like S ) in day header. |
| `Abbreviated` | Sets the min format of day name (like Sun ) in day header. |
| `Wide` | Sets the long format of day name (like Sunday ) in day header. |

{% tab template="datepicker/header-format", sourceFiles="app/**/*.tsx" %}

```typescript

// import the datepickercomponent
import { DatePickerComponent } from '@syncfusion/ej2-react-calendars';
import { DropDownListComponent } from '@syncfusion/ej2-react-dropdowns';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class App extends React.Component<{}, {}> {
    public datepickerObj: DatePickerComponent;
    public floatLabelObj: DropDownListComponent;
    private floatData: { [key: string]: Object }[];
    private fields: object;
    private value: string = 'Short';
    constructor(props: {}) {
    super(props);
    this.floatData = [
      { Id: 'Short', Label: 'Short' },
      { Id: 'Narrow', Label: 'Narrow' },
      { Id: 'Abbreviated', Label: 'Abbreviated' },
      { Id: 'Wide', Label: 'Wide' }
    ];
    this.fields = { text: 'Label', value: 'Id' };
    }
    private formatHandler(args: any): void {
        this.datepickerObj.dayHeaderFormat = args.value;
    }
    public render() {
        return (
            // specifies the tag for render the DatePicker component
            <div id='container'>
                <div id='datepicker'>
                    <DatePickerComponent ref={(datepicker) => this.datepickerObj = datepicker} dayHeaderFormat="Short"/>
                </div>
                <div id="format">
                     <label className="custom-input-label">Header Format Types</label>
                    <DropDownListComponent id="select" value = {this.value}  dataSource={this.floatData} ref={(dropdownlist) => { this.floatLabelObj = dropdownlist }} fields={this.fields} change={this.formatHandler.bind(this)}/>
            </div>
          </div>
        );
     }
 }

ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}