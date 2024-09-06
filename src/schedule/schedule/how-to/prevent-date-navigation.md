# Prevent the Date Navigation

We can prevent navigation while clicking on the date header by simply removing `e-navigate` class from header cells which can be achieved in the `renderCell` event as shown in the below demo.

{% tab template="schedule/local-data", iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, WorkWeek, Month, Agenda, Inject,
  RenderCellEventArgs } from '@syncfusion/ej2-react-schedule';
import { extend, removeClass } from '@syncfusion/ej2-base';
import { scheduleData } from './datasource';

class App extends React.Component<{}, {}>{
    private data: Object[] = extend([], scheduleData, null, true) as Object[];
    private onRenderCell(args: RenderCellEventArgs): void {
        if(args.elementType === "dateHeader" || args.elementType === "monthCells") {
            removeClass(args.element.childNodes, "e-navigate");
        }
    }
    render() {
        return <ScheduleComponent width= '100%' height='500px' selectedDate= { new Date(2018, 1, 15) } eventSettings={ { dataSource: this.data } } currentView= 'WorkWeek'
        renderCell={this.onRenderCell.bind(this)}>
        <Inject services={[Day, Week, WorkWeek, Month, Agenda]} />
        </ScheduleComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}