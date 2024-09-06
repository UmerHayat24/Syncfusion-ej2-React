# Timescale Customization

The time slots are usually the time cells that are displayed on the Day, Week and Work Week views of both the calendar (to the left most position) and timeline views (at the top position). The `timeScale` property allows you to control and set the required time slot duration for the work cells displayed on Scheduler. It includes the following sub-options such as,

* `enable` - When set to `true`, allows the Scheduler to display the appointments accurately against the exact time duration. If set to `false`, all the appointments of a day will be displayed one below the other with no gridlines displayed. Its default value is `true`.
* `interval` – Defines the time duration on which the time axis to be displayed either in 1 hour or 30 minutes interval and so on. It accepts the values in minutes and defaults to 60.
* `slotCount` – Decides the number of slot count to be split for the specified time interval duration. It defaults to 2, thus displaying two slots to represent an hour(each slot depicting 30 minutes duration).

## Setting different time slot duration

The `interval` and `slotCount` properties can be used together on the Scheduler to set different time slot duration which is depicted in the following code example. Here, six time slots together represents an hour.

{% tab template="schedule/local-data", iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  Day, Week, WorkWeek, TimelineViews, ScheduleComponent, ViewsDirective, ViewDirective, Inject
} from '@syncfusion/ej2-react-schedule';
import { extend } from '@syncfusion/ej2-base';
import { scheduleData } from './datasource';

class App extends React.Component<{}, {}>{
  private data: Object[] = extend([], scheduleData, null, true) as Object[];
    render() {
        return <ScheduleComponent width='100%' height='550px' ref={schedule => this.scheduleObj = schedule}
        selectedDate={new Date(2018, 1, 15)} eventSettings={ { dataSource: this.data } }
        timeScale={ { enable: true, interval: 60, slotCount: 6 }}>
            <ViewsDirective>
                <ViewDirective option='Day' />
                <ViewDirective option='Week' />
                <ViewDirective option='WorkWeek' />
                <ViewDirective option='TimelineDay' />
            </ViewsDirective>
            <Inject services={[Day, Week, WorkWeek, TimelineViews]} />
            </ScheduleComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}

## Customizing time cells using template

The `timeScale` property also provides template option to allow customization of time slots which are as follows,

* `majorSlotTemplate` - The template option to be applied for major time slots. Here, the template accepts either the string or HTMLElement as template design and then the parsed design is displayed onto the time cells. The time details can be accessed within this template.
* `minorSlotTemplate` - The template option to be applied for minor time slots. Here, the template accepts either the string or HTMLElement as template design and then the parsed design is displayed onto the time cells. The time details can be accessed within this template.

{% tab template="schedule/timescale", iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, ViewsDirective, ViewDirective,
  Day, Week, WorkWeek, TimelineViews, Inject
} from '@syncfusion/ej2-react-schedule';
import { scheduleData } from './datasource';
import { extend, Internationalization } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
    private data: Object[] = extend([], scheduleData, null, true) as Object[];
    private instance = new Internationalization();
    private majorSlotTemplate(props): JSX.Element {
        return (<div>{this.instance.formatDate(props.date, { skeleton: 'hm' })}</div>);
    }
    private minorSlotTemplate(props): JSX.Element {
        return (<div style={ { textAlign: 'right', marginRight: '15px' } }>
        {this.instance.formatDate(props.date, { skeleton: 'ms' }).replace(':00', '')}</div>);
    }
     render() {
        return <ScheduleComponent width='100%' height='550px' selectedDate={ new Date(2018, 1, 15)} eventSettings={ { dataSource: this.data } } timeScale={ { enable: true, interval: 60, slotCount: 6,majorSlotTemplate:this.majorSlotTemplate.bind(this),
        minorSlotTemplate:this.minorSlotTemplate.bind(this) } }>
            <ViewsDirective>
                <ViewDirective option='Day' />
                <ViewDirective option='Week' />
                <ViewDirective option='TimelineWeek' />
                <ViewDirective option='WorkWeek' />
            </ViewsDirective>
            <Inject services={[Day, Week, WorkWeek, TimelineViews]} />
        </ScheduleComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}

## Hide the timescale

The grid lines which indicates the exact time duration can be enabled or disabled on the Scheduler, by setting `true` or `false` to the `enable` option within the `timeScale` property. It's default value is `true`.

{% tab template="schedule/timescale", isDefaultActive=true, iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  Day, Week, WorkWeek, TimelineViews, ScheduleComponent, ViewsDirective, ViewDirective, Inject
} from '@syncfusion/ej2-react-schedule';
import { extend } from '@syncfusion/ej2-base';
import { scheduleData } from './datasource';

class App extends React.Component<{}, {}>{
  private data: Object[] = extend([], scheduleData, null, true) as Object[];
    render() {
        return <ScheduleComponent width='100%' height='550px'
        selectedDate={new Date(2018, 1, 15)} eventSettings={ { dataSource: this.data } } timeScale={ { enable: false }}>
            <ViewsDirective>
                <ViewDirective option='Day' />
                <ViewDirective option='Week' />
                <ViewDirective option='TimelineWeek' />
                <ViewDirective option='WorkWeek' />
            </ViewsDirective>
            <Inject services={[Day, Week, WorkWeek,TimelineViews]} />
        </ScheduleComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}

## Highlighting current date and time

By default, Scheduler indicates current date with a highlighted date header on all views, as well as marks accurately the system's current time on specific views such as Day, Week, Work Week, Timeline Day, Timeline Week and Timeline Work Week views. To stop highlighting the current time indicator on Scheduler views, set `false` to the `showTimeIndicator` property which defaults to `true`.

{% tab template="schedule/timescale", isDefaultActive=true, iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  Day, Week, TimelineViews, ScheduleComponent, ViewsDirective, ViewDirective, Inject
} from '@syncfusion/ej2-react-schedule';

class App extends React.Component<{}, {}>{
    render() {
        return <ScheduleComponent width='100%' height='550px' showTimeIndicator= {true}>
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
