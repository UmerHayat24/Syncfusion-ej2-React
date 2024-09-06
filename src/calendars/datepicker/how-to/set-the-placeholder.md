---
title: "How To"
component: "DatePicker"
description: "Miscellaneous aspects of customizing the date picker"
---

# Set the placeholder

The following example demonstrates how to set `placholder` in the DatePicker component.

Using `placeholder` you can display a short hint in the input element.

{% tab template="datepicker/default", sourceFiles="app/**/*.tsx" %}

```typescript

// import the datepickercomponent
import { DatePickerComponent } from '@syncfusion/ej2-react-calendars';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class App extends React.Component<{}, {}> {
    public render() {
        return (
            // specifies the tag for render the DatePicker component
            <DatePickerComponent  placeholder="Choose a date"/>
        );
     }
 }

ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}