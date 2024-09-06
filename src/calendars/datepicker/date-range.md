---
title: "Choose a date in range"
component: "DatePicker"
description: "Date picker has `min` and `max` properties which restricts the user from selecting a value out of given min/max date range"
---

# Date Range

DatePicker provides an option to select a date value within a specified range by using the
[`min`](../api/datepicker#min)
and
[`max`](../api/datepicker#max)
properties. Always the min value has to be
lesser than the max value.

When the min and max properties are configured and the selected date value is out-of-range or
invalid, then the model value will be set to `out of range` date value or `null` respectively
with highlighted `error` class to indicates the date is out of range or invalid.

The value property depends on the min/max with respect to [`strictMode`](./strict-mode/) property.
The below example allows to select a date within a range from 7th to 27th days in a month.

{% tab template="datepicker/default", isDefaultActive = "true", sourceFiles="app/**/*.tsx" %}

```typescript
// import the datepickercomponent
import { DatePickerComponent } from '@syncfusion/ej2-react-calendars';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class App extends React.Component<{}, {}> {

    // creates a datepicker with min and max property
    private minDate: Date = new Date(new Date().getFullYear(), new Date().getMonth(), 7);
    private  maxDate: Date = new Date(new Date().getFullYear(), new Date().getMonth(), 27);
    private  dateValue: Date = new Date(new Date().setDate(14));

    public render() {
        return <DatePickerComponent id="datepicker" value={this.dateValue} min={this.minDate} max={this.maxDate} />;
    }
}
ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}

> If the value of `min` or `max` properties changed through code behind. Then you have to update the
`value` property to set within the range.