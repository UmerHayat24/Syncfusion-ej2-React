---
title: "How To"
component: "DateTimePicker"
description: "Miscellaneous aspects of customizing the date time picker"
---

# Set the placeholder

The following example demonstrates how to set [`placeholder`](../../api/datetimepicker#placeholder) in the DateTimePicker component.

Using `placeholder` you can display a short hint in the input element.

{% tab template="datetimepicker/default", sourceFiles="app/**/*.tsx" %}

```typescript

import { DateTimePickerComponent } from '@syncfusion/ej2-react-calendars';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class App extends React.Component<{}, {}> {
    public render() {
        return <DateTimePickerComponent id="datetimepicker" placeholder='Select a date and time' />;
    }
}
ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}