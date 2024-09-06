# Recurrence Editor

The Recurrence editor is integrated into Scheduler editor window by default, to process the recurrence rule generation for events. Apart from this, it can also be used as an individual component referring from the Scheduler repository to work with the recurrence related processes.

> All the valid recurrence rule string mentioned in the [iCalendar](https://tools.ietf.org/html/rfc5545#section-3.3.10) specifications are applicable to use with the recurrence editor.

## Customizing the repeat type option in editor

By default, there are 5 types of repeat options available in recurrence editor such as,

* Never
* Daily
* Weekly
* Monthly
* Yearly

It is possible to customize the recurrence editor to display only the specific repeat options such as `Daily` and `Weekly` options alone by setting the appropriate `frequencies` option.

{% tab template="schedule/events", iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, WorkWeek, Month, Agenda, Inject, PopupOpenEventArgs
} from '@syncfusion/ej2-react-schedule';
import { scheduleData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
  private scheduleObj: ScheduleComponent;
  private data: Object[] = extend([], scheduleData, null, true) as Object[];
  private onPopupOpen(args: PopupOpenEventArgs): void {
    if (args.type == 'Editor') {
      this.scheduleObj.eventWindow.recurrenceEditor.frequencies = ['none', 'daily', 'weekly'];
    }
  }
  render() {
    return <ScheduleComponent ref={schedule => this.scheduleObj = schedule} width= '100%' height='550px' selectedDate= {new Date(2018, 1, 15)} eventSettings= { {dataSource: this.data } }
    popupOpen= {this.onPopupOpen.bind(this)}>
    <Inject services={[Day, Week, WorkWeek, Month, Agenda]} />
    </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}

The other properties available in recurrence editor are tabulated below,

| Properties | Type | Description |
|------------|------|-------------|
| firstDayOfWeek | number | Sets the first day of the week.|
| startDate | Date | Sets the start date |
| dateformat | string | Sets the specific date format on recurrence editor.|
| locale | string | Sets the locale to be applied on recurrence editor.|
| cssClass | string | Allows styling with custom class names.|
| enableRtl | boolean | Allows recurrence editor to render in RTL mode.|
| minDate | Date | Sets the minimum date on recurrence editor.|
| maxDate | Date | Sets the maximum date on recurrence editor.|
| value | string | Sets the recurrence rule as its output values.|
| selectedType | number | Sets the current repeat type to be set on the recurrence editor.|

## Accessing the recurrence rule string

The recurrence rule is usually generated based on the options selected from the recurrence editor and also it follows the [`iCalendar`](https://tools.ietf.org/html/rfc5545#section-3.3.10) specifications. The generated recurrence rule string is a valid one to be used with the Scheduler event’s recurrence rule field.

There is a `change` event available in recurrence editor, that triggers on every time the fields of recurrence editor tends to change. Within this event argument, you can access the generated recurrence value through the `value` option as shown in the following code example.

{% tab template="schedule/recur-editor", iframeHeight="588px", compileJsx=true %}

```tsx

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { RecurrenceEditorComponent, RecurrenceEditorChangeEventArgs }
from '@syncfusion/ej2-react-schedule';

class App extends React.Component<{}, {}>{
    private recObject: RecurrenceEditorComponent;
    componentDidMount(): void {
        let outputElement: HTMLElement = document.querySelector('#rule-output') as HTMLElement;
        outputElement.innerText = 'Select Rule';
    }

  private onChange(args: RecurrenceEditorChangeEventArgs): void {
    let outputElement: HTMLElement = document.querySelector('#rule-output') as HTMLElement;
    if(args.value == "") {
        outputElement.innerText = 'Select Rule';
    } else {
        outputElement.innerText = args.value;
    }
  }
   render() {
    return <div className='content-wrapper recurrence-editor-wrap'>
            <div style={ { paddingBottom: '15px' } }>
              <label>Rule Output</label>
              <div className='rule-output-container'>
                <div id='rule-output'></div>
              </div>
            </div>
            <div className='RecurrenceEditor'>
              <RecurrenceEditorComponent id='RecurrenceEditor' ref={t => this.recObject = t} change={this.onChange.bind(this)}></RecurrenceEditorComponent>
            </div>
        </div>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}

## Set specific value on recurrence editor

It is possible to display the recurrence editor with specific options loaded initially, based on the rule string that we provide. The fields of recurrence editor will change its values accordingly, when we provide a particular rule through the `setRecurrenceRule` method.

{% tab template="schedule/recur-editor", iframeHeight="588px", compileJsx=true %}

```tsx

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { RecurrenceEditorComponent, RecurrenceEditorChangeEventArgs }
from '@syncfusion/ej2-react-schedule';

class App extends React.Component<{}, {}>{
    private recObject: RecurrenceEditorComponent;
    componentDidUpdate(): void {
    let outputElement: HTMLElement = document.querySelector('#rule-output') as HTMLElement;
    this.recObject.setRecurrenceRule('FREQ=DAILY;INTERVAL=2;COUNT=8');
    outputElement.innerText = this.recObject.value as string;
  }

  private onChange(args: RecurrenceEditorChangeEventArgs): void {
    let outputElement: HTMLElement = document.querySelector('#rule-output') as HTMLElement;
    outputElement.innerText = args.value;
  }
   render() {
    return <div className='content-wrapper recurrence-editor-wrap'>
            <div style={ { paddingBottom: '15px' } }>
              <label>Rule Output</label>
              <div className='rule-output-container'>
                <div id='rule-output'></div>
              </div>
            </div>
            <div className='RecurrenceEditor'>
              <RecurrenceEditorComponent id='RecurrenceEditor' ref={t => this.recObject = t} change={this.onChange.bind(this)}></RecurrenceEditorComponent>
            </div>
        </div>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}

## Recurrence date generation

You can parse the `recurrenceRule` of an event to generate the date instances on which that particular event is going to occur, using the `getRecurrenceDates` method. It generates the dates based on the `recurrenceRule` that we provide. The parameters to be provided for `getRecurrenceDates` method are as follows.

| Field name | Type | Description |
|------------|------|-------------|
| `startDate` | Date| Appointment start date. |
| `rule` | String| Recurrence rule present in an event object. |
| `excludeDate` | String | Date collection (in ISO format) to be excluded. It is **optional**. |
| `maximumCount` | Number | Number of date count to be generated. It is **optional**. |
| `viewDate` | Date | Current view range's first date. It is **optional**. |

{% tab template="schedule/recur-editor", iframeHeight="588px", compileJsx=true %}

```tsx

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { RecurrenceEditorComponent }
from '@syncfusion/ej2-react-schedule';

class App extends React.Component<{}, {}>{
    private recObject: RecurrenceEditorComponent;
    componentDidMount(): void {
      let dates: number[] = this.recObject.getRecurrenceDates(new Date(2018, 0, 7,10, 0), 'FREQ=DAILY;INTERVAL=1', '20180108T114224Z,20180110T114224Z', 4, new Date(2018, 0, 7));
      let stringCollection: string = '';
      for (let index: number = 0; index < dates.length; index++) {
        stringCollection += new Date(dates[index]);
          if (index + 1 !== dates.length) {
            stringCollection += '\n';
          }
      }
      let outputElement: HTMLElement = document.querySelector('#rule-output') as HTMLElement;
      outputElement.innerText = stringCollection;
    }

   render() {
    return <div className='content-wrapper recurrence-editor-wrap'>
            <div style={ { paddingBottom: '15px' } }>
              <label>Date Collections</label>
              <div className='rule-output-container'>
                <div id='rule-output'></div>
              </div>
            </div>
        <div className='RecurrenceEditor' style={ { display: "none" } }>
          <RecurrenceEditorComponent id='RecurrenceEditor' ref={t => this.recObject = t}></RecurrenceEditorComponent>
        </div>
        </div>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}

> Above example will generate two dates January 7, 2018 & January 9 2018 by excluding the in between dates January 8 2018 & January 10 2018, since those dates were given in the exclusion list. Generated dates can then be utilised to create appointments.

## Recurrence date generation in server-side

It is also possible to generate recurrence date instances from server-side by manually referring the `RecurrenceHelper` class, which is specifically written and referred from application end to handle this date generation process.

> Refer [here](https://www.syncfusion.com/kb/10009/how-to-parse-the-recurrencerule-at-server-side) for the step by step procedure to achieve date generation in server-side.

## Restrict date generation with specific count

In case, if the rule is given in "NEVER ENDS" category, then you can mention the maximum count when you actually want to stop the date generation starting from the provided start date. To do so, provide the appropriate `maximumCount` value within the `getRecurrenceDates` method as shown in the following code example.

{% tab template="schedule/recur-editor", iframeHeight="588px", compileJsx=true %}

```tsx

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { RecurrenceEditorComponent }
from '@syncfusion/ej2-react-schedule';

class App extends React.Component<{}, {}>{
    private recObject: RecurrenceEditorComponent;
    componentDidMount(): void {
      let dates: number[] = this.recObject.getRecurrenceDates(new Date(2018, 0, 7,10, 0), 'FREQ=DAILY;INTERVAL=1', null, 10, null);
      let stringCollection: string = '';
      for (let index: number = 0; index < dates.length; index++) {
        stringCollection += new Date(dates[index]);
          if (index + 1 !== dates.length) {
            stringCollection += '\n';
          }
      }
      let outputElement: HTMLElement = document.querySelector('#rule-output') as HTMLElement;
      outputElement.innerText = stringCollection;
    }

   render() {
    return <div className='content-wrapper recurrence-editor-wrap'>
            <div style={ { paddingBottom: '15px' } }>
              <label>Date Collections</label>
              <div className='rule-output-container'>
                <div id='rule-output'></div>
              </div>
            </div>
            <div className='RecurrenceEditor' style={ { display: 'none' } }>
              <RecurrenceEditorComponent id='RecurrenceEditor' ref={t => this.recObject = t}></RecurrenceEditorComponent>
            </div>
        </div>
    }
};
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}

> You can refer to our [React Scheduler](https://www.syncfusion.com/react-ui-components/react-scheduler) feature tour page for its groundbreaking feature representations. You can also explore our [React Scheduler example](https://ej2.syncfusion.com/react/demos/#/material/schedule/overview) to knows how to present and manipulate data.
