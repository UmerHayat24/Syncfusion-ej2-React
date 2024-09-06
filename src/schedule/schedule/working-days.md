# Working Days and Hours

The Scheduler can be customized on various aspects as well as it inherits almost all the calendar-specific features such as options,

* To set custom time range display on Scheduler
* To set different working hours
* To set different working days
* To set different first day of week
* To show/hide weekend days
* To show the week number
* To display the current time indicator

## Set working days

By default, Scheduler considers the week days from Monday to Friday as `Working days` and therefore defaults to [1,2,3,4,5] - where 1 represents Monday, 2 represents Tuesday and so on. The days which are not defined in this working days collection are considered as non-working days. Therefore, when the weekend days are set to hide from Scheduler, all those non-working days too gets hidden from the layout.

The Work week and Timeline Work week views displays exactly the defined working days on Scheduler layout, whereas other views displays all the days and simply differentiates the non-working days on UI with inactive cell color.

> The working or business hours depiction on Scheduler are usually valid only on these specified working days.

The following example code depicts how to set the Scheduler to display Monday, Wednesday and Friday as working days of a week.

{% tab template="schedule/local-data", iframeHeight="588px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Week, WorkWeek, TimelineViews, Inject,
  ViewsDirective, ViewDirective} from '@syncfusion/ej2-react-schedule';
import { scheduleData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
    private data: Object[] = extend([], scheduleData, null, true) as Object[];
    private workingDays: number[] = [1, 3, 5];
    render() {
    return <ScheduleComponent  width= '100%' height='550px' selectedDate= {new Date(2018, 1, 15)} eventSettings= { { dataSource: this.data } } workDays= {this.workingDays} >
            <ViewsDirective>
                <ViewDirective option='Week' />
                <ViewDirective option='WorkWeek' />
                <ViewDirective option='TimelineWorkWeek' />
            </ViewsDirective>
            <Inject services={[Week, WorkWeek, TimelineViews]} />
        </ScheduleComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

## Hiding weekend days

The `showWeekend` property is used to either show or hide the weekend days of a week and it is not applicable on Work week view (as non-working days are usually not displayed on work week view). By default, it is set to `true`. The days which are not a part of the working days collection of a Scheduler are usually considered as non-working or weekend days.

Here, the working days are defined as [1, 3, 4, 5] on Scheduler and therefore the remaining days (0, 2, 6 – Sunday, Tuesday and Saturday) are considered as non-working or weekend days and will be hidden from all the views when `showWeekend` property is set to `false`.

{% tab template="schedule/local-data", iframeHeight="588px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, Month, Inject,
  ViewsDirective, ViewDirective} from '@syncfusion/ej2-react-schedule';
import { scheduleData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
    private data: Object[] = extend([], scheduleData, null, true) as Object[];
    render() {
    return <ScheduleComponent  width= '100%' height='550px' selectedDate= {new Date(2018, 1, 15)} eventSettings= { { dataSource: this.data } } showWeekend= { false }
    workDays= {[1, 3, 4, 5]} >
            <ViewsDirective>
              <ViewDirective option='Day' />
              <ViewDirective option='Week' />
              <ViewDirective option='Month' />
            </ViewsDirective>
            <Inject services={[Day, Week, Month]} />
        </ScheduleComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

## Show week numbers

It is possible to show the week number count of a week in the header bar of the Scheduler by setting true to `showWeekNumber` property. By default, its default value is `false`. In Month view, the week numbers are displayed as a first column.

> The `showWeekNumber` property is not applicable on Timeline views, as it has the equivalent [headerRows](./header-rows/#display-week-numbers-in-timeline-views) property to handle such requirement with additional customizations.

{% tab template="schedule/local-data", iframeHeight="588px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, WorkWeek, Month, Agenda, Inject,
  } from '@syncfusion/ej2-react-schedule';
import { scheduleData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
    private data: Object[] = extend([], scheduleData, null, true) as Object[];
    render() {
        return <ScheduleComponent  width= '100%' height='550px' selectedDate= {new Date(2018, 1, 15)} eventSettings= { { dataSource: this.data } } showWeekNumber= { true }
        workDays= {[1, 3, 4, 5]} >
    <Inject services={[Day, Week, Month]} />
    </ScheduleComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

### Different options in showing week numbers

By default, week numbers are shown in the Scheduler based on the first day of the year. However, the week numbers can be determined based on the following criteria.

`FirstDay` – The first week of the year is calculated based on the first day of the year.

`FirstFourDayWeek` – The first week of the year begins from the first week with four or more days.

`FirstFullWeek` – The first week of the year begins when meeting the first day of the week (firstDayOfWeek) and the first day of the year.

For more details refer to [this link](https://docs.microsoft.com/en-us/dotnet/api/system.globalization.calendarweekrule?view=net-5.0#remarks)

{% tab template="schedule/local-data", iframeHeight="588px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, WorkWeek, Month, Agenda, Inject,
  } from '@syncfusion/ej2-react-schedule';
import { scheduleData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
    private data: Object[] = extend([], scheduleData, null, true) as Object[];
    render() {
        return <ScheduleComponent  width= '100%' height='550px' selectedDate= {new Date(2020, 1, 15)} eventSettings= { { dataSource: this.data } } showWeekNumber= { true }
        workDays= {[1, 3, 4, 5]} weekRule = 'FirstFourDayWeek'>
    <Inject services={[Day, Week, Month]} />
    </ScheduleComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

**Note**: Enable the `showWeekNumber` property to configure the `weekRule` property. Also, the weekRule property depends on the value of the `firstDayOfWeek` property

## Set working hours

Working hours indicates the work hour limit within the Scheduler, which is visually highlighted with an active color on work cells. The working hours can be set on Scheduler using the `workHours` property which is of object type and includes the following sub-options,

* `highlight` – enables/disables the highlighting of work hours.
* `start` - sets the start time of the working/business hour of a day.
* `end` - sets the end time limit of the working/business hour of a day.

{% tab template="schedule/local-data", iframeHeight="588px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, WorkWeek, Inject,
  ViewsDirective, ViewDirective} from '@syncfusion/ej2-react-schedule';
import { scheduleData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
    private data: Object[] = extend([], scheduleData, null, true) as Object[];
    render() {
    return <ScheduleComponent  width= '100%' height='550px' selectedDate= {new Date(2018, 1, 15)} workHours= { {
        highlight: true, start: '11:00', end: '20:00' } } eventSettings= { { dataSource: this.data } }>
        <ViewsDirective>
            <ViewDirective option='Day' />
            <ViewDirective option='Week' />
            <ViewDirective option='WorkWeek' />
        </ViewsDirective>
        <Inject services={[Day, Week, WorkWeek]} />
    </ScheduleComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

## Scheduler displaying custom hours

It is possible to display the event Scheduler layout with specific time durations by hiding the unwanted hours. To do so, set the start and end hour for the Scheduler using the `startHour` and `endHour` properties respectively.

The following code example displays the Scheduler starting from the time range 7.00 AM to 6.00 PM and the remaining hours are hidden on the UI.

{% tab template="schedule/local-data", iframeHeight="588px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, WorkWeek, Inject,
  ViewsDirective, ViewDirective } from '@syncfusion/ej2-react-schedule';
import { scheduleData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
    private data: Object[] = extend([], scheduleData, null, true) as Object[];
    render() {
    return <ScheduleComponent  width= '100%' height='550px' selectedDate= {new Date(2018, 1, 15)} startHour= '07:00'
    endHour= '18:00' eventSettings= { { dataSource: this.data } }>
        <ViewsDirective>
            <ViewDirective option='Day' />
            <ViewDirective option='Week' />
            <ViewDirective option='WorkWeek' />
        </ViewsDirective>
    <Inject services={[Day, Week, WorkWeek]} />
    </ScheduleComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

## Setting start day of the week

By default, Scheduler defaults to `Sunday` as its first day of a week. To change the Scheduler's start day of a week with different day, set the `firstDayOfWeek` property with the values ranging from 0 to 6.

> Here, Sunday is always denoted as 0, Monday as 1 and so on.

{% tab template="schedule/local-data", iframeHeight="588px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Week, Month, Inject,
  ViewsDirective, ViewDirective} from '@syncfusion/ej2-react-schedule';
import { scheduleData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
    private data: Object[] = extend([], scheduleData, null, true) as Object[];
    render() {
    return <ScheduleComponent  width= '100%' height='550px' selectedDate= {new Date(2018, 1, 15)} eventSettings= { { dataSource: this.data } } firstDayOfWeek={1} >
            <ViewsDirective>
                <ViewDirective option='Week' />
                <ViewDirective option='Month' />
            </ViewsDirective>
            <Inject services={[Week, Month]} />
        </ScheduleComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

## Scroll to specific time and date

You can manually scroll to a specific time on Scheduler by making use of the `scrollTo` method as depicted in the following code example.

{% tab template="schedule/event-public", iframeHeight="588px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { TimePickerComponent, ChangeEventArgs } from '@syncfusion/ej2-react-calendars';
import {
  ScheduleComponent, Day, Week, TimelineViews, Inject,
  ViewsDirective, ViewDirective} from '@syncfusion/ej2-react-schedule';
import { scheduleData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
  private scheduleObj: ScheduleComponent;
  private data: Object[] = extend([], scheduleData, null, true) as Object[];
  private onChange(args: ChangeEventArgs): void {
    this.scheduleObj.scrollTo(args.text);
  }
    render() {
    return (
      <div className='content-wrapper'>
        <div className='property-section'>
            <table id='property' title='Properties' className='property-panel-table' style={{ width: '100%' }}>
              <tbody>
                <tr style={{ height: '50px' }}>
                  <td style={{ width: '30%' }}>
                    <div className='col-md-4' style={{ paddingTop: '8px' }}>Scroll To</div>
                  </td>
                  <td style={{ width: '70%' }}>
                    <div>
                      <TimePickerComponent width={100} value={new Date(2000, 0, 1, 9)} format='HH:mm'
                        change={this.onChange.bind(this)}></TimePickerComponent>
                    </div>
                  </td>
                </tr>
              </tbody>
            </table>
        </div>
        <div className='control-section'>
            <ScheduleComponent width='100%' height='550px' ref={schedule => this.scheduleObj = schedule}
              selectedDate={new Date(2018, 1, 15)} eventSettings={{ dataSource: this.data }}>
              <ViewsDirective>
                <ViewDirective option='Day' />
                <ViewDirective option='Week' />
                <ViewDirective option='TimelineDay' />
                <ViewDirective option='TimelineWeek' />
              </ViewsDirective>
              <Inject services={[Day, Week, TimelineViews]} />
            </ScheduleComponent>
        </div>
      </div>
    );
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

### How to scroll to current time on initial load

There are scenarios where you may need to load the Scheduler displaying the system's current time on the currently visible view port area. In such cases, the Scheduler needs to be scrolled to a specific time based on the system's current time which is depicted in the following code example.

{% tab template="schedule/local-data", iframeHeight="588px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, TimelineViews, Inject,
  ViewsDirective, ViewDirective} from '@syncfusion/ej2-react-schedule';
import { scheduleData } from './datasource';
import { Internationalization, extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
    private scheduleObj: ScheduleComponent;
    private data: Object[] = extend([], scheduleData, null, true) as Object[];
    private instance: Internationalization = new Internationalization();
    private onCreated(): void {
      this.scheduleObj.scrollTo(this.instance.formatDate(new Date(), { skeleton: 'hm' }));
    }
    render() {
    return <ScheduleComponent  ref={schedule => this.scheduleObj = schedule} width= '100%' height='550px' selectedDate= {new Date(2018, 1, 15)} eventSettings= { { dataSource: this.data } } created= {this.onCreated.bind(this)} >
            <ViewsDirective>
                <ViewDirective option='Day' />
                <ViewDirective option='Week' />
                <ViewDirective option='TimelineWeek' />
            </ViewsDirective>
            <Inject services={[Day, Week, TimelineViews]} />
        </ScheduleComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

> You can refer to our [React Scheduler](https://www.syncfusion.com/react-ui-components/react-scheduler) feature tour page for its groundbreaking feature representations. You can also explore our [React Scheduler example](https://ej2.syncfusion.com/react/demos/#/material/schedule/overview) to knows how to present and manipulate data.

## See Also

* [To display the current time indicator](./timescale/#highlighting-current-date-and-time)
* [To set different working hours dynamically](./how-to/set-different-work-hours)
* [To set different working hours for each resources](./resources/#set-different-work-hours)
* [To set different working days for each resources](./resources/#set-different-work-days)
