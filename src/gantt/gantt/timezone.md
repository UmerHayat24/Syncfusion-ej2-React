---
title: "Gantt Timezone"
component: "Gantt"
description: "This article explains how to handle timezone on Gantt and also lists out the generic methods available in it."
---

# Timezone

The Gantt makes use of the current system time zone by default. If it needs to follow some other user-specific time zone, then the `timezone` property needs to be used.

## Understanding date manipulation in JavaScript

The `new Date()` in JavaScript returns the exact current date object with complete time and timezone information. For example, it may return value such as `Wed Dec 12 2018 05:23:27 GMT+0530 (India Standard Time)` which indicates that the current date is December 12, 2018 and the current time is 5.23 AM on browsers following the IST timezone.

## Display same time everywhere with no time difference

Setting `timezone` to UTC for Gantt will display the same time as in the database for all the users in different time zone.

{% tab template="gantt/timezone", compileJsx=true%}

```typescript
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { GanttComponent, Inject, Selection } from '@syncfusion/ej2-react-gantt';

class App extends React.Component<{}, {}>{
   public timezoneData: any = [
    { taskID: 1, taskName: 'Project Schedule', startDate: new Date('02/04/2019 08:00'), endDate: new Date('03/10/2019')},
    { taskID: 2, taskName: 'Planning', startDate: new Date('02/04/2019 08:00'), endDate: new Date('02/10/2019'), parentID: 1},
    { taskID: 3, taskName: 'Plan timeline', startDate: new Date('02/04/2019 08:00'), endDate: new Date('02/10/2019'), duration: 6, progress: '60', parentID: 2 },
    { taskID: 4, taskName: 'Plan budget', startDate: new Date('02/04/2019 08:00'), endDate: new Date('02/10/2019'), duration: 6, progress: '90', parentID: 2 },
    { taskID: 5, taskName: 'Allocate resources', startDate: new Date('02/04/2019 08:00'), endDate: new Date('02/10/2019'), duration: 6, progress: '75', parentID: 2 },
    { taskID: 6, taskName: 'Planning complete', startDate: new Date('02/06/2019 08:00'), endDate: new Date('02/10/2019'), duration: 0,  predecessor: '3FS,4FS,5FS', parentID: 2 },
    { taskID: 7, taskName: 'Design', startDate: new Date('02/13/2019 08:00'), endDate: new Date('02/17/2019 08:00'), parentID: 1, },
    { taskID: 8, taskName: 'Software Specification', startDate: new Date('02/13/2019 08:00'), endDate: new Date('02/15/2019'), duration: 3, progress: '60', predecessor: '6FS', parentID: 7, },
    { taskID: 9, taskName: 'Develop prototype', startDate: new Date('02/13/2019 08:00'), endDate: new Date('02/15/2019'), duration: 3, progress: '100', predecessor: '6FS', parentID: 7, },
    { taskID: 10, taskName: 'Get approval from customer', startDate: new Date('02/16/2019 08:00'), endDate: new Date('02/17/2019 08:00'), duration: 2, progress: '100', predecessor: '9FS', parentID: 7 },
    { taskID: 11, taskName: 'Design complete', startDate: new Date('02/17/2019 08:00'), endDate: new Date('02/17/2019 08:00'), duration: 0, predecessor: '10FS', parentID: 7 }
  ];
  public taskFields: any = {
    id: 'taskID',
    name: 'taskName',
    startDate: 'startDate',
    duration: 'duration',
    progress: 'progress',
    dependency: 'predecessor',
    parentID: 'parentID'
  };
  public timelineSettings: any = {
    timelineUnitSize: 65,
    topTier: {
        unit: 'Day',
        format: 'MMM dd, yyyy'
    },
    bottomTier: {
        unit: 'Hour',
        format: 'hh:mm a'
    }
  };
  private dayWorkingTime: any = [{ from: 0, to: 24 }];
  render() {
    return <GanttComponent dataSource={this.timezoneData} taskFields={this.taskFields}
                timelineSettings={this.timelineSettings} allowSelection={true}
          timezone='UTC' height='450px' dateFormat='hh:mm a'
          dayWorkingTime={this.dayWorkingTime} durationUnit='Hour' includeWeekend={true}>
                  <Inject services={[Edit, Selection]} />
        </GanttComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('root'));
```

{% endtab %}

## CRUD operations with timezone

CRUD operations can be performed with timezone, and the gantt is rendered based on the timezone specified in the load time. All the editing actions will be done based on the user timezone, but on database save action, we have reversed this conversion to local time and provided data to client side events for better understanding purpose. Refer to the following code example.

{% tab template="gantt/timezone", compileJsx=true%}

```typescript
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { GanttComponent, Inject, Selection, Edit } from '@syncfusion/ej2-react-gantt';

class App extends React.Component<{}, {}>{
   public timezoneData: any = [
     {
       taskID: 1,
       taskName: 'Project Schedule',
       startDate: new Date('02/04/2019 08:00'),
       endDate: new Date('03/10/2019')
      },
      {
       taskID: 2,
       taskName: 'Planning',
       startDate: new Date('02/04/2019 08:00'),
       endDate: new Date('02/10/2019'),
       parentID: 1
      },
     {
       taskID: 3,
       taskName: 'Plan timeline',
       startDate: new Date('02/04/2019 08:00'),
       endDate: new Date('02/10/2019'),
       duration: 6,
       progress: '60',
       parentID: 2
     },
     {
       taskID: 4,
       taskName: 'Plan budget',
       startDate: new Date('02/04/2019 08:00'),
       endDate: new Date('02/10/2019'),
       duration: 6,
       progress: '90',
       parentID: 2
     },
     {
       taskID: 5,
       taskName: 'Allocate resources',
       startDate: new Date('02/04/2019 08:00'),
       endDate: new Date('02/10/2019'),
       duration: 6,
       progress: '75',
       parentID: 2
     },
     {
       taskID: 6,
       taskName: 'Planning complete',
       startDate: new Date('02/06/2019 08:00'),
       endDate: new Date('02/10/2019'),
       duration: 0,
       predecessor: '3FS,4FS,5FS',
       parentID: 2
     },
    {
      taskID: 7,
      taskName: 'Design',
      startDate: new Date('02/13/2019 08:00'),
      endDate: new Date('02/17/2019 08:00'),
      parentID: 1
    },
    {
      taskID: 8,
      taskName: 'Software Specification',
      startDate: new Date('02/13/2019 08:00'),
      endDate: new Date('02/15/2019'),
      duration: 3,
      progress: '60',
      predecessor: '6FS',
      parentID: 7
    },
    {
      taskID: 9,
      taskName: 'Develop prototype',
      startDate: new Date('02/13/2019 08:00'),
      endDate: new Date('02/15/2019'),
      duration: 3,
      progress: '100',
      predecessor: '6FS',
      parentID: 7
    },
    {
      taskID: 10,
      taskName: 'Get approval from customer',
      startDate: new Date('02/16/2019 08:00'),
      endDate: new Date('02/17/2019 08:00'),
      duration: 2,
      progress: '100',
      predecessor: '9FS',
      parentID: 7
    },
    {
      taskID: 11,
      taskName: 'Design complete',
      startDate: new Date('02/17/2019 08:00'),
      endDate: new Date('02/17/2019 08:00'),
      duration: 0,
      predecessor: '10FS',
      parentID: 7
    }];
  public taskFields: any = {
    id: 'taskID',
    name: 'taskName',
    startDate: 'startDate',
    duration: 'duration',
    progress: 'progress',
    dependency: 'predecessor',
    parentID: 'parentID'
    };
  public editSettings: any = {
    allowAdding: true,
    allowEditing: true,
    allowDeleting: true,
    allowTaskbarEditing: true,
    showDeleteConfirmDialog: true
    };
  public timelineSettings: any = {
    timelineUnitSize: 65,
    topTier: {
      unit: 'Day',
      format: 'MMM dd, yyyy'
    },
    bottomTier: {
      unit: 'Hour',
      format: 'hh:mm a'
    }
  };
  public actionComplete(args: any) {
    if(args.action == "TaskbarEditing") {
      console.log(args.data.ganttProperties.endDate);
    }
  }
  private dayWorkingTime: any = [{ from: 0, to: 24 }];
    render() {
        return <GanttComponent dataSource={this.timezoneData} taskFields={this.taskFields} editSettings={this.editSettings} allowSelection={true} durationUnit='Hour' actionComplete={this.actionComplete.bind(this)} editSettings={this.editSettings} height = '450px' includeWeekend={true} dayWorkingTime={this.dayWorkingTime} timelineSettings={this.timelineSettings} >
            <Inject services={[Edit, Selection]} />
        </GanttComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('root'));
```

{% endtab %}

## Timezone methods

### offset

This method is used to calculate the difference between passed UTC date and timezone.

| Parameters | Type | Description |
|------------|------|-------------|
| Date | Date | UTC time as date object.|
| Timezone | String | Timezone.|

Returns `number`

```typescript
    // Assume your local timezone as IST/UTC+05:30
    let timezone: Timezone = new Timezone();
    let date: Date = new Date(2018,11,5,15,25,11);
    let timeZoneOffset: number = timezone.offset(date,"Europe/Paris");
    console.log(timeZoneOffset); //-60
```

### convert

This method is used to convert the passed date from one timezone to another timezone.

| Parameters | Type | Description |
|------------|------|-------------|
| Date | Date | UTC time as date object.|
| fromOffset | number/string | Timezone from which date need to be converted.|
| toOffset | number/string | Timezone to which date need to be converted.|

Returns `Date`

```typescript
    // Assume your local timezone as IST/UTC+05:30
    let timezone: Timezone = new Timezone();
    let date: Date = new Date(2018,11,5,15,25,11);
    let convertedDate: Date = timezone.convert(date, "Europe/Paris", "Asia/Tokya");
    let convertedDate1: Date = timezone.convert(date, 60, -360);
    console.log(convertedDate); //2018-12-05T08:55:11.000Z
    console.log(convertedDate1); //2018-12-05T16:55:11.000Z
```

### remove

This method is used to remove the time difference between passed UTC date and timezone.

| Parameters | Type | Description |
|------------|------|-------------|
| Date | Date | UTC as date object.|
| Timezone | String | Timezone.|

Returns `Date`

```typescript
    // Assume your local timezone as IST/UTC+05:30
    let timezone: Timezone = new Timezone();
    let date: Date = new Date(2018,11,5,15,25,11);
    let convertedDate: Date = timezone.remove(date, "Europe/Paris");
    console.log(convertedDate); //2018-12-05T14:25:11.000Z
```