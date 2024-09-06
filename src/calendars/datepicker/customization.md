---
title: "Customization"
component: "DatePicker"
description: "Date picker gives complete control to the user to customize overall appearance of the date picker in their application."
---

# Customization

You can customize the  entire appearance of the input element and Calendar by using
custom
[`cssClass`](../api/datepicker#cssclass)
property.
and also you can use the calendar's
[`renderDayCell`](../api/datepicker/renderDayCellEventArgs#renderdaycelleventargs)
event to customize the appearance of the each day cell.

Below list of available classes are used to customize the entire DatePicker component.

| **Class Name** | **Description** |
| --- | --- |
| e-date-wrapper | Applied to DatePicker wrapper |
| e-datepicker | Applied to the DatePicker element.|
| e-float-text | Applied to the floating label.  |
| e-date-icon | Applied to the DatePicker icon. |
| e-popup-wrapper | Applied to DatePicker popup wrapper.|
| e-calendar | Applied to Calendar element. |
| e-header | Applied to Calendar header.|
| e-title |Applied to Calendar title. |
| e-icon-container | Applied to Calendar previous and next icon container.|
| e-prev |  Applied to Calendar previous icon.|
| e-next | Applied to Calendar next icon.|
| e-weekend | Applied to Calendar weekend dates.|
| e-other-month |  Applied to Calendar other month dates.|
| e-day | Applied to each day cell of the Calendar.|
| e-selected | Applied to Calendar selected dates.|
| e-disabled | Applied to Calendar disabled dates.|

The following example highlights the textbox and calendars's weekend days
by using custom CSS.
 Here we have used the `e-custom-style` class to highlight the textbox and disabled date and
`renderDayCell` event to disable the weekends of every month.

{% tab template="datepicker/customization", sourceFiles="app/**/*.tsx,styles.css" %}

```typescript

// import the datepickercomponent
import { DatePickerComponent, RenderDayCellEventArgs } from '@syncfusion/ej2-react-calendars';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class App extends React.Component<{}, {}> {

    public onRenderDayCell(args: RenderDayCellEventArgs): void {
        if ((args.date as Date).getDay() === 0 || (args.date as Date).getDay() === 6) {
            // sets isDisabled to true to disable the date.
            args.isDisabled = true;
            // To know about the disabled date customization, you can refer in "styles.css".
        }
    }

    public render() {
        return (
            // specifies the tag for render the DatePicker component
            <DatePickerComponent id="datepicker" cssClass="e-custom-style" renderDayCell={this.onRenderDayCell} placeholder="Enter date"/>
        );
     }
 }
ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}

## See Also

* [How to disable the DatePicker component](./how-to/disabled-the-datepicker-component)
* [How to set read-only for DatePicker](./how-to/set-the-readonly)
* [How to customize the DatePicker day header](./how-to/customize-the-datepicker-day-header)