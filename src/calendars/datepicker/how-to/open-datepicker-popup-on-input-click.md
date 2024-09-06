---
title: "How To"
component: "DatePicker"
description: "Explains how to open the DatePicker popup when the input is focused"
---

# Open the DatePicker popup upon focusing input of DatePicker

You can open the DatePicker popup on input focus by calling the `show` method in the input `focus` event.

The following example demonstrates how to open the DatePicker popup when the input is focused.

{% tab template="datepicker/open-popup", sourceFiles="app/**/*.tsx" %}

```typescript

// import the datepickercomponent
import { DatePickerComponent } from '@syncfusion/ej2-react-calendars';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class App extends React.Component<{}, {}> {

    public onFocus(args: FocusEventArgs){
        this.dateObj.show();
    }

    public render() {
        return (
            // Specifies the tag for render the DatePicker component
            <DatePickerComponent focus={this.onFocus.bind(this)} placeholder="Choose a date" ref = {scope => {this.dateObj = scope }}/>
        );
     }
 }

ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}