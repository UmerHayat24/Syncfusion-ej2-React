# Timeline Header Rows

The Timeline views can have additional header rows other than its default date and time header rows. It is possible to show individual header rows for displaying year, month and week separately using the `HeaderRowDirective`. This is applicable only on the timeline views. The possible rows which can be added using `HeaderRowDirective` are as follows.

* `Year`
* `Month`
* `Week`
* `Date`
* `Hour`

> The `Hour` row is not applicable for Timeline month view.

Learn to add and customize additional header rows in the Timeline views of React Scheduler from this video:

`youtube:uV5Axqj5UsI`

The following example shows the Scheduler displaying all the available header rows on timeline views.

{% tab template="schedule/views", iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent,  HeaderRowDirective, HeaderRowsDirective, TimelineViews, Inject,
  ViewsDirective, ViewDirective
} from '@syncfusion/ej2-react-schedule';
import { scheduleData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
  private data: Object[] = extend([], scheduleData, null, true) as Object[];
  render() {
    return <ScheduleComponent width='100%' height='550px' selectedDate={new Date(2018, 11, 31)}
    eventSettings= { { dataSource: this.data } } startHour='09:00' endHour='13:00'>
        <HeaderRowsDirective>
          <HeaderRowDirective option='Year' />
          <HeaderRowDirective option='Month' />
          <HeaderRowDirective option='Week' />
          <HeaderRowDirective option='Date' />
          <HeaderRowDirective option='Hour' />
        </HeaderRowsDirective>
        <ViewsDirective>
          <ViewDirective option='TimelineWeek'/>
        </ViewsDirective>
      <Inject services={[TimelineViews]} />
    </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

> Importing `HeaderRowsDirective` and `HeaderRowDirective` is mandatory.

## Display year and month rows in timeline views

To display the timeline Scheduler simply with year and month names alone, define the option `Year` and `Month` within the `HeaderRowDirective`.

{% tab template="schedule/views", iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent,  HeaderRowDirective, HeaderRowsDirective, TimelineMonth, Inject,
  ViewsDirective, ViewDirective
} from '@syncfusion/ej2-react-schedule';
import { scheduleData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
  private data: Object[] = extend([], scheduleData, null, true) as Object[];
  render() {
    return <ScheduleComponent width='100%' height='550px' selectedDate={new Date(2018, 11, 31)}
    eventSettings= { { dataSource: this.data } }>
        <HeaderRowsDirective>
          <HeaderRowDirective option='Year' />
          <HeaderRowDirective option='Month' />
        </HeaderRowsDirective>
        <ViewsDirective>
          <ViewDirective option='TimelineMonth' interval= {24}/>
        </ViewsDirective>
      <Inject services={[TimelineMonth]} />
    </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

## Display week numbers in timeline views

The week number can be displayed in a separate header row of the timeline Scheduler by setting `Week` option within `HeaderRowDirective`.

{% tab template="schedule/views", iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent,  HeaderRowDirective, HeaderRowsDirective, TimelineMonth, TimelineViews, Inject,
  ViewsDirective, ViewDirective
} from '@syncfusion/ej2-react-schedule';
import { scheduleData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
  private data: Object[] = extend([], scheduleData, null, true) as Object[];
  render() {
    return <ScheduleComponent width='100%' height='550px' selectedDate={new Date(2018, 11, 31)}
    eventSettings= { { dataSource: this.data } }>
        <HeaderRowsDirective>
          <HeaderRowDirective option='Week' />
          <HeaderRowDirective option='Date' />
          <HeaderRowDirective option='Hour' />
        </HeaderRowsDirective>
        <ViewsDirective>
          <ViewDirective option='TimelineMonth' interval= {24}/>
          <ViewDirective option='TimelineWeek' interval= {3}/>
          <ViewDirective option='TimelineDay' interval= {4}/>
        </ViewsDirective>
      <Inject services={[TimelineMonth, TimelineViews]} />
    </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

## Timeline view displaying dates of a complete year

It is possible to display a complete year in a timeline view by setting `interval` value as 12 and defining **TimelineMonth** view option within the `ViewDirective` of Scheduler.

{% tab template="schedule/views", iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent,  HeaderRowDirective, HeaderRowsDirective, TimelineMonth, Inject,
  ViewsDirective, ViewDirective
} from '@syncfusion/ej2-react-schedule';
import { eventData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
  private data: Object[] = extend([], eventData, null, true) as Object[];
  render() {
    return <ScheduleComponent width='100%' height='550px' selectedDate={new Date(2018, 0, 1)}
    eventSettings= { { dataSource: this.data } }>
        <HeaderRowsDirective>
          <HeaderRowDirective option='Month' />
          <HeaderRowDirective option='Date' />
        </HeaderRowsDirective>
        <ViewsDirective>
          <ViewDirective option='TimelineMonth' interval= {12}/>
        </ViewsDirective>
      <Inject services={[TimelineMonth]} />
    </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

## Customizing the header rows using template

You can customize the text of the header rows and display any images or formatted text on each individual header rows using the built-in `template` option available within the `HeaderRowDirective`.

{% tab template="schedule/views", iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, getWeekNumber, HeaderRowDirective, HeaderRowsDirective, TimelineMonth, Inject,
  ViewsDirective, ViewDirective
} from '@syncfusion/ej2-react-schedule';
import { scheduleData } from './datasource';
import { Internationalization, extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
  private data: Object[] = extend([], scheduleData, null, true) as Object[];
  private instance: Internationalization = new Internationalization();
  private getYearDetails(value: CellTemplateArgs) {
    return 'Year: ' + this.instance.formatDate((value as CellTemplateArgs).date, { skeleton: 'y' });
  }
  private getMonthDetails(value: CellTemplateArgs) {
    return 'Month: ' + this.instance.formatDate((value as CellTemplateArgs).date, { skeleton: 'M' });
  }
  private getWeekDetails(value: CellTemplateArgs) {
    return 'Week ' + getWeekNumber((value as CellTemplateArgs).date);;
  }
  private yearTemplate(props): JSX.Element {
    return (<span className="year">{this.getYearDetails(props)}</span>);
  }
  private monthTemplate(props): JSX.Element {
    return (<span className="month">{this.getMonthDetails(props)}</span>);
  }
  private weekTemplate(props): JSX.Element {
    return (<span className="week">{this.getWeekDetails(props)}</span>);
  }
  render() {
    return <ScheduleComponent width='100%' height='550px' selectedDate={new Date(2018, 0, 1)}
    eventSettings= { { dataSource: this.data } }>
        <HeaderRowsDirective>
           <HeaderRowDirective option='Year' template={this.yearTemplate.bind(this)} />
           <HeaderRowDirective option='Month' template={this.monthTemplate.bind(this)} />
           <HeaderRowDirective option='Week' template={this.weekTemplate.bind(this)} />
           <HeaderRowDirective option='Date' />
        </HeaderRowsDirective>
        <ViewsDirective>
          <ViewDirective option='TimelineMonth'/>
        </ViewsDirective>
      <Inject services={[TimelineMonth]} />
    </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

> You can refer to our [React Scheduler](https://www.syncfusion.com/react-ui-components/react-scheduler) feature tour page for its groundbreaking feature representations. You can also explore our [React Scheduler example](https://ej2.syncfusion.com/react/demos/#/material/schedule/overview) to knows how to present and manipulate data.
