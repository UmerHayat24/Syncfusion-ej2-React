---
title: "Islamic Calendar"
component: Calendar
description: "Calendar supports to display the Islamic Calendar (Hijri Calendar)."
---

# Islamic-Calendar

In addition to the Gregorian calendar, the Calendar control supports displaying the Islamic calendar (Hijri calendar). **Islamic calendar** or **Hijri calendar** is a `lunar calendar` consisting of 12 months in a year of 354 or 355 days. To know more about Islamic calendar, please refer this [wikipedia](https://en.wikipedia.org/wiki/Islamic_calendar).

Also, it consists of all Gregorian calendar functionalities as like min and max date, week number, start day of the week, multi selection, enable RTL, start and depth view, localization, highlight and customize the specific dates.

By default, calendar mode is in **Gregorian**. You can enable the Islamic mode by setting the **calendarMode** as **Islamic**. Also, need to import and injecting the `Islamic` module into the Calendar using the `Inject` directive from `ej2-react-calendars` as shown below.

> import { Islamic } from '@syncfusion/ej2-react-calendars';

By default, calendar mode is in **Gregorian**. You can enable the Islamic mode by setting the **calendarMode** as **Islamic** and injecting the `Islamic` module into the Calendar using the `Inject` directive.

The following example demonstrates how to display the Islamic Calendar (Hijri Calendar).

{% tab template="calendar/islamic-calendar", sourceFiles="app/**/*.tsx" %}

```typescript

import { addClass } from '@syncfusion/ej2-base';
// import the calendarcomponent
import {  CalendarComponent, CalendarType, Inject, Islamic, RenderDayCellEventArgs } from '@syncfusion/ej2-react-calendars';
import * as React from "react";
import * as ReactDOM from 'react-dom';

export default class App extends React.Component<{}, {}> {

    private calendarMode: CalendarType = 'Islamic';

    constructor(props: any) {
        super(props);
        this.disableDate = this.disableDate.bind(this);
    }
// initialize the calendar mode

public disableDate(args: RenderDayCellEventArgs) {
        /*Date need to be disabled*/
        if ((args.date as Date).getDate() === 2 || (args.date as Date).getDate() === 10 || (args.date as Date).getDate() === 28) {
            args.isDisabled = true;
        }
        if ((args.date as Date).getDate() === 13) {
            let span: HTMLElement;
            span = document.createElement('span');
            (args.element as HTMLElement).children[0].className += 'e-day sf-icon-cup highlight';
            addClass([args.element as HTMLElement], ['special', 'e-day', 'dinner']);
            (args.element as HTMLElement).setAttribute('data-val', ' Dinner !');
            (args.element as HTMLElement).appendChild(span);
        }
        if ((args.date as Date).getDate() === 23) {
            (args.element as HTMLElement).children[0].className += 'e-day sf-icon-start highlight';
            let span: HTMLElement;
            span = document.createElement('span');
            span.setAttribute('class', 'sf-icons-star highlight');
            // use the imported method to add the multiple classes to the given element
            addClass([args.element as HTMLElement], ['special', 'e-day', 'holiday']);
            (args.element as HTMLElement).setAttribute('data-val', ' Holiday !');
            (args.element as HTMLElement).appendChild(span);
        }
}

public render() {
    return <CalendarComponent calendarMode={this.calendarMode} renderDayCell={this.disableDate} ><Inject services={[Islamic]} /></CalendarComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}
