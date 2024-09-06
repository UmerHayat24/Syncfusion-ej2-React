---
title: "Multi Selection"
component: Calendar
description: "Calendar supports multiple date selection to allow users to select more than one date."
---

# Multi Selection

Calendar provides an option to select **single** or **multiple dates** by using `isMultiSelection` and `values` properties. By default, `isMultiSelection` property will be in disabled state.

| API | Type | Description |
|------|------|----------------------|
| `isMultiSelection`| **Boolean**| Enables the multi selection option in the Calendar control |
|`values`| **Date[]** | Gets or sets the date range values in multi selection option |

The following example demonstrates the functionality of  `isMultiSelection` property and `values` properties in the Calendar control.

{% tab template="calendar/multiselect", sourceFiles="app/**/*.tsx" %}

```typescript

// import the calendarcomponent
import { CalendarComponent} from '@syncfusion/ej2-react-calendars';
import * as React from "react";
import * as ReactDOM from "react-dom";

export default class App extends React.Component<{}, {}> {

//initialize the values
private values: Date[] = [new Date('1/1/2020'), new Date('1/15/2020'), new Date('1/3/2020'), new Date('1/25/2020')];


public render() {
    return <CalendarComponent id="calendar" isMultiSelection={true} values={this.values}  />
    }
};
ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}
