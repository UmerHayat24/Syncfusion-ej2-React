---
title: "Customization"
component: "DateTimePicker"
description: "Date time picker gives complete control to the user to customize overall appearance of the date time picker in their application."
---

# Customization

The DateTimePicker is available for UI customization that can be achieved by using available properties and events in the component.

## Day and Time Cell format

The DateTimePicker is available for UI customization based on your application requirements. It can be achieved by using [`renderDayCell`](../api/datetimepicker/renderDayCellEventArgs#renderdaycelleventargs)
event that provides an option to customize each day cell on rendering.

The following example disables the weekends of every month by using `renderDayCell` event.

{% tab template="datetimepicker/default", sourceFiles="app/**/*.tsx" %}

```typescript

import { DateTimePickerComponent, RenderDayCellEventArgs } from '@syncfusion/ej2-react-calendars';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class App extends React.Component<{}, {}> {

    public onRenderCell(args: RenderDayCellEventArgs): void {
        if ((args.date as Date).getDay() === 0 || (args.date as Date).getDay() === 6) {
            // sets isDisabled to true to disable the date.
            args.isDisabled = true;
        }
     }

    public render() {
        return <DateTimePickerComponent id="datetimepicker" renderDayCell={this.onRenderCell} placeholder="Select a date and time"/>
    }
};
ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}

## See Also

* [How to disable the DateTimePicker component](./how-to/disable-the-datetimepicker-component)
* [How to customize the DateTimePicker day header](./how-to/customize-the-datetimepicker-day-header)
