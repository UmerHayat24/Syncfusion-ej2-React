---
title: "How To"
component: "DatePicker"
description: "Miscellaneous aspects of customizing the date picker"
---

# Prevent the popup close

To prevent the DatePicker popup from closing, use the
preventDefault method

The following example demonstrates how to prevent the popup from closing.

{% tab template="datepicker/default", sourceFiles="app/**/*.tsx" %}

```typescript

// import the datepickercomponent
import { DatePickerComponent } from '@syncfusion/ej2-react-calendars';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class App extends React.Component<{}, {}> {

    public onClose(args: PreventableEventArgs){
     // prevent the popup close
        args.preventDefault();
    }

    public render() {
        return (
            // specifies the tag for render the DatePicker component
            <DatePickerComponent close={this.onClose} placeholder="Enter date"/>
        );
     }
 }

ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}