# Set Different Time Duration on Event Editor

In event window, start/end time duration will be processed based on the `interval` value within the `timeScale` property. By default, `interval` value is 30, therefore in event window start/end time duration will be in 30 mins duration. You can set custom interval range to the start/end time in event window using `popupOpen` event as shown below.

{% tab template="schedule/local-data", iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, WorkWeek, Month, Agenda, Inject,
  PopupOpenEventArgs } from '@syncfusion/ej2-react-schedule';
import { extend } from '@syncfusion/ej2-base';
import { scheduleData } from './datasource';

class App extends React.Component<{}, {}>{
    private data: Object[] = extend([], scheduleData, null, true) as Object[];
    private onPopupOpen(args: PopupOpenEventArgs): void {
        args.duration = 40;
    }
    render() {
        return <ScheduleComponent width= '100%' height='500px' selectedDate=
        { new Date(2018, 1, 15) } eventSettings={ { dataSource: this.data } }
        popupOpen={this.onPopupOpen.bind(this)}>
        <Inject services={[Day, Week, WorkWeek, Month, Agenda]} />
        </ScheduleComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}