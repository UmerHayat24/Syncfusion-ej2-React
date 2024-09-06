---
title: "Date Range"
component: "Calendar"
description: "Calendar has `min` and `max` properties which restricts the user from selecting a value out of given min/max date range"
---

# Date Range

Calendar provides an option to select a date value within a specified range by using the
[`min`](../api/calendar#min)
  and
  [`max`](../api/calendar#max) properties.
  Always the min date has to be lesser than the max date.

The below example allows to select a
date within a range from 7th to 27th dates in a month.

{% tab template="calendar/default", isDefaultActive = "true", sourceFiles="app/**/*.tsx" %}

```typescript

// import the calendarcomponent
import { CalendarComponent } from '@syncfusion/ej2-react-calendars';
import * as React from "react";
import * as ReactDOM from "react-dom";

export default class App extends React.Component<{}, {}> {

     // creates a calendar with min and max property
    private minDate:Date= new Date(new Date().getFullYear(), new Date().getMonth(), 7);
    private  maxDate:Date= new Date(new Date().getFullYear(), new Date().getMonth(), 27);
    private  dateValue:Date= new Date(new Date().setDate(14));

    public render() {
        return <CalendarComponent id="calendar" value={this.dateValue} min={this.minDate} max={this.maxDate} />
    }
};
ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}

> If the value of `min` or `max` properties changed through code behind. Then you have to update the
`value` property to set within
the range. Or else, if the value is out of specified date range and less than `min` date, value property will
be updated with min date or the value is higher than max date, value property will be updated with `max` date.