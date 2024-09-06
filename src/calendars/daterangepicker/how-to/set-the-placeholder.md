---
title: "How To"
component: "DateRangePicker"
description: "Miscellaneous aspects of customizing the date range picker"
---

# Set the placeholder

The following example demonstrates how to set [`placeholder`](../../api/daterangepicker#placeholder)
 in the DateRangePicker control.

Using `placeholder` you can display a short hint in the input element.

{% tab template="daterangepicker/default", isDefaultActive = "true", sourceFiles="app/**/*.tsx", iframeHeight="520px" %}

```typescript

// import the daterangepicker component
import { DateRangePickerComponent } from '@syncfusion/ej2-react-calendars';
import * as React from "react";
import * as ReactDOM from "react-dom";

export default class App extends React.Component<{}, {}> {

    public render() {
        return <DateRangePickerComponent placeholder='Select a range' />
    }
};
ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}