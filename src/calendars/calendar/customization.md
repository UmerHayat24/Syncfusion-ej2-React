---
title: "Customization"
component: "Calendar"
description: "Calendar gives complete control to the user to customize overall appearance of the calendar in their application."
---

# Customization

Calendar allows you to customize the entire appearance by
using the custom CSS and
 [`renderDayCell`](../api/calendar/renderDayCellEventArgs#renderdaycelleventargs)
 event
to customize the each day cell.

This following section demonstrates how to disable, highlights the specific dates in the Calendar.

## Disable Weekends

You can disable the weekends of every month in a Calendar by using the
[`renderDayCell`](../api/calendar/renderDayCellEventArgs#renderdaycelleventargs) event. The
`isDisabled` argument from this event allows you to define whether the
date to be disabled or not.

> Set
[`isDisabled`](../api/calendar/renderDayCellEventArgs#renderdaycelleventargs)
to true to disable the date value.

The following example demonstrates how to disable weekends of every month.

{% tab template="calendar/default", sourceFiles="app/**/*.tsx" %}

```typescript
// import the calendarcomponent
import { CalendarComponent, RenderDayCellEventArgs } from '@syncfusion/ej2-react-calendars';
import * as React from "react";
import * as ReactDOM from 'react-dom';

export default class App extends React.Component<{}, {}> {

    // initialize the value
    private dateValue: Date = new Date();

    public disabledDate(args: RenderDayCellEventArgs): void {
        if ((args.date as Date).getDay() === 0 || (args.date as Date).getDay() === 6) {
            // set 'true' to disable the weekends
            args.isDisabled = true;
        }
    }

    public render() {
        return <CalendarComponent id="calendar" renderDayCell={this.disabledDate} value={this.dateValue} />
    }
};
ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}

## Day Cell Format

You can highlight the specific dates by adding the
custom CSS or element to the day cell by using
[`renderDayCell`](../api/calendar/renderDayCellEventArgs#renderdaycelleventargs).

Below is the list of classes that provides the flexible way to customize the Calendar component.

| **Class Name** | **Description** |
| --- | --- |
| e-calendar | Applied to Calendar. |
| e-header | Applied to header.|
| e-title |Applied to title. |
| e-icon-container | Applied to previous and next icon container.|
| e-prev |  Applied to previous icon.|
| e-next | Applied to next icon.|
| e-weekend | Applied to weekend dates.|
| e-other-month |  Applied to other month dates.|
| e-day | Applied to each day cell.|
| e-selected | Applied to selected dates.|
| e-disabled | Applied to disabled dates.|

The following example highlights the world health date (7th April every year)
and world forest day (21st March every year) in the Calendar by using the
custom icon and tooltip.

{% tab template="calendar/highlight-special", sourceFiles="app/**/*.tsx,styles.css" %}

```typescript

// import the calendarcomponent
import { CalendarComponent, RenderDayCellEventArgs } from '@syncfusion/ej2-react-calendars';
import * as React from "react";
import * as ReactDOM from 'react-dom';

export default class App extends React.Component<{}, {}> {
     // initialize the value
    private dateValue: Date = new Date('03/10/2017');

    public customDates(args: RenderDayCellEventArgs): void {
        let span: HTMLElement;
        // defines the custom HTML element to be added.
        span = document.createElement('span');
        // Use "e-icons" class name to load Essential JS 2 built-in icons.
        span.setAttribute('class', 'e-icons highlight-day');
        if ((args.date as Date).getDate() === 7 && (args.date as Date).getMonth() === 3) {
            // append the span element to day cell.
            (args.element as HTMLElement).appendChild(span);
            // set the custom tooltip to the special dates.
            (args.element as HTMLElement).setAttribute('title', 'World health day!');
            // Use "special" class name to highlight the special dates, which you can refer in "styles.css".
            (args.element as HTMLElement).className = 'special';
        }
        if ((args.date as Date).getDate() === 21 && (args.date as Date).getMonth() === 2) {
            (args.element as HTMLElement).appendChild(span);
            (args.element as HTMLElement).className = 'special';
            // set the custom tooltip to the special dates.
            (args.element as HTMLElement).setAttribute('title', 'World forest day');
        }
    }

    public render() {
        return <CalendarComponent id="calendar" renderDayCell={this.customDates} value={this.dateValue} />
    }
};


ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}

## Highlight Weekends

You can highlight the weekends of every month in a Calendar by using the
[`renderDayCell`](../api/calendar/renderDayCellEventArgs#renderdaycelleventargs)
event. The following example demonstrates how to highlights the weekends of every month.

{% tab template="calendar/highlight-weekend", sourceFiles="app/**/*.tsx" %}

```typescript

// import the calendarcomponent
import { CalendarComponent, RenderDayCellEventArgs } from '@syncfusion/ej2-react-calendars';
import * as React from "react";
import * as ReactDOM from "react-dom";

export default class App extends React.Component<{}, {}> {

    // initialize the value
    private dateValue: Date = new Date();

    public highlightWeekend(args: RenderDayCellEventArgs): void {
        if ((args.date as Date).getDay() === 0 || (args.date as Date).getDay() === 6) {
            // To highlight the week end of every month
            args.element.classList.add('e-highlightweekend');
        }
    }

    public render() {
        return <CalendarComponent id="calendar" renderDayCell={this.highlightWeekend} value={this.dateValue} />
    }

};
ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}

## See Also

* [Add the external button in the Calendar popup](./how-to/set-clear-button-in-calendar)
* [How to skip a month in Calendar](./how-to/skip-a-month-in-calendar)
* [How to change the first day of week](./how-to/change-the-first-day-of-week)
* [How to customize the Calendar day header](./how-to/customize-the-calendar-day-header)
