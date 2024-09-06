---
title: "Columns"
component: "Gantt"
description: "Documentation on column reordering, resizing, header templates (custom header content), and column templates (custom cell content) in the Essential JS 2 Gantt Component."
---

# Columns

The column displays information from a bound data source, and you can edit the values of column to update the task details through TreeGrid. The operations such as sorting, filtering, and searching can be performed based on column definitions. To display a Gantt column, the [`field`](../api/gantt/column/#field) property should be mapped from the data source to the column.

> If the column [`field`](../api/gantt/column/#field) is not specified in the data source, the column values will be empty.

The [`treeColumnIndex`](../api/gantt/#treecolumnindex) property is used to define the expander column in the Gantt component to expand and collapse the child rows.

## Defining columns

Using the [`columns`](../api/gantt/#columns) property, you can define the columns in Gantt. If the columns are not defined, then the default columns will be rendered based on the mapped data source fields in the [`taskFields`](../api/gantt/taskFields/) property. Refer to the following code example for defining the columns in Gantt along with their widths.

{% tab template="gantt/headertemplate", compileJsx=true %}

```typescript
let data: Object[]  = [
  {
      TaskID: 1,
      TaskName: 'Project Initiation',
      StartDate: new Date('04/02/2019'),
      EndDate: new Date('04/21/2019'),
      subtasks: [
          { TaskID: 2, TaskName: 'Identify Site location', StartDate: new Date('04/02/2019'), Duration: 4, Progress: 50 },
          { TaskID: 3, TaskName: 'Perform Soil test', StartDate: new Date('04/02/2019'), Duration: 4, Progress: 50  },
          { TaskID: 4, TaskName: 'Soil test approval', StartDate: new Date('04/02/2019'), Duration: 4, Progress: 50 },
      ]
  },
  {
      TaskID: 5,
      TaskName: 'Project Estimation',
      StartDate: new Date('04/02/2019'),
      EndDate: new Date('04/21/2019'),
      subtasks: [
          { TaskID: 6, TaskName: 'Develop floor plan for estimation', StartDate: new Date('04/04/2019'), Duration: 3, Progress: 50 },
          { TaskID: 7, TaskName: 'List materials', StartDate: new Date('04/04/2019'), Duration: 3, Progress: 50 },
          { TaskID: 8, TaskName: 'Estimation approval', StartDate: new Date('04/04/2019'), Duration: 3, Progress: 50 }
      ]
  },
];

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { GanttComponent,ColumnsDirective,ColumnDirective } from '@syncfusion/ej2-react-gantt';

class App extends React.Component<{}, {}>{
    public taskFields: any = {
    id: 'TaskID',
    name: 'TaskName',
    startDate: 'StartDate',
    duration: 'Duration',
    progress: 'Progress',
    child: 'subtasks'
  };
    render() {
        return <GanttComponent dataSource={data} taskFields={this.taskFields} height = '450px'>
         <ColumnsDirective>
                <ColumnDirective field='TaskID' width='150' ></ColumnDirective>
                <ColumnDirective field='TaskName' width='250'></ColumnDirective>
          </ColumnsDirective>
      </GanttComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('root'));
```

{% endtab %}

## Custom column header

The column header text can be defined using the [`headerText`](../api/gantt/column/#headertext) property, and you can customize the column headers using the [`headerTemplate`](../api/gantt/column/#headertemplate) property.

{% tab template="gantt/headertemplate", compileJsx=true %}

```typescript
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { GanttComponent, ColumnsDirective, ColumnDirective } from '@syncfusion/ej2-react-gantt';
import { data } from './datasource';
class App extends React.Component<{}, {}>{
    public taskFields: any = {
    id: 'TaskID',
    name: 'TaskName',
    startDate: 'StartDate',
    duration: 'Duration',
    progress: 'Progress',
    child: 'subtasks'
 };
  public splitterSettings: any = {
      columnIndex: 7
  };
    render() {
        return <GanttComponent dataSource={data} taskFields={this.taskFields}
        splitterSettings={this.splitterSettings} height = '450px'>
            <ColumnsDirective>
                <ColumnDirective field='TaskName' headerText='Job Name' headerTemplate={() => {
                  return (<div><img src="taskname.png" width="20" height="20" className="e-image" />
                    <b className='e-header'>Task Name</b></div>);
                }}></ColumnDirective>
                <ColumnDirective field='StartDate' headerTemplate={() => {
                  return (<div><img src="startdate.png" width="20" height="20" className="e-image" />
                    <b className='e-header'>Start Date</b></div>);
                }}></ColumnDirective>
                <ColumnDirective field='Duration' headerTemplate={() => {
                  return (<div><img src="duration.png" width="20" height="20" className="e-image" />
                    <b className='e-header'>Duration</b></div>);
                }}></ColumnDirective>
                <ColumnDirective field='Progress' headerTemplate={() => {
                  return (<div><img src="progress.png" width="20" height="20" className="e-image" />
                    <b className='e-header'>Progress</b></div>);
                }}></ColumnDirective>
            </ColumnsDirective>
        </GanttComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('root'));
```

{% endtab %}

## Format

To format the cell values based on a specific culture, use the [`columns.format`](../api/gantt/column/#format) property. The Gantt component uses the [`Internationalization`](../../common/internationalization/) library to format [`number`](../../common/internationalization/#number-formatting) and [`date`](../../common/internationalization/#manipulating-datetime) values.

{% tab template="gantt/format", compileJsx=true %}

```typescript
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { GanttComponent, ColumnsDirective, ColumnDirective } from '@syncfusion/ej2-react-gantt';
import { data } from './datasource';
class App extends React.Component<{}, {}>{
    public taskFields: any = {
    id: 'TaskID',
    name: 'TaskName',
    startDate: 'StartDate',
    duration: 'Duration',
    progress: 'Progress',
    child: 'subtasks'
  };
  public splitterSettings: any = {
      columnIndex : 4
  };
    render() {
        return <GanttComponent dataSource={data} taskFields={this.taskFields}
        splitterSettings={this.splitterSettings} height = '450px'>
            <ColumnsDirective>
                <ColumnDirective field='TaskID' width='100' ></ColumnDirective>
                <ColumnDirective field='TaskName' headerText='Job Name' width='250'></ColumnDirective>
                <ColumnDirective field='StartDate'></ColumnDirective>
                <ColumnDirective field='Progress' format='P2'></ColumnDirective>
                <ColumnDirective field='Duration'></ColumnDirective>
                <ColumnDirective field='Predecessor'></ColumnDirective>
            </ColumnsDirective>
        </GanttComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('root'));
```

{% endtab %}

> By default, the number and date values are formatted in `en-US` culture.

### Number formatting

The number or integer values can be formatted using the following format strings.

Format |Description |Remarks
-----|-----
N | Denotes numeric type. | The numeric format is followed by an integer value like N2 or N3, which denotes the number of precisions to be allowed.
C | Denotes currency type. | The currency format is followed by an integer value like C2 or C3, which denotes the number of precisions to be allowed.
P | Denotes percentage type | The percentage format expects the input value to be in the range of 0 to 100. For example, the cell value `0.2` is formatted as `20%`. The percentage format is followed by an integer value like P2, P3, which denotes the number of precisions to be allowed.

### Date formatting

You can format date values either using the built-in date format string or a custom format string.

For the built-in date format, you can specify the [`columns.format`](../api/gantt/column/#format) property as string (example: `yMd`).

You can also use the custom format string to format the date values. Some of the custom formats and the formatted date values are given in the following table.

Format | Formatted value
-----|-----
{ type:'date', format:'dd/MM/yyyy' } | 04/07/2019
{ type:'date', format:'dd.MM.yyyy' } | 04.07.2019
{ type:'date', skeleton:'short' } | 7/4/19
{ type: 'dateTime', format: 'dd/MM/yyyy hh:mm a' } | 04/07/2019 12:00 AM
{ type: 'dateTime', format: 'MM/dd/yyyy hh:mm:ss a' } | 07/04/2019 12:00:00 AM

{% tab template="gantt/format", compileJsx=true %}

```typescript
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { GanttComponent, ColumnsDirective, ColumnDirective } from '@syncfusion/ej2-react-gantt';
import { data } from './datasource';
class App extends React.Component<{}, {}>{
    public taskFields: any = {
    id: 'TaskID',
    name: 'TaskName',
    startDate: 'StartDate',
    duration: 'Duration',
    progress: 'Progress',
    child: 'subtasks'
  };
  public splitterSettings: any = {
      columnIndex : 4
  };
  public formatOption: Object = {type:'date', format:'dd.MM.yyyy'};
    render() {
        return <GanttComponent dataSource={data} taskFields={this.taskFields}
        splitterSettings={this.splitterSettings} height = '450px'>
            <ColumnsDirective>
                <ColumnDirective field='TaskID' width='100' ></ColumnDirective>
                <ColumnDirective field='TaskName' headerText='Job Name' width='250'></ColumnDirective>
                <ColumnDirective field='StartDate' format={this.formatOption}></ColumnDirective>
                <ColumnDirective field='Duration'></ColumnDirective>
                <ColumnDirective field='Progress'></ColumnDirective>
            </ColumnsDirective>
        </GanttComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('root'));
```

{% endtab %}

## Column reordering

The column reordering can be done by dragging a column header from one index to another index within the TreeGrid. To enable reordering, set the [`allowReordering`](../api/gantt/#allowreordering) property to true.

To use the column reordering feature, inject the `Reorder` module to the Gantt component.

{% tab template="gantt/columnreorder", compileJsx=true %}

```typescript
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { GanttComponent, Inject, Reorder } from '@syncfusion/ej2-react-gantt';
import { data } from './datasource';
class App extends React.Component<{}, {}>{
    public taskFields: any = {
    id: 'TaskID',
    name: 'TaskName',
    startDate: 'StartDate',
    duration: 'Duration',
    progress: 'Progress',
    child: 'subtasks'
  };
  public splitterSettings: any = {
    columnIndex : 5
};
    render() {
        return <GanttComponent dataSource={data} taskFields={this.taskFields} splitterSettings={this.splitterSettings}
        allowReordering={true} height = '450px'>
           <Inject services={[Reorder]} />
        </GanttComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('root'));
```

{% endtab %}

> You can disable the reordering of a particular column by setting the [`columns.allowReordering`](../api/gantt/column/#allowreordering) property to `false`.

## Reorder Events

During the reorder action, the gantt component triggers the below three events.

1. The [`columnDragStart`](../api/gantt/#columndragstart) event triggers when column header element drag (move) starts.
2. The [`columnDrag`](../api/gantt/#columndrag) event triggers when column header element is dragged (moved) continuously.
3. The [`columnDrop`](../api/gantt/#columndrop) event triggers when a column header element is dropped on the target column.

{% tab template="gantt/reorder-events", compileJsx=true %}

```typescript
import { createElement } from '@syncfusion/ej2-base';
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { GanttComponent, Inject, Reorder } from '@syncfusion/ej2-react-gantt';
import { data } from './datasource';
class App extends React.Component<{}, {}>{
    public taskFields: any = {
    id: 'TaskID',
    name: 'TaskName',
    startDate: 'StartDate',
    duration: 'Duration',
    progress: 'Progress',
    child: 'subtasks'
  };
  public splitterSettings: any = {
    columnIndex : 5
};
    public columnDrop(){
        alert('columnDrop event is Triggered');
    }
    public columnDragStart(){
       alert('columnDragStart event is Triggered');
    }
    public columnDrag(){
       alert('columnDrag event is Triggered');
    }
    render() {
        return (<div>
        <GanttComponent dataSource={data} taskFields={this.taskFields} allowReordering={true}
        columnDragStart= { this.columnDragStart } columnDrag= { this.columnDrag } columnDrop= { this.columnDrop }
        splitterSettings={this.splitterSettings} height = '450px' ref={gantt => this.ganttInstance = gantt}>
        <Inject services={[Reorder]} />
        </GanttComponent></div>)
    }
};
ReactDOM.render(<App />, document.getElementById('root'));
```

{% endtab %}

## Reorder multiple columns

Multiple columns can be reordered at a time by using the [`reorderColumns`](../api/gantt/#reordercolumns) method.

{% tab template="gantt/multiplereorder", compileJsx=true %}

```typescript
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { GanttComponent, Inject, Reorder } from '@syncfusion/ej2-react-gantt';
import { data } from './datasource';
class App extends React.Component<{}, {}>{
    private ganttInstance: any;
    public taskFields: any = {
    id: 'TaskID',
    name: 'TaskName',
    startDate: 'StartDate',
    duration: 'Duration',
    progress: 'Progress',
    child: 'subtasks'
  };
  public splitterSettings: any = {
      position : '90%'
  };
  public clickHandler(){
    this.ganttInstance.reorderColumns(['TaskID','TaskName'],'Progress');
  }
    render() {
        return (<div>
        <ButtonComponent onClick= { this.clickHandler.bind(this)}>Reorder Task ID and Task Name to Last</ButtonComponent>
        <GanttComponent dataSource={data} taskFields={this.taskFields}
        splitterSettings={this.splitterSettings} allowReordering={true} height = '450px' ref={gantt => this.ganttInstance = gantt}>
            <Inject services={[Reorder]} />
        </GanttComponent></div>)
    }
};
ReactDOM.render(<App />, document.getElementById('root'));
```

{% endtab %}

## Column resizing

The column width can be resized by clicking and dragging the right edge of the column header. While dragging, the width of the column will be resized immediately. Each column can be auto resized by double-clicking the right edge of the column header to fit the width of that column based on the widest cell content. To resize the column, set the [`allowResizing`](../api/gantt/#allowresizing) property to `true`. The following code example shows how to enable the column resize feature in the Gantt component.

To resize the column, inject the `Resize` module into the Gantt component.

{% tab template="gantt/columnresize", compileJsx=true %}

```typescript
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { GanttComponent, Inject, Resize } from '@syncfusion/ej2-react-gantt';
import { data } from './datasource';
class App extends React.Component<{}, {}>{
    public taskFields: any = {
    id: 'TaskID',
    name: 'TaskName',
    startDate: 'StartDate',
    duration: 'Duration',
    progress: 'Progress',
    child: 'subtasks'
  };
  public splitterSettings: any = {
    position : '90%'
};
    render() {
        return <GanttComponent dataSource={data} taskFields={this.taskFields}
        allowResizing={true} splitterSettings={this.splitterSettings} height = '450px'>
            <Inject services={[Resize]} />
        </GanttComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('root'));
```

{% endtab %}

> You can disable resizing for a particular column by setting the [`columns.allowResizing`](../api/gantt/column/#allowresizing) to `false`.

### Defining minimum and maximum column width

The column resizing can be restricted between minimum and maximum widths by defining the [`columns->minWidth`](../api/gantt/column/#minwidth) and [`columns->maxWidth`](../api/gantt/column/#maxwidth) properties.

In the following example, the minimum and maximum widths are defined for the `Duration`, and `Task Name` columns.

{% tab template="gantt/columnwidth", compileJsx=true %}

```typescript
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { GanttComponent, Inject, Resize, ColumnsDirective, ColumnDirective } from '@syncfusion/ej2-react-gantt';
import { data } from './datasource';
class App extends React.Component<{}, {}>{
    public taskFields: any = {
    id: 'TaskID',
    name: 'TaskName',
    startDate: 'StartDate',
    duration: 'Duration',
    progress: 'Progress',
    child: 'subtasks'
  };
  public splitterSettings: any = {
      columnIndex: 6
  };
    render() {
        return <GanttComponent dataSource={data} taskFields={this.taskFields}
        splitterSettings={this.splitterSettings} allowResizing={true} height = '450px'>
            <ColumnsDirective>
                <ColumnDirective field='TaskID' width='100' ></ColumnDirective>
                <ColumnDirective field='TaskName' headerText='Task Name' minWidth='200' width='250' maxWidth='300'></ColumnDirective>
                <ColumnDirective field='StartDate'></ColumnDirective>
                <ColumnDirective field='Duration' minWidth='100' maxWidth='200'></ColumnDirective>
                <ColumnDirective field='Predecessor'></ColumnDirective>
                <ColumnDirective field='Progress'></ColumnDirective>
            </ColumnsDirective>
            <Inject services={[Resize]} />
        </GanttComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('root'));
```

{% endtab %}

## Column template

A column template is used to customize the column’s look. The following code example explains how to define the custom template in Gantt using the [`template`](../api/gantt/column/#template) property.

You can check this video to learn about how to use templates for column(based on conditions) and headers in Gantt.

`youtube:llhPqZOsLdY`

{% tab template="gantt/columntemplate", compileJsx=true %}

```typescript
let ProjectResources: Object[]  = [
  { resourceId: 1, resourceName: 'Martin Tamer' },
  { resourceId: 2, resourceName: 'Rose Fuller' },
  { resourceId: 3, resourceName: 'Margaret Buchanan' },
  { resourceId: 4, resourceName: 'Fuller King' },
  { resourceId: 5, resourceName: 'Davolio Fuller' },
  { resourceId: 6, resourceName: 'Van Jack' },
  { resourceId: 7, resourceName: 'Fuller Buchanan' },
  { resourceId: 8, resourceName: 'Jack Davolio' },
  { resourceId: 9, resourceName: 'Tamer Vinet' },
  { resourceId: 10, resourceName: 'Vinet Fuller' },
  { resourceId: 11, resourceName: 'Bergs Anton' },
  { resourceId: 12, resourceName: 'Construction Supervisor' }
];

let data: Object[]  = [
  {
      TaskID: 1,
      TaskName: 'Project initiation',
      StartDate: new Date('04/02/2019'),
      EndDate: new Date('04/21/2019'),
      subtasks: [
          {TaskID: 2, TaskName: 'Identify site location', StartDate: new Date('04/02/2019'), Duration: 4,Progress: 50, resources: [1]},
          {TaskID: 3, TaskName: 'Perform soil test', StartDate: new Date('04/02/2019'), Duration: 4,Progress: 50, resources: [2]},
          {TaskID: 4, TaskName: 'Soil test approval', StartDate: new Date('04/02/2019'), Duration: 4, Progress: 50 ,resources: [3]},
      ]
  },
  {
      TaskID: 5,
      TaskName: 'Project estimation',
      StartDate: new Date('04/02/2019'),
      EndDate: new Date('04/21/2019'),
      subtasks: [
          {TaskID: 6, TaskName: 'Develop floor plan for estimation', StartDate: new Date('04/04/2019'),Duration: 3, Progress: 50, resources: [4]},
          {TaskID: 7, TaskName: 'List materials', StartDate: new Date('04/04/2019'),Duration: 3, resources: [3],Progress: 50},
          {TaskID: 8, TaskName: 'Estimation approval', StartDate: new Date('04/04/2019'),Duration: 3,Progress: 50
          }
      ]
  }];

  import * as React from 'react';
  import * as ReactDOM from 'react-dom';
  import { GanttComponent, ColumnsDirective, ColumnDirective } from '@syncfusion/ej2-react-gantt';
  
  class App extends React.Component<{}, {}>{
      public taskFields: any = {
      id: 'TaskID',
      name: 'TaskName',
      startDate: 'StartDate',
      duration: 'Duration',
      progress: 'Progress',
      child: 'subtasks',
      resourceInfo: 'resources'
    };
    public splitterSettings: any = {
        columnIndex: 7
    };
    public resourceFields: any = {
        id: 'resourceId',
        name: 'resourceName',
    };
    public ganttTemplate(props:any) {
      var src = props.TaskID + '.png';
          return (<div className='image' >
              <img src={src} style={{height:'42px'}}/>
          </div>);
    };
      public template: any = this.ganttTemplate;
      render() {
          return <GanttComponent dataSource={data} rowHeight={60} taskFields={this.taskFields}
          splitterSettings={this.splitterSettings} resourceFields={this.resourceFields} resources={ProjectResources} height = '450px'>
              <ColumnsDirective>
                  <ColumnDirective field='TaskID'></ColumnDirective>
                  <ColumnDirective field='resources' headerText='Resources' width='250' template={this.template} textAlign='Center'></ColumnDirective>
                  <ColumnDirective field='TaskName'></ColumnDirective>
                  <ColumnDirective field='StartDate'></ColumnDirective>
                  <ColumnDirective field='Duration'></ColumnDirective>
                  <ColumnDirective field='Progress'></ColumnDirective>
              </ColumnsDirective>
          </GanttComponent>
      }
  };
  ReactDOM.render(<App />, document.getElementById('root'));
```

{% endtab %}

## Column menu

The column menu has options to integrate features like sorting, filtering, and autofit. It will show a menu with the integrated feature when users click the Multiple icon of the column. To enable the column menu, you should set the [`showColumnMenu`](../api/gantt/#showcolumnmenu) property to true.
The default items are displayed in the following table:

| Item | Description |
|-----|-----|
| `SortAscending` | Sort the current column in ascending order. |
| `SortDescending` | Sort the current column in descending order. |
| `AutoFit` | Auto fit the current column. |
| `AutoFitAll` | Auto fit all columns. |
| `Filter` | Show the filter option as given in the `filterSettings.type` property. |

{% tab template="gantt/columnmenu", compileJsx=true %}

```typescript
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { GanttComponent, Inject, Sort, Filter, Resize, ColumnMenu } from '@syncfusion/ej2-react-gantt';
import { data } from './datasource';
class App extends React.Component<{}, {}>{
    public taskFields: any = {
    id: 'TaskID',
    name: 'TaskName',
    startDate: 'StartDate',
    duration: 'Duration',
    progress: 'Progress',
    child: 'subtasks'
  };
    render() {
        return <GanttComponent dataSource={data} taskFields={this.taskFields}
        allowSorting={true} allowFiltering={true} allowResizing={true} showColumnMenu = {true} height = '450px'>
            <Inject services={[Sort, Filter, Resize, ColumnMenu]} />
        </GanttComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('root'));
```

{% endtab %}

> You can disable column menu for a particular column by defining the `columns.showColumnMenu` as `false`.

### Column menu Events

During the resizing action, the gantt component triggers the below two events.

1. The [`columnMenuOpen`](../api/gantt/#columnmenuopen) event triggers before the column menu opens.
2. The [`columnMenuClick`](../api/gantt/#columnmenuclick) event triggers when the user clicks the column menu of the gantt.

{% tab template="gantt/colmenu-events", compileJsx=true %}

```typescript
import { createElement } from '@syncfusion/ej2-base';
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { GanttComponent, Inject, Sort, Filter, ColumnMenu } from '@syncfusion/ej2-react-gantt';
import { data } from './datasource';
class App extends React.Component<{}, {}>{
    public taskFields: any = {
    id: 'TaskID',
    name: 'TaskName',
    startDate: 'StartDate',
    duration: 'Duration',
    progress: 'Progress',
    child: 'subtasks'
  };
  public splitterSettings: any = {
    columnIndex : 5
};
    public columnMenuOpen(){
        alert('columnMenuOpen event is Triggered');
    }
    public columnMenuClick(){
        alert('columnMenuClick event is Triggered');
    }
    render() {
        return (<div>
        <GanttComponent dataSource={data} taskFields={this.taskFields} showColumnMenu={true}
        columnMenuOpen= { this.columnMenuOpen } columnMenuClick= { this.columnMenuClick }
        allowFiltering={true} allowSorting={true}
        splitterSettings={this.splitterSettings} height = '450px' ref={gantt => this.ganttInstance = gantt}>
        <Inject services={[Sort, Filter, ColumnMenu]} />
        </GanttComponent></div>)
    }
};
ReactDOM.render(<App />, document.getElementById('root'));
```

{% endtab %}

### Custom Column Menu Item

Custom column menu items can be added by defining the [`columnMenuItems`](../api/gantt/#columnmenuitems).
Actions for this customized items can be defined in the [`columnMenuClick`](../api/gantt/#columnmenuclick) event.

{% tab template="gantt/colmenu-item", compileJsx=true %}

```typescript
import { createElement } from '@syncfusion/ej2-base';
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { GanttComponent, ColumnMenu, ColumnDirective, ColumnsDirective } from '@syncfusion/ej2-react-gantt';
import { ColumnMenuItemModel, Inject, Sort, SortSettingsModel } from '@syncfusion/ej2-react-gantt';
import { data } from './datasource';
class App extends React.Component<{}, {}>{
    private ganttInstance: any;
    public taskFields: any = {
        id: 'TaskID',
        name: 'TaskName',
        startDate: 'StartDate',
        duration: 'Duration',
        progress: 'Progress',
        child: 'subtasks'
    };
    public columnMenuItems: ColumnMenuItemModel[] =  [{text:'Clear Sorting', id:'ganttclearsorting'}];
    public sortSettings: SortSettingsModel = { columns:[{direction: "Ascending", field: "TaskName"}] };
    public columnMenuClick(args: any){
        if(args.item.id === 'ganttclearsorting'){
            this.clearSorting();
        }
    }

    public splitterSettings: any = {
        columnIndex : 5
    };
    render() {
        return (<div>
        <GanttComponent dataSource={data} taskFields={this.taskFields} showColumnMenu={true}
        columnMenuItems={this.columnMenuItems} columnMenuClick={this.columnMenuClick} sortSettings={this.sortSettings} allowSorting={true}
        splitterSettings={this.splitterSettings} height = '450px' ref={gantt => this.ganttInstance = gantt}>
        <ColumnsDirective>
            <ColumnDirective field='TaskID' width='100' ></ColumnDirective>
            <ColumnDirective field='TaskName' headerText='Task Name'></ColumnDirective>
            <ColumnDirective field='StartDate'></ColumnDirective>
            <ColumnDirective field='Duration'></ColumnDirective>
            <ColumnDirective field='Progress'></ColumnDirective>
        </ColumnsDirective>
        <Inject services={[ColumnMenu, Sort]} />
        </GanttComponent></div>)
    }
};
ReactDOM.render(<App />, document.getElementById('root'));
```

{% endtab %}

### Customize menu items for particular columns

Sometimes, you have a scenario that to hide an item from column menu for particular columns. In that case, you need to define the [`columnMenuOpenEventArgs.hide`](../api/grid/columnMenuOpenEventArgs) as true in the [`columnMenuOpen`](../api/gantt/#columnmenuopen) event.

The following sample, **Filter** item was hidden in column menu when opens for the **Task Name** column.

{% tab template="gantt/colmenu-action", compileJsx=true %}

```typescript
import { createElement } from '@syncfusion/ej2-base';
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { GanttComponent, ColumnMenu, ColumnDirective, ColumnsDirective, ColumnMenuOpenEventArgs } from '@syncfusion/ej2-react-gantt';
import { ColumnMenuItemModel, Inject, Sort, Filter } from '@syncfusion/ej2-react-gantt';
import { data } from './datasource';
class App extends React.Component<{}, {}>{
    public taskFields: any = {
        id: 'TaskID',
        name: 'TaskName',
        startDate: 'StartDate',
        duration: 'Duration',
        progress: 'Progress',
        child: 'subtasks'
    };
    public columnMenuOpen (args: ColumnMenuOpenEventArgs) {
        for (const item of args.items) {
            if (item.text === 'Filter' && (args.column as Column).field === 'TaskName') {
                (item as ColumnMenuItemModel).hide = true;
            } else {
                (item as ColumnMenuItemModel).hide = false;
            }
        }
    }

    public splitterSettings: any = {
        columnIndex : 5
    };
    render() {
        return (<div>
        <GanttComponent dataSource={data} taskFields={this.taskFields} showColumnMenu={true}
        columnMenuItems={this.columnMenuItems} columnMenuClick={this.columnMenuClick}  columnMenuOpen={this.columnMenuOpen} allowFiltering={true} allowSorting={true}
        splitterSettings={this.splitterSettings} height = '450px'>
        <ColumnsDirective>
            <ColumnDirective field='TaskID' width='100' ></ColumnDirective>
            <ColumnDirective field='TaskName' headerText='Task Name'></ColumnDirective>
            <ColumnDirective field='StartDate'></ColumnDirective>
            <ColumnDirective field='Duration'></ColumnDirective>
            <ColumnDirective field='Progress'></ColumnDirective>
        </ColumnsDirective>
        <Inject services={[ColumnMenu, Sort, Filter]} />
        </GanttComponent></div>)
    }
};
ReactDOM.render(<App />, document.getElementById('root'));
```

{% endtab %}

## Responsive columns

You can toggle the column visibility based on media queries, which are defined in the [`hideAtMedia`](../api/gantt/column/#hideatmedia). The [`hideAtMedia`](../api/gantt/column/#hideatmedia) accepts valid [Media Queries]( http://cssmediaqueries.com/what-are-css-media-queries.html ).

{% tab template="gantt/column", compileJsx=true %}

```typescript
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { GanttComponent, ColumnsDirective, ColumnDirective } from '@syncfusion/ej2-react-gantt';
import { data } from './datasource';
class App extends React.Component<{}, {}>{
    public taskFields: any = {
    id: 'TaskID',
    name: 'TaskName',
    startDate: 'StartDate',
    duration: 'Duration',
    progress: 'Progress',
    child: 'subtasks'
  };
    render() {
        return <GanttComponent dataSource={data} taskFields={this.taskFields}
        height = '450px'>
            <ColumnsDirective>
                <ColumnDirective field='TaskID' width='100' hideAtMedia = '(min-width:700px)'></ColumnDirective>
                //  column visibility hide when browser screen width lessthan 700px;
                <ColumnDirective field='TaskName' headerText='Job Name' width='250'></ColumnDirective>
                //  it is always shown;
                <ColumnDirective field='StartDate' hideAtMedia = '(max-width:500px)'></ColumnDirective>
                // column Visibility show when browser screen width  500px or less;
                <ColumnDirective field='Duration' hideAtMedia = '(min-width:500px)'></ColumnDirective>
                //  column visibility hide when browser screen width lessthan 700px;
                <ColumnDirective field='Progress'></ColumnDirective>
            </ColumnsDirective>
        </GanttComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('root'));
```

{% endtab %}

## Change tree/expander column

The tree/expander column is a column in the Gantt component, that has icons to expand or collapse the parent records. You can define the tree column index in the Gantt component by using the [`treeColumnIndex`](../api/gantt/#treecolumnindex) property and the default value of this property is `0`. The following code example shows how to use this property.

{% tab template="gantt/treecolumnindex", compileJsx=true %}

```typescript
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { GanttComponent } from '@syncfusion/ej2-react-gantt';
import { data } from './datasource';
class App extends React.Component<{}, {}>{
    public taskFields: any = {
    id: 'TaskID',
    name: 'TaskName',
    startDate: 'StartDate',
    duration: 'Duration',
    progress: 'Progress',
    child: 'subtasks'
  };
  public splitterSettings: any = {
    position : '90%'
};
    render() {
        return <GanttComponent dataSource={data} splitterSettings={this.splitterSettings} taskFields={this.taskFields} treeColumnIndex={2}
        height = '450px'>
        </GanttComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('root'));
```

{% endtab %}

## Show or Hide columns dynamically

You can show or hide gantt columns dynamically using external buttons by invoking the [`showColumn`](../api/gantt/#showcolumn) or [`hideColumn`](../api/gantt/#hidecolumn) method.

{% tab template="gantt/show-hide", compileJsx=true %}

```typescript
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { GanttComponent, Inject, ColumnsDirective, ColumnDirective } from '@syncfusion/ej2-react-gantt';
import { data } from './datasource';

class App extends React.Component<{}, {}>{
    private ganttInstance: GanttComponent;
    public taskFields: any = {
        id: 'TaskID',
        name: 'TaskName',
        startDate: 'StartDate',
        duration: 'Duration',
        progress: 'Progress',
        child: 'subtasks'
    };
    public splitterSettings: any = {
        columnIndex : 5
    };
    public show() {
        /** show by HeaderText */
        this.ganttInstance.showColumn(['Duration']);
    }

    public hide(){
        /** hide by HeaderText */
        this.ganttInstance.hideColumn(['Duration']);
    }
    render() {
        this.show = this.show.bind(this);
        this.hide = this.hide.bind(this);
        return (<div>
        <ButtonComponent onClick= { this.show }>Show</ButtonComponent>
        <ButtonComponent onClick= { this.hide }>Hide</ButtonComponent>
        <GanttComponent dataSource={data} taskFields={this.taskFields}
        splitterSettings={this.splitterSettings} height = '450px'
        ref={gantt => this.ganttInstance = gantt}>
        <ColumnsDirective>
            <ColumnDirective field='TaskID' width='100' ></ColumnDirective>
            <ColumnDirective field='TaskName' headerText='Task Name'></ColumnDirective>
            <ColumnDirective field='StartDate'></ColumnDirective>
            <ColumnDirective field='Duration' headerText='Duration'></ColumnDirective>
            <ColumnDirective field='Progress'></ColumnDirective>
        </ColumnsDirective>
        </GanttComponent></div>)
    }
};
ReactDOM.render(<App />, document.getElementById('root'));
```

{% endtab %}

## Checkbox Column

To render boolean values as checkbox in columns, you need to set [`displayAsCheckBox`](../api/gantt/column/#displayascheckbox) property as **true**.

{% tab template="gantt/checkbox" compileJsx=true %}

```typescript
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { GanttComponent, ColumnsDirective, ColumnDirective } from '@syncfusion/ej2-react-gantt';
import { data } from './datasource';

class App extends React.Component {
    constructor() {
        super(...arguments);
        this.taskFields = {
            id: 'TaskID',
            name: 'TaskName',
            startDate: 'StartDate',
            duration: 'Duration',
            progress: 'Progress',
            child: 'subtasks',
            verified: 'verified'
        };
    }
    public splitterSettings: any = {
        position : '80%'
    };
    render() {
        return (<div>
        <GanttComponent dataSource={data} taskFields={this.taskFields} splitterSettings={this.splitterSettings} height='450px' ref={gantt => this.ganttInstance = gantt}>
         <ColumnsDirective>
            <ColumnDirective field='TaskID' width='100' ></ColumnDirective>
            <ColumnDirective field='TaskName' headerText='Task Name'></ColumnDirective>
            <ColumnDirective field='StartDate'></ColumnDirective>
            <ColumnDirective field='Duration'></ColumnDirective>
            <ColumnDirective field='verified' headerText= 'Verified' type= 'boolean' displayAsCheckBox= {true}></ColumnDirective>
            <ColumnDirective field='Progress'></ColumnDirective>
        </ColumnsDirective>
        </GanttComponent></div>);
    }
}
;
ReactDOM.render(<App />, document.getElementById('root'));
```

{% endtab %}

## Controlling Grid Actions

You can enable or disable gantt action for a particular column by setting the [`allowFiltering`](../api/gantt/#allowfiltering), [`allowSorting`](../api/gantt/#allowsorting), [`allowReordering`](../api/gantt/#allowreordering), and [`allowEditing`](../api/gantt/#editsettings) properties.

{% tab template="gantt/grid-actions" compileJsx=true %}

```typescript
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { GanttComponent, ColumnsDirective, ColumnDirective, Inject, Resize, Sort, Filter, Edit, Reorder } from '@syncfusion/ej2-react-gantt';
import { data } from './datasource';

    class App extends React.Component<{}, {}>{
        public taskFields: any = {
        id: 'TaskID',
        name: 'TaskName',
        startDate: 'StartDate',
        duration: 'Duration',
        progress: 'Progress',
        child: 'subtasks'
    };
    public splitterSettings: any = {
        position : '90%'
    };
    public editSettings: any = {
        allowEditing : true
    };
    render() {
        return (<div>
        <GanttComponent dataSource={data} taskFields={this.taskFields} splitterSettings={this.splitterSettings} height='450px' allowSorting={true} allowFiltering={true} allowReordering={true} editSettings={this.editSettings}
        ref={gantt => this.ganttInstance = gantt}>
         <ColumnsDirective>
            <ColumnDirective field='TaskID' width='100' ></ColumnDirective>
            <ColumnDirective field='TaskName' headerText='Task Name' allowSorting= {false}></ColumnDirective>
            <ColumnDirective field='StartDate' allowEditing= {false}></ColumnDirective>
            <ColumnDirective field='Duration' allowFiltering= {false}></ColumnDirective>
            <ColumnDirective field='Progress' allowReordering= {false}></ColumnDirective>
        </ColumnsDirective>
        <Inject services={[Sort, Filter, Reorder, Edit]}/>
        </GanttComponent></div>);
    }
}
;
ReactDOM.render(<App />, document.getElementById('root'));
```

{% endtab %}

## Column type

Column type can be specified using the `columns.type` property. It specifies the type of data the column binds.

If the `format` is defined for a column, the column uses `type` to select the appropriate format option [number](../common/internationalization/#number-formatting) or [date](../common/internationalization/#manipulating-datetime).

Gantt column supports the following types:
* string
* number
* boolean
* date
* datetime

> If the `type` is not defined, it will be determined from the first record of the [`dataSource`](../api/gantt/#datasource).
> In case if the first record of the [`dataSource`](../api/gantt/#datasource) is null/blank value for a column then it is necessary to define the `type` for that column.

## Column Spanning

The gantt has option to span the adjacent cells. You need to define the [`colSpan`](../api/gantt/queryCellInfoEventArgs/#colspan) attribute to span cells in the [`QueryCellInfo`](../api/gantt/queryCellInfoEventArgs) event. In the following demo, **Work 1** cells have been spanned.

{% tab template="gantt/column-span" compileJsx=true %}

```typescript
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { GanttComponent, ColumnsDirective, ColumnDirective } from '@syncfusion/ej2-react-gantt';
import { data } from './datasource';
import { QueryCellInfoEventArgs } from '@syncfusion/ej2-react-gantt';

class App extends React.Component<{}, {}>{
    public queryCellInfoEvent = (args: QueryCellInfoEventArgs) => {
        switch(args.data.TaskID) {
            case 1:
            if ((args.column.field == 'work1') && (args.data.taskData.work1 == 'support')) {
                args.colSpan= 2;
            }
            break;
            case 2:
            if ((args.column.field == 'work1') && (args.data.taskData.work1 == 'support')) {
                args.colSpan= 2;
            }
            break;
            case 3:
            if ((args.column.field == 'work1') && (args.data.taskData.work1 == 'support')) {
                args.colSpan = 2;
            }
            break;
            case 4:
            if ((args.column.field == 'work1') && (args.data.taskData.work1 == 'support')) {
                args.colSpan = 2;
            }
            break;
            case 5  :
            if ((args.column.field == 'work1') && (args.data.taskData.work1 == 'support')) {
                args.colSpan = 2;
            }
            break;
            case 7:
            if ((args.column.field == 'work1') && (args.data.taskData.work1 == 'support')) {
                args.colSpan = 2;
            }
            break;
        }
    }
    public taskFields: any = {
        id: 'TaskID',
        name: 'TaskName',
        startDate: 'StartDate',
        duration: 'Duration',
        progress: 'Progress',
        child: 'subtasks',
        work1: 'work1',
        work2: 'work2',
    };
    public splitterSettings: any = {
        position : '75%'
    };
    render() {
        return (<div>
        <GanttComponent dataSource={data} taskFields={this.taskFields} queryCellInfo={this.queryCellInfoEvent} splitterSettings={this.splitterSettings} gridLines='Both' height='450px' ref={gantt => this.ganttInstance = gantt}>
         <ColumnsDirective>
            <ColumnDirective field='TaskID' width='100' ></ColumnDirective>
            <ColumnDirective field='TaskName' headerText='Task Name'></ColumnDirective>
            <ColumnDirective field='work1' headerText='Work 1'></ColumnDirective>
            <ColumnDirective field='work2' headerText='Work 2'></ColumnDirective>
            <ColumnDirective field='StartDate'></ColumnDirective>
            <ColumnDirective field='Duration'></ColumnDirective>
            <ColumnDirective field='Progress'></ColumnDirective>
        </ColumnsDirective>
        </GanttComponent></div>);
    }
}
;
ReactDOM.render(<App />, document.getElementById('root'));
```

{% endtab %}