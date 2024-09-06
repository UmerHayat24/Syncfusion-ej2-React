# Scheduler Dimensions

The Scheduler dimensions refers to both height and width of the entire layout and it accepts 3 types of values.

* auto
* pixel
* percentage

## Auto Height and Width

When height and width of the Scheduler are set to `auto`, it will try as hard as possible to keep an element the same width as its parent container. In other words, the parent container that holds Scheduler, it's width/height will be the sum of its children. By default, Scheduler is assigned with `auto` values for both height and width properties.

{% tab template="schedule/events", iframeHeight="1085px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, WorkWeek, Month, Agenda, Inject
} from '@syncfusion/ej2-react-schedule';
import { scheduleData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
    private data: Object[] = extend([], scheduleData, null, true) as Object[];
    render() {
    return <ScheduleComponent height='auto' width='auto' selectedDate= {new Date(2018, 1, 15)} eventSettings={ { dataSource: this.data } }>
    <Inject services={[Day, Week, WorkWeek, Month, Agenda]} />
    </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

## Height and Width in pixel

The Scheduler height and width will be rendered exactly as per the given pixel values. It accepts both string and number values.

{% tab template="schedule/events", iframeHeight="588px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, WorkWeek, Month, Agenda, Inject
} from '@syncfusion/ej2-react-schedule';
import { scheduleData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
    private data: Object[] = extend([], scheduleData, null, true) as Object[];
    render() {
    return <ScheduleComponent height='550px' width='650px' selectedDate= {new Date(2018, 1, 15)} eventSettings={ { dataSource: this.data } }>
    <Inject services={[Day, Week, WorkWeek, Month, Agenda]} />
    </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

## Height and Width in percentage

When height and width of the Scheduler are given as percentage, it will make the Scheduler as wide as the parent container.

{% tab template="schedule/events", iframeHeight="1085px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, WorkWeek, Month, Agenda, Inject
} from '@syncfusion/ej2-react-schedule';
import { scheduleData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
    private data: Object[] = extend([], scheduleData, null, true) as Object[];
    render() {
    return <ScheduleComponent height='100%' width='100%' selectedDate= {new Date(2018, 1, 15)} eventSettings={ { dataSource: this.data } }>
    <Inject services={[Day, Week, WorkWeek, Month, Agenda]} />
    </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

> You can refer to our [React Scheduler](https://www.syncfusion.com/react-ui-components/react-scheduler) feature tour page for its groundbreaking feature representations. You can also explore our [React Scheduler example](https://ej2.syncfusion.com/react/demos/#/material/schedule/overview) to knows how to present and manipulate data.

## See Also

* [How to Change Scheduler Cell Dimensions](./cell-customization/#setting-cell-dimensions-in-all-views)
