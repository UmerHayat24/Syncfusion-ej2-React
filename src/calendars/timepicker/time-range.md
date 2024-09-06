---
title: "Time Range"
component: "TimePicker"
description: "Time picker has `min` and `max` properties which restricts the user from selecting a value out of given time range"
---

# Time Range

TimePicker provides an option to select a time value within a specified range by using the
[`min`](../api/timepicker#min)
and
[`max`](../api/timepicker#max)
properties.  The min value should always be lesser than the max value.

When the min and max properties are configured and the selected time value is out-of-range or
invalid, then the model value will be set to `out of range` time value or `null` respectively
with highlighted `error` class to indicates the time is out of range or invalid.

The value property depends on the min/max with respect to [`strictMode`](./strict-mode/) property.
The following example allows you to select a time value within a range of `9:00 AM` to `11:30 AM`.

{% tab template="timepicker/default", isDefaultActive = "true", sourceFiles="app/**/*.tsx" %}

```typescript

// import the ripple effect
import { enableRipple } from '@syncfusion/ej2-base';
// import the timepicker
import { TimePickerComponent } from '@syncfusion/ej2-react-calendars';
import * as React from "react";
import * as ReactDOM from "react-dom";

// enable ripple effect
enableRipple(true);

export default class App extends React.Component<{}, {}> {

    // initialize the min and max time value
    private minTime: Date = (new Date('8/3/2017 9:00 AM'));
    private maxTime: Date = (new Date('8/3/2017 11:30 AM'));

    public render() {
        return <TimePickerComponent id="timepicker" placeholder="Select a Time" min={this.minTime} max={this.maxTime} />
    }
};
ReactDOM.render(<App />, document.getElementById('timer'));

```

{% endtab %}

> If the value of `min` or `max` property is changed through code behind you have to update the `value` property to set within the range.