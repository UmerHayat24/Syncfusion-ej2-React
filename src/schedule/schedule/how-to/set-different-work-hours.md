# Set Different Working Hours on Different Days

By default, the work hours of the Scheduler is highlighted based on the start and end values provided within the `workHours` property which remains same for all days. To highlight different work hours range for different days,`setWorkHours` method can be used as follows.

{% tab template="schedule/editor-open", iframeHeight="616px", compileJsx=true %}

```tsx

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import {
    Day, Week, WorkWeek, Month, ScheduleComponent, ResourcesDirective,
    ResourceDirective, ViewsDirective, ViewDirective,
    Inject
} from '@syncfusion/ej2-react-schedule';
import { extend } from '@syncfusion/ej2-base';
import { scheduleData } from './datasource';
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';

class App extends React.Component<{}, {}>{
    private scheduleObj: ScheduleComponent;
    private data: Object[] = extend([], scheduleData, null, true) as Object[];
    private onClick(): void{
      let btnElement: HTMLElement = document.querySelector('#btn1') as HTMLElement;
      let btnElement2: HTMLElement = document.querySelector('#btn2') as HTMLElement;
      btnElement.innerText = 'Change the work hours';
      btnElement2.style.display='none';
      let dates: Date[] = [new Date(2018, 1, 15), new Date(2018, 1, 17)];
      this.scheduleObj.setWorkHours(dates, '11:00','20:00');
    }
    render() {
        return ( <div>
            <ButtonComponent id='btn1' title='Click to open Editor' onClick={ this.onClick.bind(this) }>Click to open Editor</ButtonComponent>
            <ButtonComponent id='btn2' title='Click to open Event Editor' onClick={ this.onClick.bind(this) }>Click to open Event Editor</ButtonComponent>
            <ScheduleComponent ref={t => this.scheduleObj = t}  height='550px' selectedDate= {new Date(2018, 1, 15)}
            workHours= { { highlight: true, start: '09:00', end: '11:00'} }
            eventSettings= { { dataSource: this.data } }>
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