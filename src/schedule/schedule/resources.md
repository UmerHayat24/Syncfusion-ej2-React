# Resources and Grouping

Resources and grouping support allows the Scheduler to be shared by multiple resources. Also, the appointments of each resources are displayed under relevant resources. Each resource in the Scheduler is arranged in a column/row wise order, with individual spacing to display all its respective appointments on a single page. It also supports the multiple levels of grouping of resources, thus enabling the categorization of resources in a hierarchical structure and shows it either in expandable groups (Timeline views) or else vertical hierarchy one after the other (Calendar views).

It is also possible to assign one or more resources to the same appointment, by allowing multiple selection of resource options available in the event editor window.

The HTML5 JavaScript Scheduler groups the resources based on different criteria. It includes grouping appointments based on resources, grouping resources based on dates, and timeline scheduling. Also, the data for resources bind with Scheduler either as a local JSON collection or URL, retrieving data from remote data services.

Learn how to add appointments of multiple resources to the React Scheduler from this video:

`youtube:uzlwjdvaJzw`

## Resource fields

The default options available within the `resources` collection are as follows,

| Field name | Type | Description |
|-------|---------| --------------- |
| `field` | String | A value that binds to the resource field of event object. |
| `title` | String | It holds the title of the resource field to be displayed on the event editor window. |
| `name` | String | A unique resource name used for differentiating various resource objects while grouping. |
| `allowMultiple` | Boolean | When set to `true`, allows multiple selection of resource names, thus creating multiple instances of same appointment for the selected resources. |
| `dataSource` | Object | Assigns the resource `dataSource`, where data can be passed either as an array of JavaScript objects, or else can create an instance of [`DataManager`](http://ej2.syncfusion.com/documentation/data/api-dataManager.html) in case of processing remote data and can be assigned to the `dataSource` property. With the remote data assigned to `dataSource`, check the available [adaptors](http://ej2.syncfusion.com/documentation/data/adaptors.html) to customize the data processing. |
| `query` | Query | Defines the external [`query`](http://ej2.syncfusion.com/documentation/data/api-query.html) that will be executed along with the data processing. |
| `idField` | String | Binds the resource ID field name from the resources `dataSource`. |
| `textField` | String | Binds the text field name from the resources `dataSource`. It usually holds the resource names. |
| `groupIDField` | String | Binds the group ID field name from the resource `dataSource`. It usually holds the value of resource IDs of parent level resources. |
| `colorField` | String | Binds the color field name from the resource `dataSource`. The color value mapped in this field will be applied to the events of resources. |
| `startHourField` | String | Binds the start hour field name from the resource `dataSource`. It allows to provide different work start hour for the resources. |
| `endHourField` | String | Binds the end hour field name from the resource `dataSource`. It allows to provide different work end hour for the resources. |
| `workDaysField` | String | Binds the work days field name from the resources `dataSource`. It allows to provide different working days collection for the resources. |
| `cssClassField` | String | Binds the custom CSS class field name from the resources `dataSource`. It maps the CSS class written for the specific resources and applies it to the events of those resources. |

## Resource data binding

The data for resources can bind with Scheduler either as a local JSON collection or a service URL, retrieving resource data from remote data services.

### Using local JSON data

The following code example depicts how to bind the local JSON data to the `dataSource` of `resources` collection.

{% tab compileJsx=true%}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  Week, Month, Agenda, ScheduleComponent, ResourcesDirective, ResourceDirective,
  Inject
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
            <ResourcesDirective>
                <ResourceDirective field='OwnerId' title='Owner' name='Owners' allowMultiple={true}
                  dataSource={this.ownerData} textField='OwnerText' idField='Id' colorField='OwnerColor'>
                </ResourceDirective>
            </ResourcesDirective>
            <Inject services={[Week, Month, Agenda]} />
        </ScheduleComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

### Using remote service URL

The following code example depicts how to bind the remote data for resources `dataSource`.

{% tab compileJsx=true%}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  Week, Month, Agenda, ScheduleComponent, ResourcesDirective, ResourceDirective,
  Inject
} from '@syncfusion/ej2-react-schedule';
import { resourceData } from './datasource';
import { extend } from '@syncfusion/ej2-base';
import { DataManager, UrlAdaptor } from '@syncfusion/ej2-data';

class App extends React.Component<{}, {}>{
    private data: Object[] = extend([], resourceData, null, true) as Object[];
    private ownerData: DataManager = new DataManager({
        url: 'Home/GetResourceData',
        adaptor: new UrlAdaptor,
        crossDomain: true
  });
    render() {
        return <ScheduleComponent width='100%' height='550px' selectedDate= {new Date(2018, 3, 1)} eventSettings={ { dataSource: this.data } } >
            <ResourcesDirective>
                <ResourceDirective field='OwnerId' title='Owner' name='Owners' allowMultiple={true}
                  dataSource={this.ownerData} textField='OwnerText' idField='Id' colorField='OwnerColor'>
                </ResourceDirective>
            </ResourcesDirective>
            <Inject services={[Week, Month, Agenda]} />
        </ScheduleComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

## Scheduler with multiple resources

It is possible to display the Scheduler in default mode without visually showcasing all the resources in it, but allowing to assign the required resources to the appointments through the event editor resource options.

The appointments belonging to the different resources will be displayed altogether on the default Scheduler, which will be differentiated based on the resource color assigned in the **resources** (depicting to which resource that particular appointment belongs) collection.

**Example:** To display default Scheduler with multiple resource options in the event editor, ignore the group option and simply define the `resources` property with all its internal options.

{% tab template="schedule/resource", iframeHeight="588px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  Week, Month, Agenda, ScheduleComponent, ViewsDirective, ViewDirective,
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
                <ViewDirective option='Week' />
                <ViewDirective option='Month' />
                <ViewDirective option='Agenda' />
            </ViewsDirective>
            <ResourcesDirective>
                <ResourceDirective field='OwnerId' title='Owner' name='Owners' allowMultiple={true}
                  dataSource={this.ownerData} textField='OwnerText' idField='Id' colorField='OwnerColor'>
                </ResourceDirective>
            </ResourcesDirective>
            <Inject services={[Week, Month, Agenda]} />
        </ScheduleComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

> Setting `allowMultiple` to `true` in the above code example allows you to select multiple resources from the event editor and also creates multiple copies of the same appointment in the Scheduler for each resources while rendering.

## Resource grouping

Resource grouping support allows the Scheduler to group the resources in a hierarchical structure both as an expandable groups (Timeline views) and as vertical hierarchy displaying resources one after the other (Resources view).

Scheduler supports both single and multiple levels of resource grouping that can be customized both in timeline and vertical Scheduler views.

Explore the advanced options available with the multiple resources and grouping concepts of React Scheduler by watching this video:

`youtube:IkZ-Rmt0Fiw`

### Vertical resource view

The following code example displays how the multiple resources are grouped and its events are portrayed in the default calendar views.

{% tab template="schedule/resource", iframeHeight="588px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from "react-dom";
import {
  Week, Month, Agenda, ScheduleComponent, ViewsDirective, ViewDirective, ResourcesDirective, ResourceDirective, Inject
} from '@syncfusion/ej2-react-schedule';
import { timelineResourceData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
    private data: Object[] = extend([], timelineResourceData, null, true) as Object[];
    private projectData: Object[] = [
    { text: 'PROJECT 1', id: 1, color: '#cb6bb2' },
    { text: 'PROJECT 2', id: 2, color: '#56ca85' },
    { text: 'PROJECT 3', id: 3, color: '#df5286' },
    ];
    private categoryData: Object[] = [
    { text: 'Development', id: 1, color: '#1aaa55' },
    { text: 'Testing', id: 2, color: '#7fa900' }
    ];
    render() {
        return <ScheduleComponent width='100%' height='550px' currentView='Month' selectedDate= {new Date(2018, 3, 4)} eventSettings={ { dataSource: this.data } } group={ { byGroupID: false, resources: ['Projects', 'Categories'] } } >
              <ViewsDirective>
                <ViewDirective option='Week' />
                <ViewDirective option='Month' />
                <ViewDirective option='Agenda' />
              </ViewsDirective>
              <ResourcesDirective>
                <ResourceDirective field='ProjectId' title='Choose Project' name='Projects' allowMultiple={false}
                  dataSource={this.projectData} textField='text' idField='id' colorField='color'>
                </ResourceDirective>
                <ResourceDirective field='TaskId' title='Category' name='Categories' allowMultiple={true}
                  dataSource={this.categoryData} textField='text' idField='id' colorField='color'>
                </ResourceDirective>
              </ResourcesDirective>
            <Inject services={[Week, Month, Agenda]} />
        </ScheduleComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

### Timeline resource view

The following code example depicts how to group the multiple resources on Timeline Scheduler views and its relevant events are displayed accordingly under those resources.

{% tab template="schedule/resource", iframeHeight="588px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  TimelineViews, TimelineMonth, ScheduleComponent, ViewsDirective, ViewDirective,
   ResourcesDirective, ResourceDirective, Inject
} from '@syncfusion/ej2-react-schedule';
import { resourceData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
    private data: Object[] = extend([], resourceData, null, true) as Object[];
    private roomData: Object[] = [
            { RoomText: 'ROOM 1', Id: 1, RoomColor: '#cb6bb2' },
            { RoomText: 'ROOM 2', Id: 2, RoomColor: '#56ca85' }
            ]
    private ownerData: Object[] = [
        { OwnerText: 'Nancy', Id: 1, GroupId: 1, OwnerColor: '#ffaa00' },
        { OwnerText: 'Steven', Id: 2, GroupId: 2, OwnerColor: '#f8a398' },
        { OwnerText: 'Michael', Id: 3, GroupId: 1, OwnerColor: '#7499e1' }
    ];
    render() {
        return <ScheduleComponent width='100%' height='550px' currentView='TimelineWeek' selectedDate= {new Date(2018, 3, 1)} eventSettings={ { dataSource: this.data } } group={ { resources: ['Rooms', 'Owners'] } }>
            <ViewsDirective>
                <ViewDirective option='TimelineDay' />
                <ViewDirective option='TimelineWeek' />
                <ViewDirective option='TimelineMonth' />
            </ViewsDirective>
            <ResourcesDirective>
                <ResourceDirective field='RoomId' title='Room' name='Rooms'
                  dataSource={this.roomData} textField='RoomText' idField='Id' colorField='RoomColor'>
                </ResourceDirective>
                <ResourceDirective field='OwnerId' title='Owner' name='Owners' allowMultiple={true}
                  dataSource={this.ownerData} textField='OwnerText' idField='Id' groupIDField='GroupId' colorField='OwnerColor'>
                </ResourceDirective>
            </ResourcesDirective>
            <Inject services={[TimelineViews, TimelineMonth]} />
        </ScheduleComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

### Grouping single-level resources

This kind of grouping allows the Scheduler to display all the resources at a single level simultaneously. The appointments mapped under resources will be displayed with the colors as per the `colorField` defined on the resources collection.

**Example:** To display the Scheduler with single level resource grouping,

{% tab template="schedule/resource", iframeHeight="588px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  Week, Month, TimelineViews, TimelineMonth, Agenda, ScheduleComponent, ViewsDirective, ViewDirective,
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
        return <ScheduleComponent width='100%' height='550px' currentView='Week' selectedDate= {new Date(2018, 3, 1)} eventSettings={ { dataSource: this.data } } group={ { resources: ['Owners'] } }>
            <ViewsDirective>
                <ViewDirective option='Week' />
                <ViewDirective option='Month' />
                <ViewDirective option='TimelineWeek' />
                <ViewDirective option='TimelineMonth' />
                <ViewDirective option='Agenda' />
            </ViewsDirective>
            <ResourcesDirective>
                <ResourceDirective field='OwnerId' title='Owner' name='Owners' allowMultiple={true}
                  dataSource={this.ownerData} textField='OwnerText' idField='Id' colorField='OwnerColor'>
                </ResourceDirective>
            </ResourcesDirective>
            <Inject services={[Week, Month, TimelineViews, TimelineMonth, Agenda]} />
        </ScheduleComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

> The `name` field defined in the **resources** collection namely `Owners` will be mapped within the `group` property, in order to enable the grouping option with those resource levels on the Scheduler.

### Grouping multi-level resources

It is possible to group the resources of Scheduler in multiple levels, by mapping the child resources to each parent resource. In the following example, there are 2 levels of resources, on which the second level resources are defined with `groupID` mapping to the first level resource's ID so as to establish the parent-child relationship between them.

**Example:** To display the Scheduler with multiple level resource grouping options,

{% tab template="schedule/resource", iframeHeight="588px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  Week, Month, TimelineViews, TimelineMonth, Agenda, ScheduleComponent, ViewsDirective, ViewDirective,
   ResourcesDirective, ResourceDirective, Inject
} from '@syncfusion/ej2-react-schedule';
import { resourceData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
    private data: Object[] = extend([], resourceData, null, true) as Object[];
    private roomData: Object[] = [
            { RoomText: 'ROOM 1', Id: 1, RoomColor: '#cb6bb2' },
            { RoomText: 'ROOM 2', Id: 2, RoomColor: '#56ca85' }
            ]
    private ownerData: Object[] = [
        { OwnerText: 'Nancy', Id: 1, GroupId: 1, OwnerColor: '#ffaa00' },
        { OwnerText: 'Steven', Id: 2, GroupId: 2, OwnerColor: '#f8a398' },
        { OwnerText: 'Michael', Id: 3, GroupId: 1, OwnerColor: '#7499e1' }
    ];
    render() {
        return <ScheduleComponent width='100%' height='550px' selectedDate= {new Date(2018, 3, 1)} eventSettings={ { dataSource: this.data } } group={ { resources: ['Rooms', 'Owners'] } } >
            <ResourcesDirective>
                <ResourceDirective field='RoomId' title='Room' name='Rooms'
                  dataSource={this.roomData} textField='RoomText' idField='Id' colorField='RoomColor'>
                </ResourceDirective>
                <ResourceDirective field='OwnerId' title='Owner' name='Owners' allowMultiple={true}
                  dataSource={this.ownerData} textField='OwnerText' idField='Id' groupIDField='GroupId' colorField='OwnerColor'>
                </ResourceDirective>
            </ResourcesDirective>
            <ViewsDirective>
                <ViewDirective option='Week' />
                <ViewDirective option='Month' />
                <ViewDirective option='TimelineWeek' />
                <ViewDirective option='TimelineMonth' />
            </ViewsDirective>
            <Inject services={[Week, Month, TimelineViews, TimelineMonth]} />
        </ScheduleComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

### One-to-One grouping

In multi-level grouping, Scheduler usually groups the resources on the child level based on the `GroupID` that maps with the `Id` field of parent level resources (as `byGroupID` set to true by default). There are also option which allows you to group all the child resource(s) against each of its parent resource(s). To enable this kind of grouping, set `false` to the `byGroupID` option within the `group` property. In the following code example, there are two levels of resources, on which all the 3 resources at the child level is mapped one to one with each resource on the first level.

{% tab template="schedule/resource", iframeHeight="588px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  Week, Month, TimelineViews, TimelineMonth, Agenda, ScheduleComponent, ViewsDirective, ViewDirective,
   ResourcesDirective, ResourceDirective, Inject
} from '@syncfusion/ej2-react-schedule';
import { resourceData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
    private data: Object[] = extend([], resourceData, null, true) as Object[];
    private roomData: Object[] = [
            { RoomText: 'ROOM 1', Id: 1, RoomColor: '#cb6bb2' },
            { RoomText: 'ROOM 2', Id: 2, RoomColor: '#56ca85' }
            ]
    private ownerData: Object[] = [
        { OwnerText: 'Nancy', Id: 1, OwnerColor: '#ffaa00' },
        { OwnerText: 'Steven', Id: 2, OwnerColor: '#f8a398' }
    ];
    render() {
        return <ScheduleComponent width='100%' height='550px' currentView='Week' selectedDate= {new Date(2018, 3, 1)} eventSettings={ { dataSource: this.data } } group={ { byGroupID: false, resources: ['Rooms', 'Owners'] } }>
            <ViewsDirective>
                <ViewDirective option='Week' />
                <ViewDirective option='Month' />
                <ViewDirective option='TimelineWeek' />
                <ViewDirective option='TimelineMonth' />
                <ViewDirective option='Agenda' />
            </ViewsDirective>
            <ResourcesDirective>
                <ResourceDirective field='RoomId' title='Room' name='Rooms' allowMultiple={false}
                  dataSource={this.roomData} textField='RoomText' idField='Id' colorField='RoomColor'>
                </ResourceDirective>
                <ResourceDirective field='OwnerId' title='Owner' name='Owners' allowMultiple={true}
                  dataSource={this.ownerData} textField='OwnerText' idField='Id' colorField='OwnerColor'>
                </ResourceDirective>
            </ResourcesDirective>
            <Inject services={[Week, Month, TimelineViews, TimelineMonth, Agenda]} />
        </ScheduleComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

### Grouping resources by date

It groups the number of resources under each date and is applicable only on the calendar views such as Day, Week, Work Week, Month, Agenda and Month-Agenda. To enable such grouping, set `byDate` option to `true` within the `group` property.

**Example:** To display the Scheduler with resources grouped by date,

{% tab template="schedule/resource", iframeHeight="588px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  Week, Month, Agenda, ScheduleComponent, ViewsDirective, ViewDirective,
  ResourcesDirective, ResourceDirective, Inject
} from '@syncfusion/ej2-react-schedule';
import { resourceData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
    private data: Object[] = extend([], resourceData, null, true) as Object[];
    private resourceData: Object[] = [
    { text: 'Alice', id: 1, color: '#1aaa55' },
    { text: 'Smith', id: 2, color: '#7fa900' }
    ];
    render() {
        return <ScheduleComponent width='100%' height='550px' selectedDate= {new Date(2018, 3, 1)} eventSettings={ { dataSource: this.data } }
        group={ { byDate: true, resources: ['Owners'] } } >
            <ResourcesDirective>
                <ResourceDirective field='OwnerId' title='Owner' name='Owners' allowMultiple={true}
                  dataSource={this.resourceData} textField='text' idField='id' colorField='color'>
                </ResourceDirective>
            </ResourcesDirective>
            <ViewsDirective>
                <ViewDirective option='Week' />
                <ViewDirective option='Month' />
                <ViewDirective option='Agenda' />
              </ViewsDirective>
            <Inject services={[Week, Month, Agenda]} />
        </ScheduleComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

> This kind of grouping by date is not applicable on any of the timeline views.

## Working with shared events

Multiple resources can share the same events, thus allowing the CRUD action made on it to reflect on all other shared instances simultaneously. To enable such option, set `allowGroupEdit` option to `true` within the `group` property. With this property enabled, a single appointment
object will be maintained within the appointment collection, even if it is shared by more than one resource – whereas the resource fields of such appointment object will hold the IDs of the multiple resources.

> Any actions such as create, edit or delete held on any one of the shared event instances, will be reflected on all other related instances visible on the UI.

**Example:** To edit all the resource events simultaneously,

{% tab template="schedule/resource", iframeHeight="588px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  Week, Month, TimelineViews, TimelineMonth, Agenda, ScheduleComponent, ResourcesDirective, ResourceDirective, ViewsDirective, ViewDirective, Inject
} from '@syncfusion/ej2-react-schedule';

class App extends React.Component<{}, {}>{
private conferenceData: Object[] = [
  { Text: 'Margaret', Id: 1, Color: '#1aaa55' },
  { Text: 'Robert', Id: 2, Color: '#357cd2' },
  { Text: 'Laura', Id: 3, Color: '#7fa900' }
];
private data: Object[] = [
    {
        Id: 1,
        Subject: 'Burning Man',
        StartTime: new Date(2018, 5, 1, 15, 0),
        EndTime: new Date(2018, 5, 1, 17, 0),
        ConferenceId: [1, 2, 3]
    }, {
        Id: 2,
        Subject: 'Data-Driven Economy',
        StartTime: new Date(2018, 5, 2, 12, 0),
        EndTime: new Date(2018, 5, 2, 14, 0),
        ConferenceId: [1, 2]
    }, {
        Id: 3,
        Subject: 'Techweek',
        StartTime: new Date(2018, 5, 2, 15, 0),
        EndTime: new Date(2018, 5, 2, 17, 0),
        ConferenceId: [2, 3]
    }, {
        Id: 4,
        Subject: 'Content Marketing World',
        StartTime: new Date(2018, 5, 2, 18, 0),
        EndTime: new Date(2018, 5, 2, 20, 0),
        ConferenceId: [1, 3]
    }, {
        Id: 5,
        Subject: 'B2B Marketing Forum',
        StartTime: new Date(2018, 5, 3, 10, 0),
        EndTime: new Date(2018, 5, 3, 12, 0),
        ConferenceId: [1, 2, 3]
    }];
render() {
    return <ScheduleComponent width='100%' height='550px' selectedDate={new Date(2018, 5, 5)} currentView='WorkWeek' eventSettings={ { dataSource: this.data } }
    group={ { allowGroupEdit: true, resources: ['Conferences'] } } >
        <ViewsDirective>
            <ViewDirective option='Week' />
            <ViewDirective option='Month' />
            <ViewDirective option='TimelineWeek' />
            <ViewDirective option='TimelineMonth' />
            <ViewDirective option='Agenda' />
        </ViewsDirective>
        <ResourcesDirective>
        <ResourceDirective field='ConferenceId' title='Conference' name='Conferences' allowMultiple={true}
            dataSource={this.conferenceData} textField='Text' idField='Id' colorField='Color'>
        </ResourceDirective>
        </ResourcesDirective>
        <Inject services={[Week, Month, TimelineViews, TimelineMonth, Agenda]} />
    </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

## Simple resource header customization

It is possible to customize the resource header cells using built-in template option and change the look and appearance of it in both the vertical and timeline view modes. All the resource related fields and other information can be accessed within the resource header template option.

**Example:** To customize the resource header and display it along with designation field, refer the below code example.

{% tab template="schedule/resource-header", iframeHeight="588px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from "react-dom";
import {
  Week, Month, TimelineViews, TimelineMonth, Agenda, ScheduleComponent, ViewsDirective, ViewDirective, ResourceDetails, ResourcesDirective, ResourceDirective, Inject
} from '@syncfusion/ej2-react-schedule';
import { doctorData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
private getDoctorName(value: ResourceDetails | TreeViewArgs): string {
    return (((value as ResourceDetails).resourceData) ?
        (value as ResourceDetails).resourceData[(value as ResourceDetails).resource.textField] :
        (value as TreeViewArgs).resourceName) as string;
}

private getDoctorLevel(value: ResourceDetails | TreeViewArgs): string {
let resourceName: string = this.getDoctorName(value);
return (resourceName === 'Will Smith') ? 'Cardiologist' : (resourceName === 'Alice') ? 'Neurologist' : 'Orthopedic Surgeon';
}
private data: Object[] = extend([], doctorData, null, true) as Object[];
private resourceData: Object[] = [
  { text: 'Will Smith', id: 1, color: '#ea7a57', designation: 'Cardioligst' },
  { text: 'Alice', id: 2, color: '#7fa900', designation: 'Neurologist' },
  { text: 'Robson', id: 3, color: '#7fa900', designation: 'Orthopedic Surgeon'  }
];
private resourceHeaderTemplate(props): JSX.Element {
    return (<div className="template-wrap">
        <div className="resource-detail"><div className="resource-name">{this.getDoctorName(props)}</div>
        <div className="resource-designation">{this.getDoctorLevel(props)}</div></div></div>
    );
}
render() {
    return <ScheduleComponent width='100%' height='550px' selectedDate={new Date(2018, 3, 1)} currentView='WorkWeek' resourceHeaderTemplate= { this.resourceHeaderTemplate.bind(this) } eventSettings={ { dataSource: this.data } } group={ { resources: ['Doctors'] } }>
            <ResourcesDirective>
                <ResourceDirective field='DoctorId' title='Doctor' name='Doctors' dataSource={this.resourceData} textField='text' idField='id' DesignationField='designation' colorField='color' >
                </ResourceDirective>
            </ResourcesDirective>
            <ViewsDirective>
                <ViewDirective option='Week' />
                <ViewDirective option='Month' />
                <ViewDirective option='TimelineWeek' />
                <ViewDirective option='TimelineMonth' />
                <ViewDirective option='Agenda' />
            </ViewsDirective>
            <Inject services={[Week, Month, TimelineViews, TimelineMonth, Agenda]} />
        </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

> To customize the resource header in compact mode properly make use of the class `e-device` as in the code example.

![Resource header template in compact mode](./images/header-template.png)

## Customizing resource header with multiple columns

It is possible to customize the resource headers to display with multiple columns such as Room, Type and Capacity. The following code example depicts the way to achieve it and is applicable only on timeline views.

{% tab template="schedule/multiple-column", iframeHeight="588px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from "react-dom";
import {
  TimelineViews, TimelineMonth, ScheduleComponent, ViewsDirective, ViewDirective, RenderCellEventArgs,
  ResourceDetails, ResourcesDirective, ResourceDirective, Inject
} from '@syncfusion/ej2-react-schedule';
import { roomData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
private getRoomName(value: ResourceDetails) {
    return (value as ResourceDetails).resourceData[(value as ResourceDetails).resource.textField];
}
private getRoomType(value: ResourceDetails) {
    return (value as ResourceDetails).resourceData.type;
}
private getRoomCapacity(value: ResourceDetails) {
    return (value as ResourceDetails).resourceData.capacity;
}
private data: Object[] = extend([], roomData, null, true) as Object[];
private ownerData: Object[] = [
    { text: 'Jammy', id: 1, color: '#ea7a57', capacity: 20, type: 'Conference' },
    { text: 'Tweety', id: 2, color: '#7fa900', capacity: 7, type: 'Cabin' },
    { text: 'Nestle', id: 3, color: '#5978ee', capacity: 5, type: 'Cabin' },
    { text: 'Phoenix', id: 4, color: '#fec200', capacity: 15, type: 'Conference' },
    { text: 'Mission', id: 5, color: '#df5286', capacity: 25, type: 'Conference' },
    { text: 'Hangout', id: 6, color: '#00bdae', capacity: 10, type: 'Cabin' },
    { text: 'Rick Roll', id: 7, color: '#865fcf', capacity: 20, type: 'Conference' },
    { text: 'Rainbow', id: 8, color: '#1aaa55', capacity: 8, type: 'Cabin' },
    { text: 'Swarm', id: 9, color: '#df5286', capacity: 30, type: 'Conference' },
    { text: 'Photogenic', id: 10, color: '#710193', capacity: 25, type: 'Conference' }
];
private resourceHeaderTemplate(props): JSX.Element {
    return (<div className="template-wrap">
        <div className="room-name">{this.getRoomName(props)}</div>
        <div className="room-type">{this.getRoomType(props)}</div>
        <div className="room-capacity">{this.getRoomCapacity(props)}</div>
    </div>
    );
}
private onRenderCell(args: RenderCellEventArgs): void {
    if (args.elementType === 'emptyCells' && args.element.classList.contains('e-resource-left-td')) {
        let target: HTMLElement = args.element.querySelector('.e-resource-text') as HTMLElement;
        target.innerHTML = '<div class="name">Rooms</div><div class="type">Type</div><div class="capacity">Capacity</div>';
    }
}
render() {
    return <ScheduleComponent width='100%' height='550px' selectedDate={new Date(2018, 7, 1)} currentView='TimelineWeek' resourceHeaderTemplate= { this.resourceHeaderTemplate.bind(this) }  eventSettings={ { dataSource: this.data } } renderCell={this.onRenderCell.bind(this)} group={ { resources: ['MeetingRoom'] } }>
            <ResourcesDirective>
                <ResourceDirective field='RoomId' title='Room Type' name='MeetingRoom' dataSource={this.ownerData} textField='text' idField='id' colorField='color' >
                </ResourceDirective>
            </ResourcesDirective>
            <ViewsDirective>
                <ViewDirective option='TimelineWeek' />
                <ViewDirective option='TimelineMonth' />
            </ViewsDirective>
            <Inject services={[TimelineViews, TimelineMonth]} />
        </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

## Displaying tooltip for resource headers

It is possible to display tooltips over the resource headers showing the resource information. By default, there won't be any tooltips displayed on the resource headers, and to enable it, you need to assign the customized template design to the `headerTooltipTemplate` option within the `group` property.

{% tab template="schedule/resource", iframeHeight="588px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  Week, Month, TimelineViews, TimelineMonth, ScheduleComponent, ViewsDirective, ViewDirective,
   ResourcesDirective, ResourceDirective, Inject
} from '@syncfusion/ej2-react-schedule';
import { resourceData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
    private data: Object[] = extend([], resourceData, null, true) as Object[];
    private getRoomName(value: ResourceDetails) {
        return (value as ResourceDetails).resourceData[(value as ResourceDetails).resource.textField];
    }
    private roomData: Object[] = [
            { RoomText: 'ROOM 1', Id: 1, RoomColor: '#cb6bb2' },
            { RoomText: 'ROOM 2', Id: 2, RoomColor: '#56ca85' }
            ]
    private ownerData: Object[] = [
        { OwnerText: 'Nancy', Id: 1, GroupId: 1, OwnerColor: '#ffaa00' },
        { OwnerText: 'Steven', Id: 2, GroupId: 2, OwnerColor: '#f8a398' },
        { OwnerText: 'Michael', Id: 3, GroupId: 1, OwnerColor: '#7499e1' }
    ];
    private headerTooltipTemplate(props): JSX.Element {
        return (<div className="template-wrap">
            <div className="room-name">{this.getRoomName(props)}</div>
        </div>
        );
    }
    render() {
        return <ScheduleComponent width='100%' height='550px' currentView='TimelineWeek' selectedDate= {new Date(2018, 3, 1)} eventSettings={ { dataSource: this.data } } group={ { resources: ['Rooms', 'Owners'] , headerTooltipTemplate: this.headerTooltipTemplate.bind(this)} } >
            <ResourcesDirective>
                <ResourceDirective field='RoomId' title='Room' name='Rooms'
                  dataSource={this.roomData} textField='RoomText' idField='Id' colorField='RoomColor'>
                </ResourceDirective>
                <ResourceDirective field='OwnerId' title='Owner' name='Owners' allowMultiple={true}
                  dataSource={this.ownerData} textField='OwnerText' idField='Id' groupIDField='GroupId' colorField='OwnerColor'>
                </ResourceDirective>
            </ResourcesDirective>
            <ViewsDirective>
                <ViewDirective option='Week' />
                <ViewDirective option='Month' />
                <ViewDirective option='TimelineWeek' />
                <ViewDirective option='TimelineMonth' />
            </ViewsDirective>
            <Inject services={[ Week, Month, TimelineViews, TimelineMonth]} />
        </ScheduleComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

## Choosing between resource colors for appointments

By default, the colors defined on the top level resources collection will be applied for the events. In case, if you want to apply specific resource color to events irrespective of its top-level parent resource color, it can be achieved by defining `resourceColorField` option within the `eventSettings` property.

In the following example, the colors mentioned in the second level will get applied over the events.

{% tab template="schedule/resource", iframeHeight="588px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  Week, Month, TimelineViews, TimelineMonth, Agenda, ScheduleComponent, ViewsDirective, ViewDirective,
   ResourcesDirective, ResourceDirective, Inject
} from '@syncfusion/ej2-react-schedule';
import { RadioButtonComponent } from '@syncfusion/ej2-react-buttons';
import { ChangeArgs } from '@syncfusion/ej2-buttons';
import { resourceData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
    private scheduleObj: ScheduleComponent;
    private data: Object[] = extend([], resourceData, null, true) as Object[];
    private roomData: Object[] = [
            { RoomText: 'ROOM 1', Id: 1, RoomColor: '#cb6bb2' },
            { RoomText: 'ROOM 2', Id: 2, RoomColor: '#56ca85' }
            ]
    private ownerData: Object[] = [
        { OwnerText: 'Nancy', Id: 1, GroupId: 1, OwnerColor: '#ffaa00' },
        { OwnerText: 'Steven', Id: 2, GroupId: 2, OwnerColor: '#f8a398' },
        { OwnerText: 'Michael', Id: 3, GroupId: 1, OwnerColor: '#7499e1' }
    ];
    private eventSettings: EventSettingsModel = { dataSource: this.data, resourceColorField: 'Rooms' };
    private group: GroupModel = { resources: ['Rooms', 'Owners'] };
    private onChange(args: ChangeArgs ): void {
        this.scheduleObj.eventSettings.resourceColorField = args.value;
    }

    render() {
        return ( <div>
        <RadioButtonComponent value='Rooms' name='default' label='Rooms' checked={true} change={this.onChange.bind(this)} ></RadioButtonComponent>
        <RadioButtonComponent value='Owners' name='default' label='Owners' checked={false} change={this.onChange.bind(this)}></RadioButtonComponent>
        <ScheduleComponent  ref={schedule => this.scheduleObj = schedule} width='100%' height='550px' currentView='Week' selectedDate= {new Date(2018, 3, 1)} eventSettings={ this.eventSettings } group={ this.group }>
        <ViewsDirective>
            <ViewDirective option='Week' />
            <ViewDirective option='Month' />
            <ViewDirective option='TimelineWeek' />
            <ViewDirective option='TimelineMonth' />
            <ViewDirective option='Agenda' />
        </ViewsDirective>
        <ResourcesDirective>
        <ResourceDirective field='RoomId' title='Room' name='Rooms'
                  dataSource={this.roomData} textField='RoomText' idField='Id' allowMultiple={false} colorField='RoomColor'>
                </ResourceDirective>
            <ResourceDirective field='OwnerId' title='Owner' name='Owners' allowMultiple={true}
              dataSource={this.ownerData} textField='OwnerText' idField='Id' groupIDField='GroupId' colorField='OwnerColor'>
            </ResourceDirective>
        </ResourcesDirective>
        <Inject services={[Week, Month, TimelineViews, TimelineMonth, Agenda]} />
        </ScheduleComponent>
        </div>)
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

> The value of the `resourceColorField` field should be mapped with the `name` value given within the `resources` property.

## Dynamically add and remove resources

It is possible to add or remove the resources dynamically to and from the Scheduler respectively. In the following example, when the checkboxes are checked and unchecked, the respective resources gets added up or removed from the Scheduler layout. To add new resource dynamically, `addResource` method is used which accepts the arguments such as resource object, resource name (within which level, the resource object to be added) and index (position where the resource needs to be added).

To remove the resources dynamically, `removeResource` method is used which accepts the index (position from where the resource to be removed) and resource name (within which level, the resource object presents) as parameters.

{% tab template="schedule/resource", iframeHeight="622px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { CheckBoxComponent, ChangeEventArgs } from '@syncfusion/ej2-react-buttons';
import {
    TimelineMonth, Month, EventFieldsMapping, EventClickArgs, ScheduleComponent,
    ViewsDirective, ViewDirective, ResourcesDirective, ResourceDirective, Inject
} from '@syncfusion/ej2-react-schedule';
import { extend } from '@syncfusion/ej2-base';
import { holidayData, birthdayData, companyData, personalData } from './datasource';

class App extends React.Component<{}, {}>{
    private scheduleObj: ScheduleComponent;
    private calendarCollections: Object[] = [
    { CalendarText: 'My Calendar', CalendarId: 1, CalendarColor: '#c43081' },
    { CalendarText: 'Company', CalendarId: 2, CalendarColor: '#ff7f50' },
    { CalendarText: 'Birthday', CalendarId: 3, CalendarColor: '#AF27CD' },
    { CalendarText: 'Holiday', CalendarId: 4, CalendarColor: '#808000' }
    ];

    private generateCalendarData(): Object[] {
        let collections: Object[] = [];
        let dataCollections: Object[][] = [personalData, companyData, birthdayData, holidayData];
        for (let data of dataCollections) {
        collections = collections.concat(data);
        }
        return collections;
    }

    private onChange(args: ChangeEventArgs): void {
        let value: number = parseInt((args.event.target as Element).getAttribute('value'), 10);
        let resourceData: Object[] = this.calendarCollections.filter((calendar: { [key: string]: Object }) => calendar.CalendarId === value);
        if (args.checked) {
            this.scheduleObj.addResource(resourceData[0], 'Calendars', value - 1);
        } else {
            this.scheduleObj.removeResource(value, 'Calendars');
        }
    }
    render() {
        return (<div>
                <tbody>
                    <tr style={ { height: '50px' } }>
                        <td style={ { width: '100%' } }>
                            <CheckBoxComponent value='1' id='personal' checked={true} label='My Calendar' disabled={true}
                            change={this.onChange.bind(this)} ></CheckBoxComponent>
                            <CheckBoxComponent value='2' id='company' checked={false} label='Company'
                            change={this.onChange.bind(this)} ></CheckBoxComponent>
                            <CheckBoxComponent value='3' id='birthdays' checked={false} label='Birthday'
                                change={this.onChange.bind(this)} ></CheckBoxComponent>
                            <CheckBoxComponent value='4' id='holidays' checked={false} label='Holiday'
                            change={this.onChange.bind(this)} ></CheckBoxComponent>
                        </td>
                        </tr>
                </tbody>
                <ScheduleComponent ref={schedule => this.scheduleObj = schedule} width='100%' height='550px' selectedDate={new Date(2018, 3, 1)} group={ { resources: ['Calendars'] } }
                eventSettings={ { dataSource: this.generateCalendarData() } } >
                    <ResourcesDirective>
                        <ResourceDirective field='CalendarId' title='Calendar' name='Calendars' allowMultiple={true}
                        dataSource={[this.calendarCollections[0]]} textField='CalendarText' idField='CalendarId' colorField='CalendarColor'>
                        </ResourceDirective>
                    </ResourcesDirective>
                    < ViewsDirective >
                        <ViewDirective option='Month' />
                        <ViewDirective option='TimelineMonth' />
                    </ViewsDirective>
                    <Inject services={[TimelineMonth, Month]} />
                </ScheduleComponent>
            </div>)
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

## Setting different working days and hours for resources

Each resource in the Scheduler can have different working hours as well as different working days set to it. There are default options available within the `resources` collection, to customize the default working hours and days of the Scheduler.

### Set different work days

Different working days can be set for the resources of Scheduler using the `workDaysField` property which maps the working days field from the resource dataSource. This field accepts the collection of day indexes (from 0 to 6) of a week. By default, it is set to [1, 2, 3, 4, 5] and in the following example, each resource has been set with different values and therefore each of them will render only those working days. This option is applicable only on the calendar views and is not applicable on timeline views.

{% tab template="schedule/resource", iframeHeight="588px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from "react-dom";
import {
  WorkWeek, Month, TimelineViews, ScheduleComponent, ViewsDirective, ViewDirective,
  ResourcesDirective, ResourceDirective, Inject
} from '@syncfusion/ej2-react-schedule';
import { doctorData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
private data: Object[] = extend([], doctorData, null, true) as Object[];
private resourceData: Object[] = [
  { text: 'Will Smith', id: 1, color: '#ea7a57', workDays: [1, 2, 4, 5] },
  { text: 'Alice', id: 2, color: '#357cd2', workDays: [1, 3, 5] },
  { text: 'Robson', id: 3, color: '#7fa900',  workDays: [2,6] }
];
render() {
    return <ScheduleComponent width='100%' height='550px' selectedDate={new Date(2018, 3, 1)} currentView='WorkWeek' eventSettings={ { dataSource: this.data } } group={ { resources: ['Doctors'] } }>
            <ResourcesDirective>
                <ResourceDirective field='DoctorId' title='Doctor' name='Doctors' dataSource={this.resourceData} textField='text' idField='id' colorField='color' workDaysField='workDays' >
                </ResourceDirective>
            </ResourcesDirective>
            <ViewsDirective>
                <ViewDirective option='TimelineWeek' />
                <ViewDirective option='WorkWeek' />
                <ViewDirective option='Month' />
            </ViewsDirective>
            <Inject services={[TimelineViews, WorkWeek, Month]} />
        </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

### Set different work hours

Working hours indicates the work hour duration of a day, which is highlighted visually with active color over the work cells. Each resource on the Scheduler can be defined with its own set of working hours as depicted in the following example.

* `startHourField` - Denotes the start time of the working/business hour in a day.
* `endHourField` - Denotes the end time limit of the working/business hour in a day.

{% tab template="schedule/resource", iframeHeight="588px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from "react-dom";
import {
  WorkWeek, Month, TimelineViews, ScheduleComponent, ViewsDirective, ViewDirective,
  ResourcesDirective, ResourceDirective, Inject
} from '@syncfusion/ej2-react-schedule';
import { doctorData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
private data: Object[] = extend([], doctorData, null, true) as Object[];
private resourceData: Object[] = [
  { text: 'Will Smith', id: 1, color: '#ea7a57', workDays: [1, 2, 4, 5], startHour: '07:00', endHour: '13:00' },
  { text: 'Alice', id: 2, color: '#357cd2', workDays: [1, 3, 5], startHour: '09:00', endHour: '17:00' },
  { text: 'Robson', id: 3, color: '#7fa900', startHour: '08:00', endHour: '16:00' }
];
render() {
    return <ScheduleComponent width='100%' height='550px' selectedDate={new Date(2018, 3, 1)} currentView='WorkWeek' eventSettings={ { dataSource: this.data } } group={ { resources: ['Doctors'] } }>
            <ResourcesDirective>
                <ResourceDirective field='DoctorId' title='Doctor' name='Doctors' dataSource={this.resourceData} textField='text' idField='id' colorField='color'
                workDaysField='workDays' startHourField='startHour' endHourField='endHour' >
                </ResourceDirective>
            </ResourcesDirective>
            <ViewsDirective>
                <ViewDirective option='TimelineWeek' />
                <ViewDirective option='WorkWeek' />
                <ViewDirective option='Month' />
            </ViewsDirective>
            <Inject services={[TimelineViews, WorkWeek, Month]} />
        </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

In this example, a resource named `Will Smith` is depicted with working hours ranging from 7.00 AM to 3.00 PM and is visually illustrated with active colors, whereas the other two resources have different working hours set.

## Compact view in mobile

Although the Scheduler views are designed keeping in mind the responsiveness of the control in mobile devices, however when using Scheduler with multiple resources - it is difficult to view all the resources and its relevant events at once on the mobile. Therefore, we have introduced a new compact mode specially for displaying multiple resources of Scheduler on mobile devices. By default, this mode is enabled while using Scheduler with multiple resources on mobile devices. If in case, you need to disable this compact mode, set `false` to the `enableCompactView` option within the `group` property. Disabling this option will display the exact desktop mode of Scheduler view on mobile devices.

With this compact view enabled on mobile, you can view only single resource at a time and to switch to other resources, there is a tree view at the left listing out all other available resources - clicking on which will display that particular resource and its related appointments.

![Resources in compact mode](./images/resource-mobile.png)

Clicking on the menu icon before the resource text will show the resources available in the Scheduler as following.

![Resources menu option in compact mode](./images/resource-menu.png)

## Adaptive UI in desktop

By default, the Scheduler layout adapts automatically in the desktop and mobile devices with appropriate UI changes. In case, if the user wants to display the Adaptive scheduler in desktop mode with adaptive enhancements, then the property `enableAdaptiveUI` can be set to true. Enabling this option will display the exact mobile mode of Scheduler view on desktop devices.

Some of the default changes made for compact Scheduler to render in desktop devices are as follows,
* View options displayed in the Navigation drawer.
* Plus icon is added to the header for new event creation.
* Today icon is added to the header instead of the Today button.
* With Multiple resources – only one resource has been shown to enhance the view experience of resource events details clearly. To switch to other resources, there is a TreeView on the left that lists all other available resources, clicking on which will display that particular resource and its related events.

{% tab template="schedule/resource", iframeHeight="588px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, Month, Year, Resize, DragAndDrop, Inject, ResourcesDirective, ResourceDirective, GroupModel, ViewsDirective, ViewDirective
} from '@syncfusion/ej2-react-schedule';
import { extend } from '@syncfusion/ej2-base';
import { resourceData, timelineResourceData } from './datasource';

class App extends React.Component<{}, {}> {
  private data: Object[] = extend([], resourceData.concat(timelineResourceData), null, true ) as Object[];
  private projectData: Object[] = [
    { text: 'PROJECT 1', id: 1, color: '#cb6bb2' },
    { text: 'PROJECT 2', id: 2, color: '#56ca85' },
    { text: 'PROJECT 3', id: 3, color: '#df5286' }
  ];
  private categoryData: Object[] = [
    { text: 'Nancy', id: 1, groupId: 1, color: '#df5286' },
    { text: 'Steven', id: 2, groupId: 1, color: '#7fa900' },
    { text: 'Robert', id: 3, groupId: 2, color: '#ea7a57' },
    { text: 'Smith', id: 4, groupId: 2, color: '#5978ee' },
    { text: 'Micheal', id: 5, groupId: 3, color: '#df5286' },
    { text: 'Root', id: 6, groupId: 3, color: '#00bdae' }
  ];
  private group: GroupModel = { resources: ['Projects', 'Categories'] };

  render() {
    return (
      <ScheduleComponent width='100%' height='650px' id='schedule'
      selectedDate={new Date(2018, 3, 4)} group={this.group} enableAdaptiveUI={true} currentView='Month' eventSettings={{ dataSource: this.data }}>
      <ViewsDirective>
          <ViewDirective option='Day' />
          <ViewDirective option='Week' />
          <ViewDirective option='Month' />
      </ViewsDirective>
      <ResourcesDirective>
          <ResourceDirective field='ProjectId' title='Choose Project' name='Projects' allowMultiple={false}
              dataSource={this.projectData} textField='text' idField='id' colorField='color'>
          </ResourceDirective>
          <ResourceDirective field='TaskId' title='Category' name='Categories' allowMultiple={true}
              dataSource={this.categoryData} textField='text' idField='id' groupIDField='groupId' colorField='color'>
          </ResourceDirective>
      </ResourcesDirective>
      <Inject services={[Day, Week, Month, Year, Resize, DragAndDrop]} />
  </ScheduleComponent>
    );
  }
}
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}

> You can refer to our [React Scheduler](https://www.syncfusion.com/react-ui-components/react-scheduler) feature tour page for its groundbreaking feature representations. You can also explore our [React Scheduler example](https://ej2.syncfusion.com/react/demos/#/material/schedule/overview) to knows how to present and manipulate data.
