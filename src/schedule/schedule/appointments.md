# Appointments

Appointments can be anything that are scheduled for a specific time period. It can be created on varied time range and each appointments are categorized based on this range. The Scheduler events can be categorized as,
* Normal events
* Spanned events
* All-day events
* Recurring events

To have a quick glance on how to add appointments to the React Scheduler and some of its advanced event-handling options, watch this video:

`youtube:lk-P4YV8xaw`

## Normal events

Represents an appointment that is created for any specific time interval within a day.

### Creating a normal event

The following example depicts how to define a normal event on the Scheduler, with event data being loaded from simple JSON data.

{% tab template="schedule/events", iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, WorkWeek, Month, Agenda,Inject
} from '@syncfusion/ej2-react-schedule';

class App extends React.Component<{}, {}>{
   private data: object [] = [{
    Id: 2,
    Subject: 'Paris',
    StartTime: new Date(2018, 1, 15, 10, 0),
    EndTime: new Date(2018, 1, 15, 12, 30),
  }];
    render() {
    return <ScheduleComponent height='550px' selectedDate= {new Date(2018, 1, 15)} eventSettings={ { dataSource: this.data } }>
    <Inject services={[Day, Week, WorkWeek, Month, Agenda]} />
    </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}

## Spanned events

Represents an appointment that is created for more than 24 hours, and usually displayed on the all-day row. Also, represents another type of appointment that is created for more than one day but less than 24 hours, and usually displayed appropriately on both the days.

> For example, if an appointment is created for two days say from November 25, 2018 – 11.00 PM to November 26, 2018 2.00 AM but less than 24 hours time interval, then the appointment is split into two partitions and will be displayed on both the days.

## All-day events

Represents an appointment that is created for an entire day such as holiday events. It is usually displayed separately in an all-day row, a separate row for all-day appointments below the date header section. In Timeline views, the all-day appointments displays in the working space area, and no separate all-day row is present in that view.

> To change normal appointment into all-day event, set `isAllDay` field to true.

### Hide all-day row events

You can make use of the CSS customization to prevent the display of all-day row appointments on the Scheduler UI.

```tsx
    <style>
        .e-schedule .e-date-header-wrap .e-schedule-table thead {
           display: none;
        }
    </style>
```

## Recurring events

Represents an appointment that is created for a certain time interval and occurring repeatedly on a daily, weekly, monthly or yearly basis at the same time interval based on the provided recurrence rule. Usually, the recurring events are indicated by a repeat marker added at the bottom-right position.

### Creating a recurring event

The following example depicts how to create a recurring event on Scheduler with the specific recurrence rule. In the following example, an event is made to repeat on daily mode and ends after 5 occurrences.

{% tab template="schedule/events", iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, WorkWeek, Month, Agenda,Inject
} from '@syncfusion/ej2-react-schedule';

class App extends React.Component<{}, {}>{
   private data: object [] = [{
    Id: 2,
    Subject: 'Paris',
    StartTime: new Date(2018, 1, 15, 10, 0),
    EndTime: new Date(2018, 1, 15, 12, 30),
    IsAllDay: false,
    RecurrenceRule: 'FREQ=DAILY;INTERVAL=1;COUNT=5',
  }];
    render() {
    return <ScheduleComponent height='550px' selectedDate= {new Date(2018, 1, 15)} eventSettings={ { dataSource: this.data } }>
    <Inject services={[Day, Week, WorkWeek, Month, Agenda]} />
    </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}

### Adding exceptions

A few instance of the recurrence series can be excluded on specific dates, by adding those exceptional dates to the `recurrenceException` field. These date values should be given in the ISO date time format with no hyphens(-) separating the date elements.

For example, 22nd February 2018 can be represented as 20180222. Also, the time part being represented in UTC format needs to add "Z" after the time portion with no space. "07:30:00 UTC" is therefore represented as "073000Z".

{% tab template="schedule/events", iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, WorkWeek, Month, Agenda,Inject
} from '@syncfusion/ej2-react-schedule';

class App extends React.Component<{}, {}>{
   private data: object [] = [{
    Id: 1,
    Subject: 'Paris',
    StartTime: new Date(2018, 0, 28, 10, 0),
    EndTime: new Date(2018, 0, 28, 12, 30),
    IsAllDay: false,
    RecurrenceRule: 'FREQ=DAILY;INTERVAL=1;COUNT=8',
    RecurrenceException:'20180129T043000Z,20180131T043000Z,20180202T043000Z'
  }];
    render() {
    return <ScheduleComponent height='550px' selectedDate= {new Date(2018, 0, 28)} eventSettings={ { dataSource: this.data } }>
    <Inject services={[Day, Week, WorkWeek, Month, Agenda]} />
    </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}

### Editing an occurrence from a series

To dynamically edit a particular occurrence from an event series and display it on the initial load of Scheduler, the edited occurrence needs to be added as a new event to the dataSource collection, with an additional `recurrenceID` field defined to it. The `recurrenceID` field of edited occurrence usually maps the ID value of the parent event.

In this example, a recurring instance that displays on the date 30th Jan 2018 is edited with different timings. Therefore, this particular date is excluded from the parent recurring event that repeats from 28th January 2018 to 4th February 2018. This can be done by adding the `recurrenceException` field with the excluded date value on the parent event. Also, the edited occurrence event which is created as a new event should carry the `recurrenceID` field pointing to the parent event's `Id` value.

{% tab template="schedule/events", iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, WorkWeek, Month, Agenda,Inject
} from '@syncfusion/ej2-react-schedule';

class App extends React.Component<{}, {}>{
   private data: object [] = [{
    Id: 1,
    Subject: 'Scrum Meeting',
    StartTime: new Date(2018, 0, 28, 10, 0),
    EndTime: new Date(2018, 0, 28, 12, 30),
    IsAllDay: false,
    RecurrenceRule: 'FREQ=DAILY;INTERVAL=1;COUNT=8',
    RecurrenceException:'20180130T043000Z'
  },
  {
    Id: 2,
    Subject: 'Scrum Meeting',
    StartTime: new Date(2018, 0, 30, 9, 0),
    EndTime: new Date(2018, 0, 30, 10, 30),
    Description: "Meeting time changed based on team activities.",
    RecurrenceID: 1
  }];
    render() {
    return <ScheduleComponent height='550px' selectedDate= {new Date(2018, 0, 28)} eventSettings={ { dataSource: this.data } }>
    <Inject services={[Day, Week, WorkWeek, Month, Agenda]} />
    </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

### Edit only the current and following events

To edit only the current and following events enable the property `editFollowingEvents` within `eventSettings` property. The edited occurrence needs to be added as a new event to the dataSource collection, with an additional `followingID` field defined to it. The `followingID` field of edited occurrence usually maps the ID value of the immediate parent event.

In this example, a recurring instance that displays on the date 30th Jan 2018 and its following dates are edited with different subject. Therefore, this particular date and its following dates are excluded from the parent recurring event that repeats from 28th January 2018 to 4th February 2018. This can be done by updating the `recurrenceRule` field with the until date value on the parent event. Also, the edited events which is created as a new event should carry the `followingID` field pointing to the immediate parent event's `Id` value.

{% tab template="schedule/events", iframeHeight="588px", compileJsx=true %}

 ```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, WorkWeek, Month, Agenda, EventSettingsModel, Inject
} from '@syncfusion/ej2-react-schedule';

export class App extends React.Component<{}, {}>{
  private data: object [] = [{
    Id: 1,
    Subject: 'Scrum Meeting',
    StartTime: new Date(2018, 0, 28, 10, 0),
    EndTime: new Date(2018, 0, 28, 12, 30),
    IsAllDay: false,
    RecurrenceRule: 'FREQ=DAILY;INTERVAL=1;UNTIL=20180129T043000Z;',
  },
  {
    Id: 2,
    Subject: 'Scrum Meeting - Following Edited',
    StartTime: new Date(2018, 0, 30, 10, 0),
    EndTime: new Date(2018, 0, 30, 12, 30),
    RecurrenceRule: 'FREQ=DAILY;INTERVAL=1;UNTIL=20180204T043000Z;',
    FollowingID: 1
  }];
  private eventSettings: EventSettingsModel = { dataSource: this.data, editFollowingEvents: true };
  render() {
    return <ScheduleComponent height='550px' selectedDate= {new Date(2018, 0, 28)} eventSettings= { this.eventSettings }>
    <Inject services={[Day, Week, WorkWeek, Month, Agenda]} />
    </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

### Recurrence options and rules

Events can be repeated on a daily, weekly, monthly or yearly basis based on the recurrence rule which accepts the string value. The following details should be assigned to the `recurrenceRule` property to generate the recurring instances.

* Repeat type - daily/weekly/monthly/yearly.
* How many times it needs to be repeated?
* The interval duration.
* The time period to render the appointment, etc.

There are four repeat types available namely,
* **Daily** - Creates the recurring instances on daily basis.
* **Weekly** - Creates the recurring instances on weekly basis for the selected days.
* **Monthly** - Creates the recurring instances on monthly basis for the selected months and other provided recurrence criteria.
* **Yearly** - Creates the recurring instances on yearly basis.

### Recurrence properties

 The properties based on which the recurrence appointments are created with its respective time period are depicted in the following table. Also, the valid rule string can be referred from [iCalendar](https://tools.ietf.org/html/rfc5545#section-3.3.10) specifications.

 > Refer [iCalendar](https://tools.ietf.org/html/rfc5545#section-3.3.10) specifications for valid recurrence rule string.

| Property | Purpose | Example |
|-------|---------| --------- |
| FREQ | Maintains the repeat type (Daily, Weekly, Monthly, Yearly) value of the appointment. | FREQ=DAILY;INTERVAL=1|
| INTERVAL | Maintains the interval value of the appointments. When you create the daily appointment at an interval of 2, the appointments are rendered on the days Monday, Wednesday and Friday (Creates an appointment on all days by leaving the interval of one day gap). | FREQ=DAILY;INTERVAL=2|
| COUNT | It holds the appointment’s count value. When the COUNT value is 10, then 10 instances of appointments are created in the recurrence series. | FREQ=DAILY;INTERVAL=1;COUNT=10|
| UNTIL | This property holds the end date value (in ISO format) denoting when the recurrence actually ends. | FREQ=DAILY;INTERVAL=1;UNTIL=20180530T041343Z;|
| BYDAY | It holds the day value(s), representing on which the appointments actually renders. Create the weekly appointment, and select the day(s) from the day options (Monday/Tuesday/Wednesday/Thursday/Friday/Saturday/Sunday). When Monday is selected, the first two letters of the selected day "MO" is saved in the BYDAY property. When multiple days are selected, the values are separated by commas. | FREQ=WEEKLY;INTERVAL=1;BYDAY=MO,WE;COUNT=10|
| BYMONTHDAY | This property is used to store the date value of the Month, while creating the Month recurrence appointment. When you create a Monthly recurrence appointment for every 3rd day of the month, then BYMONTHDAY holds the value 3 and creates the appointment on 3rd day of every month. | FREQ=MONTHLY;BYMONTHDAY=3;INTERVAL=1;COUNT=10|
| BYMONTH | This property is used to store the index value of the selected Month while creating the yearly appointments. When you create the yearly appointment on June month, the index value of June month 6 will get stored in the BYMONTH field. The appointment is created on every 6th month of a year. | FREQ=YEARLY;BYMONTHDAY=16;BYMONTH=6;INTERVAL=1;COUNT=10|
| BYSETPOS | This property is used to store the index value of the week. When you create the monthly appointment in second week of a month, the index value of the second week (2) is stored in BYSETPOS. | FREQ=MONTHLY;BYDAY=MO;BYSETPOS=2;COUNT=10|

> The default recurrence related validation has been included for recurrence appointments similar to the one available in Outlook. The validation usually occurs during the recurrence appointment creation, editing, drag and drop or resizing of the recurrence appointments and also if any single occurrence changes.

### Daily Frequency

| Description | Example |
|-------------|---------|
| Daily recurring event that never ends | FREQ=DAILY; INTERVAL=1 |
| Daily recurring event that ends after 5 occurrences | FREQ=DAILY; INTERVAL=1; COUNT=5 |
| Daily recurring event that ends exactly on 12/12/2018 | FREQ=DAILY; INTERVAL=1; UNTIL=20181212T041343Z |
| Daily event that recurs on alternative days and repeats for 10 occurrences | FREQ=DAILY; INTERVAL=2; COUNT=10 |
| Daily recurring appointment ends on 12/12/2018 by excluding single occurrence on 12/10/2018 | FREQ=DAILY; INTERVAL=2; UNTIL=20181212T041343Z; |

### Weekly Frequency

| Description | Example |
|-------------|---------|
| Weekly recurring event that repeats on every Monday, Wednesday and Friday and never ends | FREQ=WEEKLY; INTERVAL=1; BYDAY=MO,WE,FR |
| Repeats every week Thursday and ends after 10 occurrences | FREQ=WEEKLY; INTERVAL=1; BYDAY=TH; COUNT=10 |
| Repeats every week Monday and ends on 12/12/2018 | FREQ=WEEKLY; INTERVAL=1; BYDAY=MO; UNTIL=20181212T041343Z |
| Repeats on Monday, Wednesday and Friday of alternative weeks and ends after 10 occurrences | FREQ=WEEKLY; INTERVAL=2; BYDAY=MO, WE, FR; COUNT=10 |
| Repeats every week on weekdays and ends after 12/12/2018 by excluding single occurrence on 12/10/2018 | FREQ=WEEKLY; BYDAY=MO, TU, WE, TH, FR; UNTIL=20181212T041343Z; |

### Monthly Frequency

| Description | Example |
|-------------|---------|
| Monthly recurring event that repeats on every 15th day of a month and never ends | FREQ=MONTHLY; BYMONTHDAY=15; INTERVAL=1 |
| Monthly recurring event that repeats on every 16th day of a month and ends after 10 occurrences | FREQ=MONTHLY; BYMONTHDAY=16; INTERVAL=1; COUNT=10 |
| Repeats every 17th day of a month and ends on 12/12/2018 | FREQ=MONTHLY; BYMONTHDAY=17; INTERVAL=1; UNTIL=20181212T041343Z |
| Repeats every 2nd Friday of a month and never ends | FREQ=MONTHLY; BYDAY=FR; BYSETPOS=2; INTERVAL=1 |
| Repeats every 4th Wednesday of a month and ends after 10 occurrences | FREQ=MONTHLY; BYDAY=WE; BYSETPOS=4; INTERVAL=1; COUNT=10 |
| Repeats every 4th Friday of a month and ends on 12/12/2018 | FREQ=MONTHLY; BYDAY=FR; BYSETPOS=4; INTERVAL=1; UNTIL=20181212T041343Z |

### Yearly Frequency

| Description | Example |
|-------------|---------|
| Yearly event that repeats on every 15th day of December month and never ends | FREQ=YEARLY; BYMONTHDAY=15; BYMONTH=12; INTERVAL=1 |
| Event that repeats on every 10th day of December month and ends after 10 occurrences | FREQ=YEARLY; BYMONTHDAY=10; BYMONTH=12; INTERVAL=1; COUNT=10 |
| Repeats on every 12th day of December month and ends on 12/12/2025 | FREQ=YEARLY; BYMONTHDAY=12; BYMONTH=12; INTERVAL=1; UNTIL=20251212T041343Z |
| Repeats on every 3rd Friday of December month and never ends | FREQ=YEARLY; BYDAY=FR; BYMONTH=12; BYSETPOS=3; INTERVAL=1 |
| Repeats on every 3rd Tuesday of December month and ends after 10 occurrences | FREQ=YEARLY; BYDAY=TU; BYMONTH=12; BYSETPOS=3; INTERVAL=1; COUNT=10 |
| Repeats on every 4th Wednesday of December month and ends on 12/12/2028 | FREQ=YEARLY; BYDAY=WE; BYMONTH=12; BYSETPOS=4; INTERVAL=1; UNTIL=20181212T041343Z |

### Recurrence Validation

The built-in validation support has been added by default for recurring appointments during its creation, edit, drag and drop or resize action. The following are the possible validation alerts that displays on Scheduler while creating or editing the recurring events.

| Validation messages | Description |
|-------|---------|
| The recurrence pattern is not valid. | This alert will raise, when the selected recurrence rule value is not a valid one. For example, when you try to select the end date value (using `Until` option) for a recurring event, which occurs before the start date, an alert will popup out saying that the chosen pattern is invalid. |
| The changes made to specific instances of this series will be cancelled and those events will match the series again. | This alert will raise, when you try to edit the whole series, whose occurrence might have been already edited. For example, If there are five occurrences and one of the occurrence is already edited. Now, when you try to edit the entire series, you will get this validation alert. |
| The duration of the event must be shorter than how frequently it occurs. Shorten the duration, or change the recurrence pattern in the recurrence event editor. | This validation will occur, if the event duration is longer than the selected frequency. For example, if you create a recurring appointment with two days duration in `Daily` frequency with no intervals set to it, you may get this alert. |
| Some months have fewer than the selected date. For these months, the occurrence will fall on the last date of the month. | When you try to create a recurring appointment on 31st of every month, where few months won’t have 31 days and in this scenario, you will get this alert. |
| Two occurrences of the same event cannot occur on the same day. | This validation will occur, when you try to edit or move any single occurrence to some other date, where another occurrence of the same event is already present. |

## Event fields

The Scheduler dataSource usually holds the event instances, where each of the instance includes a collection of appropriate [fields](../api/schedule/field). It is mandatory to map these fields with the equivalent fields of database, when remote data is bound to it. When the local JSON data is bound, then the field names defined within the instances needs to be mapped with the scheduler event fields correctly.

> To create an event on Scheduler, it is enough to define the `startTime` and `endTime`. Also `id` field becomes mandatory to process CRUD actions on appropriate events.

### Built-in fields

The built-in fields available on Scheduler event object are as follows.

| Field name | Description |
|-------|---------|
| id | The `id` field needs to be defined as mandatory and this field usually assigns a unique ID value to each of the events.|
| subject | The `subject` field is optional, and usually assigns the summary text to each of the events.|
| startTime | The `startTime` field defines the start time of an event and it is mandatory to provide it for any of the valid event objects.|
| endTime | The `endTime` field defines the end time of an event and it is mandatory to provide the end time for any of the valid event objects.|
| startTimezone | It maps the `startTimezone` field from the dataSource and usually accepts the valid IANA timezone names. It is assumed that the value provided for this field is taken into consideration while processing the `startTime` field. When this field is not mapped with any timezone names, then the events will be processed based on the timezone assigned to the Scheduler.|
| endTimezone | It maps the `endTimezone` field from the dataSource and usually accepts the valid IANA timezone names. It is assumed that the value provided for this field is taken into consideration while processing the `endTime` field. When this field is not mapped with any timezone names, then the events will be processed based on the timezone assigned to the Scheduler.|
| location | It maps the `location` field from the dataSource and the location text value will be displayed over the events.|
| description | It maps the `description` field from the dataSource and denotes the event description which is optional.|
| isAllDay | The `isAllDay` field is mapped from the dataSource and is used to denote whether an event is created for an entire day or for specific time alone. Usually, an event with `isAllDay` field set to true will be considered as an all-day event. |
| recurrenceID | It maps the `recurrenceID` field from dataSource and usually holds the ID value of the parent recurrence event. This field is applicable only for the edited occurrence events.|
| recurrenceRule | It maps the `recurrenceRule` field from dataSource and holds the recurrence rule value in a string format. Also, it uniquely identifies whether the event belongs to a recurring type or normal ones. |
| recurrenceException | It maps the `recurrenceException` field from dataSource and is used to hold the collection of exception dates, on which the recurring occurrences needs to be excluded. |
| isReadonly | It maps the `isReadonly` field from dataSource. It is mainly used to make specific appointments as readonly when set to `true`. |
| isBlock | It maps the `isBlock` field from dataSource. It is used to block the particular time ranges in the Scheduler and prevents the event creation on those time slots. |  

### Binding different field names

When the fields of event instances has the default mapping name, it is not mandatory to map them manually. If a Scheduler's dataSource holds the events collection with different field names, then it is necessary to map them with its equivalent field name within the `eventSettings` property.

{% tab template="schedule/events", iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, WorkWeek, Month, Agenda, Inject
} from '@syncfusion/ej2-react-schedule';

class App extends React.Component<{}, {}>{
  private data: object [] = [{
    TravelId: 2,
    TravelSummary: 'Paris',
    DepartureTime: new Date(2018, 1, 15, 10, 0),
    ArrivalTime: new Date(2018, 1, 15, 12, 30),
    FullDay: false,
    Source: 'London',
    Comments: 'Summer vacation planned for outstation.',
    Origin: 'Asia/Yekaterinburg',
    Destination: 'Asia/Yekaterinburg'
  }];
  render() {
    return <ScheduleComponent height='550px' selectedDate= {new Date(2018, 1, 15)} eventSettings={ { dataSource: this.data,
            fields: {
              id: 'TravelId',
              subject: { name: 'TravelSummary' },
              isAllDay: { name: 'FullDay' },
              location: { name: 'Source' },
              description: { name: 'Comments' },
              startTime: { name: 'DepartureTime' },
              endTime: { name: 'ArrivalTime' },
              startTimezone: { name: 'Origin' },
              endTimezone: { name: 'Destination' }
            }
        } }>
      <Inject services={[Day, Week, WorkWeek, Month, Agenda]} />
      </ScheduleComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}

> The mapper field `id` is of string type and has no additional validation options, whereas all other fields are of `Object` type and has additional options.

### Event field settings

Each field of the Scheduler events are provided with additional settings such as options to set default value, to map with appropriate data source fields, to validate every event fields and to provide label values for those fields in the event window.

| Options | Description |
| ------- | ----------- |
| default | Accepts the default value to the applicable fields (Subject, Location and Description), when no values are provided to them from dataSource. |
| name | Accepts the field name to be mapped from the dataSource fields. |
| title | Accepts the label values to be displayed for the fields of event editor. |
| validation | Defines the validation rules to be applied on the event fields within the event editor. |

In following example, the Subject field in event editor will display its appropriate label as **Summary**. When no subject value is provided while saving an event, then the appointment will be saved with the default subject value as **Add Summary**.

{% tab template="schedule/events", iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, WorkWeek, Month, Agenda, Inject
} from '@syncfusion/ej2-react-schedule';

class App extends React.Component<{}, {}>{
  private data: object [] = [{
    TravelId: 2,
    TravelSummary: 'Paris',
    DepartureTime: new Date(2018, 1, 15, 10, 0),
    ArrivalTime: new Date(2018, 1, 15, 12, 30),
    Source: 'London',
    Comments: 'Summer vacation planned for outstation.'
  }];
  render() {
    return <ScheduleComponent height='550px' selectedDate= {new Date(2018, 1, 15)} eventSettings={ { dataSource: this.data,
            fields: {
              id: 'TravelId',
              subject: { name: 'TravelSummary', title: 'Summary', default: 'Add Summary' },
              location: { name: 'Source', default: 'USA' },
              description: { name: 'Comments' },
              startTime: { name: 'DepartureTime' },
              endTime: { name: 'ArrivalTime' }
            }
        } }>
      <Inject services={[Day, Week, WorkWeek, Month, Agenda]} />
      </ScheduleComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}

## Adding Custom fields

Apart from the default Scheduler fields, the user can include 'n' number of custom fields for appointments. The following code example shows how to include two custom fields namely **Status** and **Priority** within event collection. It is not necessary to bind the custom fields within the `eventSettings`. However, those additional fields can be accessed easily, for internal processing as well as from application end.

{% tab template="schedule/events", iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, WorkWeek, Month, Agenda, Inject
} from '@syncfusion/ej2-react-schedule';

class App extends React.Component<{}, {}>{
  private data: Object[] = [{
    Id: 2,
    Subject: 'Meeting',
    StartTime: new Date(2018, 1, 15, 10, 0),
    EndTime: new Date(2018, 1, 15, 12, 30),
    IsAllDay: false,
    Status: 'Completed',
    Priority: 'High'
  }];
  render() {
    return <ScheduleComponent height='550px' selectedDate= {new Date(2018, 1, 15)} eventSettings={ { dataSource: this.data,
            fields: {
              id: 'Id',
              subject: { name: 'Subject' },
              isAllDay: { name: 'IsAllDay' },
              startTime: { name: 'StartTime' },
              endTime: { name: 'EndTime' }
            }
        } }>
      <Inject services={[Day, Week, WorkWeek, Month, Agenda]} />
      </ScheduleComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}

## Customize the order of the overlapping events

By default, the scheduler will render the overlapping events based on the start and end time. Now we can customize the order of the overlapping events based on the custom fields by using the `sortComparer` property grouped under the `eventSettings` property. The following code example shows how to sort the appointments based on the custom field as follows.

{% tab template="schedule/events", iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, WorkWeek, Month, Agenda, SortComparerFunction, Inject
} from '@syncfusion/ej2-react-schedule';

class App extends React.Component<{}, {}>{
  private data: Object[] = [{
    Id: 1,
    Subject: 'Rank 1',
    StartTime: new Date(2017, 9, 29, 10, 0),
    EndTime: new Date(2017, 9, 29, 11, 30),
    IsAllDay: false,
    RankId: '1'
  }, {
    Id: 2,
    Subject: 'Rank 3',
    StartTime: new Date(2017, 9, 29, 10, 30),
    EndTime: new Date(2017, 9, 29, 12, 30),
    IsAllDay: false,
    RankId: '3'
  }, {
    Id: 3,
    Subject: 'Rank 6',
    StartTime: new Date(2017, 9, 29, 7, 0),
    EndTime: new Date(2017, 9, 29, 14, 30),
    IsAllDay: false,
    RankId: '6'
  }, {
    Id: 4,
    Subject: 'Rank 9',
    StartTime: new Date(2017, 9, 29, 11, 0),
    EndTime: new Date(2017, 9, 29, 15, 30),
    IsAllDay: false,
    RankId: '9'
  }];
  private comparerFun: SortComparerFunction = (args: Record<string, any>[]) => {
    args.sort((event1: Record<string, any>, event2: Record<string, any>) => event1.RankId.localeCompare(event2.RankId, undefined, { numeric: true }));
    return args;
  }
  render() {
    return <ScheduleComponent height='550px' selectedDate= {new Date(2017, 9, 29)} eventSettings={ { dataSource: this.data,
            sortComparer: this.comparerFun
        } }>
      <Inject services={[Day, Week, WorkWeek, Month, Agenda]} />
      </ScheduleComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}

## Drag and drop appointments

Appointments can be rescheduled to any time by dragging and dropping them onto the desired location. To work with drag and drop functionality, it is necessary to inject the module `DragAndDrop` and make sure that `allowDragAndDrop` is set to true on Scheduler. In mobile mode, you can drag and drop the events by tap holding an event and dropping them on to the desired location.

Learn the advanced options of Drag and Resize actions for React Scheduler from this video:

`youtube:DYM3kyJy7sw`

> By default, drag and drop action is applicable on all Scheduler views, except Agenda, Month-Agenda and Year view.

{% tab template="schedule/events", iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, TimelineViews, TimelineMonth, Month, Agenda, DragAndDrop, ViewsDirective, ViewDirective, Inject
} from '@syncfusion/ej2-react-schedule';
import { scheduleData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
    private data: Object[] = extend([], scheduleData, null, true) as Object[];
    render() {
    return <ScheduleComponent height='550px' selectedDate= {new Date(2018, 1, 15)} eventSettings={ { dataSource: this.data } }>
      <ViewsDirective>
        <ViewDirective option='TimelineDay' />
        <ViewDirective option='Day' />
        <ViewDirective option='Week' />
        <ViewDirective option='TimelineMonth' />
        <ViewDirective option='Month' />
        <ViewDirective option='Agenda' />
      </ViewsDirective>
    <Inject services={[Day, Week, TimelineViews, TimelineMonth, Month, Agenda, DragAndDrop]} />
    </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}

### Drag and drop multiple appointments

We can drag and drop multiple appointments by enabling the `allowMultiDrag` property. We can select multiple appointments by holding the CTRL key. Once the events are selected, we can leave the CTRL key and start dragging the event.

We can also drag multiple events from one resource to another resource. In this case, if all the selected events are in the different resources, then all the events should be moved to the single resource that is related to the target event.

{% tab template="schedule/events", iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, WorkWeek, Month, Agenda, DragAndDrop, Inject
} from '@syncfusion/ej2-react-schedule';
import { scheduleData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
    private data: Object[] = extend([], scheduleData, null, true) as Object[];
    render() {
    return <ScheduleComponent height='550px' selectedDate= {new Date(2018, 1, 15)} allowMultiDrag= {true} eventSettings={ { dataSource: this.data } }>
    <Inject services={[Day, Week, WorkWeek, Month, Agenda, DragAndDrop]} />
    </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}

### Disable the drag action

By default, you can drag and drop the events within any of the applicable scheduler views, and to disable it, set `false` to the `allowDragAndDrop` property.

{% tab template="schedule/events", iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, WorkWeek, Month, Agenda, DragAndDrop, Inject
} from '@syncfusion/ej2-react-schedule';
import { scheduleData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
    private data: Object[] = extend([], scheduleData, null, true) as Object[];
    render() {
    return <ScheduleComponent height='550px' selectedDate= {new Date(2018, 1, 15)} allowDragAndDrop= {false} eventSettings={ { dataSource: this.data } }>
    <Inject services={[Day, Week, WorkWeek, Month, Agenda, DragAndDrop]} />
    </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}

### Preventing drag and drop on specific targets

It is possible to prevent the drag action on particular target, by passing the target to be excluded in the `excludeSelectors` option within `dragStart` event. In the following example, we have prevented the drag action on all-day row.

{% tab template="schedule/events", iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, WorkWeek, Month, Agenda, DragAndDrop, Inject
} from '@syncfusion/ej2-react-schedule';
import { scheduleData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
    private onDragStart(args: DragEventArgs): void {
      args.excludeSelectors = 'e-header-cells,e-header-day,e-header-date,e-all-day-cells';
    }
    private data: Object[] = extend([], scheduleData, null, true) as Object[];
    private eventSettings: EventSettingsModel = { dataSource: this.data };
    render() {
      return <ScheduleComponent height='550px' selectedDate= {new Date(2018, 1, 15)} eventSettings= { this.eventSettings } dragStart={(this.onDragStart.bind(this))}>
      <Inject services={[Day, Week, WorkWeek, Month, Agenda, DragAndDrop]} />
      </ScheduleComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}

### Disable scrolling on drag action

By default, while dragging an appointment to the edges, either top or bottom of the Scheduler, scrolling action takes place automatically. To prevent this scrolling, set `false` to the `scroll` value within the `dragStart` event arguments.

{% tab template="schedule/events", iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, WorkWeek, Month, Agenda, DragAndDrop, Inject
} from '@syncfusion/ej2-react-schedule';
import { scheduleData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
    private onDragStart(args: DragEventArgs): void {
      args.scroll = { enable: false };
    }
    private data: Object[] = extend([], scheduleData, null, true) as Object[];
    render() {
    return <ScheduleComponent height='550px' selectedDate= {new Date(2018, 1, 15)} eventSettings={ { dataSource: this.data } } dragStart={(this.onDragStart.bind(this))}>
    <Inject services={[Day, Week, WorkWeek, Month, Agenda, DragAndDrop]} />
    </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}

### Controlling scroll speed while dragging an event

The speed of the scrolling action while dragging an appointment to the Scheduler edges, can be controlled within the `dragStart` event by setting the desired value to the `scrollBy` and `timeDelay` option whereas its default value is 30 minutes and 100ms.

{% tab template="schedule/events", iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, WorkWeek, Month, Agenda, DragAndDrop, Inject
} from '@syncfusion/ej2-react-schedule';
import { scheduleData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
    private onDragStart(args: DragEventArgs): void {
      args.scroll = { enable: true, scrollBy: 5, timeDelay: 200 };
    }
    private data: Object[] = extend([], scheduleData, null, true) as Object[];
    render() {
    return <ScheduleComponent height='550px' selectedDate= {new Date(2018, 1, 15)} eventSettings={ { dataSource: this.data } } dragStart={(this.onDragStart.bind(this))}>
    <Inject services={[Day, Week, WorkWeek, Month, Agenda, DragAndDrop]} />
    </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}

### Auto navigation of date ranges on dragging an event

When an event is dragged either to the left or right extreme edges of the Scheduler and kept hold for few seconds without dropping, the auto navigation of date ranges will be enabled allowing the Scheduler to navigate from current date range to back and forth respectively. This action is set to `false` by default and to enable it, you need to set `navigation` to true within the `dragStart` event.

By default, the navigation delay is set to 2000ms. The navigation delay decides how long the user needs to drag and hold the appointments at the extremities. You can also set your own delay value for letting the users to navigate based on it, using the `timeDelay` within the `dragStart` event.

{% tab template="schedule/events", iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, WorkWeek, Month, Agenda, DragAndDrop, Inject
} from '@syncfusion/ej2-react-schedule';
import { scheduleData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
   private onDragStart(args: DragEventArgs): void {
     args.navigation = { enable: true, timeDelay: 4000 }
   }
   private data: Object[] = extend([], scheduleData, null, true) as Object[];
    render() {
    return <ScheduleComponent height='550px' selectedDate= {new Date(2018, 1, 15)} eventSettings={ { dataSource: this.data } } dragStart={(this.onDragStart.bind(this))}>
    <Inject services={[Day, Week, WorkWeek, Month, Agenda, DragAndDrop]} />
    </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}

### Setting drag time interval

By default, while dragging an appointment, it moves at an interval of 30 minutes. To change the dragging time interval, pass the appropriate values to the `interval` option within the `dragStart` event.

{% tab template="schedule/events", iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, WorkWeek, Month, Agenda, DragAndDrop, Inject
} from '@syncfusion/ej2-react-schedule';
import { scheduleData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
    private onDragStart(args: DragEventArgs): void {
      args.interval = 10;
    }
    private data: Object[] = extend([], scheduleData, null, true) as Object[];
    render() {
    return <ScheduleComponent height='550px' selectedDate= {new Date(2018, 1, 15)} eventSettings={ { dataSource: this.data } } dragStart={(this.onDragStart.bind(this))}>
    <Inject services={[Day, Week, WorkWeek, Month, Agenda, DragAndDrop]} />
    </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}

### Drag and drop items from external source

It is possible to drag and drop the unplanned items from any of the external source into the scheduler, by manually saving those dropped item as a new appointment data through `addEvent` method of Scheduler.

In this example, we have used the tree view control as an external source and the child nodes from the tree view component are dragged and dropped onto the Scheduler. Therefore, it is necessary to make use of the `nodeDragStop` event of the TreeView component, where we can form an event object and save it using the `addEvent` method.

Learn how to drag an external item into the React Scheduler by watching this video:

`youtube:2qyKuXJ1zmQ`

{% tab template="schedule/external-drag", iframeHeight="588px", compileJsx=true %}

```tsx
import * as ReactDOM from 'react-dom';
import * as React from 'react';
import {
  ScheduleComponent, ViewsDirective, ViewDirective, Inject, TimelineViews,
  Resize, DragAndDrop, ActionEventArgs, CellClickEventArgs
} from '@syncfusion/ej2-react-schedule';
import { eventData, waitingList } from './datasource';
import { extend, closest, remove, addClass } from '@syncfusion/ej2-base';
import { DragAndDropEventArgs } from '@syncfusion/ej2-navigations';
import { TreeViewComponent } from '@syncfusion/ej2-react-navigations';

export class App extends React.Component<{}, {}>{
  private scheduleObj: ScheduleComponent;
  private treeObj: TreeViewComponent;
  private isTreeItemDropped: boolean = false;
  private draggedItemId: string = '';
  private allowDragAndDrops: boolean = true;

  private fields: Object = { dataSource: waitingList, id: 'Id', text: 'Name' };
  private data: Object[] = extend([], eventData, null, true) as Object[];

  private treeTemplate(props: any): JSX.Element {
    return (<div id="waiting"><div id="waitdetails"><div id="waitlist">{props.Name}</div>
      <div id="waitcategory">{props.DepartmentName}</div></div></div>);
  }

  private onItemDrag(event: any): void {
    if (this.scheduleObj.isAdaptive) {
      let classElement: HTMLElement = this.scheduleObj.element.querySelector('.e-device-hover');
      if (classElement) {
        classElement.classList.remove('e-device-hover');
      }
      if (event.target.classList.contains('e-work-cells')) {
        addClass([event.target], 'e-device-hover');
      }
    }
    if (document.body.style.cursor === 'not-allowed') {
      document.body.style.cursor = '';
    }
    if (event.name === 'nodeDragging') {
      let dragElementIcon: NodeListOf<HTMLElement> =
        document.querySelectorAll('.e-drag-item.treeview-external-drag .e-icon-expandable');
      for (let i: number = 0; i < dragElementIcon.length; i++) {
        dragElementIcon[i].style.display = 'none';
      }
    }
  }

  private onActionBegin(event: ActionEventArgs): void {
    if (event.requestType === 'eventCreate' && this.isTreeItemDropped) {
      let treeViewdata: { [key: string]: Object }[] = this.treeObj.fields.dataSource as { [key: string]: Object }[];
      const filteredPeople: { [key: string]: Object }[] =
        treeViewdata.filter((item: any) => item.Id !== parseInt(this.draggedItemId, 10));
      this.treeObj.fields.dataSource = filteredPeople;
      let elements: NodeListOf<HTMLElement> = document.querySelectorAll('.e-drag-item.treeview-external-drag');
      for (let i: number = 0; i < elements.length; i++) {
        remove(elements[i]);
      }
    }
  }

  private onTreeDragStop(event: DragAndDropEventArgs): void {
    let treeElement: Element = closest(event.target, '.e-treeview');
    let classElement: HTMLElement = this.scheduleObj.element.querySelector('.e-device-hover');
    if (classElement) {
      classElement.classList.remove('e-device-hover');
    }
    if (!treeElement) {
      event.cancel = true;
      let scheduleElement: Element = closest(event.target, '.e-content-wrap');
      if (scheduleElement) {
        let treeviewData: { [key: string]: Object }[] =
          this.treeObj.fields.dataSource as { [key: string]: Object }[];
        if (event.target.classList.contains('e-work-cells')) {
          const filteredData: { [key: string]: Object }[] =
            treeviewData.filter((item: any) => item.Id === parseInt(event.draggedNodeData.id as string, 10));
          let cellData: CellClickEventArgs = this.scheduleObj.getCellDetails(event.target);
          let eventData: { [key: string]: Object } = {
            Name: filteredData[0].Name,
            StartTime: cellData.startTime,
            EndTime: cellData.endTime,
            IsAllDay: cellData.isAllDay,
            Description: filteredData[0].Description
          };
          this.scheduleObj.addEvent(eventData);
          this.isTreeItemDropped = true;
          this.draggedItemId = event.draggedNodeData.id as string;
        }
      }
    }
  }

  render() {
    return (
      <div className='schedule-control-section'>
        <div className='col-lg-12 control-section'>
          <div className='content-wrapper'>
            <div className="schedule-container">
              <div className="title-container">
                <div className="title-text">Scheduler</div>
              </div>
              <ScheduleComponent ref={schedule => this.scheduleObj = schedule} cssClass='schedule-drag-drop' width='100%' height='650px' selectedDate={new Date(2018, 7, 1)}
                currentView='TimelineDay'
                eventSettings={{
                  dataSource: this.data,
                  fields: {
                    subject: { title: 'Patient Name', name: 'Name' },
                    startTime: { title: "From", name: "StartTime" },
                    endTime: { title: "To", name: "EndTime" },
                    description: { title: 'Reason', name: 'Description' }
                  }
                }}
                actionBegin={this.onActionBegin.bind(this)} drag={this.onItemDrag.bind(this)} >
                <ViewsDirective>
                  <ViewDirective option='TimelineDay' />
                </ViewsDirective>
                <Inject services={[TimelineViews, Resize, DragAndDrop]} />
              </ScheduleComponent>
            </div>
            <div className="treeview-container">
              <div className="title-container">
                <div className="title-text">Waiting List</div>
              </div>
              <TreeViewComponent ref={tree => this.treeObj = tree} cssClass='treeview-external-drag' nodeTemplate={this.treeTemplate.bind(this)} fields={this.fields} nodeDragStop={this.onTreeDragStop.bind(this)} nodeDragging={this.onItemDrag.bind(this)} allowDragAndDrop={this.allowDragAndDrops} />
            </div>
          </div>
        </div>
      </div>
    );
  }
}
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}

### Opening the editor window on drag stop

There are scenarios where you want to open the editor filled with data on newly dropped location and may need to proceed to save it, only when `Save` button is clicked on the editor. On clicking the cancel button should revert these changes. This can be achieved using the `dragStop` event of Scheduler.

{% tab template="schedule/events", iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, WorkWeek, Month, Agenda, DragAndDrop, Inject
} from '@syncfusion/ej2-react-schedule';
import { scheduleData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
    private onDragStop(args: DragEventArgs): void {
      args.cancel = true; //cancels the drop action
      this.scheduleObj.openEditor(args.data, "Save"); //open the event window with updated start and end time
    }
    private data: Object[] = extend([], scheduleData, null, true) as Object[];
    render() {
    return <ScheduleComponent height='550px' ref={schedule => this.scheduleObj = schedule} selectedDate= {new Date(2018, 1, 15)} eventSettings={ { dataSource: this.data } } dragStop={(this.onDragStop.bind(this))}>
    <Inject services={[Day, Week, WorkWeek, Month, Agenda, DragAndDrop]} />
    </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}

## Inline Appointment

In Scheduler, another easier way for `adding` or `editing` the appointment’s subject alone can be achieved by using the inline Add/Edit support. It allows the user to add and edit the appointments inline. To get familiar with the inline Add mode, single click on any of the Scheduler cells or press enter key on the selected cells.

When the inline adding mode is ON, a text box will get created within the clicked Scheduler cells with a blinking cursor in it, requiring the user to enter the subject of an appointment. Once the subject is entered, the appointment will be saved on pressing the enter key.

To enable the inline edit mode, single click on any of the existing appointment’s subject, so that the user can edit the subject of that appointment. The edited subject of that appointment will be updated on pressing the enter key.

The inline option can be enabled/disabled on the Scheduler by using the allowInline API, whereas its default value is set to false.

While using the `allowInline` the `showQuickInfo` will be turned off. The `quickPopup` will not show on clicking the work cell or clicking the appointment when the `allowInline` property is set to true.
In work cells, select multiple cells using keyboard, and then press enter key. The appointment wrapper will be created, and focus will be on the subject field. Also, consider the overlapping scenarios when creating an inline event.

### Normal Event

While editing appointments, single-click the appointment subject, the `editable` option will be enabled in UI and the cursor will focus at the end of the text. Inline editing will be considered for all possible views.

### Recurrence Event

While editing the occurrence from the recurrence series, it is only possible to edit a `single occurrence`, not an entire series.

{% tab template="schedule/events", iframeHeight="588px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, WorkWeek, Agenda, Month, Inject,
  ViewsDirective, ViewDirective
} from '@syncfusion/ej2-react-schedule';
import { scheduleData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}> {
  private data: Object[] = extend([], scheduleData, null, true) as Object[];
  render() {
    return <ScheduleComponent width='100%' height='550px' currentView='Month'
    selectedDate={new Date(2018, 1, 17)} allowInline= {true} eventSettings={ { dataSource: this.data } }>
      <ViewsDirective>
        <ViewDirective option='Day' />
        <ViewDirective option='Week' />
        <ViewDirective option='WorkWeek' />
        <ViewDirective option='Month' />
        <ViewDirective option='Agenda' />
      </ViewsDirective>
    <Inject services={[Day, Week, WorkWeek, Agenda, Month]} />
    </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

## Appointment Resizing

Another way of rescheduling an appointment can be done by resizing it through either of its handlers. To work with resizing functionality, it is necessary to inject the module `Resize` and make sure that `allowResizing` property is set to true.

{% tab template="schedule/events", iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, TimelineViews, TimelineMonth, Month, Agenda, Resize, ViewsDirective, ViewDirective, Inject
} from '@syncfusion/ej2-react-schedule';
import { scheduleData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
    private data: Object[] = extend([], scheduleData, null, true) as Object[];
    render() {
    return <ScheduleComponent height='550px' selectedDate= {new Date(2018, 1, 15)} eventSettings={ { dataSource: this.data } }>
      <ViewsDirective>
        <ViewDirective option='Day' />
        <ViewDirective option='TimelineWeek' />
        <ViewDirective option='Week' />
        <ViewDirective option='TimelineMonth' />
        <ViewDirective option='Month' />
        <ViewDirective option='Agenda' />
      </ViewsDirective>
    <Inject services={[Day, Week, TimelineViews, TimelineMonth, Month, Agenda, Resize]} />
    </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}

### Disable the resize action

By default, resizing of events is allowed on all Scheduler views except Agenda and Month-Agenda view. To disable this event resizing action, set false to the `allowResizing` property.

{% tab template="schedule/events", iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, WorkWeek, Month, Agenda, Resize, Inject
} from '@syncfusion/ej2-react-schedule';
import { scheduleData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
    private data: Object[] = extend([], scheduleData, null, true) as Object[];
    render() {
    return <ScheduleComponent height='550px' selectedDate= {new Date(2018, 1, 15)} allowResizing= {false} eventSettings={ { dataSource: this.data } }>
    <Inject services={[Day, Week, WorkWeek, Month, Agenda, Resize]} />
    </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}

### Disable scrolling on resize action

By default, while resizing an appointment, when its handler reaches the extreme edges of the Scheduler, scrolling action will takes place along with event resizing. To prevent this scrolling action, set false to `scroll` value within the `resizeStart` event.

{% tab template="schedule/events", iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, WorkWeek, Month, Agenda, Resize, ResizeEventArgs, Inject
} from '@syncfusion/ej2-react-schedule';
import { scheduleData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
    private onResizeStart(args: ResizeEventArgs): void {
      args.scroll = { enable: false };
    }
    private data: Object[] = extend([], scheduleData, null, true) as Object[];
    render() {
    return <ScheduleComponent height='550px' selectedDate= {new Date(2018, 1, 15)} eventSettings={ { dataSource: this.data } } resizeStart={(this.onResizeStart.bind(this))}>
    <Inject services={[Day, Week, WorkWeek, Month, Agenda, Resize]} />
    </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}

### Controlling scroll speed while resizing an event

The speed of the scrolling action while resizing an appointment to the Scheduler edges, can be controlled within the `resizeStart` event by setting the desired value to the `scrollBy` option.

{% tab template="schedule/events", iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, WorkWeek, Month, Agenda, Resize, ResizeEventArgs, Inject
} from '@syncfusion/ej2-react-schedule';
import { scheduleData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
    private onResizeStart(args: ResizeEventArgs): void {
      args.scroll = { enable: true, scrollBy: 15 };
    }
    private data: Object[] = extend([], scheduleData, null, true) as Object[];
    render() {
    return <ScheduleComponent height='550px' selectedDate= {new Date(2018, 1, 15)} eventSettings={ { dataSource: this.data } } resizeStart={(this.onResizeStart.bind(this))}>
    <Inject services={[Day, Week, WorkWeek, Month, Agenda, Resize]} />
    </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}

### Setting resize time interval

By default, while resizing an appointment, it extends or shrinks at an interval of 30 minutes. To change this default resize interval, set appropriate values to `interval` option within the `resizeStart` event.

{% tab template="schedule/events", iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, WorkWeek, Month, Agenda, Resize, ResizeEventArgs, Inject
} from '@syncfusion/ej2-react-schedule';
import { scheduleData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
    private onResizeStart(args: ResizeEventArgs): void {
      args.interval = 10;
    }
    private data: Object[] = extend([], scheduleData, null, true) as Object[];
    render() {
    return <ScheduleComponent height='550px' selectedDate= {new Date(2018, 1, 15)} eventSettings={ { dataSource: this.data } } resizeStart={(this.onResizeStart.bind(this))}>
    <Inject services={[Day, Week, WorkWeek, Month, Agenda, Resize]} />
    </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}

## Appointment customization

The look and feel of the Scheduler events can be customized using any one of the following ways.
* [Using event templates](#using-template)
* [Using eventRendered event](#using-eventrendered-event)
* [Using customCSS class](#using-cssclass)

### Using template

Any kind of text, images and links can be added to customize the look of the events. The user can format and change the default appearance of the events by making use of the `template` option available within the `eventSettings` property. The following code example customizes the appointment's default color and time format.

Learn how easily you can customize the basic look and feel of React Scheduler appointments using template from this video:

`youtube:WPffSww3J-Y`

{% tab template="schedule/event-template", iframeHeight="588px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, WorkWeek, Month, Agenda, Inject
} from '@syncfusion/ej2-react-schedule';
import { webinarData } from './datasource';
import { Internationalization, extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
  private data: Object[] = extend([], webinarData, null, true) as Object[];
  private instance: Internationalization = new Internationalization();
  private getTimeString(value: Date) {
    return this.instance.formatDate(value, { skeleton: 'hm' });
  }
  private eventTemplate(props): JSX.Element {
    return (<div className="template-wrap" style={ { background: props.SecondaryColor } }>
    <div className="subject" style={ { background: props.PrimaryColor } }>{props.Subject}</div>
    <div className="time" style={ { background: props.PrimaryColor } }>
    Time: {this.getTimeString(props.StartTime)} - {this.getTimeString(props.EndTime)}</div>
   </div>);
  }
  render() {
    return <ScheduleComponent  width= '100%' height='550px' selectedDate= {new Date(2018, 1, 15) } eventSettings= { {
      dataSource:this.data, template:this.eventTemplate.bind(this) } } readonly= {true}>
      <Inject services={[Day, Week, WorkWeek, Month, Agenda]} />
    </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

> All the built-in fields that are mapped to the appropriate field properties within the `eventSettings`, as well as custom mapped fields from the Scheduler dataSource can be accessed within the template code.

### Using eventRendered event

The `eventRendered` event triggers before the appointment renders on the Scheduler. Therefore, this client-side event can be utilized to customize the look of events based on any specific criteria, before rendering them on the scheduler.

{% tab template="schedule/events", iframeHeight="588px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, WorkWeek, Month, Agenda, Inject, EventRenderedArgs
} from '@syncfusion/ej2-react-schedule';
import { scheduleData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
  private scheduleObj: ScheduleComponent;
  private data: Object[] = extend([], scheduleData, null, true) as Object[];
  private onEventRendered(args: EventRenderedArgs): void {
    this.applyCategoryColor(args, this.scheduleObj.currentView);
  }
  private applyCategoryColor(args: EventRenderedArgs, currentView: string): void {
    let categoryColor: string = args.data.CategoryColor as string;
    if (!args.element || !categoryColor) {
        return;
    }
    if (currentView === 'Agenda') {
        (args.element.firstChild as HTMLElement).style.borderLeftColor = categoryColor;
    } else {
        args.element.style.backgroundColor = categoryColor;
    }
  }

  render() {
    return <ScheduleComponent  width= '100%' height='550px' ref={schedule => this.scheduleObj = schedule} selectedDate= {new Date(2018, 1, 15) } eventSettings= { { dataSource:this.data } }eventRendered={this.onEventRendered.bind(this)}>
      <Inject services={[Day, Week, WorkWeek, Month, Agenda]} />
    </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

### Using cssClass

The customization of events can also be achieved using `cssClass` property of the Scheduler. In the following example, the background of appointments has been changed using the cssClass.

{% tab template="schedule/events", iframeHeight="588px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, WorkWeek, Month, Agenda, Inject
} from '@syncfusion/ej2-react-schedule';
import { scheduleData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
  private data: Object[] = extend([], scheduleData, null, true) as Object[];

  render() {
    return <ScheduleComponent  width= '100%' height='550px' cssClass='custom-class' selectedDate= {new Date(2018, 1, 15) } eventSettings= {{ dataSource:this.data }}>
      <Inject services={[Day, Week, WorkWeek, Month, Agenda]} />
    </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

## Setting minimum height

It is possible to set minimal height for appointments on Scheduler using `eventRendered` event, when its start and end time duration is less than the default duration of a single slot.

{% tab template="schedule/events", iframeHeight="588px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, WorkWeek, Month, Agenda, Inject, EventRenderedArgs
} from '@syncfusion/ej2-react-schedule';

class App extends React.Component<{}, {}>{
  private data: Object[] = [{
      Id: 13,
      Subject: 'Myths of Andromeda Galaxy',
      StartTime: new Date(2018, 1, 16, 10, 30),
      EndTime: new Date(2018, 1, 16, 10, 40)
  }, {
      Id: 14,
      Subject: 'Aliens vs Humans',
      StartTime: new Date(2018, 1, 15, 10, 0),
      EndTime: new Date(2018, 1, 15, 10, 20)
  }];
  private onEventRendered(args: EventRenderedArgs): void {
    let cellHeight: number = (this.scheduleObj.element.querySelector('.e-work-cells') as HTMLElement).offsetHeight;
    let appHeight: number = ((args.data.EndTime as Date).getTime() - (args.data.StartTime as Date).getTime()) / (60 * 1000) * (cellHeight * this.scheduleObj.timeScale.slotCount) / this.scheduleObj.timeScale.interval;
    args.element.style.height = appHeight+'px';
  }

  render() {
    return <ScheduleComponent  width= '100%' height='550px' ref={schedule => this.scheduleObj = schedule} selectedDate= {new Date(2018, 1, 15) } eventSettings= { { dataSource:this.data } }eventRendered={this.onEventRendered.bind(this)}>
      <Inject services={[Day, Week, WorkWeek, Month, Agenda]} />
    </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

## Block Dates and Times

It is possible to block a set of dates or a particular time ranges on the Scheduler. To do so, define an appointment object within `eventSettings` along with the required time range to block and set the `IsBlock` field to true. Usually, the event objects defined with isBlock field set to true will block the entire time cells lying within the appropriate time ranges specified through `startTime` and `endTime` fields.

{% tab template="schedule/events", iframeHeight="588px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, WorkWeek, Month, Agenda, Inject
} from '@syncfusion/ej2-react-schedule';
import { blockData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
    private data: Object[] = extend([], blockData, null, true) as Object[];
    render() {
    return <ScheduleComponent height='550px' selectedDate= {new Date(2018, 1, 15)} eventSettings={ { dataSource: this.data } }>
    <Inject services={[Day, Week, WorkWeek, Month, Agenda]} />
    </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

Block events can also be defined to repeat on several days as shown in the following code example.

{% tab template="schedule/events", iframeHeight="588px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, TimelineViews, Month, Agenda,
  ViewsDirective, ViewDirective, Inject
} from '@syncfusion/ej2-react-schedule';

class App extends React.Component<{}, {}>{
    private data: Object[] = [{
        Id: 1,
        Subject: 'Explosion of Betelgeuse Star',
        StartTime: new Date(2018, 1, 15, 9, 30),
        EndTime: new Date(2018, 1, 15, 11, 0),
        RecurrenceRule: 'FREQ=DAILY;INTERVAL=1;COUNT=5',
        IsBlock: true
    }, {
        Id: 2,
        Subject: 'Thule Air Crash Report',
        StartTime: new Date(2018, 1, 14, 12, 0),
        EndTime: new Date(2018, 1, 14, 14, 0)
    }];
    render() {
    return <ScheduleComponent height='550px' selectedDate= {new Date(2018, 1, 15)} eventSettings={ { dataSource: this.data } }>
    <ViewsDirective>
      <ViewDirective option='Day' />
      <ViewDirective option='Week' />
      <ViewDirective option='TimelineWeek' />
      <ViewDirective option='Month' />
      <ViewDirective option='Agenda' />
    </ViewsDirective>
    <Inject services={[Day, Week, TimelineViews, Month, Agenda]} />
    </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

## Readonly

An interaction with the appointments of Scheduler can be enabled/disabled using the `readonly` property. With this property enabled, you can simply navigate between the Scheduler dates, views and can be able to view the appointment details in the quick info window. Most importantly, the users are not allowed to perform any CRUD actions on Scheduler, when this property is set to true. By default, it is set as `false`.

{% tab template="schedule/events", iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, WorkWeek, Month, Agenda, Inject
} from '@syncfusion/ej2-react-schedule';
import { scheduleData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
    private data: Object[] = extend([], scheduleData, null, true) as Object[];
    render() {
    return <ScheduleComponent height='550px' selectedDate= {new Date(2018, 1, 15)} readonly= {true} eventSettings={ { dataSource: this.data } }>
    <Inject services={[Day, Week, WorkWeek, Month, Agenda]} />
    </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}

## Make specific events readonly

There are scenarios where you need to restrict the CRUD action on specific appointments alone based on certain conditions. In the following example, the events that has occurred on the past hours from the current date of the Scheduler are made as read-only and the CRUD actions has been prevented only on those appointments. This can be achieved by setting `isReadonly` field of read-only events to `true`.

{% tab template="schedule/events", iframeHeight="588px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, WorkWeek, Month, Agenda, Inject
} from '@syncfusion/ej2-react-schedule';
import { readOnlyData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
    private data: Object[] = extend([], readOnlyData, null, true) as Object[];
    render() {
    return <ScheduleComponent height='550px' selectedDate= {new Date(2018, 1, 15)} eventSettings={ { dataSource: this.data } }>
    <Inject services={[Day, Week, WorkWeek, Month, Agenda]} />
    </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}

> By default, the event editor is prevented to open on the read-only events when `isReadonly` field is set to `true`.

## Restricting event creation on specific time slots

You can restrict the users to create and update more than one appointment on specific time slots. Also, you can disable the CRUD action on those time slots if it is already occupied, which can be achieved using Scheduler's public method `isSlotAvailable`.

{% tab template="schedule/events", iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, WorkWeek, Inject,
  ActionEventArgs,  EventFieldsMapping
} from '@syncfusion/ej2-react-schedule';
import { extend } from '@syncfusion/ej2-base';
import { scheduleData } from './datasource';

class App extends React.Component<{}, {}>{
  private scheduleObj: ScheduleComponent;
  private data: Object[] = extend([], scheduleData, null, true) as Object[];
  private onActionBegin(args: ActionEventArgs): void {
    if (args.requestType === 'eventCreate' && (args.data as Object).length > 0) {
    let eventData: { [key: string]: Object } = args.data[0] as { [key: string]: Object };
    let eventField: EventFieldsMapping = this.scheduleObj.eventFields;
    let startDate: Date = eventData[eventField.startTime] as Date;
    let endDate: Date = eventData[eventField.endTime] as Date;
    args.cancel = !this.scheduleObj.isSlotAvailable(startDate, endDate);
    }
  }
  render() {
    return <ScheduleComponent ref={schedule => this.scheduleObj = schedule} width= '100%' height='550px' selectedDate= {new Date(2018, 1, 15)} eventSettings={ { dataSource: this.data } } actionBegin={this.onActionBegin.bind(this)}>
      <Inject services={[Day, Week, WorkWeek]} />
    </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}

## Differentiate the past time events

To differentiate the appearance of the appointments based on specific criteria such as displaying the past hour appointments with different colors on Scheduler, `eventRendered` event can be used which triggers before the appointment renders on the Scheduler.

{% tab template="schedule/events", iframeHeight="588px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, WorkWeek, Month, Agenda, Inject, EventRenderedArgs
} from '@syncfusion/ej2-react-schedule';
import { scheduleData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
  private scheduleObj: ScheduleComponent;
  private data: Object[] = extend([], scheduleData, null, true) as Object[];
  private onEventRendered(args: EventRenderedArgs): void {
    if (args.data.EndTime < this.scheduleObj.selectedDate) {
      args.element.classList.add('e-past-app');
    }
  }

  render() {
    return <ScheduleComponent  width= '100%' height='550px' ref={schedule => this.scheduleObj = schedule} selectedDate= {new Date(2018, 1, 15) } eventSettings= { { dataSource:this.data } }eventRendered={this.onEventRendered.bind(this)}>
      <Inject services={[Day, Week, WorkWeek, Month, Agenda]} />
    </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

## Appointments occupying entire cell

The Scheduler allows the event to occupies the full height of the cell without its header part by setting `true` for `enableMaxHeight` Property.

We can show more indicator if more than one appointment is available in a same cell by setting `true` to `enableIndicator` property whereas its default value is false.

{% tab template="schedule/events", iframeHeight="588px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, TimelineViews, TimelineMonth, ViewsDirective, ViewDirective, Inject
} from '@syncfusion/ej2-react-schedule';
import { scheduleData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
   private data: Object[] = extend([], scheduleData, null, true) as Object[];
render() {
    return <ScheduleComponent width='100%' height='500px' selectedDate={new Date(2018, 1, 15)} eventSettings={ { dataSource: this.data, enableMaxHeight: true, enableIndicator: false } }>
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

## Display tooltip for appointments

The tooltip shows the Scheduler appointment's information in a formatted style by making use of the tooltip related options.

### Show or hide built-in tooltip

The tooltip can be displayed for appointments by setting `true` to the `enableTooltip` option within the `eventSettings` property.

{% tab template="schedule/events", iframeHeight="588px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, TimelineViews, Month, Agenda, Inject
} from '@syncfusion/ej2-react-schedule';
import { scheduleData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
   private data: Object[] = extend([], scheduleData, null, true) as Object[];
render() {
    return <ScheduleComponent width='100%' height='500px' selectedDate={new Date(2018, 1, 15)} eventSettings={ { dataSource: this.data, enableTooltip: true } }>
         <Inject services={[Day, Week, TimelineViews, Month, Agenda]} />
      </ScheduleComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

### Customizing event tooltip using template

After enabling the default tooltip, it is possible to customize the display of needed event information on tooltip by making use of the `tooltipTemplate` option within the `eventSettings`.

{% tab template="schedule/tooltip", iframeHeight="588px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, WorkWeek, Month, Agenda, Inject
} from '@syncfusion/ej2-react-schedule';
import { eventsData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
   private data: Object[] = extend([], eventsData, null, true) as Object[];
   private template(props): JSX.Element {
    return (<div className="tooltip-wrap">
      <div className="content-area"><div className="name">{props.Subject}</div>
      {(props.City !== null && props.City !== undefined) ? <div className="city">{props.City}</div> : ''}
     <div className="time">From :{props.StartTime.toLocaleString()}</div>
     <div className="time">To  :{props.EndTime.toLocaleString()}</div></div></div>);
    }
render() {
    return <ScheduleComponent width='100%' height='500px' selectedDate={new Date(2018, 1, 15)} eventSettings={ {
            dataSource: this.data, enableTooltip: true,
            tooltipTemplate: this.template.bind(this)
        } }>
         <Inject services={[Day, Week, WorkWeek, Month, Agenda]} />
      </ScheduleComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

> All the field names that are mapped from the Scheduler dataSource to the appropriate field properties such as subject, description, location, startTime and endTime within the `eventSettings` can be accessed within the template.

## Appointment selection

Appointment selection can be done either through mouse or keyboard actions. The selected events in UI will have a box shadow effect around to differentiate it from other appointments.

| Action | Description |
|-------|---------|
| Mouse click or Single tap on appointments | Selects single appointment. |
| Ctrl + [Mouse click] or [Single tap] on appointments | Selects multiple appointments.|

## Deleting multiple appointments

With the options available to select multiple appointments, it is also possible to delete the multiple selected appointments simply by pressing the `delete` key. In case of deleting multiple selected occurrences of an event series, only those occurrences will be deleted and not the entire series.

## Retrieve event details from the UI of an event

It is possible to access the information about the event fields of an appointment element displayed on the Scheduler UI. This can be achieved by passing an appointment element as argument to the public method `getEventDetails`.

In the following example, the subject of the appointment clicked has been displayed.

{% tab template="schedule/event-public", iframeHeight="588px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import {
  ScheduleComponent, Day, Week, WorkWeek, Month, Agenda, Inject, EventClickArgs
} from '@syncfusion/ej2-react-schedule';
import { scheduleData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
  private scheduleObj: ScheduleComponent;
  private data: Object[] = extend([], scheduleData, null, true) as Object[];
  private onEventClick(args: EventClickArgs): void {
    let event: Object = this.scheduleObj.getEventDetails(args.element);
    this.appendElement(event.Subject +'<hr>');
  }
  private appendElement(html: string): void {
    let span: HTMLElement = document.createElement('span');
    span.innerHTML = html;
    let log: HTMLElement = document.getElementById('EventLog');
    log.insertBefore(span, log.firstChild);
  }
  private onClick(): void {
    document.getElementById('EventLog').innerHTML = '';
  }

  render() {
    return(  <div className='content-wrapper'>
    <div className='col-lg-9 control-section'>
          <ScheduleComponent ref={t => this.scheduleObj = t} width= '100%' height='550px' selectedDate=
        { new Date(2018, 1, 15) } eventSettings={ { dataSource: this.data } } eventClick={this.onEventClick.bind(this)}>
            <Inject services={[Day, Week, WorkWeek, Month, Agenda ]} />
        </ScheduleComponent>
        </div>
        <div className='col-lg-3 property-section'>
          <div title='Event Trace'>
            <table id='property' title='Properties' className='property-panel-table' style={{ width: '100%' }}>
              <tbody>
                <tr style={{ height: '250px' }}>
                  <td>
                    <div className='eventarea' style={{ height: '245px', overflow: 'auto' }}>
                      <span className='EventLog' id='EventLog' style={{ wordBreak: 'normal' }}></span>
                    </div>
                  </td>
                </tr>
                <tr style={{ height: '50px' }}>
                  <td style={{ width: '30%' }}>
                    <div className='evtbtn' style={{ paddingBottom: '10px' }}>
                        <ButtonComponent title='Clear' onClick={ this.onClick.bind(this) }>Clear</ButtonComponent>
                    </div>
                  </td>
                </tr>
              </tbody>
            </table>
            </div>
        </div>
    </div>)
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

## Get the current view appointments

To retrieve the appointments present in the current view of the Scheduler, you can make use of the `getCurrentViewEvents` public method. In the following example, the count of current view appointment collection rendered has been traced in `dataBound` event.

{% tab template="schedule/event-public", iframeHeight="588px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import {
  ScheduleComponent, Day, Week, WorkWeek, Month, Agenda, Inject
} from '@syncfusion/ej2-react-schedule';
import { scheduleData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
  private scheduleObj: ScheduleComponent;
  private data: Object[] = extend([], scheduleData, null, true) as Object[];
  private onDataBound(): void {
      let event: Object[] = this.scheduleObj.getCurrentViewEvents();
      if (event.length > 0) {
        this.appendElement('Events present on current view <b>' + event.length +'<b><hr>');
      } else {
        this.appendElement('No Events available in this view.<hr>');
      }
  }
  private appendElement(html: string): void {
    let span: HTMLElement = document.createElement('span');
    span.innerHTML = html;
    let log: HTMLElement = document.getElementById('EventLog');
    log.insertBefore(span, log.firstChild);
  }
  private onClick(): void {
    document.getElementById('EventLog').innerHTML = '';
  }
   render() {
    return(  <div className='content-wrapper'>
    <div className='col-lg-9 control-section'>
          <ScheduleComponent ref={t => this.scheduleObj = t} width= '100%' height='550px' selectedDate=
        { new Date(2018, 1, 15) } eventSettings={ { dataSource: this.data } } dataBound={this.onDataBound.bind(this)}>
            <Inject services={[Day, Week, WorkWeek, Month, Agenda ]} />
        </ScheduleComponent>
        </div>
        <div className='col-lg-3 property-section'>
          <div title='Event Trace'>
            <table id='property' title='Properties' className='property-panel-table' style={{ width: '100%' }}>
              <tbody>
                <tr style={{ height: '250px' }}>
                  <td>
                    <div className='eventarea' style={{ height: '245px', overflow: 'auto' }}>
                      <span className='EventLog' id='EventLog' style={{ wordBreak: 'normal' }}></span>
                    </div>
                  </td>
                </tr>
                <tr style={{ height: '50px' }}>
                  <td style={{ width: '30%' }}>
                    <div className='evtbtn' style={{ paddingBottom: '10px' }}>
                        <ButtonComponent title='Clear' onClick={ this.onClick.bind(this) }>Clear</ButtonComponent>
                    </div>
                  </td>
                </tr>
              </tbody>
            </table>
            </div>
        </div>
    </div>)
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

## Get the entire appointment collections

The entire collection of appointments rendered on the Scheduler can be accessed using the `getEvents` public method. In the following example, the count of entire appointment collection rendered on the Scheduler has been traced in `dataBound` event.

{% tab template="schedule/event-public", iframeHeight="588px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import {
  ScheduleComponent, Day, Week, WorkWeek, Month, Agenda, Inject
} from '@syncfusion/ej2-react-schedule';
import { scheduleData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
  private scheduleObj: ScheduleComponent;
  private data: Object[] = extend([], scheduleData, null, true) as Object[];
  private onDataBound(): void {
      let event: Object[] = this.scheduleObj.getEvents();
      this.appendElement('Events present on scheduler <b>' + event.length +'<b><hr>');
  }
  private appendElement(html: string): void {
    let span: HTMLElement = document.createElement('span');
    span.innerHTML = html;
    let log: HTMLElement = document.getElementById('EventLog');
    log.insertBefore(span, log.firstChild);
  }
  private onClick(): void {
    document.getElementById('EventLog').innerHTML = '';
  }
   render() {
    return(  <div className='content-wrapper'>
    <div className='col-lg-9 control-section'>
          <ScheduleComponent ref={t => this.scheduleObj = t} width= '100%' height='550px' selectedDate=
        { new Date(2018, 1, 15) } eventSettings={ { dataSource: this.data } } dataBound={this.onDataBound.bind(this)}>
            <Inject services={[Day, Week, WorkWeek, Month, Agenda ]} />
        </ScheduleComponent>
        </div>
        <div className='col-lg-3 property-section'>
          <div title='Event Trace'>
            <table id='property' title='Properties' className='property-panel-table' style={{ width: '100%' }}>
              <tbody>
                <tr style={{ height: '250px' }}>
                  <td>
                    <div className='eventarea' style={{ height: '245px', overflow: 'auto' }}>
                      <span className='EventLog' id='EventLog' style={{ wordBreak: 'normal' }}></span>
                    </div>
                  </td>
                </tr>
                <tr style={{ height: '50px' }}>
                  <td style={{ width: '30%' }}>
                    <div className='evtbtn' style={{ paddingBottom: '10px' }}>
                        <ButtonComponent title='Clear' onClick={ this.onClick.bind(this) }>Clear</ButtonComponent>
                    </div>
                  </td>
                </tr>
              </tbody>
            </table>
            </div>
        </div>
    </div>)
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

## Refresh appointments

If your requirement is to simply refresh the appointments instead of refreshing the entire Scheduler elements from your application end, make use of the `refreshEvents` public method.

```tsx
this.scheduleObj.refreshEvents();
```

> You can refer to our [React Scheduler](https://www.syncfusion.com/react-ui-components/react-scheduler) feature tour page for its groundbreaking feature representations. You can also explore our [React Scheduler example](https://ej2.syncfusion.com/react/demos/#/material/schedule/overview) to knows how to present and manipulate data.
