# Customize the Events Dynamically Before it Renders on UI

The `eventRendered` event will be triggered before rendering the appointments on Schedule where it can be customized. In the below demo, custom field `CategoryColor` is added to the appointment collection and based on certain condition, appointment background color is changed with `CategoryColor` field value.

{% tab template="schedule/local-data", iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, WorkWeek, Month, Agenda, Inject,
EventRenderedArgs } from '@syncfusion/ej2-react-schedule';
import { extend } from '@syncfusion/ej2-base';
import { scheduleData } from './datasource';

class App extends React.Component<{}, {}>{
    private data: Object[] = extend([], scheduleData, null, true) as Object[];
    private onEventRendered(args: EventRenderedArgs): void {
        if(args.data.StartTime.getDate()===11 || args.data.StartTime.getDate() === 15){
            (args.element as HTMLElement).style.backgroundColor = args.data.CategoryColor;
        }
    }
    render() {
        return <ScheduleComponent width= '100%' height='500px' selectedDate=
        { new Date(2018, 1, 15) }eventSettings={ { dataSource: this.data } }
        eventRendered={this.onEventRendered.bind(this)}>
        <Inject services={[Day, Week, WorkWeek, Month, Agenda]} />
        </ScheduleComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}