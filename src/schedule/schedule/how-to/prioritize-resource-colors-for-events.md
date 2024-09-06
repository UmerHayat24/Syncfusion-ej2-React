# Prioritize the Resource Color for Events

By default top level resource color will be applied for the events. If user wants to apply specific resource color to events irrespective of its parent resource color, it can be achieved by `resourceColorField` field within `eventSettings` property as shown below.

{% tab template="schedule/resource", iframeHeight="588px", compileJsx=true %}

```tsx

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import {
    Week, Month, Agenda, ScheduleComponent, ResourcesDirective,
    ResourceDirective, Inject
} from '@syncfusion/ej2-react-schedule';
import { extend } from '@syncfusion/ej2-base';
import { resourceData } from './datasource';

class App extends React.Component<{}, {}>{
    private data: Object[] = extend([], resourceData, null, true) as Object[];
    private roomData: Object[] = [
     { RoomText: 'ROOM 1', Id: 1, RoomGroupId: 1, RoomColor: '#cb6bb2' },
     { RoomText: 'ROOM 2', Id: 2, RoomGroupId: 2, RoomColor: '#56ca85' }
  ];
  private ownerData: Object[] = [
   { OwnerText: 'Nancy', Id: 1, OwnerGroupId: 1, OwnerColor: '#ffaa00' },
   { OwnerText: 'Steven', Id: 2, OwnerGroupId: 2, OwnerColor: '#f8a398' },
   { OwnerText: 'Michael', Id: 3, OwnerGroupId: 1, OwnerColor: '#7499e1' }
  ];
  render() {
    return <ScheduleComponent  width= '100%' height='550px' selectedDate= {new Date(2018, 3, 1)}
        eventSettings= { { dataSource: this.data, resourceColorField: 'Owners'  } }
        group={ {  resources: ['Rooms', 'Owners'] } } >
        <ResourcesDirective>
                <ResourceDirective field='RoomId' title='Room' name='Rooms'
                 allowMultiple={false}
                  dataSource={this.roomData} textField='RoomText' idField='Id' groupIDField= 'RoomGroupId' colorField='RoomColor'>
                </ResourceDirective>
                <ResourceDirective field='OwnerId' title='Owner' name='Owners'
                 allowMultiple={true}
                  dataSource={this.ownerData} textField='OwnerText' idField='Id' groupIDField= 'OwnerGroupId' colorField='OwnerColor'>
                </ResourceDirective>
        </ResourcesDirective>
        <Inject services={[Week, Month, Agenda]} />
    </ScheduleComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));


```

{% endtab %}

> The `resourceColorField` field value should be as same as the `name` field value given with in `resources` property.