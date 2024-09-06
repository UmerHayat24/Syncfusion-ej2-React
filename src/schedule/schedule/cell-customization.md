# Cell Customizations

The cells of the Scheduler can be easily customized either using the cell template or `RenderCell` event.

## Setting cell dimensions in all views

The height and width of the Scheduler cells can be customized either to increase or reduce its size through the `cssClass` property, which overrides the default CSS applied on cells.

{% tab template="schedule/cell-dimension", iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, WorkWeek, Month, Inject,
  ActionEventArgs, ViewsDirective, ViewDirective
} from '@syncfusion/ej2-react-schedule';
import { scheduleData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
  private scheduleObj: ScheduleComponent;
  private data: Object[] = extend([], scheduleData, null, true) as Object[];
  render() {
    return <ScheduleComponent ref={schedule => this.scheduleObj = schedule} width= '100%' height='550px' selectedDate= {new Date(2018, 1, 15)} cssClass= 'schedule-cell-dimension' eventSettings= { {dataSource: this.data } }>
        <ViewsDirective>
            <ViewDirective option='Day' />
            <ViewDirective option='Week' />
            <ViewDirective option='WorkWeek' />
            <ViewDirective option='Month' />
        </ViewsDirective>
        <Inject services={[Day, Week, WorkWeek, Month]} />
    </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}

## Check for cell availability

You can check whether the given time range slots are available for event creation or already occupied by other events using the `isSlotAvailable` method. In the following code example, if a specific time slot already contains an appointment, then no more appointments can be added to that cell.

{% tab template="schedule/local-data", iframeHeight="588px", compileJsx=true %}

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

## Customizing cells in all the views

It is possible to customize the appearance of the cells using both template options and `renderCell` event on all the views.

### Using template

The `cellTemplate` option accepts the template string and is used to customize the cell background with specific images or appropriate text on the given date values.

{% tab template="schedule/cell", iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, TimelineViews, Month, Inject,
  ViewsDirective, ViewDirective, CellTemplateArgs
} from '@syncfusion/ej2-react-schedule';

class App extends React.Component<{}, {}> {
  private getMonthCellContent(date: Date) {
    if (date.getMonth() === 10 && date.getDate() === 23) {
      return '<img src= "https://ej2.syncfusion.com/demos/src/schedule/images/birthday.svg" />';
    } else if (date.getMonth() === 11 && date.getDate() === 9) {
      return '<img src= "https://ej2.syncfusion.com/demos/src/schedule/images/get-together.svg" />';
    } else if (date.getMonth() === 11 && date.getDate() === 13) {
      return '<img src= "https://ej2.syncfusion.com/demos/src/schedule/images/birthday.svg" />';
    } else if (date.getMonth() === 11 && date.getDate() === 22) {
      return '<img src= "https://ej2.syncfusion.com/demos/src/schedule/images/thanksgiving-day.svg" />';
    } else if (date.getMonth() === 11 && date.getDate() === 24) {
      return '<img src="https://ej2.syncfusion.com/demos/src/schedule/images/christmas-eve.svg" />';
    } else if (date.getMonth() === 11 && date.getDate() === 25) {
      return '<img src= "https://ej2.syncfusion.com/demos/src/schedule/images/christmas.svg" />';
    } else if (date.getMonth() === 0 && date.getDate() === 1) {
      return '<img src= "https://ej2.syncfusion.com/demos/src/schedule/images/newyear.svg" />';
    } else if (date.getMonth() === 0 && date.getDate() === 14) {
      return '<img src= "https://ej2.syncfusion.com/demos/src/schedule/images/birthday.svg" />';
    }
    return '';
  }
  private getWorkCellText(date: Date) {
    let weekEnds: number[] = [0, 6];
    if (weekEnds.indexOf(date.getDay()) >= 0) {
      return "<img src='https://ej2.syncfusion.com/demos/src/schedule/images/newyear.svg' />";
    }
    return '';
};
  private cellTemplate(props: CellTemplateArgs): JSX.Element {
    if (props.type === "workCells") {
      return (<div className="templatewrap" dangerouslySetInnerHTML={ { __html: this.getWorkCellText(props.date) } }></div>);
    }
    if (props.type === "monthCells") {
      return (<div className="templatewrap" dangerouslySetInnerHTML={ { __html: this.getMonthCellContent(props.date) } }></div>);
    }
    return (<div></div>);
  }
  render() {
    return <ScheduleComponent width='100%' height='550px' selectedDate={new Date(2017, 11, 15)} cellTemplate={this.cellTemplate.bind(this)}>
      <ViewsDirective>
        <ViewDirective option='Day' />
        <ViewDirective option='Week' />
        <ViewDirective option='TimelineWeek' />
        <ViewDirective option='Month' />
      </ViewsDirective>
      <Inject services={[Day, Week, TimelineViews,Month]} />
    </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));

```

{% endtab %}

### Using renderCell event

An alternative to `cellTemplate` is the `renderCell` event, which can also be used to customize the cells with appropriate images or formatted text values.

{% tab template="schedule/cell-dimension", iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, Month, Inject,
  RenderCellEventArgs,  ViewsDirective, ViewDirective
} from '@syncfusion/ej2-react-schedule';
import { extend, createElement } from '@syncfusion/ej2-base';
import { scheduleData } from './datasource';

class App extends React.Component<{}, {}>{
  private data: Object[] = extend([], scheduleData, null, true) as Object[];
  private onRenderCell(args: RenderCellEventArgs): void {
    if (args.elementType == 'workCells' || args.elementType == 'monthCells') {
      let weekEnds: number[] = [0, 6];
      if (weekEnds.indexOf((args.date).getDay()) >= 0) {
          let ele: HtmlElement = createElement('div', {
              innerHTML: "<img src='https://ej2.syncfusion.com/demos/src/schedule/images/newyear.svg' />",
              className: 'templatewrap'
          });
          (args.element).appendChild(ele);
      }
    }
  }
  render() {
    return <ScheduleComponent height='550px' currentView='Month' selectedDate={new Date(2018, 1, 15)} eventSettings={ { dataSource: this.data } } renderCell={this.onRenderCell.bind(this)}
    cssClass= 'schedule-cell-template'>
        <ViewsDirective>
          <ViewDirective option='Week' />
          <ViewDirective option='WorkWeek' />
          <ViewDirective option='Month' />
        </ViewsDirective>
        <Inject services={[Day, Week, Month]} />
      </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

You can customize cells such as work cells, month cells, all-day cells, header cells, resource header cells using `renderCell` event by checking the `elementType` option within the event. You can check elementType with any of the following.

| Element type | Description |
|-------|---------|
| dateHeader | triggers on header cell rendering.|
| monthDay | triggers on header cell in month view rendering.|
| resourceHeader | triggers on resource header cell rendering.|
| alldayCells | triggers on all day cell rendering.|
| emptyCells | triggers on empty cell rendering on header bar.|
| resourceGroupCells | triggers on rendering of work cells for parent resource.|
| workCells | triggers on work cell rendering.|
| monthCells | triggers on month cell rendering.|
| majorSlot | triggers on major time slot cell rendering.|
| minorSlot | triggers on minor time slot cell rendering.|
| weekNumberCell | triggers on cell displaying week number.|

## Customizing cell header in month view

The month header of each date cell in the month view can be customized using the `cellHeaderTemplate` option which accepts the string or HTMLElement. The corresponding date can be accessed with the template.

{% tab template="schedule/cell-dimension", iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Month, Inject, ViewsDirective,
  ViewDirective
} from "@syncfusion/ej2-react-schedule";
import { Internationalization } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
  private instance = new Internationalization();
  private getDateHeaderText(props): JSX.Element {
    return (<div>{this.instance.formatDate(props.date, { skeleton: "Ed" })}</div>);
  }
  render() {
    return <ScheduleComponent height='550px' cellHeaderTemplate={this.getDateHeaderText.bind(this)}>
        <ViewsDirective>
          <ViewDirective option='Month' />
        </ViewsDirective>
        <Inject services={[Month]} />
      </ScheduleComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

## Customizing the minimum and maximum date values

Providing the `minDate` and `maxDate` property with some date values, allows the Scheduler to set the minimum and maximum date range. The Scheduler date that lies beyond this minimum and maximum date range will be in a disabled state so that the date navigation will be blocked beyond the specified date range.

{% tab template="schedule/cell-dimension", iframeHeight="588px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  ScheduleComponent, Day, Week, WorkWeek, Agenda, Month, Inject,
  ViewsDirective, ViewDirective
} from '@syncfusion/ej2-react-schedule';
import { extend } from '@syncfusion/ej2-base';
import { scheduleData } from './datasource';

class App extends React.Component<{}, {}> {
  private data: Object[] = extend([], scheduleData, null, true) as Object[];
  render() {
    return <ScheduleComponent width='100%' height='550px' currentView='Month'
    selectedDate={new Date(2018, 1, 17)} minDate={new Date(2017, 4, 17)}
    maxDate={new Date(2018, 5, 17)} eventSettings={ { dataSource: this.data } }>
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

>By default, the `minDate` property value is set to new Date(1900, 0, 1) and `maxDate` property value is set to new Date(2099, 11, 31). The user can also set the customized `minDate` and `maxDate` property values.

## How to disable multiple cell and row selection in Schedule

By default, the `allowMultiCellSelection` and `allowMultiRowSelection` properties of the Schedule are set to `true`. So, the Schedule allows user to select multiple cells and rows. If the user want to disable this multiple cell and row selection. The user can disable this feature by setting up `false` to these properties.

> You can refer to our [React Scheduler](https://www.syncfusion.com/react-ui-components/react-scheduler) feature tour page for its groundbreaking feature representations. You can also explore our [React Scheduler example](https://ej2.syncfusion.com/react/demos/#/material/schedule/overview) to knows how to present and manipulate data.
