# Open Editor Window Manually

## Open Editor Window externally

Schedule allows user to manually open the event editor on specific time or on certain events using `openEditor` method as shown below.

{% tab template="schedule/editor-open", iframeHeight="616px", compileJsx=true %}

```tsx

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import {
    Day, Week, WorkWeek, Month, ScheduleComponent, ViewsDirective, ViewDirective, Inject
} from '@syncfusion/ej2-react-schedule';
import { scheduleData } from './datasource';
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';

class App extends React.Component<{}, {}>{
    private scheduleObj: ScheduleComponent;
    private onClickButton1(): void {
        let cellData: Object ={
        startTime: new Date(2018, 1, 15, 10, 0),
        endTime: new Date(2018, 1, 15, 11, 0),
        };
        this.scheduleObj.openEditor(cellData,'Add');
    }
    private onClickButton2(): void {
        let eventData: Object ={
        Id: 4,
        Subject: 'Meteor Showers in 2018',
        StartTime: new Date(2018, 1, 14, 13, 0),
        EndTime: new Date(2018, 1, 14, 14, 30)
    };
    this.scheduleObj.openEditor(eventData,'Save');
    }
    render() {
    return (<div>
        <ButtonComponent id='btn1' title='Click to open Editor' onClick={this.onClickButton1.bind(this)}>Click to open Editor</ButtonComponent>
        <ButtonComponent id='btn2' title='Click to open Event Editor' onClick={this.onClickButton2.bind(this)}>Click to open Event Editor</ButtonComponent>
        <ScheduleComponent ref={t => this.scheduleObj = t} height='550px' selectedDate= {new Date(2018, 1, 15)}
        eventSettings= { { dataSource: this.scheduleData } } >
            <ViewsDirective>
                <ViewDirective option='Day' />
                <ViewDirective option='Week' />
                <ViewDirective option='WorkWeek' />
                <ViewDirective option='Month' />
            </ViewsDirective>
            <Inject services={[Day, Week, WorkWeek, Month]} />
        </ScheduleComponent>
    </div>)
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}

## Open editor window on single click

By default, Scheduler Editor window will open when double clicking the cells or appointments. You can also open the editor window with single click by using `openEditor` method in `eventClick` and `cellClick` events of scheduler and setting false to `showQuickInfo`. The following example shows how to open editor window on single click of cells and appointments.

{% tab template="schedule/editor-open", iframeHeight="616px", compileJsx=true %}

```tsx

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import {
    Day, Week, WorkWeek, Month, ScheduleComponent, ViewsDirective, ViewDirective, CellClickEventArgs, EventClickArgs, Inject
} from '@syncfusion/ej2-react-schedule';
import { schedulerData } from './datasource';

class App extends React.Component<{}, {}>{
    private scheduleObj: ScheduleComponent;
    private onCellClick(args: CellClickEventArgs): void {
        this.scheduleObj.openEditor(args, 'Add');
    }
    private onEventClick(args: EventClickArgs): void {
      if (!(args.event as any).RecurrenceRule) {
        this.scheduleObj.openEditor(args.event, 'Save');
        }
        else {
        this.scheduleObj.quickPopup.openRecurrenceAlert();
        }
    }
  
    render() {
    return (<div>
        <ScheduleComponent ref={t => this.scheduleObj = t} height='550px' selectedDate= {new Date(2021, 7, 15)}
        eventSettings= { { dataSource: this.schedulerData } } showQuickInfo = {false} eventClick={this.onEventClick.bind(this)}
        cellClick={this.onCellClick.bind(this)} >
            <ViewsDirective>
                <ViewDirective option='Day' />
                <ViewDirective option='Week' />
                <ViewDirective option='WorkWeek' />
                <ViewDirective option='Month' />
            </ViewsDirective>
            <Inject services={[Day, Week, WorkWeek, Month]} />
        </ScheduleComponent>
    </div>)
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}
