---
title: "All-day scroller"
component: "Scheduler"
description: "This section explains how to enable scroller for all-day row in the scheduler"
---

# Enable scroll option on all-day section

When you have larger number of appointments in all-day row, it is difficult to view all the appointments properly. In that case you can enable scroller option for all-day row by setting true to `enableAllDayScroll` whereas its default value is false. When setting this property to true, individual scroller for all-day row is enabled when it reaches its maximum height on expanding.

> Note: This property is not applicable for Scheduler with height `auto`.

{% tab template="schedule/local-data" iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, WorkWeek, Month, Agenda, Inject } from '@syncfusion/ej2-react-schedule';
import { generateObject } from './datasource';

class App extends React.Component<{}, {}>{
    private data: Object[] = generateObject() as Object[];
    render() {
    return <ScheduleComponent  width= '100%' height='500px' selectedDate= {new Date(2021, 3, 28) } enableAllDayScroll = {true} eventSettings={ {dataSource:this.data
        } }>
          <Inject services={[Day, Week, WorkWeek, Month, Agenda]} />
        </ScheduleComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}