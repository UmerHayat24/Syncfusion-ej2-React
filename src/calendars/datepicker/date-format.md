---
title: "Date Formats"
component: "DatePicker"
description: "Date picker supports to format date object into specific string format to simplify the date representation. It adapts to any culture specific date formats when it is globalized."
---

# Date Format

Date format is a way of representing the date value in different string format in the textbox.

By default, the DatePicker's format is based on the culture. You can also set the own
custom format by using the
[`format`](../api/datepicker#format)
property.

> Once the date format property has been defined it will be common to all the cultures.

To know more about the date format standards, refer to the
[Internationalization Date Format](http://ej2.syncfusion.com/documentation/base/internationalization/)
section.

The following example demonstrates the DatePicker with the custom format (`yyyy-MM-dd`).

{% tab template="datepicker/default", isDefaultActive = "true", sourceFiles="app/**/*.tsx" %}

```typescript

// import the datepickercomponent
import { DatePickerComponent } from '@syncfusion/ej2-react-calendars';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class App extends React.Component<{}, {}> {

    private dateValue:Date=new Date();

    public render() {
        return <DatePickerComponent id="datepicker"  value={this.dateValue} format='yyyy-MM-dd' placeholder='Enter date' />
    }
};

ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}
