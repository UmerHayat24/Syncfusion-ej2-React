# Perform CRUD Actions Dynamically

CRUD actions can be manually performed on appointments using `addEvent`, `saveEvent` and `deleteEvent` methods as shown below.

## Normal event

{% tab template="schedule/app-crud", iframeHeight="616px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, WorkWeek, Month, Inject,
  ViewsDirective, ViewDirective
} from '@syncfusion/ej2-react-schedule';
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';

class App extends React.Component<{}, {}>{
    private scheduleObj: ScheduleComponent;
    private scheduleData: Object[] = [{
        Id: 3,
        Subject: 'Testing',
        StartTime: new Date(2018, 1, 11, 9, 0),
        EndTime: new Date(2018, 1, 11, 10, 0),
        IsAllDay: false
    },{
        Id: 4,
        Subject: 'Vacation',
        StartTime: new Date(2018, 1, 13, 9, 0),
        EndTime: new Date(2018, 1, 13, 10, 0),
        IsAllDay: false
    }];
    private onClickAdd(): void {
       let Data: Object[] = [{
        Id: 1,
        Subject: 'Conference',
        StartTime: new Date(2018, 1, 12, 9, 0),
        EndTime: new Date(2018, 1, 12, 10, 0),
        IsAllDay: false
    },{
        Id: 2,
        Subject: 'Meeting',
        StartTime: new Date(2018, 1, 15, 10, 0),
        EndTime: new Date(2018, 1, 15, 11, 30),
        IsAllDay: false
        }];
       this.scheduleObj.addEvent(Data);
    }
     private onClickSave(): void {
        let Data: Object = {
        Id: 3,
        Subject: 'Testing-edited',
        StartTime: new Date(2018, 1, 11, 10, 0),
        EndTime: new Date(2018, 1, 11, 11, 0),
        IsAllDay: false
    };
        this.scheduleObj.saveEvent(Data);
    }
    private onClickDelete(): void {
        this.scheduleObj.deleteEvent(4);
    }

    render() {
        return( <div>
            <ButtonComponent id='add' title='Add' onClick={ this.onClickAdd.bind(this) }>Add</ButtonComponent>
            <ButtonComponent id='edit' title='Edit' onClick={ this.onClickSave.bind(this) }>Edit</ButtonComponent>
            <ButtonComponent id='delete' title='Delete' onClick={ this.onClickDelete.bind(this) }>Delete</ButtonComponent> <ScheduleComponent ref={t => this.scheduleObj = t} width= '100%' height='550px' selectedDate=
            { new Date(2018, 1, 15) } eventSettings={ { dataSource: this. scheduleData } }>
                <ViewsDirective>
                    <ViewDirective option='Day' />
                    <ViewDirective option='Week' />
                    <ViewDirective option='WorkWeek' />
                    <ViewDirective option='Month' />
                </ViewsDirective>
                <Inject services={[Day, Week, WorkWeek, Month ]} />
            </ScheduleComponent>
        </div>)
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}

## Recurrence event

{% tab template="schedule/app-crud", isDefaultActive=true, iframeHeight="616px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, WorkWeek, Month, Inject,
  ViewsDirective, ViewDirective } from '@syncfusion/ej2-react-schedule';
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';

class App extends React.Component<{}, {}>{
    private scheduleObj: ScheduleComponent;
    private scheduleData: Object[] = [{
        Id: 3,
        Subject: 'Testing',
        StartTime: new Date(2018, 1, 11, 9, 0),
        EndTime: new Date(2018, 1, 11, 10, 0),
        IsAllDay: false,
        RecurrenceRule: 'FREQ=DAILY;INTERVAL=1;COUNT=3'
    },{
        Id: 4,
        Subject: 'Vacation',
        StartTime: new Date(2018, 1, 12, 11, 0),
        EndTime: new Date(2018, 1, 12, 12, 0),
        IsAllDay: false,
        RecurrenceRule: 'FREQ=DAILY;INTERVAL=1;COUNT=2'
        }];
    private onClickAdd(): void {
        let Data: Object[] = [{
        Id: 1,
        Subject: 'Conference',
        StartTime: new Date(2018, 1, 15, 9, 0),
        EndTime: new Date(2018, 1, 15, 10, 0),
        IsAllDay: false,
        RecurrenceRule: 'FREQ=DAILY;INTERVAL=1;COUNT=2'
    }];
        this.scheduleObj.addEvent(Data);
    }
    private onClickSave(): void {
        let data: Object = new DataManager(scheduleObj.getCurrentViewEvents()).executeLocal(new Query().where('RecurrenceID', 'equal', 3));
        data[0].Subject = 'Occurrence edited';
        this.scheduleObj.saveEvent(data[0],'EditOccurrence');
    }
    private onClickDelete(): void {
        let Data: Object[] = [{
        Id: 4,
        Subject: 'Vacation',
        RecurrenceID: 4,
        StartTime: new Date(2018, 1, 12, 11, 0),
        EndTime: new Date(2018, 1, 12, 12, 0),
        IsAllDay: false,
        RecurrenceRule: 'FREQ=DAILY;INTERVAL=1;COUNT=2'
       }];
        this.scheduleObj.deleteEvent(Data,'DeleteSeries');
    }
    render() {
        return( <div>
            <ButtonComponent id='add' title='Add' onClick=
            { this.onClickAdd.bind(this) }>Add</ButtonComponent>
            <ButtonComponent id='edit' title='Edit' onClick={ this.onClickSave.bind(this) }>Edit</ButtonComponent>
            <ButtonComponent id='delete' title='Delete' onClick={ this.onClickDelete.bind(this) }>Delete</ButtonComponent> <ScheduleComponent ref={t => this.scheduleObj = t} width= '100%' height='550px' selectedDate=
            { new Date(2018, 1, 15) } eventSettings={ { dataSource: this.scheduleData } }>
                <ViewsDirective>
                    <ViewDirective option='Day' />
                    <ViewDirective option='Week' />
                    <ViewDirective option='WorkWeek' />
                    <ViewDirective option='Month' />
                    </ViewsDirective>
                <Inject services={[Day, Week, WorkWeek, Month ]} />
            </ScheduleComponent>
        </div>)
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}

> When a single occurrence of the recurrence appointment is edited, `recurrenceID` field will be added which holds the `id` value of its parent recurrence appointment. It is applicable only for the edited occurrence appointments. Therefore the collection passing to the `saveEvent` with action as **EditOccurrence** should have `RecurrenceID` field as shown above.