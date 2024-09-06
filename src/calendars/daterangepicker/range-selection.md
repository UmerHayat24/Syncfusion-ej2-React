---
title: "Range Restriction"
control: "DateRangePicker"
description: "Date range picker has `min` and `max` properties which restricts the user from selecting a date range value out of given min/max date range"
---

# Range Restriction

Range selection in a DateRangePicker can be made-to-order with desire restrictions based on application needs.

## Restrict the range within a range

You can restrict the minimum and maximum date that can be allowed as start date,
  end date in a range selection with help of [`min`](../api/daterangepicker#min),
  [`max`](../api/daterangepicker#max) properties.
* `min` – sets the minimum  date that can be selected as startDate.
* `max` – sets the maximum date that can be selected as endDate

In the following sample, you can select a date range from 15th date of this month to 15th date of next month.

{% tab template="daterangepicker/default", isDefaultActive = "true", sourceFiles="app/**/*.tsx" %}

```typescript
// import the daterangepicker component
import { DateRangePickerComponent } from '@syncfusion/ej2-react-calendars';
import * as React from "react";
import * as ReactDOM from "react-dom";

export default class App extends React.Component<{}, {}> {

    // creates a daterangepicker with min and max property
    private minDate:Date= new Date(new Date().getFullYear(), new Date().getMonth(), 15);
    private  maxDate:Date= new Date(new Date().getFullYear(), new Date().getMonth()+1, 15);

    public render() {
        return <DateRangePickerComponent id="daterangepicker" placeholder='Select a range' min={this.minDate} max={this.maxDate} />
    }
};
ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}

> If the value of `min` or `max` properties
changed through code behind, then you have to
update the `start date`, `end date` property to set within the
range. Or else , if the `start` and `end` date is out of specified date range, a validation error class will be appended to the input element. If `strictMode` is enabled, and both the start, end date is lesser than the min date then start and end date will be updated with `min` date. If both the start and end date is higher than the max date then start and end date will be updated with `max` date. Or else, if startDate is less than `min` date, startDate will be updated with `min` date or if endDate is greater than `max` date, endDate will be updated with the `max` date.

## Range span

Days span between ranges can be limited in order to avoid excess or less days selection towards the required days in a range.
In this, minimum and maximum span that can be allowed within the date range can be
customized by [`minDays`](../api/daterangepicker#mindays),
[`maxDays`](../api/daterangepicker#maxdays) properties.

* `minDays`- Sets the minimum number of days between start date and end date.
* `maxDays`- Sets the maximum number of days between start date and end date.

In the following sample, the range selection should be greater than 3 days and less than 8 days else it won’t set.

{% tab template="daterangepicker/default", isDefaultActive = "true", sourceFiles="app/**/*.tsx" %}

```typescript

// import the daterangepicker component
import { DateRangePickerComponent } from '@syncfusion/ej2-react-calendars';
import * as React from "react";
import * as ReactDOM from "react-dom";

export default class App extends React.Component<{}, {}> {
    public render() {
        return (
        <DateRangePickerComponent id="daterangepicker" placeholder='Select a range' minDays={3} maxDays={7} />
        )
    }
};
ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}

## Strict mode

DateRangePicker provides the option to limit the user towards entering the valid date only.
 With strict mode, you can set only valid selection.
 Also, If any invalid range is specified then the date range value will reset to previous value.
 This restriction can be availed by enabling the strict mode by setting true
  to [`strictMode`](../api/daterangepicker#strictmode) property.

{% tab template="daterangepicker/default", isDefaultActive = "true", sourceFiles="app/**/*.tsx" %}

```typescript
// import the daterangepicker component
import { DateRangePickerComponent } from '@syncfusion/ej2-react-calendars';
import * as React from "react";
import * as ReactDOM from "react-dom";

export default class App extends React.Component<{}, {}> {
    public render() {
        return <DateRangePickerComponent id="daterangepicker" placeholder='Select a range' strictMode={true} />
    }
};
ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}