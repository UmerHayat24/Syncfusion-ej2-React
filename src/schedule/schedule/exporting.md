---
title: "Exporting"
component: "Schedule"
description: "Learn how to export Scheduler events to an excel file."
---

# Exporting

The Scheduler supports exporting all its appointments both to an Excel or ICS extension file at client-side. It offers different client-side methods to export its appointments in an Excel or ICal format file. Let's look onto the ways on how to implement the exporting functionality in Scheduler.

## Excel Exporting

The Scheduler allows you to export all its events into an Excel format file by using the [`exportToExcel`] client-side method. By default, it exports all the default fields of Scheduler mapped through `eventSettings` property.

> Before you start with excel exporting functionality, you need to import and inject the `ExcelExport` module from the '@syncfusion/ej2-schedule' package using the `Inject` method of Scheduler.

{% tab template="schedule/excel-export", iframeHeight="588px", compileJsx=true %}

```tsx
import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { extend } from '@syncfusion/ej2-base';
import { ItemModel } from '@syncfusion/ej2-react-navigations';
import {
  ScheduleComponent, ViewDirective, Week, Resize, ExcelExport, ExportOptions,
  ActionEventArgs, ToolbarActionArgs, DragAndDrop, Inject, ViewsDirective
} from '@syncfusion/ej2-react-schedule';
import { scheduleData } from './datasource';

/**
 *  Schedule header customization sample
 */

class App extends React.Component<{}, {}>{
  public scheduleObj: ScheduleComponent;
  private data: Object[] = extend([], scheduleData, null, true) as Object[];

  private onActionBegin(args: ActionEventArgs & ToolbarActionArgs): void {
    if (args.requestType === 'toolbarItemRendering') {
      let exportItem: ItemModel = {
        align: 'Right', showTextOn: 'Both', prefixIcon: 'e-icon-schedule-excel-export',
        text: 'Excel Export', cssClass: 'e-excel-export', click: this.onExportClick.bind(this)
      };
      args.items.push(exportItem);
    }
  }

  private onExportClick(): void {
    this.scheduleObj.exportToExcel();
  }

  render() {
    return (
            <ScheduleComponent cssClass='excel-export' width='100%' height='550px' id='schedule' ref={t => this.scheduleObj = t}
              selectedDate={new Date(2019, 0, 10)} eventSettings={{ dataSource: this.data }}
              actionBegin={this.onActionBegin.bind(this)}>
              <ViewsDirective>
                <ViewDirective option='Week' />
              </ViewsDirective>
              <Inject services={[Week, Resize, DragAndDrop, ExcelExport]} />
            </ScheduleComponent>
    );
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

### Exporting with custom fields

By default, Scheduler exports all the default event fields that are mapped to it through the `eventSettings` property. To limit the number of fields on the exported excel file, it provides an option to export only the custom fields of the event data. To export such custom fields alone, define the required `fields` through the `ExportOptions` interface and pass it as argument to the `exportToExcel` method as shown in the following example. For example: `['Id', 'Subject', 'StartTime', 'EndTime', 'Location']`.

{% tab template="schedule/excel-export", iframeHeight="588px", compileJsx=true %}

```tsx
import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { extend } from '@syncfusion/ej2-base';
import { ItemModel } from '@syncfusion/ej2-react-navigations';
import {
  ScheduleComponent, ViewDirective, Week, Resize, ExcelExport, ExportOptions,
  ActionEventArgs, ToolbarActionArgs, DragAndDrop, Inject, ViewsDirective
} from '@syncfusion/ej2-react-schedule';
import { scheduleData } from './datasource';

/**
 *  Schedule header customization sample
 */

class App extends React.Component<{}, {}>{
  public scheduleObj: ScheduleComponent;
  private data: Object[] = extend([], scheduleData, null, true) as Object[];

  private onActionBegin(args: ActionEventArgs & ToolbarActionArgs): void {
    if (args.requestType === 'toolbarItemRendering') {
      let exportItem: ItemModel = {
        align: 'Right', showTextOn: 'Both', prefixIcon: 'e-icon-schedule-excel-export',
        text: 'Excel Export', cssClass: 'e-excel-export', click: this.onExportClick.bind(this)
      };
      args.items.push(exportItem);
    }
  }

  private onExportClick(): void {
    let exportValues: ExportOptions = {
      fields: ['Id', 'Subject', 'StartTime', 'EndTime', 'Location']
    };
    this.scheduleObj.exportToExcel(exportValues);
  }

  render() {
    return (
            <ScheduleComponent cssClass='excel-export' width='100%' height='550px' id='schedule' ref={t => this.scheduleObj = t}
              selectedDate={new Date(2019, 0, 10)} eventSettings={{ dataSource: this.data }}
              actionBegin={this.onActionBegin.bind(this)}>
              <ViewsDirective>
                <ViewDirective option='Week' />
              </ViewsDirective>
              <Inject services={[Week, Resize, DragAndDrop, ExcelExport]} />
            </ScheduleComponent>
    );
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

### Exporting individual occurrences of a recurring series

By default, the Scheduler exports recurring events as a single data by exporting only its parent record into the excel file. If you want to export each individual occurrences of a recurring series appointment as separate records in an Excel file, define the `includeOccurrences` option as `true` through the `ExportOptions` interface and pass it as argument to the `exportToExcel` method. By default, the `includeOccurrences` option is set to `false`.

{% tab template="schedule/excel-export", iframeHeight="588px", compileJsx=true %}

```tsx
import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { extend } from '@syncfusion/ej2-base';
import { ItemModel } from '@syncfusion/ej2-react-navigations';
import {
  ScheduleComponent, ViewDirective, Week, Resize, ExcelExport, ExportOptions,
  ActionEventArgs, ToolbarActionArgs, DragAndDrop, Inject, ViewsDirective
} from '@syncfusion/ej2-react-schedule';
import { scheduleData } from './datasource';

/**
 *  Schedule header customization sample
 */

class App extends React.Component<{}, {}>{
  public scheduleObj: ScheduleComponent;
  private data: Object[] = extend([], scheduleData, null, true) as Object[];

  private onActionBegin(args: ActionEventArgs & ToolbarActionArgs): void {
    if (args.requestType === 'toolbarItemRendering') {
      let exportItem: ItemModel = {
        align: 'Right', showTextOn: 'Both', prefixIcon: 'e-icon-schedule-excel-export',
        text: 'Excel Export', cssClass: 'e-excel-export', click: this.onExportClick.bind(this)
      };
      args.items.push(exportItem);
    }
  }

  private onExportClick(): void {
    let exportValues: ExportOptions = { includeOccurrences: true };
    this.scheduleObj.exportToExcel(exportValues);
  }

  render() {
    return (
            <ScheduleComponent cssClass='excel-export' width='100%' height='550px' id='schedule' ref={t => this.scheduleObj = t}
              selectedDate={new Date(2019, 0, 10)} eventSettings={{ dataSource: this.data }}
              actionBegin={this.onActionBegin.bind(this)}>
              <ViewsDirective>
                <ViewDirective option='Week' />
              </ViewsDirective>
              <Inject services={[Week, Resize, DragAndDrop, ExcelExport]} />
            </ScheduleComponent>
    );
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

### Exporting custom event data

By default, the whole event collection bound to the Scheduler gets exported as an excel file. To export only specific events of Scheduler or some custom event collection, you need to pass those custom data collection as a parameter to the `exportToExcel` method as shown in this following example, through the `customData` option of `ExportOptions` interface.

> By default, the event data are taken from Scheduler dataSource.

{% tab template="schedule/excel-export", iframeHeight="588px", compileJsx=true %}

```tsx
import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { extend } from '@syncfusion/ej2-base';
import { ItemModel } from '@syncfusion/ej2-react-navigations';
import {
  ScheduleComponent, ViewDirective, Week, Resize, ExcelExport, ExportOptions,
  ActionEventArgs, ToolbarActionArgs, DragAndDrop, Inject, ViewsDirective
} from '@syncfusion/ej2-react-schedule';
import { scheduleData } from './datasource';

/**
 *  Schedule header customization sample
 */

class App extends React.Component<{}, {}>{
  public scheduleObj: ScheduleComponent;
  private data: Object[] = extend([], scheduleData, null, true) as Object[];

  private onActionBegin(args: ActionEventArgs & ToolbarActionArgs): void {
    if (args.requestType === 'toolbarItemRendering') {
      let exportItem: ItemModel = {
        align: 'Right', showTextOn: 'Both', prefixIcon: 'e-icon-schedule-excel-export',
        text: 'Excel Export', cssClass: 'e-excel-export', click: this.onExportClick.bind(this)
      };
      args.items.push(exportItem);
    }
  }

  private onExportClick(): void {
    let exportValues: ExportOptions = {
        customData: [{
            Id: 1,
            Subject: 'Explosion of Betelgeuse Star',
            Location: 'Space Centre USA',
            StartTime: new Date(2019, 0, 6, 9, 30),
            EndTime: new Date(2019, 0, 6, 11, 0),
            CategoryColor: '#1aaa55'
        }, {
            Id: 2,
            Subject: 'Thule Air Crash Report',
            Location: 'Newyork City',
            StartTime: new Date(2019, 0, 7, 12, 0),
            EndTime: new Date(2019, 0, 7, 14, 0),
            CategoryColor: '#357cd2'
        }]
     };
    this.scheduleObj.exportToExcel(exportValues);
  }

  render() {
    return (
            <ScheduleComponent cssClass='excel-export' width='100%' height='550px' id='schedule' ref={t => this.scheduleObj = t}
              selectedDate={new Date(2019, 0, 10)} eventSettings={{ dataSource: this.data }}
              actionBegin={this.onActionBegin.bind(this)}>
              <ViewsDirective>
                <ViewDirective option='Week' />
              </ViewsDirective>
              <Inject services={[Week, Resize, DragAndDrop, ExcelExport]} />
            </ScheduleComponent>
    );
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

### Export with custom file name

By default, the Scheduler allows you to download the exported Excel file with a name `Schedule.xlsx`. It also provides an option to export the excel file with a custom file name, by defining the desired `fileName` through the `ExportOptions` interface and passing it as an argument to the `exportToExcel` method.

{% tab template="schedule/excel-export", iframeHeight="588px", compileJsx=true %}

```tsx
import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { extend } from '@syncfusion/ej2-base';
import { ItemModel } from '@syncfusion/ej2-react-navigations';
import {
  ScheduleComponent, ViewDirective, Week, Resize, ExcelExport, ExportOptions,
  ActionEventArgs, ToolbarActionArgs, DragAndDrop, Inject, ViewsDirective
} from '@syncfusion/ej2-react-schedule';
import { scheduleData } from './datasource';

/**
 *  Schedule header customization sample
 */

class App extends React.Component<{}, {}>{
  public scheduleObj: ScheduleComponent;
  private data: Object[] = extend([], scheduleData, null, true) as Object[];

  private onActionBegin(args: ActionEventArgs & ToolbarActionArgs): void {
    if (args.requestType === 'toolbarItemRendering') {
      let exportItem: ItemModel = {
        align: 'Right', showTextOn: 'Both', prefixIcon: 'e-icon-schedule-excel-export',
        text: 'Excel Export', cssClass: 'e-excel-export', click: this.onExportClick.bind(this)
      };
      args.items.push(exportItem);
    }
  }

  private onExportClick(): void {
    let exportValues: ExportOptions = { fileName: "SchedulerData" };
    this.scheduleObj.exportToExcel(exportValues);
  }

  render() {
    return (
            <ScheduleComponent cssClass='excel-export' width='100%' height='550px' id='schedule' ref={t => this.scheduleObj = t}
              selectedDate={new Date(2019, 0, 10)} eventSettings={{ dataSource: this.data }}
              actionBegin={this.onActionBegin.bind(this)}>
              <ViewsDirective>
                <ViewDirective option='Week' />
              </ViewsDirective>
              <Inject services={[Week, Resize, DragAndDrop, ExcelExport]} />
            </ScheduleComponent>
    );
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

### Excel file formats

By default, the Scheduler exports event data to an excel file in the `.xlsx` format. You can also export the Scheduler data in either of the file type such as `.xlsx` or `csv` formats, by defining the `exportType` option as either `csv` or `xlsx` through the `ExportOptions` interface. By default, the `exportType` is set to `xlsx`.

{% tab template="schedule/excel-export", iframeHeight="588px", compileJsx=true %}

```tsx
import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { extend } from '@syncfusion/ej2-base';
import { ItemModel } from '@syncfusion/ej2-react-navigations';
import {
  ScheduleComponent, ViewDirective, Week, Resize, ExcelExport, ExportOptions,
  ActionEventArgs, ToolbarActionArgs, DragAndDrop, Inject, ViewsDirective
} from '@syncfusion/ej2-react-schedule';
import { scheduleData } from './datasource';

/**
 *  Schedule header customization sample
 */

class App extends React.Component<{}, {}>{
  public scheduleObj: ScheduleComponent;
  private data: Object[] = extend([], scheduleData, null, true) as Object[];

  private onActionBegin(args: ActionEventArgs & ToolbarActionArgs): void {
    if (args.requestType === 'toolbarItemRendering') {
      let exportItem: ItemModel = {
        align: 'Right', showTextOn: 'Both', prefixIcon: 'e-icon-schedule-excel-export',
        text: 'Excel Export', cssClass: 'e-excel-export', click: this.onExportClick.bind(this)
      };
      args.items.push(exportItem);
    }
  }

  private onExportClick(): void {
    let exportValues: ExportOptions = { exportType: "csv" };
    this.scheduleObj.exportToExcel(exportValues);
  }

  render() {
    return (
            <ScheduleComponent cssClass='excel-export' width='100%' height='550px' id='schedule' ref={t => this.scheduleObj = t}
              selectedDate={new Date(2019, 0, 10)} eventSettings={{ dataSource: this.data }}
              actionBegin={this.onActionBegin.bind(this)}>
              <ViewsDirective>
                <ViewDirective option='Week' />
              </ViewsDirective>
              <Inject services={[Week, Resize, DragAndDrop, ExcelExport]} />
            </ScheduleComponent>
    );
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

## Exporting calendar events as ICS file

You can export the Scheduler events to a calendar (.ics) file format, and open it on any of the other default calendars such as Google or Outlook. To export the events of Scheduler to an ICS file, you need to first import the `ICalendarExport` module from `@syncfusion/ej2-schedule` package and then inject it using the `Schedule.Inject(ICalendarExport)` method.

The following code example shows how the Scheduler events are exported to a calendar (.ics) file by making use of the `exportToICalendar` public method.

{% tab template="schedule/calendar-export", iframeHeight="588px", compileJsx=true %}

```tsx
import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { extend } from '@syncfusion/ej2-base';
import {
  ScheduleComponent, Day, Week, WorkWeek, Month, Agenda, DragAndDrop, ICalendarExport, ICalendarImport, Resize, Inject
} from '@syncfusion/ej2-react-schedule';
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { scheduleData } from './datasource';

/**
 *  Schedule header customization sample
 */

class App extends React.Component<{}, {}>{
  public scheduleObj: ScheduleComponent;
  private data: Object[] = extend([], scheduleData, null, true) as Object[];

  private onClick(): void {
    this.scheduleObj.exportToICalendar();
  }

  render() {
    return ( <div>
            <ButtonComponent id='ics-export' title='Export' onClick={this.onClick.bind(this)}>Export</ButtonComponent>
            <ScheduleComponent ref={schedule => this.scheduleObj = schedule} width='100%' height='520px' id='schedule' selectedDate= {new Date(2018, 1, 15)} eventSettings={ { dataSource: this.data } }>
            <Inject services={[Day, Week, WorkWeek, Month, Agenda, DragAndDrop, ICalendarExport, ICalendarImport, Resize, DragAndDrop]} />
              </ScheduleComponent></div>
          );
      }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

### Exporting calendar with custom file name

By default, the calendar is exported with a file name `Calendar.ics`. To change this file name on export, pass the custom string value as `fileName` to the method argument so as to get the file downloaded with this provided name.

The following example downloads the iCal file with a name `ScheduleEvents.ics`.

{% tab template="schedule/calendar-export", iframeHeight="588px", compileJsx=true %}

```tsx
import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { extend } from '@syncfusion/ej2-base';
import {
  ScheduleComponent, Day, Week, WorkWeek, Month, Agenda, DragAndDrop, ICalendarExport, ICalendarImport, Resize, Inject
} from '@syncfusion/ej2-react-schedule';
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { scheduleData } from './datasource';

/**
 *  Schedule header customization sample
 */

class App extends React.Component<{}, {}>{
  public scheduleObj: ScheduleComponent;
  private data: Object[] = extend([], scheduleData, null, true) as Object[];

  private onClick(): void {
    this.scheduleObj.exportToICalendar('ScheduleEvents');
  }

  render() {
    return ( <div>
            <ButtonComponent id='ics-export' title='Export' onClick={this.onClick.bind(this)}>Export</ButtonComponent>
            <ScheduleComponent ref={schedule => this.scheduleObj = schedule} width='100%' height='520px' id='schedule' selectedDate= {new Date(2018, 1, 15)} eventSettings={ { dataSource: this.data } }>
            <Inject services={[Day, Week, WorkWeek, Month, Agenda, DragAndDrop, ICalendarExport, ICalendarImport, Resize, DragAndDrop]} />
              </ScheduleComponent></div>
          );
      }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

## Import events from other calendars

The events from external calendars (ICS files) can be imported into Scheduler by using the `importICalendar` method. This method accepts the `blob object` of an .ics file to be imported, as a mandatory argument.

> To import an ICS file containing events into Scheduler, you need to first import the `ICalendarImport` module from `@syncfusion/ej2-schedule` package and then inject it using the `Schedule.Inject(ICalendarImport)` method.

The following example shows how to import an ICS file into Scheduler, using the `importICalendar` method.

{% tab template="schedule/calendar-import", iframeHeight="588px", compileJsx=true %}

```tsx
import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { ScheduleComponent, Day, Week, WorkWeek, Month, Agenda, DragAndDrop, Resize, Inject, ICalendarExport, ICalendarImport
} from '@syncfusion/ej2-react-schedule';
import { scheduleData } from './datasource';
import { extend } from '@syncfusion/ej2-base';
import { UploaderComponent } from '@syncfusion/ej2-react-inputs';

class App extends React.Component<{}, {}>{
    public scheduleObj: ScheduleComponent;
    private multiple: boolean = false;
    private showFileList: boolean = false;
    private allowedExtensions: string = '.ics';
    private data: Object[] = extend([], scheduleData, null, true) as Object[];

    private onSelect(args): void {
    this.scheduleObj.importICalendar(args.event.target.files[0]);
    }

    render() {
    return (<div>
    <UploaderComponent id='fileUpload' type='file' allowedExtensions={this.allowedExtensions} cssClass='calendar-import'
    buttons={{ browse: 'Choose file' }} multiple={this.multiple} showFileList={this.showFileList}
    selected={this.onSelect.bind(this)}></UploaderComponent>
    <ScheduleComponent ref={schedule => this.scheduleObj = schedule} width='100%' height='520px' selectedDate= {new Date(2018, 1, 15)} allowDragAndDrop= {false} eventSettings={ { dataSource: this.data } }>
    <Inject services={[Day, Week, WorkWeek, Month, Agenda, DragAndDrop, ICalendarExport, ICalendarImport, Resize, DragAndDrop]} />
    </ScheduleComponent></div>
    );
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

## How to print the Scheduler element

The Scheduler allows you to print the Scheduler element by using the `print` client-side method. The print method works in two ways. You can find it below.

* Using print method without options.
* Using a print method with options.

> To print the Schedule, you need to import the `Print` module from the `@syncfusion/ej2-react-schedule` package and then inject it using `<Inject services={[Print]} />`.

### Using print method without options

You can print the Schedule element with the current view by using the `print` method without passing the options. The following example shows how to print the Scheduler using the `print` method without passing options.

{% tab template="schedule/print", iframeHeight="588px", compileJsx=true %}

```tsx
import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { ScheduleComponent, Day, Week, WorkWeek, Month, Agenda, Print, Inject } from '@syncfusion/ej2-react-schedule';
import { scheduleData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
  public scheduleObj: ScheduleComponent;
  private data: Object[] = extend([], scheduleData, null, true) as Object[];

  private onActionBegin(args: ActionEventArgs & ToolbarActionArgs): void {
    if (args.requestType === 'toolbarItemRendering') {
      let exportItem: ItemModel = {
        align: 'Right', showTextOn: 'Both', prefixIcon: 'e-icon-schedule-print',
        text: 'Print', cssClass: 'e-schedule-print', click: this.onPrintIconClick.bind(this)
      };
      args.items.push(exportItem);
    }
  }

  private onPrintIconClick(): void {
    this.scheduleObj.print();
  }

    render() {
    return (<div>
    <ScheduleComponent ref={schedule => this.scheduleObj = schedule} width='100%' height='520px' selectedDate={new Date(2018, 1, 15)} eventSettings={ { dataSource: this.data } } actionBegin={this.onActionBegin.bind(this)}>
    <Inject services={[Day, Week, WorkWeek, Month, Agenda, Print]} />
    </ScheduleComponent></div>
    );
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

### Using a print method with options

You can print the Schedule element based on your needs using the `print` method by passing the print options used in this example with its values. The following example shows how to print the Scheduler using the `print` method by passing the options.

{% tab template="schedule/print", iframeHeight="588px", compileJsx=true %}

```tsx
import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { ScheduleComponent, Day, Week, WorkWeek, Month, Agenda, Print, Inject, ScheduleModel } from '@syncfusion/ej2-react-schedule';
import { scheduleData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}>{
  public scheduleObj: ScheduleComponent;
  private data: Object[] = extend([], scheduleData, null, true) as Object[];

  private onActionBegin(args: ActionEventArgs & ToolbarActionArgs): void {
    if (args.requestType === 'toolbarItemRendering') {
      let exportItem: ItemModel = {
        align: 'Right', showTextOn: 'Both', prefixIcon: 'e-icon-schedule-print',
        text: 'Print', cssClass: 'e-schedule-print', click: this.onPrintIconClick.bind(this)
      };
      args.items.push(exportItem);
    }
  }

  private onPrintIconClick(): void {
    let printModel: ScheduleModel = {
      agendaDaysCount: 14,
      cssClass: 'e-print-schedule',
      currentView: this.scheduleObj.currentView,
      dateFormat: 'dd-MMM-yyyy',
      enableRtl: false,
      endHour: '18:00',
      firstDayOfWeek: 1,
      firstMonthOfYear: 0,
      group: {},
      height: 'auto',
      locale: this.scheduleObj.locale,
      maxDate: this.scheduleObj.selectedDate,
      minDate: this.scheduleObj.getCurrentViewDates()[0],
      readonly: true,
      resources: [],
      rowAutoHeight: false,
      selectedDate: new Date(),
      showHeaderBar: false,
      showTimeIndicator: false,
      showWeekNumber: false,
      showWeekend: false,
      startHour: '06:00',
      timeFormat: 'HH',
      timeScale: { enable: true },
      width: 'auto',
      workDays: [1, 2, 3, 4, 5],
      workHours: { highlight: true, start: '10:00', end: '20:00' }
    };
    this.scheduleObj.print(printModel);
  }

    render() {
    return (<div>
    <ScheduleComponent ref={schedule => this.scheduleObj = schedule} width='100%' height='520px' selectedDate={new Date(2018, 1, 15)} eventSettings={ { dataSource: this.data } } actionBegin={this.onActionBegin.bind(this)}>
    <Inject services={[Day, Week, WorkWeek, Month, Agenda, Print]} />
    </ScheduleComponent></div>
    );
  }
};
ReactDOM.render(<App />, document.getElementById('schedule'));
```

{% endtab %}

> You can refer to our [React Scheduler](https://www.syncfusion.com/react-ui-components/react-scheduler) feature tour page for its groundbreaking feature representations. You can also explore our [React Scheduler example](https://ej2.syncfusion.com/react/demos/#/material/schedule/overview) to knows how to present and manipulate data.
