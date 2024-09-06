---
title: "Columns"
component: "TreeGrid"
description: "Documentation on column reordering, resizing, header templates (custom header content), and column templates (custom cell content) in the Essential JS 2 TreeGrid control."
---

# Columns

The column definitions are used as the [`dataSource`](../api/treegrid#dataSource) schema in the TreeGrid. This plays a vital role in rendering column values in the required format.
The treegrid operations such as sorting, filtering and searching etc. are performed based on column definitions. The [`field`](../api/treegrid/column#field) property of the [`columns`](../api/treegrid#column)
is necessary to map the data source values in TreeGrid columns.

> 1. If the column [`field`](../api/treegrid/column/#field) is not specified in the dataSource, the column values will be empty.
> 2. If the [`field`](../api/treegrid/column/#field) name contains “dot” operator, it is considered as complex binding.

[`treeColumnIndex`](../api/treegrid/#treecolumnindex) property denotes the column that is used to expand and collapse child rows.

## Header Template

You can customize the header element by using the [`headerTemplate`](../api/treegrid/column/#headertemplate)property.

{% tab template="treegrid/column", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public taskName = () => {
        return (<div><img src="taskname.png" width="20" height="20" className="e-image" />
        <b>Task Name</b></div>);
    }
    public startDate = () => {
        return (<div><img src="startdate.png" width="20" height="20" className="e-image" />
        <b>Start Date</b></div>);
    }
    public duration = () => {
        return (<div><img src="duration.png" width="20" height="20" className="e-image" />
        <b>Duration</b></div>);
    }
    public progress = () => {
        return (<div><img src="progress.png" width="20" height="20" className="e-image" />
        <b>Progress</b></div>);
    }
    public render() {
        return <TreeGridComponent dataSource={sampleData} childMapping='subtasks' height='315'>
            <ColumnsDirective>
                <ColumnDirective field='taskName' width='220' headerTemplate={this.taskName}/>
                <ColumnDirective field='startDate' headerText='Start Date' format='yMd' type='date' textAlign='Right' headerTemplate={this.startDate}/>
                <ColumnDirective field='duration' textAlign='Right' headerTemplate={this.duration}/>
                <ColumnDirective field='progress' headerText='progress' textAlign='Right' headerTemplate={this.progress}/>
            </ColumnsDirective>
        </TreeGridComponent>
    }
};
```

{% endtab %}

## Header Text

By default, column header title is displayed from column [`field`](../api/treegrid/column#field) value. To override the default header title, you have to define the [`headerText`](../api/treegrid/column#headertext)value.

{% tab template="treegrid/column", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks'
            height='315'>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
        </TreeGridComponent>
    }
};
```

{% endtab %}

> * If both the [`field`](../api/treegrid/column/#field) and [`headerText`](../api/treegrid/column/#headertext)
are not defined in the column, the column renders with **“empty”** header text.

## Format

To format cell values based on specific culture, use the [`columns.format`](../api/treegrid/column/#format) property. The TreeGrid uses [Internalization](../common/internationalization/) library to format [`number`](../common/internationalization/#number-formatting) and [`date`](../common/internationalization/#manipulating-datetime)
values.

{% tab template="treegrid/column", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { orderData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public render() {
        return <TreeGridComponent dataSource={orderData} treeColumnIndex={1} childMapping='subtasks' height='315'>
            <ColumnsDirective>
              <ColumnDirective field='orderID' headerText='Order ID' width='90' textAlign='Right'/>
              <ColumnDirective field='orderName' headerText='Order Name' width='180'/>
              <ColumnDirective field='unitPrice' headerText='Price Per Unit' width='90' format='c2' textAlign='Right' type='number' />
            </ColumnsDirective>
        </TreeGridComponent>
    }
};
```

{% endtab %}

> By default, the [`number`](../common/internationalization/#number-formatting)
and [`date`](../common/internationalization/#manipulating-datetime) values are formatted in **en-US** locale.

### Number formatting

The number or integer values can be formatted using the below format strings.

Format |Description |Remarks
-----|-----|-----
N | Denotes numeric type. | The numeric format is followed by integer value as N2, N3. etc which denotes the number of precision to be allowed.
C | Denotes currency type. | The currency format is followed by integer value as C2, C3. etc which denotes the number of precision to be allowed.
P | Denotes percentage type | The percentage format expects the input value to be in the range of 0 to 100. For example the cell value `0.2` is formatted as `20%`. The percentage format is followed by integer value as P2, P3. etc which denotes the number of precision to be allowed.

Please refer to the link to know more about [`Number formatting`](../common/internationalization/#number-formatting).

### Date formatting

You can format date values either using built-in date format string or custom format string.

For built-in date format you can specify [`columns.format`](../api/treegrid/column/#format) property as string   (Example: `yMd`). Please refer to the link to know more about [`Date formatting`](../common/internationalization/#manipulating-datetime).

You can also use custom format string to format the date values. Some of the custom formats and the formatted date values are given in the below table.

Format | Formatted value
-----|-----
{ type:'date', format:'dd/MM/yyyy' } | 04/07/1996
{ type:'date', format:'dd.MM.yyyy' } | 04.07.1996
{ type:'date', skeleton:'short' } | 7/4/96
{ type: 'dateTime', format: 'dd/MM/yyyy hh:mm a' } | 04/07/1996 12:00 AM
{ type: 'dateTime', format: 'MM/dd/yyyy hh:mm:ss a' } | 07/04/1996 12:00:00 AM

{% tab template="treegrid/column", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { orderData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public formatOption: object = {type:'date', format:'dd/MM/yyyy'};

    public render() {
        return <TreeGridComponent dataSource={orderData} treeColumnIndex={1} childMapping='subtasks' height='315'>
            <ColumnsDirective>
              <ColumnDirective field='orderID' headerText='Order ID' width='90' textAlign='Right'/>
              <ColumnDirective field='orderName' headerText='Order Name' width='180'/>
              <ColumnDirective field='orderDate' headerText='Order Date' width='160' textAlign='Right' format={this.formatOption}/>
              <ColumnDirective field='price' headerText='Price' width='90' format='c2' textAlign='Right' type='number' />
            </ColumnsDirective>
        </TreeGridComponent>
    }
};
```

{% endtab %}

## AutoFit specific columns

The [`autoFitColumns`](../api/treegrid/#autofitcolumns) method resizes the column to fit the widest cell's content without wrapping. You can autofit a specific column at initial rendering by invoking the [`autoFitColumns`](../api/treegrid/#autofitcolumns) method in [`dataBound`](../api/treegrid/#databound) event.

{% tab template="treegrid/column", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, Inject, Resize, TreeGrid, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{

    private treegrid: TreeGrid | null;
    public dataBound(){
        if (this.treegrid) {
            this.treegrid.autoFitColumns(['taskName']);
        }
    }
    public render() {
        this.dataBound = this.dataBound.bind(this);
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks'
            height='315' allowResizing='true' dataBound= { this.dataBound }
            ref={g => this.treegrid = g}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='60'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='120' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='120' textAlign='Right' />
              <ColumnDirective field='progress' headerText='Progress' width='120' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Resize]}/>
        </TreeGridComponent>
    }
};
```

{% endtab %}

> You can autofit all columns, by invoking [`autoFitColumns`](../api/treegrid/#autofitcolumns) method without column name.

## Reorder

Reordering can be done by drag and drop of a particular column header from one index to another index within the treegrid. To enable reordering, set the [`allowReordering`](../api/treegrid/#allowreordering) to true.

To use reordering, inject the [`Reorder`](../api/treegrid/#reordermodule) module in the treegrid.

{% tab template="treegrid/column", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, Inject, Reorder, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{

    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks'
            allowReordering='true' height='315'>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
              <ColumnDirective field='progress' headerText='Progress' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Reorder]}/>
        </TreeGridComponent>
    }
};
```

{% endtab %}

> You can disable reordering a particular column by setting the [`columns.allowReordering`](../api/treegrid/column/#reordermodule) to false.

### Reorder Multiple Columns

Multiple columns can be reordered at a time by using the [`reorderColumns`](../api/treegrid/column#reordercolumns) method.

{% tab template="treegrid/column", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { ColumnDirective, ColumnsDirective, Inject, Reorder, TreeGrid, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public treegrid: TreeGrid | null;
    public reorder(){
        if (this.treegrid) {
            this.treegrid.reorderColumns(['taskID','duration'],'progress');
        }
    }

    public render() {
        this.reorder = this.reorder.bind(this);
        return (<div>
        <ButtonComponent id='reorderMultipleCols' onClick= { this.reorder }>Reorder Task ID and Duration to Last</ButtonComponent>
        <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks' allowReordering='true' height='285'
        ref={g => this.treegrid = g}>
            <ColumnsDirective>
               <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
               <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
               <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
               <ColumnDirective field='progress' headerText='Progress' width='80' textAlign='Right' />
             </ColumnsDirective>
             <Inject services={[Reorder]}/>
         </TreeGridComponent></div>)
     }
};
```

{% endtab %}

## Lock Columns

You can lock columns by using [`column.lockColumn`](../api/treegrid/column/#lockcolumn) property. The locked columns will be moved to the first position. Also you can’t reorder its position.

In the below example, duration column is locked and its reordering functionality is disabled.

{% tab template="treegrid/lock-column", sourceFiles="app/App.tsx,custom.css", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, Inject, Reorder, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import './custom.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public customAttributes: any = {class: 'customcss'};
    public render() {
        return <TreeGridComponent dataSource={sampleData} allowReordering={true} allowSelection={false}
        treeColumnIndex={1} childMapping='subtasks' height='315'>
        <Inject services={[Reorder]}/>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='110' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='110' lockColumn= {true} textAlign='Right' customAttributes={this.customAttributes} />
              <ColumnDirective field='progress' headerText='Progress' width='180'/>
            </ColumnsDirective>
        </TreeGridComponent>
    }
}
```

{% endtab %}

## Column Resizing

Column width can be resized by clicking and dragging the right edge of the column header. While dragging, the width of the respective column will be resized immediately. Each column can be auto resized by double-clicking the right edge of the column header to fit the width of that column based on the widest cell content. To enable column resize, set the [`allowResizing`](../api/treegrid/#allowresizing) property to true.

To use the column resize, inject **Resize** module in the treegrid.

{% tab template="treegrid/column", sourceFiles="app/App.tsx,custom.css", compileJsx=true %}

```typescript

import { ColumnDirective, ColumnsDirective, Inject, Resize, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import './custom.css'
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public render() {
        return <TreeGridComponent dataSource={sampleData} allowResizing={true} allowSelection={false} treeColumnIndex={1} childMapping='subtasks' height='315'>
        <Inject services={[Resize]}/>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right'/>
            </ColumnsDirective>
        </TreeGridComponent>
    }
}
```

{% endtab %}

> You can disable Resizing for a particular column,
by specifying [`columns.allowResizing`](../api/treegrid/columnModel/#allowresizing) to false.
> In RTL mode, you can click and drag the left edge of header cell to resize the column.

### Min and Max width

Column resize can be restricted between minimum and maximum width by defining the [`columns->minWidth`](../api/treegrid/column/#minwidth) and [`columns->maxWidth`](../api/treegrid/column/#maxwidth).

In the following sample, minimum and maximum width are defined for **Duration**, and **Task Name** columns.

{% tab template="treegrid/column", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, Inject, Resize, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks'
            allowResizing='true' height='315'>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' minWidth= '130' width='180' maxWidth='300'/>
              <ColumnDirective field='duration' headerText='Duration' minWidth= '50' width='80' maxWidth='150' textAlign='Right' />
              <ColumnDirective field='progress' headerText='Progress' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Resize]}/>
        </TreeGridComponent>
    }
};
```

{% endtab %}

### Resize Stacked Column

Stacked columns can be resized by clicking and dragging the right edge of the stacked column header. While dragging, the width of the respective child columns will be resized at the same time. You can disable resize for particular stacked column by setting [`allowResizing`](../api/treegrid/column/#allowresizing) as **false** to its columns.

{% tab template="treegrid/column", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnModel, ColumnsDirective,  Inject, Resize, TreeGridComponent  } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { orderData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public colStack1: ColumnModel[] = [
        { field: 'orderID', headerText: 'Order ID', width: 90, textAlign: 'Right' },
        { field: 'orderName', headerText: 'Order Name', width: 170, textAlign: 'Left' }
    ];
    public colStack2: ColumnModel[] = [
        { field: 'Category', allowResizing: false, headerText: 'Shipment Category', width: 150, textAlign: 'Left' },
        { field: 'shippedDate', headerText: 'Shipped Date', width: 120, textAlign: 'Right', format:'yMd' }
    ];
    public render() {
        return <TreeGridComponent dataSource={orderData} treeColumnIndex={1} childMapping='subtasks' allowResizing='true' height='260'>
            <ColumnsDirective>
                <ColumnDirective columns={this.colStack1} headerText='Order Details' textAlign='Center'/>
                <ColumnDirective columns={this.colStack2} headerText='Shipment Details' textAlign='Center' />
            </ColumnsDirective>
            <Inject services={[Resize]}/>
        </TreeGridComponent>
    }
};
```

{% endtab %}

### Touch Interaction

When the right edge of the header cell is tapped, a floating handler will be visible over the right border of the column. To resize the column, tap and drag the floating handler as needed.

The following screenshot represents the column resizing in touch device.

<!-- markdownlint-disable MD033 -->
<img src="../images/column-resizing.png" alt="Touch interaction image" style="width:320px;height: 620px">
<!-- markdownlint-enable MD033 -->

## Column Template

The column [`template`](../api/treegrid/column/#template) has options to display custom element instead of a field value in the column.

You can check this video to learn about how to use templates for column(based on conditions) and headers in Tree Grid.
`youtube:o0rX1nkTINo`

{% tab template="treegrid/column", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { getObject } from '@syncfusion/ej2-grids';
import { ISparklineLoadedEventArgs, SparklineComponent, SparklineTheme } from '@syncfusion/ej2-react-charts';
import { ColumnDirective, ColumnsDirective, Inject, Page, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { getSparkData, textdata } from './datasource';

export default class App extends React.Component<{}, {}>{

  public load(args: ISparklineLoadedEventArgs): void {
    let theme: string = location.hash.split('/')[1];
    theme = theme ? theme : 'Material';
    args.sparkline.theme = (theme.charAt(0).toUpperCase() + theme.slice(1)) as SparklineTheme;
  }
  
  public taxColTemplate (props: object) {
    return (<SparklineComponent id={"spkline" + getObject('EmployeeID', props)}
        fill='#3C78EF'
        height='50px'
        load={this.load}
        lineWidth= {2}
        valueType='Numeric'
        width='150px'
        dataSource={getSparkData('line', +getObject('EmployeeID', props))}/>);
  }
  public dayColTemplate (props: object) {
    return (<SparklineComponent id={"spkarea" + getObject('EmployeeID', props)}
    fill='#3C78EF'
    height='50px'
    load={this.load}
    negativePointColor='#f7a816'
    type='Column'
    valueType='Numeric'
    width='150px'
    dataSource={getSparkData('column', +getObject('EmployeeID', props))}/>);
  }
  public yearColTemplate (props: object) {
    return (<SparklineComponent id={"spkwl" + getObject('EmployeeID', props)}
    fill='#3C78EF'
    height='50px'
    load={this.load}
    negativePointColor='#f7a816'
    type='WinLoss'
    tiePointColor= 'darkgray'
    valueType='Numeric'
    width='150px'
    dataSource={getSparkData('column', +getObject('EmployeeID', props))}/>);
  }
  public render() {
    this.taxColTemplate = this.taxColTemplate.bind(this);
    this.dayColTemplate = this.dayColTemplate.bind(this);
    this.yearColTemplate = this.yearColTemplate.bind(this);
    return <TreeGridComponent dataSource={textdata} treeColumnIndex={0} childMapping='Children'
            allowPaging='true' height='410'>
        <ColumnsDirective>
            <ColumnDirective field='EmpID' headerText='Employee ID' width='95'/>
            <ColumnDirective field='Name' headerText='Name' width='90'/>
            <ColumnDirective field='DOB' headerText='DOB' width='90' format='yMd' textAlign='Right' />
            <ColumnDirective headerText='Tax per annum' width='90' template={this.taxColTemplate} textAlign='Center' />
            <ColumnDirective headerText='One Day Index' template={this.dayColTemplate} textAlign='Center' width='100' />
            <ColumnDirective headerText='Year GR' template={this.yearColTemplate} textAlign='Center' width='100' />
        </ColumnsDirective>
        <Inject services={[Page]} />
        </TreeGridComponent>
    }
}
```

{% endtab %}

### Using condition template

You can render the template elements based on condition.

In the following code, checkbox is rendered based on *Approved* field value.

{% tab template="treegrid/column", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { getObject } from '@syncfusion/ej2-grids';
import { ColumnDirective, ColumnsDirective,  Inject, Page, TreeGridComponent  } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{

    public treegridTemplate(props: object): any {
        if(getObject('approved', props)){
            return (<div className="template_checkbox">
                     <input type="checkbox" checked={true}/>
                 </div>);
        } else {
            return (<div className="template_checkbox">
                <input type="checkbox"/>
            </div>);
        }
    }

    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks' height='315'>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective headerText='approved' width='120' template={this.treegridTemplate} textAlign='Center' />
              <ColumnDirective field='progress' headerText='Progress' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Page]}/>
        </TreeGridComponent>
    }
};
```

{% endtab %}

## Column Type

Column type can be specified using the [`columns.type`](../api/treegrid/column/#type) property. It specifies the type of data the column binds.

If the [`format`](../api/treegrid/column/#format)  is defined for a column, the column uses [`type`](../api/treegrid/column/#type) to select the appropriate format option ([number](../common/internationalization/#number-formatting)
 or [date](../common/internationalization/#manipulating-datetime)).

TreeGrid column supports the following types:
* string
* number
* boolean
* date
* datetime

> If the [`type`](../api/treegrid/column/#type) is not defined, it will be determined from the first record of the [`dataSource`](../api/treegrid/column/#datasource).

## Column menu

The column menu has options to integrate features like sorting, filtering, and autofit. It will show a menu with the integrated feature when users click on multiple icon of the column. To enable column menu, you need to define the [`showColumnMenu`](../api/treegrid/#showcolumnmenu) property as true.

To use the column menu, inject the **ColumnMenu** module in the treegrid.

The default items are displayed in following table.

| Item | Description |
|-----|-----|
| **SortAscending** | Sort the current column in ascending order. |
| **SortDescending** | Sort the current column in descending order. |
| **AutoFit** | Auto fit the current column. |
| **AutoFitAll** | Auto fit all columns. |
| **Filter** | Show the filter option as given in [`filterSettings.type`](../api/treegrid/filterSettings/#type) |

{% tab template="treegrid/column", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective,  Inject, TreeGridComponent  } from '@syncfusion/ej2-react-treegrid';
import { ColumnMenu, Filter,  FilterSettingsModel, Sort } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public filterSettings: FilterSettingsModel = { type:'Menu' };
    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks'  height='315' allowFiltering={true}
            allowSorting={true} showColumnMenu={true} filterSettings={this.filterSettings}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='120' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='150' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='130' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Sort, Filter, ColumnMenu]}/>
        </TreeGridComponent>
    }
};
```

{% endtab %}

> You can disable column menu for a particular column by defining the [`columns.showColumnMenu`](../api/treegrid/column/#showcolumnmenu) as **false**.

## Checkbox Column

To render checkboxes in existing column, you need to set [`columns.showCheckbox`](../api/treegrid/column/#showcheckbox) property as **true**

It is also possible to select the rows hierarchically using checkboxes in TreeGrid by enabling [`autoCheckHierarchy`](../api/treegrid/#autocheckhierarchy) property. When we check on any parent record checkbox then the child record checkboxes will get checked.

{% tab template="treegrid/column", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, TreeGridComponent  } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks'
            height='315' autoCheckHierarchy={true}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='120' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180' showCheckbox={true}/>
              <ColumnDirective field='startDate' headerText='Start Date' width='150' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='130' textAlign='Right' />
            </ColumnsDirective>
        </TreeGridComponent>
    }
};
```

{% endtab %}

> For hierarchy selection between the records, we need to enable the [`autoCheckHierarchy`](../api/treegrid/#autocheckhierarchy) property.

## Responsive Columns

You can toggle column visibility based on media queries which are defined
at the [`hideAtMedia`](../api/treegrid/column/#hideatmedia). The [`hideAtMedia`](../api/treegrid/column/#hideatmedia) accepts valid [Media Queries]( http://cssmediaqueries.com/what-are-css-media-queries.html ).

{% tab template="treegrid/column", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, TreeGridComponent  } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks' height='315'>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right' hideAtMedia='(min-width:700px)'/>  
              // column hides when browser screen width lessthan 700px;
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd'
               textAlign='Right' type='date' hideAtMedia = '(max-width:500px)'/>
              // column shows when browser screen width lessthan or equalto 500px;
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
        </TreeGridComponent>
    }

};
```

{% endtab %}

## Controlling TreeGrid actions

You can enable or disable treegrid action for a particular column by setting the [`allowFiltering`](../api/treegrid/column/#allowfiltering), and [`allowSorting`](../api/treegrid/column/#allowsorting) properties.

{% tab template="treegrid/column", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, TreeGridComponent  } from '@syncfusion/ej2-react-treegrid';
import { Filter, Inject, Sort } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks'
            allowSorting='true' allowFiltering='true' height='270'>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right' allowSorting={false}/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' allowFiltering={false} />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Filter,Sort]}/>
        </TreeGridComponent>
    }
};
```

{% endtab %}

## Show/Hide Columns by External Button

You can show or hide treegrid columns dynamically using external buttons by invoking the [`showColumns`](../api/treegrid/#showcolumns) or [`hideColumns`](../api/treegrid/#hidecolumns) method.

{% tab template="treegrid/column", sourceFiles="app/App.tsx",compileJsx=true %}

```typescript
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { ColumnDirective, ColumnsDirective, TreeGridComponent  } from '@syncfusion/ej2-react-treegrid';
import { Inject, Page, TreeGrid } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public treegrid: TreeGrid | null;
    public show() {
        if (this.treegrid) {
            this.treegrid.showColumns(['Task ID', 'Duration']); // show by HeaderText
        }
    }

    public hide(){
        if (this.treegrid) {
            this.treegrid.hideColumns(['Task ID', 'Duration']); // hide by HeaderText
        }
    }

    public render() {
        this.show = this.show.bind(this);
        this.hide = this.hide.bind(this);
        return (<div>
        <ButtonComponent cssClass= 'e-flat' onClick= { this.show }>Show</ButtonComponent>
        <ButtonComponent cssClass= 'e-flat' onClick= { this.hide }>Hide</ButtonComponent><TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks' height='270' ref={g => this.treegrid = g}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Page]}/>
        </TreeGridComponent>
        </div>)
    }
};
```

{% endtab %}

## Complex Data Binding

You can achieve complex data binding in the treegrid by using the dot(.) operator in the [`column.field`](../api/treegrid/column/#field).

{% tab template="treegrid/column", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, TreeGridComponent  } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { complexData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public render() {
        return <TreeGridComponent dataSource={complexData} treeColumnIndex={1} childMapping='subtasks' height='315'>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='assignee.firstName' headerText='Assignee' width='90' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
        </TreeGridComponent>
    }
};
```

{% endtab %}

## ValueAccessor

The [`valueAccessor`](../api/treegrid/column/#valueaccessor) is used to access/manipulate the value of display data. You can achieve custom value formatting by using the [`valueAccessor`](../api/treegrid/column/#valueaccessor).

{% tab template="treegrid/column", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { getValue } from '@syncfusion/ej2-base';
import { ColumnDirective, ColumnsDirective, Inject, Page, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { orderData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public currencyFormatter(field: string, data: object, column: object) {
        return '€' + getValue('price', data);
    }

    public orderFormatter(field: string, data: object, column: object) {
        return data[field] + '-' + getValue('Category', data);
    }

    public render() {
        this.currencyFormatter = this.currencyFormatter.bind(this);
        this.orderFormatter = this.orderFormatter.bind(this);
        return <TreeGridComponent dataSource={orderData} treeColumnIndex={1} childMapping='subtasks' height='315'>
            <ColumnsDirective>
              <ColumnDirective field='orderID' headerText='Order ID' width='90' textAlign='Right'/>
              <ColumnDirective field='orderName' headerText='Order Name' width='210' valueAccessor={this.orderFormatter}/>
              <ColumnDirective field='orderDate' headerText='Order Date' width='110' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='price' headerText='Price' width='80' valueAccessor={this.currencyFormatter} textAlign='Right' type='number' />
            </ColumnsDirective>
            <Inject services={[Page]}/>
        </TreeGridComponent>
    }
};
```

{% endtab %}

### Display Array type Columns

You can bind an array of objects in a column by using the [`valueAccessor`](../api/treegrid/column/#valueaccessor) property.
In this example, the name field has an array of two objects, FirstName and LastName. These two objects are joined and bound to a column using the
[`valueAccessor`](../api/treegrid/column/#valueaccessor).

{% tab template="treegrid/column", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { stringData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public orderFormatter(field: string, data: object, column: object): string {
        return data[field].map((s: {lastName: string, firstName: string}): string => {
            return s.lastName || s.firstName }).join(' ');
    }

    public render() {
        return <TreeGridComponent dataSource={stringData} treeColumnIndex={1} childMapping='subtasks' height='315'>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='110' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='name' headerText='Assignee' width='150' textAlign='Left'
              valueAccessor={this.orderFormatter} />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
        </TreeGridComponent>
    }
};
```

{% endtab %}

### Expression Column

You can achieve the expression column by using the [`valueAccessor`](../api/treegrid/column/#valueaccessor)property.

{% tab template="treegrid/column", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { orderData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public totalPrice (field: string, data: { units: number, unitPrice: number }, column: object): number {
        return data.units * data.unitPrice;
    };

    public render() {
        return <TreeGridComponent dataSource={orderData} treeColumnIndex={1} childMapping='subtasks' height='315'>
            <ColumnsDirective>
                <ColumnDirective field='orderID' headerText='Order ID' width='110' textAlign='Right'/>
                <ColumnDirective field='orderName' headerText='Order Name' width='210' textAlign='Left'/>
                <ColumnDirective field='units' headerText='Units' width='120' textAlign='Right' />
                <ColumnDirective field='unitPrice' headerText='Unit Price' width='120' textAlign='Right'
                format='c2' type='number' />
                <ColumnDirective field='price' headerText='Total Price' width='120' textAlign='Right'
                format='c2' type='number' valueAccessor= {this.totalPrice} />
            </ColumnsDirective>
        </TreeGridComponent>
    }
};
```

{% endtab %}

## Render boolean value as checkbox

To render boolean values as checkbox in columns, you need to set [`displayAsCheckBox`](../api/treegrid/column/#displayascheckbox) property as **true**.

{% tab template="treegrid/column", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks' height='315'>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='approved' headerText='Approved' width='90' format='yMd' textAlign='Right' displayAsCheckBox={true} />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
        </TreeGridComponent>
    }
};
```

{% endtab %}
