---
title: "How To"
component: "Calendar"
description: "Miscellaneous aspects of customizing the calendar"
---

# Select a sequence of dates in Calendar

The following example demonstrates how to select the week dates of chosen date in the Calendar using [`values`](../../api/calendar#values) property, when [`isMultiSelection`](../../api/calendar#ismultiselection) property is enabled. Methods of Moment.js is used in this sample for calculating the start and end of week from the selected date.

>To parse, format and manipulating the date values, here we used momentum. You can install it by using below command

`npm i moment`

{% tab template="calendar/howto-multi-selection", sourceFiles="app/**/*.tsx" %}

```typescript

import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
// import the calendarcomponent
import {  Calendar, CalendarComponent, ChangedEventArgs } from '@syncfusion/ej2-react-calendars';
import * as moment from "moment";
import * as React from "react";
import * as ReactDOM from "react-dom";

export default class App extends React.Component<{}, {}> {

private calendarInstance: Calendar;

constructor(props: any) {
    super(props);
    this.onchange = this.onchange.bind(this);
    this.onweekChange = this.onweekChange.bind(this);
    this.onworkweekChange = this.onworkweekChange.bind(this);
}
public onchange(args: ChangedEventArgs){
    const startOfWeek: any = moment(args.value).startOf('week');
    const endOfWeek: any = moment(args.value).endOf('week');
    if (this.calendarInstance.element.classList.contains('workweek')) {
        this.getWeekArray(startOfWeek.day(1) , endOfWeek.day(5)) ;
    } else if (this.calendarInstance.element.classList.contains("week")) {
        this.getWeekArray(startOfWeek, endOfWeek);
    }
}

public onworkweekChange(): void {
     if (this.calendarInstance.element.classList.contains('week')) {
        this.calendarInstance.element.classList.remove('week')
    }
    this.calendarInstance.element.classList.add('workweek');
}

public onweekChange(): void{
     if (this.calendarInstance.element.classList.contains('workweek')) {
         this.calendarInstance.element.classList.remove('workweek')
    }
    this.calendarInstance.element.classList.add('week');
}

public getWeekArray(startOfWeek: any ,endOfWeek: any) {
    const days = [];
    let day = startOfWeek;
    while (day <= endOfWeek) {
        days.push(day.toDate());
        day = day.clone().add(1, 'd');
    }
   this.calendarInstance.values = days;
   }

    public render() {
        return (
    <div id="app">
        <div className="wrap">
         <CalendarComponent id="calendar" isMultiSelection={true}  change={this.onchange} ref={(element) => {(this.calendarInstance as Calendar | null) = element }} />
        </div>
        <div id="btncontainer" className="e-btn-group e-vertical">
            <ButtonComponent onClick={this.onweekChange} id="week" className="e-btn"> Week </ButtonComponent>
            <ButtonComponent onClick={this.onworkweekChange} id="workweek" className="e-btn"> Work Week </ButtonComponent>
    </div>
  </div>
  );
}
}
ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}