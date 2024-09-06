---
title: "How To"
component: "DateRangePicker"
description: "Miscellaneous aspects of customizing the date range picker"
---

# Disable the component

DateRangePicker can be inactivated on a page, by setting [`enabled`](../../api/daterangepicker#enabled)
value as false which will disable the component completely from all user interactions including in the form post.
The following example demonstrate the disabled component.

{% tab template="daterangepicker/default", isDefaultActive = "true", sourceFiles="app/**/*.tsx" %}

```typescript

// import the datepickercomponent
import { DateRangePickerComponent } from '@syncfusion/ej2-react-calendars';
import * as React from "react";
import * as ReactDOM from "react-dom";

export default class App extends React.Component<{}, {}> {

    private disable:boolean = false;

    public render() {
        return <DateRangePickerComponent placeholder='Select a range' enabled={this.disable} />
    }
};
ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}