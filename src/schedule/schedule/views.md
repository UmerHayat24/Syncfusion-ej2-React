# Views

The Scheduler includes wide variety of view modes with unique configuration options for each view. The available view modes are listed below, out of which the `Week` view is set as active.

* Day
* Week
* Work week
* Month
* Year
* Agenda
* Month-Agenda
* Timeline Day
* Timeline Week
* Timeline Work Week
* Timeline Month
* Timeline Year

To navigate between different views and dates, the navigation options are available at the Scheduler header bar. The active view option is usually highlighted by default. The date range of the active view will also be displayed at the left corner of the header bar, clicking on which will open a calendar popup for the ease of desired date selection.

Learn how to customize each individual view of React Scheduler with different settings by watching this video:

`youtube:EhoLFF7kwX0`

> By default, Scheduler displays the calendar views such as day, week, work week, month and agenda.

## Setting specific view on scheduler

As the Scheduler displays `week` view by default, therefore to change the active view, set `currentView` property with the desired view name. The applicable view names that the Scheduler accepts are as follows,

* Day
* Week
* WorkWeek
* Month
* Year
* Agenda
* MonthAgenda
* TimelineDay
* TimelineWeek
* TimelineWorkWeek
* TimelineMonth
* TimelineYear

It is necessary to import and inject the appropriate view modules into the application to make use of these view modes on the Scheduler. Also, it is possible to display only the desired views on the Scheduler. To define and configure specific views, use the [`views`](../api/schedule/views) property.

In the following example, the Scheduler displays 4 views namely, Week, Month, TimelineWeek and Timeline Month. The appropriate view modules are imported and injected properly to display those views on the Scheduler.

{% tab template="schedule/views", iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Week, Month, TimelineViews, TimelineMonth, Inject,
  ViewsDirective, ViewDirective} from '@syncfusion/ej2-react-schedule';
import { appData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
    private data: Object[] = extend([], appData, null, true) as Object[];
    render() {
    return <ScheduleComponent  width= '100%'  height='550px' selectedDate= {new Date(2018, 1, 15)} eventSettings= { { dataSource: this.data } } >
            <ViewsDirective>
              <ViewDirective option='Week'/>
              <ViewDirective option='TimelineWeek' />
              <ViewDirective option='Month' />
              <ViewDirective option='TimelineMonth' />
            </ViewsDirective>
            <Inject services={[Week, Month, TimelineViews, TimelineMonth]} />
        </ScheduleComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}

> `ViewDirective` and `ViewsDirective` needs to be imported to define views.

To configure Scheduler with simply 2 views, but with different configurations on each view, refer the following code example. Here, the Week view displays the dates in `dd-MM-yyyy` format whereas the Month view hides the weekend days and also displays it in readonly mode.

{% tab template="schedule/views", iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, Month, Inject,
  ViewsDirective, ViewDirective} from '@syncfusion/ej2-react-schedule';
import { appData } from './datasource';
import { extend } from '@syncfusion/ej2-base';
class App extends React.Component<{}, {}>{
    private data: Object[] = extend([], appData, null, true) as Object[];
    render() {
    return <ScheduleComponent  width= '100%'  height='550px' selectedDate= {new Date(2018, 1, 15)} eventSettings= { { dataSource: this.data } } >
            <ViewsDirective>
            <ViewDirective option='Week' dateFormat='dd-MMM-yyyy' />
                <ViewDirective option='Month' showWeekend={false} readonly={true} />
            </ViewsDirective>
            <Inject services={[Week, Month]} />
        </ScheduleComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}

## View specific configuration

There are scenarios where each view may need to have different configurations. For such cases, you can define the applicable scheduler properties within the `views` Property for each view option as depicted in the following examples. The fields available to be used within each view options are as follows.

| Property | Type | Description | Applicable views |
|----------|------|-------------|------------------|
| `option` | View | It accepts the Scheduler view name, based on which we can define its related properties. The view names can be `Day`, `Week` and so on. | All views.|
| `isSelected` | Boolean | It acts similar to the `currentView` property and defines the active view of the Scheduler.| All views. |
| `dateFormat` | Date | By default, Scheduler follows the date format as per the default culture assigned to it. When it is defined under specific view, only those assigned views follows this date format. | All views. |
| `readonly` | Boolean | When set to `true`, prevents the CRUD actions on the respective view under where it is defined. | All views. |
| `resourceHeaderTemplate` | String | The template option which is used to customize the resource header cells on the Scheduler. It gets applied only on the views, wherever it is defined.| All views. |
| `dateHeaderTemplate` | String | The template option which is used to customize the date header cells and is applied only on the views, wherever it is defined. | All views. |
| `eventTemplate` | String | The template option to customize the events background. It will get applied to the events of the view to which it is currently being defined. | All views. |
| `showWeekend` | Boolean | When set to `false`, it hides the weekend days of a week from the views on which it is defined.| All views. |
| `group` | GroupModel | Allows to set different resource grouping options on all available Scheduler view modes. | All views. |
| `cellTemplate` | String | The template option to customize the work cells of the Scheduler and is applied only on the views, on which it is defined. | Applicable on all views except Agenda view. |
| `workDays` | Number[] | It is used to set the working days on the Scheduler views. | Applicable on all views except Agenda view. |
| `displayName` | String | When a particular view is customized to display with different intervals, this property allows the user to set different display name for each of the views. | Applicable on all views except Agenda and Month Agenda. |
| `interval` | Number | It allows to customize the default Scheduler views with different set of days, weeks, work weeks or months on the applicable view type. | Applicable on all views except Agenda and Month Agenda. |
| `startHour` | String | It is used to specify the start hour, from which the Scheduler should be displayed. It accepts the time string in a short skeleton format and also, hides the time beyond the specified start time. | Applicable on Day, Week, Work Week, Timeline Day, Timeline Week and Timeline Work Week views. |
| `endHour` | String | It is used to specify the end hour, at which the Scheduler ends. It accepts the time string in a short skeleton format. | Applicable on Day, Week, Work Week, Timeline Day, Timeline Week, and Timeline Work Week views. |
| `timeScale` | TimeScaleModel | Allows to set different timescale configuration on each applicable view modes. | Applicable on Day, Week, Work Week, Timeline Day, Timeline Week, and Timeline Work Week views. |
| `showWeekNumber` | Boolean | When set to `true`, shows the week number on the respective weeks.| Applicable on Day, Week, Work Week, and Month views. |
| `allowVirtualScrolling` | Boolean | It is used to enable or disable the virtual scrolling functionality. | Applicable on Agenda and Timeline views. |
| `headerRows` | HeaderRowsModel | Allows defining the custom header rows on timeline views of the Scheduler to display the year, month, week, date and hour label as an individual row. | Applicable only on all timeline views. |

### Day view

Usually a day view displays a single day with all its related appointments. It is possible to customize the day view to display more number of days by extending the `ViewDirective` with `interval` option. You can also define any of the above defined properties within the `ViewDirective` definition as depicted in the following code example.

{% tab template="schedule/views", iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Inject,
  ViewsDirective, ViewDirective
} from '@syncfusion/ej2-react-schedule';
import { appData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
  private data: Object[] = extend([], appData, null, true) as Object[];
  render() {
    return <ScheduleComponent width='100%' height='550px' selectedDate={new Date(2018, 1, 15)}
    eventSettings= { { dataSource: this.data } }>
      <ViewsDirective>
        <ViewDirective option='Day' startHour= '09:30' endHour= '18:00' timeScale= { {enable: true, slotCount: 5 }}/>
      </ViewsDirective>
      <Inject services={[Day]} />
    </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

> All the above defined properties can be accessed within Day view except `allowVirtualScrolling` and `headerRows`.

### Week view

The Week view displays a count of 7 days (from Sunday to Saturday) with all its related appointments. The first day of the week can be changed using the `firstDayOfWeek` which accepts the integer (Sunday=0, Monday=1, Tuesday=2 and so on) value. You can navigate to a particular date in day view from the week view by clicking on the appropriate dates on the date header bar.

{% tab template="schedule/views", iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, Inject,
  ViewsDirective, ViewDirective
} from '@syncfusion/ej2-react-schedule';
import { appData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
  private data: Object[] = extend([], appData, null, true) as Object[];
  render() {
    return <ScheduleComponent width='100%' height='550px' selectedDate={new Date(2018, 1, 15)}
    eventSettings= { { dataSource: this.data } }>
      <ViewsDirective>
        <ViewDirective option='Day' interval={2} displayName= '2 Days' startHour= '09:30' endHour= '18:00' timeScale= { {enable: true, slotCount: 5 }}/>
        <ViewDirective option='Week' interval={2} displayName= '2 Weeks' showWeekend= {false} isSelected= {true}/>
      </ViewsDirective>
      <Inject services={[Day, Week]} />
    </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

### Work Week view

The Work week view displays only the working days of a week (count of 5 days) and its associated appointments. It is possible to customize the working days on the work week view by using the `workDays` property which accepts an array of integer values (such as Sunday=0, Monday=1, Tuesday=2 and so on). By default, it displays from Monday to Friday (5 days). You can also navigate to a particular date in the day view from the work week view by clicking on the appropriate dates in the date header bar.

The following code example depicts how to customize the resource header cells only on the `Work Week` view of the Scheduler.

{% tab template="schedule/views", iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, WorkWeek, Inject,
  ViewsDirective, ViewDirective
} from '@syncfusion/ej2-react-schedule';
import { appData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
  private data: Object[] = extend([], appData, null, true) as Object[];
  private workDays: number[] = [2, 3, 5];
  render() {
    return <ScheduleComponent width='100%' height='550px' selectedDate={new Date(2018, 1, 15)}
    eventSettings= { { dataSource: this.data } }>
      <ViewsDirective>
        <ViewDirective option='WorkWeek' workDays={this.workDays}/>
      </ViewsDirective>
      <Inject services={[WorkWeek]} />
    </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

> The Week, Work week and Day views can display the all-day row appointments in a separate all-day row with an expand/collapse option to view it.

### Month view

A Month view displays the entire days of a particular month and all its related appointments. You can navigate to a particular date in the day view by clicking on the appropriate date text on the month cells.

By default, when you try to create an appointment through Month view, it is considered as created for an entire day. You can explicitly change this behavior by unchecking the `All-day` option from editor window, so that it defaults to the start time duration as 9.00 AM and end time as 9.30 AM.

You can also have the `+ more` text indicator on each day cell of a Month view, clicking on which will allows you to view the hidden appointments of a day.

{% tab template="schedule/views", iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Month, Inject,
  ViewsDirective, ViewDirective
} from '@syncfusion/ej2-react-schedule';
import { appData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
  private data: Object[] = extend([], appData, null, true) as Object[];
  render() {
    return <ScheduleComponent width='100%' height='550px' selectedDate={new Date(2018, 1, 15)}
    eventSettings= { { dataSource: this.data } }>
      <ViewsDirective>
        <ViewDirective option='Month' showWeekNumber= {true} readonly= {true}/>
      </ViewsDirective>
      <Inject services={[Month]} />
    </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

### Year view

A Year view displays all the days of a particular year with months and all its related appointments. You can navigate to a particular date in the day view by clicking on the appropriate date text on the year cells.

Year view is available in both the `Horizontal` and `Vertical` orientations. You can manage the orientation of year view through `views` property.

{% tab template="schedule/views", iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Year, Inject,
  ViewsDirective, ViewDirective
} from '@syncfusion/ej2-react-schedule';
import { appData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
  private data: Object[] = extend([], appData, null, true) as Object[];
  render() {
    return <ScheduleComponent width='100%' height='550px' selectedDate={new Date(2018, 1, 15)}
    eventSettings= { { dataSource: this.data } }>
      <ViewsDirective>
        <ViewDirective option='Year' showWeekNumber= {true} readonly= {true}/>
      </ViewsDirective>
      <Inject services={[Year]} />
    </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

> The year view also has module support. In that, you can get all the months of a particular year in a calendar view format. In that calendar view, appointment contained dates are highlighted with dots placed under the individual date. When you click on the date, the event popup will be displayed and the events will be listed.

### Agenda view

The Agenda view lists out the appointments in a grid-like view for the next 7 days by default from the current date. The count of the days can be changed using the API `agendaDaysCount`. It allows virtual scrolling of dates by enabling the `allowVirtualScrolling` property. Also, you can enable or disable the display of days on Scheduler that has no appointments by setting true or false to the `hideEmptyAgendaDays` property.

The following code example depicts how to customize the display of events within Agenda view alone.

{% tab template="schedule/views", iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Agenda, Inject,
  ViewsDirective, ViewDirective
} from '@syncfusion/ej2-react-schedule';
import { appData } from './datasource';
import { Internationalization, extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
  private data: Object[] = extend([], appData, null, true) as Object[];
  private instance: Internationalization = new Internationalization();
  private getTimeString(value: Date) {
      return this.instance.formatDate(value, { skeleton: 'hm' });
    }
  private eventTemplate(props): JSX.Element {
    return (<div className="template-wrap">
      <div className="subject">{props.Subject}</div>
      <div className="time">
        Time: {this.getTimeString(props.StartTime)} - {this.getTimeString(props.EndTime)}</div>
      </div>
    );
  }
  render() {
    return <ScheduleComponent width='100%' height='550px' agendaDaysCount= {3} selectedDate={new Date(2018, 1, 15)}
    eventSettings= { { dataSource: this.data } }>
      <ViewsDirective>
        <ViewDirective option='Agenda' eventTemplate= {this.eventTemplate.bind(this)}allowVirtualScrolling= {false}/>
      </ViewsDirective>
      <Inject services={[Agenda]} />
    </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

> Schedule Height is mandatory to set in pixels for Agenda view alone.

### Month Agenda view

A Month-Agenda view shows a month calendar, where clicking on a particular day will display the appointments present on that date below the calendar. The day with appointments are differentiated with a circular dot below the date of the calendar.

The following code example shows how to hide the weekend days on `MonthAgenda` view as well as the working days list is modified on Month Agenda view alone.

{% tab template="schedule/views", iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, MonthAgenda, Inject,
  ViewsDirective, ViewDirective
} from '@syncfusion/ej2-react-schedule';
import { appData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
  private data: Object[] = extend([], appData, null, true) as Object[];
  private workDays: number[] = [1,2, 3];
  render() {
    return <ScheduleComponent width='100%' height='550px' selectedDate={new Date(2018, 1, 14)}
    eventSettings= { { dataSource: this.data } }>
      <ViewsDirective>
        <ViewDirective option='MonthAgenda' showWeekend= {false} workDays= {this.workDays}/>
      </ViewsDirective>
      <Inject services={[MonthAgenda]} />
    </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

### Timeline views – Day, Week, Work Week

Similar to the day view, it shows a single day with all its appointments where the time slots are displayed horizontally. By default, the cell height adjusts as per the height set to Scheduler. When the number of appointments exceeds the visible area of the cells, the `+ more` text indicator will be displayed at the bottom to denote the presence of few more appointments in that time range.

To make use of the timeline views (Timeline Day, Timeline Week and Timeline Work Week) on Scheduler, import and inject the module `TimelineViews` from the `ej2-schedule` package.

{% tab template="schedule/views", iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, TimelineViews, Inject,
  ViewsDirective, ViewDirective
} from '@syncfusion/ej2-react-schedule';
import { appData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
  private data: Object[] = extend([], appData, null, true) as Object[];
  render() {
    return <ScheduleComponent width='100%' height='550px' selectedDate={new Date(2018, 1, 15)}
    eventSettings= { { dataSource: this.data } }>
      <ViewsDirective>
        <ViewDirective option='TimelineDay' startHour= '10:00' endHour= '15:30'/>
      </ViewsDirective>
      <Inject services={[TimelineViews]} />
    </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

Similar to the Week view, the timeline week view shows 7 days with its associated appointments with the time slots displayed horizontally.

{% tab template="schedule/views", iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, TimelineViews, Inject,
  ViewsDirective, ViewDirective
} from '@syncfusion/ej2-react-schedule';
import { appData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
  private data: Object[] = extend([], appData, null, true) as Object[];
  render() {
    return <ScheduleComponent width='100%' height='550px' selectedDate={new Date(2018, 1, 15)}
    eventSettings= { { dataSource: this.data } }>
      <ViewsDirective>
        <ViewDirective option='TimelineWeek' timeScale= {{enable: false}}/>
      </ViewsDirective>
      <Inject services={[TimelineViews]} />
    </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

The following code example depicts how to display the timeline work week view on Scheduler,

{% tab template="schedule/views", iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, TimelineViews, Agenda, Inject,
  ViewsDirective, ViewDirective
} from '@syncfusion/ej2-react-schedule';
import { appData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
  private data: Object[] = extend([], appData, null, true) as Object[];
  private workDays: number[] = [2, 3, 5];
  render() {
    return <ScheduleComponent width='100%' height='550px' selectedDate={new Date(2018, 1, 15)}
    eventSettings= { { dataSource: this.data } }>
      <ViewsDirective>
        <ViewDirective option='TimelineWorkWeek' interval= {3} workDays= {this.workDays} dateFormat= 'dd-MMM-yyyy'/>
        <ViewDirective option='Agenda'/>
      </ViewsDirective>
      <Inject services={[TimelineViews, Agenda]} />
    </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

> Clicking on the dates in the date header bar of Timeline day, Timeline week and Timeline work week will allow you to navigate to the Agenda view.

### Timeline Month view

A Timeline Month view displays the current month days along with its appointments. To make use of the timeline Month view on Scheduler, import and inject `TimelineMonth` module from the `ej2-schedule` package.

{% tab template="schedule/views", iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, TimelineMonth, TimelineViews, Inject,
  ViewsDirective, ViewDirective
} from '@syncfusion/ej2-react-schedule';
import { appData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
  private data: Object[] = extend([], appData, null, true) as Object[];
  render() {
    return <ScheduleComponent width='100%' height='550px' selectedDate={new Date(2018, 1, 15)}
    eventSettings= { { dataSource: this.data } }>
      <ViewsDirective>
        <ViewDirective option='TimelineMonth' showWeekend= {false}/>
        <ViewDirective option='TimelineDay'/>
      </ViewsDirective>
      <Inject services={[TimelineMonth, TimelineViews]} />
    </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

> Clicking on the dates in the date header bar of Timeline month will allow you to navigate to the Timeline day view.

### Timeline Year view

In Timeline Year view, each row depicts a single resource. Whereas in the vertical view, each resource is grouped parallelly as columns. Here, the resource grouping follows the tree-view like hierarchical grouping structure and can contain any level of child resources.

To make use of the timeline Year view on Scheduler, import and inject `TimelineYear` module from the `ej2-schedule` package.

{% tab template="schedule/views", iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, TimelineYear, Inject,
  ViewsDirective, ViewDirective
} from '@syncfusion/ej2-react-schedule';
import { appData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
  private data: Object[] = extend([], appData, null, true) as Object[];
  render() {
    return <ScheduleComponent width='100%' height='550px' selectedDate={new Date(2018, 1, 15)}
    eventSettings= { { dataSource: this.data } }>
      <ViewsDirective>
        <ViewDirective option='TimelineYear' displayName='Horizontal Timeline Year' isSelected={true} />
      </ViewsDirective>
      <Inject services={[TimelineYear]} />
    </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

#### Resource grouping

The following code example depicts how to group the multiple resources on Timeline Year view and its relevant events are displayed accordingly under those resources.

{% tab template="schedule/resource", iframeHeight="588px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, TimelineYear, ViewsDirective, ViewDirective,
  ResourcesDirective, ResourceDirective, Inject
} from '@syncfusion/ej2-react-schedule';
import { resourceData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
    private data: Object[] = extend([], resourceData, null, true) as Object[];
    private ownerData: Object[] = [
    { OwnerText: 'Nancy', Id: 1, OwnerColor: '#ffaa00' },
    { OwnerText: 'Steven', Id: 2, OwnerColor: '#f8a398' },
    { OwnerText: 'Michael', Id: 3, OwnerColor: '#7499e1' }
    ];
    render() {
        return <ScheduleComponent width='100%' height='550px' selectedDate= {new Date(2018, 3, 1)} eventSettings={ { dataSource: this.data } } >
            <ViewsDirective>
                <ViewDirective option='TimelineYear' displayName='Horizontal Timeline Year' isSelected={true}/>
                <ViewDirective option='TimelineYear' displayName='Vertical Timeline Year' orientation= 'Vertical' group={{ resources: ['Owners'] }}/>
            </ViewsDirective>
            <ResourcesDirective>
                <ResourceDirective field='OwnerId' title='Owner' name='Owners' allowMultiple={true}
                  dataSource={this.ownerData} textField='OwnerText' idField='Id' colorField='OwnerColor'>
                </ResourceDirective>
            </ResourcesDirective>
            <Inject services={[TimelineYear]} />
        </ScheduleComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

#### Auto row height

Timeline Year view supports Auto row height. When the feature `rowAutoHeight` is enabled, the row height gets auto-adjusted based on the number of overlapping events occupied in the same time range. If you disable the Auto row height, you have the `+ more` text indicator on each day cell of a Timeline Year view, clicking on which will allow you to view the hidden appointments of a day.

{% tab template="schedule/events", iframeHeight="588px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { ScheduleComponent, TimelineYear, Inject, ViewsDirective, ViewDirective } from '@syncfusion/ej2-react-schedule';
import { extend } from '@syncfusion/ej2-base';
import { scheduleData } from './datasource';

class App extends React.Component<{}, {}> {
  private data: Object[] = extend([], scheduleData, null, true) as Object[];
  render() {
    return <ScheduleComponent width='100%' height='550px' currentView='Month'
    selectedDate={new Date(2018, 1, 17)} rowAutoHeight= {true} eventSettings={ { dataSource: this.data } }>
      <ViewsDirective>
      <ViewDirective option='TimelineYear' displayName='Horizontal Timeline Year' isSelected={true}/>
      <ViewDirective option='TimelineYear' displayName='Vertical Timeline Year' orientation= 'Vertical'/>
      </ViewsDirective>
    <Inject services={[TimelineYear]} />
    </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

## Extending view intervals

It is possible to customize the display of default number of days on different Scheduler view modes. For example, a day view can be extended to display 3 days by setting the `interval` option as 3 for the `Day` option within the `ViewDirective` as depicted in the following code example. In the same way, you can also display 2 weeks by setting interval 2 for the `Week` option.

You can provide the alternative display name for such customized views on the Scheduler header bar, by setting the appropriate `displayName` property.

{% tab template="schedule/views", iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, Inject,
  ViewsDirective, ViewDirective
} from '@syncfusion/ej2-react-schedule';
import { appData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
  private data: Object[] = extend([], appData, null, true) as Object[];
  render() {
    return <ScheduleComponent width='100%' height='550px' selectedDate={new Date(2018, 1, 15)}
    eventSettings= { { dataSource: this.data } }>
      <ViewsDirective>
        <ViewDirective option='Day' interval={3} displayName= '3 Days'/>
        <ViewDirective option='Week' interval={2} displayName= '2 Weeks'/>
      </ViewsDirective>
      <Inject services={[Day, Week]} />
    </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

> The view intervals can be extended on all the Scheduler view modes except Agenda and Month-Agenda views.

## See Also

* [How to restrict view navigation while clicking on dates](./how-to/prevent-date-navigation)

> You can refer to our [React Scheduler](https://www.syncfusion.com/react-ui-components/react-scheduler) feature tour page for its groundbreaking feature representations. You can also explore our [React Scheduler example](https://ej2.syncfusion.com/react/demos/#/material/schedule/overview) to knows how to present and manipulate data.
