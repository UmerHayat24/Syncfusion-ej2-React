---
title: "Columns"
component: "Grid"
description: "Documentation on column reordering, resizing, header templates (custom header content), and column templates (custom cell content) in the Essential JS 2 DataGrid control."
---

# Columns

The column definitions are used as the [`dataSource`](../api/grid/#datasource) schema in the Grid.
 This plays a vital role in rendering column values in the required format.
The grid operations such as sorting, filtering and grouping etc. are performed based on column definitions.
 The [`field`](../api/grid/column/#field) property of the [`columns`](../api/grid/column)
is necessary to map the data source values in Grid columns.

> 1. If the column with [`field`](../api/grid/column/#field) is not in the dataSource, then the column values will be displayed as empty.
> 2. If the [`field`](../api/grid/column/#field) name contains **“dot”** operator then it is considered as complex binding.

## Auto generation

The [`columns`](../api/grid/column/) are automatically generated when
[`columns`](../api/grid/column/) declaration is empty or undefined while initializing the grid.
All the columns in the [`dataSource`](../api/grid/#datasource) are bound as grid columns.

{% tab template="grid/column", sourceFiles="app/App.tsx" %}

```typescript
import { GridComponent } from '@syncfusion/ej2-react-grids';
import * as React from 'react';

const data: object[] = [
  { OrderID: 10248, CustomerID: 'VINET', EmployeeID: 5 },
  { OrderID: 10249, CustomerID: 'TOMSP', EmployeeID: 6 },
  { OrderID: 10250, CustomerID: 'HANAR', EmployeeID: 4 }];

export default class App extends React.Component<{}, {}>{
  public render() {
      return <GridComponent dataSource={data}/>
  }
}
```

{% endtab %}

### Set Primary key column for auto generated columns when editing is enabled

Primary key can be defined in the declaration of column object of the grid. When we didn't declare the columns, the grid will generate the columns automatically. For these auto generated columns, you can set [`isPrimaryKey`](../api/grid/column/#isprimarykey) column property as true by using the following ways,

If Primary key "column index" is known then refer the following code example

{% tab template="grid/column", sourceFiles="app/App.tsx" %}

```typescript
import { ColumnModel, Edit, EditSettingsModel, Grid, GridComponent, Inject } from '@syncfusion/ej2-react-grids';
import * as React from 'react';

const data: object[] = [
  { OrderID: 10248, CustomerID: 'VINET', EmployeeID: 5 },
  { OrderID: 10249, CustomerID: 'TOMSP', EmployeeID: 6 },
  { OrderID: 10250, CustomerID: 'HANAR', EmployeeID: 4 }];

export default class App extends React.Component<{}, {}>{
  public grid: Grid | null;
  public editOptions: EditSettingsModel = {
    allowAdding: true, allowDeleting: true, allowEditing: true
  };
  public dataBound(){
    if (this.grid) {
      const column: ColumnModel = this.grid.columns[0] as ColumnModel;
      column.isPrimaryKey = true;
    }
  }
  public render() {
      this.dataBound = this.dataBound.bind(this);
      return <GridComponent dataSource={data} dataBound= { this.dataBound }
                editSettings={this.editOptions} ref={g => this.grid = g}>
              <Inject services={[Edit]} />
             </GridComponent>
  }
}
```

{% endtab %}

If Primary key **column** and its **field** is known then primary key for the respective [`column`](https://ej2.syncfusion.com/documentation/api/grid/column/) can be defined as follows.

```typescript

  const column: ColumnModel = this.grid.getColumnByField('OrderID');
  column.isPrimaryKey = true;

```

### Set column options to auto generated columns

You can set column options such as [`format`](../api/grid/column/#format), [`width`](../api/grid/column/#width) to the auto generated columns by using [`dataBound`](../api/grid/#databound) event of the grid.

In the below example, [`width`](../api/grid/column/#width) is set for **OrderID** column, [`date`](../../base/internationalization.html#date-formatting) type is set for **OrderDate** column and **numeric** type is set for **Freight** column.

{% tab template="grid/column", sourceFiles="app/App.tsx" %}

```typescript
import { ColumnModel, Grid, GridComponent } from '@syncfusion/ej2-react-grids';
import * as React from 'react';


const data: object = [
  { OrderID: 10248, CustomerID: 'VINET', Freight: 32.3800, OrderDate: "1996-07-02T00:00:00.000Z" },
  { OrderID: 10249, CustomerID: 'TOMSP', Freight: 32.3800, OrderDate: "1996-07-19T00:00:00.000Z" },
  { OrderID: 10250, CustomerID: 'HANAR', Freight: 32.3800, OrderDate: "1996-07-22T00:00:00.000Z" }];

export default class App extends React.Component<{}, {}>{
  public grid: Grid | null;
  public dataBound() {
    if (this.grid) {  
      const columns: ColumnModel[] = this.grid.columns as ColumnModel[];
      columns[0].width = 120;
      for (const col of columns) {
        if(col.field === "OrderDate"){
            col.type="date";
        }
        if (col.type === "date") {
            col.format = { type: "date", format: "dd/MM/yyyy" };
        }
        if (col.field === 'Freight') {
          col.format = "P2";
        }
      }
      this.grid.refreshColumns();
    }
  }
  public render() {
    this.dataBound = this.dataBound.bind(this);
    return <GridComponent dataSource={data} dataBound= { this.dataBound }
            ref={g => this.grid = g}/>
  }
}
```

{% endtab %}

## Complex Data Binding

You can achieve complex data binding in the grid by using the dot(.) operator in the [`column.field`](../api/grid/column/#field).

{% tab template="grid/complex-binding", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { complexData } from './datasource';

export default class App extends React.Component<{}, {}>{
  public render() {
      return (<div>
      <GridComponent dataSource={ complexData } height={315 }>
          <ColumnsDirective>
              <ColumnDirective field='EmployeeID' headerText='Employee ID' width='120' textAlign="Right"/>
              <ColumnDirective field='Name.FirstName' headerText='First Name' width='120'/>
              <ColumnDirective field='Name.LastName' headerText='Last Name' width='120'/>
              <ColumnDirective field='Title' headerText='Title' width='150'/>
          </ColumnsDirective>
      </GridComponent>
      </div>)
  }
};
```

{% endtab %}

For OData and ODataV4 adaptors, you need to add [`expand`](https://ej2.syncfusion.com/documentation/api/data/query/#expand) query to the [`query`](../api/grid/#query) property (of Grid), to eager load the complex data.

```typescript
import { DataManager, ODataAdaptor, Query } from '@syncfusion/ej2-data';
import { ColumnDirective, ColumnsDirective, GridComponent, Inject, Page } from '@syncfusion/ej2-react-grids';
import * as React from 'react';

export default class App extends React.Component<{}, {}>{
    public data: DataManager = new DataManager({
      adaptor: new ODataAdaptor ,
      crossDomain: true,
      url: 'https://js.syncfusion.com/demos/ejServices/Wcf/Northwind.svc/Orders'
    });
    public query = new Query().expand('Employee');
    public render() {
        return <GridComponent dataSource={this.data} query={this.query} height={315} allowPaging={true}>
                <Inject services={[Page]}/>
                <ColumnsDirective>
                    <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign="Right"/>
                    <ColumnDirective field='CustomerID' headerText='Customer ID' width='150'/>
                    <ColumnDirective field='ShipCity' headerText='Ship City' width='150'/>
                    <ColumnDirective field='Employee.City' headerText='City Name' width='150'/>
                </ColumnsDirective>
               </GridComponent>
    }
}
```

## Foreign Key Column

Foreign key column can be enabled by using [`column.dataSource`](../api/grid/column/#datasource),
[`column.foreignKeyField`](../api/grid/column/#foreignkeyfield) and
[`column.foreignKeyValue`](../api/grid/column/#foreignkeyvalue) properties.

* [`column.dataSource`](../api/grid/column/#datasource) - Defines the foreign data.
* [`column.foreignKeyField`](../api/grid/column/#foreignkeyfield) - Defines the mapping column name to the foreign data.
* [`column.foreignKeyValue`](../api/grid/column/#foreignkeyvalue) - Defines the display field from the foreign data.

In the following example, **Employee Name** is a foreign column which shows **FirstName** column from foreign data.

{% tab template="grid/column", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, ForeignKey, GridComponent, Inject } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data, employeeData } from './datasource';

export default class App extends React.Component<{}, {}>{
  public render() {
    return <GridComponent dataSource={data} height={315}>
        <ColumnsDirective>
            <ColumnDirective field='OrderID' headerText='Order ID' width='100' textAlign="Right"/>
            <ColumnDirective field='EmployeeID' foreignKeyValue='FirstName' foreignKeyField='EmployeeID' dataSource={employeeData} headerText='Employee Name' width='150'/>
            <ColumnDirective field='Freight' headerText='Freight' width='80' textAlign="Right" format='C2'/>
            <ColumnDirective field='ShipCountry' headerText='Ship Country' width='100' />
        </ColumnsDirective>
        <Inject services={[ForeignKey]} />
    </GridComponent>
  }
};
```

{% endtab %}

> For remote data, the sorting and grouping is done based on [`column.foreignKeyField`](../api/grid/column/#foreignkeyfield) instead of [`column.foreignKeyValue`](../api/grid/column/#foreignkeyvalue).
> If [`column.foreignKeyField`](../api/grid/column/#foreignkeyfield) is not defined, then the column uses [`column.field`](../api/grid/column/#field).

## Header Template

You can customize the header element by using the [`headerTemplate`](../api/grid/column/#headertemplate) property. In this demo, the custom element is rendered for both CustomerID and OrderDate column headers.

{% tab template="grid/header-template", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
    public data: object[] = data;
    public orderTemplate: any = this.gridOTemplate;
    public dateTemplate: any = this.gridDTemplate;
    public gridOTemplate(props: any): any {
      return (<div>
          <span className="e-icon-userlogin e-icons employee"></span> Customer ID
      </div>);
    }
    public gridDTemplate(props: any): any {
      return (<div>
          <span className="e-icon-calender e-icons headericon"></span> Order Date
      </div>);
    }
    public render() {
        return <GridComponent dataSource={this.data} height={315}>
                <ColumnsDirective>
                    <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign="Right"/>
                    <ColumnDirective field='CustomerID' headerText='Customer ID' headerTemplate={this.orderTemplate} width='150'/>
                    <ColumnDirective field='ShipCity' headerText='Ship City' width='150'/>
                    <ColumnDirective field='OrderDate' headerText='Order Date' width='135' headerTemplate={this.dateTemplate}  format='yMd' textAlign='Right' />
                    <ColumnDirective field='ShipName' headerText='Ship Name' width='150'/>
                </ColumnsDirective>
               </GridComponent>
    }
}
```

{% endtab %}

## Header Text

By default, column header title is displayed from column [`field`](../api/grid/column/#field) value.
To override the default header title by defining [`headerText`](../api/grid/column/#headertext) value.

{% tab template="grid/column", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
    public data: object[] = data;
    public render() {
        return <GridComponent dataSource={this.data} height={315}>
                <ColumnsDirective>
                    <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign="Right"/>
                    <ColumnDirective field='CustomerID' headerText='Customer ID' width='150'/>
                    <ColumnDirective field='ShipCity' headerText='Ship City' width='150'/>
                    <ColumnDirective field='ShipName' headerText='Ship Name' width='150'/>
                </ColumnsDirective>
               </GridComponent>
    }
}
```

{% endtab %}

> * If both the [`field`](../api/grid/column/#field) and [`headerText`](../api/grid/column/#headertext) are not defined in the column, the column renders with “empty” header text.

## Format

To format cell values based on specific culture, use the
[`columns.format`](../api/grid/column/#format) property.
 The grid uses [Internalization](../../base/internationalization.html) library to format [`number`](../../base/internationalization.html#number-formatting) and
  [`date`](../../base/internationalization.html#date-formatting)
values.

{% tab template="grid/column", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';


export default class App extends React.Component<{}, {}>{
  public data: object[] = data;
  public render() {
      return <GridComponent dataSource={this.data} height={315}>
              <ColumnsDirective>
               <ColumnDirective field='OrderID' width='100' textAlign="Right"/>
               <ColumnDirective field='CustomerID' width='100'/>
               <ColumnDirective field='Freight' width='100' format="C2" textAlign="Right"/>
               <ColumnDirective field='OrderDate' width='140' format="yMd" textAlign="Right"/>
              </ColumnsDirective>
             </GridComponent>
  }
}
```

{% endtab %}

> By default, the [`number`](../../common/internationalization/#number-formatting)
and [`date`](../../common/internationalization/#date-formatting) values are formatted in **en-US** locale. You can localize the **currency** and [`date`](../../common/internationalization/#date-formatting) in different locale as explained [`here`](./global-local).

### Number formatting

The number or integer values can be formatted using the below format strings.

Format |Description |Remarks
-----|-----|-----
N | Denotes numeric type. | The numeric format is followed by integer value as N2, N3. etc which denotes the number of precision to be allowed.
C | Denotes currency type. | The currency format is followed by integer value as C2, C3. etc which denotes the number of precision to be allowed.
P | Denotes percentage type | The percentage format expects the input value to be in the range of 0 to 1. For example the cell value **0.2** is formatted as **20%**. The percentage format is followed by integer value as P2, P3. etc which denotes the number of precision to be allowed.

Please refer to the link to know more about [`Number formatting`](../../base/internationalization.html#number-formatting) format.

### Date formatting

You can format date values either using built-in date format string or custom format string.

For built-in date format you can specify [`columns.format`](../api/grid/column/#format) property as string   (Example: `yMd`). Please refer to the link to know more about [`Date formatting`](../../base/internationalization.html#date formatting).

You can also use custom format string to format the date values. Some of the custom formats and the formatted date values are given in the below table.

Format | Formatted value
-----|-----
{ type:'date', format:'dd/MM/yyyy' } | 04/07/1996
{ type:'date', format:'dd.MM.yyyy' } | 04.07.1996
{ type:'date', skeleton:'short' } | 7/4/96
{ type: 'dateTime', format: 'dd/MM/yyyy hh:mm a' } | 04/07/1996 12:00 AM
{ type: 'dateTime', format: 'MM/dd/yyyy hh:mm:ss a' } | 07/04/1996 12:00:00 AM

{% tab template="grid/column", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public data: object[] = data;
  public formatOption: object = {type:'date', format:'dd/MM/yyyy'};
  public shipFormat: object = { type: 'dateTime', format: 'dd/MM/yyyy hh:mm a' };
  public render() {
      return <GridComponent dataSource={this.data} height={315}>
              <ColumnsDirective>
               <ColumnDirective field='OrderID' width='100' textAlign="Right"/>
               <ColumnDirective field='Freight' width='100' format="C2" textAlign="Right"/>
               <ColumnDirective field='OrderDate' width='140' textAlign="Right" format={this.formatOption} />
               <ColumnDirective field='OrderDate' headerText='Ship Date' width='180' textAlign="Right" format={this.shipFormat}/>
              </ColumnsDirective>
             </GridComponent>
  }
}
```

{% endtab %}

## Visibility

You can hide any particular column in Grid before rendering by defining [`visible`](../api/grid/column/#visible) property as false. In the below sample **ShipCity** column is defined [`visible`](../api/grid/column/#visible) as **false**.

{% tab template="grid/column", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public data: object[] = data;
  public render() {
      return <GridComponent dataSource={this.data} height={315} >
              <ColumnsDirective>
                <ColumnDirective field='OrderID' headerText= 'Order ID' width='150'/>
                <ColumnDirective field='CustomerID' headerText= 'Customer ID' width='150'/>
                <ColumnDirective field='ShipName' headerText= 'Ship Name' width='150'/>
                <ColumnDirective field='ShipAddress' headerText= 'Ship Address' width='150' format="yMd"/>
                <ColumnDirective field='ShipCity' headerText= 'Ship City' visible={false} width='150' />
              </ColumnsDirective>
             </GridComponent>
  }
}
```

{% endtab %}

## AutoFit specific columns

The [`autoFitColumns`](../api/grid/#autofitcolumns) method resizes the column to fit the widest
cell's content without wrapping. You can autofit a specific columns at initial rendering by invoking
the [`autoFitColumns`](../api/grid/#autofitcolumns) method in [`dataBound`](../api/grid/#databound) event.

To use the [`autoFitColumns`](../api/grid/#autofitcolumns) method, inject the **Resize** module in the grid.

{% tab template="grid/column", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, Grid, GridComponent, Inject, Resize } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public data: object[] = data;
  public grid: Grid | null;
  public dataBound(){
    if (this.grid) {
      this.grid.autoFitColumns(['ShipName', 'ShipAddress']);
    }
  }
  public render() {
      this.dataBound = this.dataBound.bind(this);
      return <GridComponent dataSource={this.data} height={315}
                dataBound= { this.dataBound } ref={g => this.grid = g}>
              <Inject services={[Resize]}/>
              <ColumnsDirective>
                <ColumnDirective field='OrderID' headerText= 'Order ID' width='150'/>
                <ColumnDirective field='CustomerID' headerText= 'Customer ID' width='150'/>
                <ColumnDirective field='ShipName' headerText= 'Ship Name' width='150'/>
                <ColumnDirective field='ShipAddress' headerText= 'Ship Address' width='150' format="yMd"/>
                <ColumnDirective field='ShipCity' headerText= 'Ship City' width='150' />
              </ColumnsDirective>
             </GridComponent>
  }
}
```

{% endtab %}

> You can autofit all columns, by invoking [`autoFitColumns`](../api/grid/#autofitcolumns) method without column name.

## Reorder

Reordering can be done by drag and drop of a particular column header from one index to another index within the Grid.
To enable reordering, set the [`allowReordering`](../api/grid/#allowreordering) to true.

To use reordering, inject the [`Reorder`](../api/grid/reorder/) module in the grid.

{% tab template="grid/column", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent, Inject, Reorder } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public data: object[] = data;
  public render() {
      return <GridComponent dataSource={this.data} allowReordering={true} height={315}>
              <Inject services={[Reorder]}/>
              <ColumnsDirective>
               <ColumnDirective field='OrderID' width='100' textAlign="Right"/>
               <ColumnDirective field='CustomerID' width='100'/>
               <ColumnDirective field='Freight' width='100' format="C2" textAlign="Right"/>
               <ColumnDirective field='OrderDate' width='140' format="yMd" textAlign="Right"/>
              </ColumnsDirective>
             </GridComponent>
  }
}
```

{% endtab %}

> You can disable reordering a particular column by setting the [`columns.allowReordering`](../api/grid/column/#allowreordering) to false.

### Reorder Single Column

Grid have option to reorder Columns either by Interaction or by using the [`reorderColumns`](../api/grid/reorder/#reordercolumns) method. In the below sample, **ShipCity** column is reordered to last column position by using the method.

{% tab template="grid/column", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { ColumnDirective, ColumnsDirective, Grid, GridComponent, Inject, Reorder } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';


export default class App extends React.Component<{}, {}>{

  public data: object[] = data;

  private grid: Grid | null;

  public reorder(){
    if (this.grid) {
      this.grid.reorderColumns('ShipCity','ShipName');
    }
  }

  public render() {
      this.reorder = this.reorder.bind(this);
      return (<div>
      <ButtonComponent id='reorderSingleCols' onClick= { this.reorder }>Reorder Ship City to Last</ButtonComponent>
      <GridComponent dataSource={this.data} allowReordering={true} height={275} ref={g => this.grid = g}>
              <Inject services={[Reorder]}/>
              <ColumnsDirective>
               <ColumnDirective field='OrderID' width='100' textAlign="Right"/>
               <ColumnDirective field='CustomerID' width='100'/>
               <ColumnDirective field='ShipCity' headerText= 'Ship City' width='100' textAlign="Right"/>
               <ColumnDirective field='ShipRegion' headerText= 'Ship Region' width='100' textAlign="Right"/>
               <ColumnDirective field='ShipName' headerText= 'Ship Name' width='150' textAlign="Right"/>
              </ColumnsDirective>
             </GridComponent></div>)
  }
};
```

{% endtab %}

### Reorder Multiple Columns

User can reorder a single column at a time by Interaction. Sometimes we need to have reorder multiple columns at the same time, It can be achieved through programmatically by using [`reorderColumns`](../api/grid/reorder/#reordercolumns) method.

In the below sample, **Ship City** and **Ship Region** column is reordered to last column position.

{% tab template="grid/column", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { ColumnDirective, ColumnsDirective, Grid, GridComponent, Inject, Reorder } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';


export default class App extends React.Component<{}, {}>{

  public data: object[] = data;
  public grid: Grid | null;

  public reorder(){
    if (this.grid) {
      this.grid.reorderColumns(['ShipCity','ShipRegion'],'ShipName');
    }
  }
  public render() {
      this.reorder = this.reorder.bind(this);
      return (<div>
      <ButtonComponent id='reorderMultipleCols' onClick= { this.reorder }>Reorder Ship City and Ship Region to Last</ButtonComponent>
      <GridComponent dataSource={this.data} allowReordering={true} height={275} ref={g => this.grid = g}>
              <Inject services={[Reorder]}/>
              <ColumnsDirective>
               <ColumnDirective field='OrderID' width='100' textAlign="Right"/>
               <ColumnDirective field='CustomerID' width='100'/>
               <ColumnDirective field='ShipCity' headerText= 'Ship City' width='100' textAlign="Right"/>
               <ColumnDirective field='ShipRegion' headerText= 'Ship Region' width='100' textAlign="Right"/>
               <ColumnDirective field='ShipName' headerText= 'Ship Name' width='150' textAlign="Right"/>
              </ColumnsDirective>
             </GridComponent></div>)
  }
};
```

{% endtab %}

### Reorder Events

During the reorder action, the grid component triggers the below three events.

1. The [`columnDragStart`](../api/grid/#columndragstart) event triggers when column header element drag (move) starts.
2. The [`columnDrag`](../api/grid/#columnDrag) event triggers when column header element is dragged (moved) continuously.
3. The [`columnDrop`](../api/grid/#columnDrop) event triggers when a column header element is dropped on the target column.

{% tab template="grid/column", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { createElement } from '@syncfusion/ej2-base';
import { ColumnDirective, ColumnsDirective, GridComponent, Inject, Reorder } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';


export default class App extends React.Component<{}, {}>{

  public data: object[] = data;
  public columnDrop(){
    const span: HTMLElement = createElement('span');
    span.innerHTML='columnDrop event is Triggered </br>';
    (document.getElementById('events') as HTMLElement).append(span);
  }
  public columnDragStart(){
    const span: HTMLElement = createElement('span');
    span.innerHTML='columnDragStart event is Triggered </br>';
    (document.getElementById('events') as HTMLElement).append(span);
  }
  public columnDrag(){
    const span: HTMLElement = createElement('span');
    span.innerHTML='columnDrag event is Triggered </br>';
    (document.getElementById('events') as HTMLElement).append(span);
  }

  public render() {
      const styles: object = {
        'borderStyle': 'outset',
        'fontSize': '14px',
        'height': '40px',
        'overflowY': 'scroll',
        'width': '240px'
      }
      return (<div>
        <div id='events' style={styles}/>
      <GridComponent dataSource={this.data} allowReordering={true} height={275}
      columnDragStart= { this.columnDragStart } columnDrag= { this.columnDrag } columnDrop= { this.columnDrop }>
              <Inject services={[Reorder]}/>
              <ColumnsDirective>
               <ColumnDirective field='OrderID' headerText='Order ID' width='100' textAlign="Right"/>
               <ColumnDirective field='CustomerID' headerText='Customer ID' width='100'/>
               <ColumnDirective field='ShipCity' headerText= 'Ship City' width='100' textAlign="Right"/>
               <ColumnDirective field='ShipRegion' headerText= 'Ship Region' width='100' textAlign="Right"/>
               <ColumnDirective field='ShipName' headerText= 'Ship Name' width='150' textAlign="Right"/>
              </ColumnsDirective>
             </GridComponent></div>)
  }
};
```

{% endtab %}

## Lock Columns

You can lock columns by using [`column.lockColumn`](../api/grid/column/#lockcolumn) property. The locked columns will be moved to the first position. Also you can’t reorder its position.

In the below example, **Ship City** column is locked and its reordering functionality is disabled.

{% tab template="grid/column", sourceFiles="app/App.tsx,custom.css,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent, Inject, Reorder } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import './custom.css';
import { data } from './datasource';


export default class App extends React.Component<{}, {}>{
  public data: object[] = data;
  public customAttributes: any = {class: 'customcss'};
  public render() {
      return <GridComponent dataSource={this.data} allowReordering={true} allowSelection={false} height={315}>
              <Inject services={[Reorder]}/>
              <ColumnsDirective>
               <ColumnDirective field='OrderID' width='100' textAlign="Right"/>
               <ColumnDirective field='CustomerID' width='100'/>
               <ColumnDirective field='ShipCity' width='100' lockColumn= {true} customAttributes={this.customAttributes}/>
               <ColumnDirective field='ShipName' width='100'/>
               <ColumnDirective field='ShipPostalCode' width='120'/>
               <ColumnDirective field='ShipRegion' width='140'/>
              </ColumnsDirective>
             </GridComponent>
  }
};
```

{% endtab %}

## Column Resizing

Columns width can be resized by clicking and dragging at the right edge of column header.
While dragging, the width of respective column will be resized immediately.
Each columns can be auto resized by double clicking at the right edge of column header.
It will fit the width of that column based on widest cell content.
To enable the column resize, set the [`allowResizing`](../api/grid/#allowresizing) property to true.

To use the column resize, inject **Resize** module in the grid.

{% tab template="grid/column", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent, Inject, Resize } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';


export default class App extends React.Component<{}, {}>{
  public data: object[] = data;
  public render() {
      return <GridComponent dataSource={this.data} allowResizing={true} height={315}>
              <Inject services={[Resize]}/>
              <ColumnsDirective>
               <ColumnDirective field='OrderID' headerText= 'Order ID' width='150' textAlign="Right"/>
               <ColumnDirective field='CustomerID' headerText= 'Customer ID' width='150'/>
               <ColumnDirective field='Freight' width='150' format="C2" textAlign="Right"/>
               <ColumnDirective field='OrderDate' headerText= 'Order ID' width='150' format="yMd" textAlign="Right"/>
               <ColumnDirective field='ShipName' headerText= 'Ship Name' width='150' textAlign="Right"/>
               <ColumnDirective field='ShipAddress' headerText= 'Ship Address' width='150' format="yMd" textAlign="Right"/>
               <ColumnDirective field='ShipCountry' headerText= 'Ship Country' width='150'/>
               <ColumnDirective field='ShipCity' headerText= 'Ship City' width='150' textAlign="Right"/>
              </ColumnsDirective>
             </GridComponent>
  }
};
```

{% endtab %}

> You can disable Resizing for a particular column, by specifying [`columns.allowResizing`](../api/grid/columnModel/#allowresizing) to false.
> In RTL mode, you can click and drag the left edge of header cell to resize the column.

### Min and Max width

Columns can be restricted to resize in between minimum and maximum width by defining the
[`columns->minWidth`](../api/grid/columnModel/#minwidth) and [`columns->maxWidth`](../api/grid/columnModel/#maxwidth).

In the below sample, **OrderID**, **Ship Name** and **Ship Country** columns are defined with minimum and maximum width.

{% tab template="grid/column", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent, Inject, Resize } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';


export default class App extends React.Component<{}, {}>{
  public data: object[] = data;
  public render() {
      return <GridComponent dataSource={this.data} allowResizing={true} height={315}>
              <Inject services={[Resize]}/>
              <ColumnsDirective>
               <ColumnDirective field='OrderID' headerText= 'Order Id' minWidth= '100' width='150' maxWidth='250' textAlign="Right"/>
               <ColumnDirective field='CustomerID' headerText= 'Customer ID' width='150'/>
               <ColumnDirective field='Freight' width='150' format="C2" textAlign="Right"/>
               <ColumnDirective field='OrderDate' headerText= 'Order Date' width='120' format="yMd" textAlign="Right"/>
               <ColumnDirective field='ShipName' headerText= 'Ship Name' minWidth= '120' width='150' maxWidth='200' textAlign="Right"/>
               <ColumnDirective field='ShipAddress' headerText= 'Ship Address' width='150' format="yMd" textAlign="Right"/>
               <ColumnDirective field='ShipCountry' headerText= 'Ship Country' minWidth= '150' width='180' maxWidth='300' />
               <ColumnDirective field='ShipCity' headerText= 'Ship City' width='150' textAlign="Right"/>
              </ColumnsDirective>
             </GridComponent>
  }
};
```

{% endtab %}

### Resize Stacked Column

Stacked columns can be resized by clicking and dragging the right edge of the stacked column header. While dragging, the width of the respective child columns will be resized at the same time. You can disable resize for any particular stacked column by setting [`allowResizing`](../api/grid/columnModel/#allowresizing) as **false** to its columns.

In this example, we have disabled resize for **Ship City** column.

{% tab template="grid/column", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnModel, ColumnsDirective, GridComponent, Inject, Resize } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';


export default class App extends React.Component<{}, {}>{
  public data: object[] = data;
  public stackedCols1: ColumnModel[] = [
    { field: 'OrderDate', headerText: 'Order Date', format: 'yMd', width: 120, textAlign: 'Right' },
    { field: 'Freight', headerText: 'Freight ($)', width: 100, format: 'C1', textAlign: 'Right' }
  ];
  public stackedCols2: ColumnModel[] = [
    { field: 'ShipCity', headerText: 'Ship City', allowResizing: false, width: 120 },
    { field: 'ShipCountry', headerText: 'Ship Country', width: 120 }
  ];
  public render() {
      return <GridComponent dataSource={this.data} allowResizing={true} height={315} width='auto'>
              <Inject services={[Resize]}/>
              <ColumnsDirective>
                  <ColumnDirective field='OrderID' headerText='Order ID' width='100' textAlign='Right'/>
                  <ColumnDirective columns={this.stackedCols1} headerText='Order Details' />
                  <ColumnDirective columns={this.stackedCols2} headerText='Ship Details' />
              </ColumnsDirective>
             </GridComponent>
  }
};
```

{% endtab %}

### Touch Interaction

When you tap at the right edge of header cell, a floating handler will be visible over the right border of column.
To resize the column, tap and drag the floating handler as much you need. You can also autoFit a column by using the Column menu of the grid.

The following screenshot represents the column resizing in the touch device.

![Touch Interaction](images/column-resizing.jpg)

### Resizing Events

During the resizing action, the grid component triggers the below three events.

1. The [`resizeStart`](../api/grid/#resizestart) event triggers when column resize starts.
2. The [`resizing`](../api/grid/#resizing) event triggers when column header element is dragged (moved) continuously..
3. The [`resizeStop`](../api/grid/#resizeStop) event triggers when column resize ends.

{% tab template="grid/column", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { createElement } from '@syncfusion/ej2-base';
import { ColumnDirective, ColumnsDirective, GridComponent, Inject, Resize } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public data: object[] = data;
  public resizeStart(){
    const span: HTMLElement = createElement('span');
    span.innerHTML='resizeStart event is Triggered </br>';
    (document.getElementById('events') as HTMLElement).append(span);
  }
  public resizing(){
    const span: HTMLElement = createElement('span');
    span.innerHTML='resizing event is Triggered </br>';
    (document.getElementById('events') as HTMLElement).append(span);
  }
  public resizeStop(){
    const span: HTMLElement = createElement('span');
    span.innerHTML='resizeStop event is Triggered </br>';
    (document.getElementById('events') as HTMLElement).append(span);
  }
  public render() {
      const styles: object = {
        'borderStyle': 'outset',
        'fontSize': '14px',
        'height': '40px',
        'overflowY': 'scroll',
        'width': '240px'
      }
      return (<div>
        <div id='events' style={styles}/>
        <GridComponent dataSource={this.data} allowResizing={true} height={315}
        resizeStart= { this.resizeStart } resizing= { this.resizing } resizeStop= { this.resizeStop }>
                <Inject services={[Resize]}/>
                <ColumnsDirective>
                <ColumnDirective field='OrderID' headerText= 'Order ID' width='150' textAlign="Right"/>
                <ColumnDirective field='CustomerID' headerText= 'Customer ID' width='150'/>
                <ColumnDirective field='Freight' width='150' format="C2" textAlign="Right"/>
                <ColumnDirective field='OrderDate' headerText= 'Order ID' width='150' format="yMd" textAlign="Right"/>
                <ColumnDirective field='ShipName' headerText= 'Ship Name' width='150' textAlign="Right"/>
                <ColumnDirective field='ShipAddress' headerText= 'Ship Address' width='150' format="yMd" textAlign="Right"/>
                <ColumnDirective field='ShipCountry' headerText= 'Ship Country' width='150'/>
                <ColumnDirective field='ShipCity' headerText= 'Ship City' width='150' textAlign="Right"/>
                </ColumnsDirective>
              </GridComponent>
      </div>)
  }
};
```

{% endtab %}

## Column Template

The column [`template`](../api/grid/column/#template) has options to display custom element instead of a field value in the column.

{% tab template="grid/column-template", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { employeeData } from './datasource';

export default class App extends React.Component<{}, {}>{
  public template: any = this.gridTemplate;
  public gridTemplate(props: any): any {
      const src = props.EmployeeID + '.png';
      return (<div className='image'>
          <img src={src} alt={props.EmployeeID} />
      </div>);
  }

  public render() {
      return <GridComponent dataSource={employeeData} height={315}>
                  <ColumnsDirective>
                      <ColumnDirective headerText='Employee Image' width='180' template={this.template} textAlign='Center' />
                      <ColumnDirective field='EmployeeID' headerText='Employee ID' width='125' textAlign='Right' />
                      <ColumnDirective field='FirstName' headerText='Name' width='120' />
                      <ColumnDirective field='Title' headerText='Title' width='170' />
                      <ColumnDirective field='HireDate' headerText='Hire Date' width='135' format='yMd' textAlign='Right' />
                      <ColumnDirective field='ReportsTo' headerText='Reports To' width='120' textAlign='Right' />
                  </ColumnsDirective>
      </GridComponent>
  }
};
```

{% endtab %}

### Using condition template

You can render the template elements based on condition.

In the following code, checkbox is rendered based on **Discontinued** field value.

```typescript
  public gridTemplate(props: any): any {
    if(props.Discontinued){
   return (<div className="template_checkbox">
            <input type="checkbox" checked={true}/>
        </div>);
    }else{
         return (<div className="template_checkbox">
            <input type="checkbox"/>
        </div>);
    }
  }
```

{% tab template="grid/column-template", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { productData } from './datasource';

export default class App extends React.Component<{}, {}>{
  public template: any = this.gridTemplate;
  public gridTemplate(props: any): any {
    if(props.Discontinued){
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
      return <GridComponent dataSource={productData} height={315}>
                  <ColumnsDirective>
                      <ColumnDirective headerText='Discontinued' width='180' template={this.template} textAlign='Center' />
                      <ColumnDirective field='ProductID' headerText='Product ID' width='125' />
                      <ColumnDirective field='ProductName' headerText='Product Name' width='120' />
                      <ColumnDirective field='SupplierID' headerText='Supplier ID' width='170' />
                      <ColumnDirective field='UnitPrice' headerText='Unit Price' width='135' />
                  </ColumnsDirective>
      </GridComponent>
  }
};
```

{% endtab %}

## Column Type

Column type can be specified using the [`columns.type`](../api/grid/column/#type)
property. It specifies the type of the data the column bounded.

If the [`format`](../api/grid/column/#format)  is defined for a column, the column uses [`type`](../api/grid/column/#type) to select the appropriate format option ([number](../../base/internationalization.html#number-formatting) or [date](../../base/internationalization.html#date-formatting)).

Grid column supports the following types:

* string
* number
* boolean
* date
* datetime

> If the [`type`](../api/grid/column/#type) is not defined, then it will be determined from the first record of the [`dataSource`](../api/grid/#datasource).
> Incase if the first record of the [`dataSource`](../api/grid/#datasource) is null/blank value for a column then it is necessary to define the [`type`](../api/grid/column/#type) for that column.

## Column chooser

The column chooser has options to show or hide columns dynamically. It can be enabled by defining the [`showColumnChooser`](../api/grid/#showcolumnchooser) as true.

To use the column chooser, inject the **ColumnChooser** module in the grid.

{% tab template="grid/column", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnChooser, ColumnDirective, ColumnsDirective, GridComponent } from '@syncfusion/ej2-react-grids';
import { Inject, Toolbar, ToolbarItems } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public toolbarOptions : ToolbarItems[] = ['ColumnChooser'];
  public render(){
      return <GridComponent  dataSource={data} toolbar={this.toolbarOptions} height={272} showColumnChooser={true} >
                 <ColumnsDirective>
                  <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign='Right'/>
                  <ColumnDirective field='CustomerID' headerText='Customer ID' width='150' showInColumnChooser={false} />
                  <ColumnDirective field='Freight' width='100' format='C2' textAlign='Right'/>
                  <ColumnDirective field='OrderDate' width='140' format='yMd' textAlign='Right'/>
                  <ColumnDirective field='ShipCity' headerText='Ship City' width='150'/>
                  <ColumnDirective field='ShipName' headerText='Ship Name' width='150' visible = {false} />
              </ColumnsDirective>
              <Inject services={[Toolbar, ColumnChooser]}/>
          </GridComponent >
      }
};
```

{% endtab %}

> You can hide the column names in column chooser by defining the
[`columns.showInColumnChooser`](../api/grid/column/#showincolumnchooser) as **false**.

### Open column chooser by external button

The Column chooser can be displayed on a page through external button by invoking
the [`openColumnChooser`](../api/grid/columnChooser/#opencolumnchooser) method with **X** and **Y** axis positions.

{% tab template="grid/column", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { ColumnChooser, ColumnDirective, ColumnsDirective, Grid, GridComponent } from '@syncfusion/ej2-react-grids';
import { Inject } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{

  private grid: Grid | null;
  public show() {
    if (this.grid) {
      /* give X and Y axis */
      this.grid.columnChooserModule.openColumnChooser(200,50);
    }
  }
  public render() {
      this.show = this.show.bind(this);
      return (<div>
      <ButtonComponent cssClass= 'e-flat' onClick= { this.show}>Open Column Chooser</ButtonComponent>
      <GridComponent dataSource={data} showColumnChooser={true} height={295} ref={g => this.grid = g}>
          <ColumnsDirective>
                  <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign='Right'/>
                  <ColumnDirective field='CustomerID' headerText='Customer ID' width='150' showInColumnChooser={false} />
                  <ColumnDirective field='Freight' width='100' format='C2' textAlign='Right'/>
                  <ColumnDirective field='OrderDate' width='140' format='yMd' textAlign='Right'/>
                  <ColumnDirective field='ShipCity' headerText='Ship City' width='150'/>
                  <ColumnDirective field='ShipName' headerText='Ship Name' width='150' visible = {false} />
          </ColumnsDirective>
          <Inject services={[ColumnChooser]}/>
      </GridComponent>
      </div>)
  }
};
```

{% endtab %}

## Column menu

The column menu has options to integrate features like sorting, grouping, filtering, column chooser, and autofit.
It will show a menu with the integrated feature when users click on multiple icon of the column.
To enable column menu, you need to define the [`showColumnMenu`](../api/grid/#showcolumnmenu) property as true.

To use the column menu, inject the **ColumnMenu** module in the grid.

The default items are displayed in following table.

| Item | Description |
|-----|-----|
| **SortAscending** | Sort the current column in ascending order. |
| **SortDescending** | Sort the current column in descending order. |
| **Group** | Group the current column. |
| **Ungroup** | Ungroup the current column. |
| **AutoFit** | Auto fit the current column. |
| **AutoFitAll** | Auto fit all columns. |
| **ColumnChooser** | Choose the column visibility. |
| **Filter** | Show the filter option as given in **filterSettings.type** |

{% tab template="grid/column", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnMenu, ColumnsDirective, GridComponent, GroupSettingsModel } from '@syncfusion/ej2-react-grids';
import { Edit, ExcelExport, Group } from '@syncfusion/ej2-react-grids';
import { Filter, FilterSettingsModel, Inject, Page, PdfExport, Sort } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public groupOptions: GroupSettingsModel = { showGroupedColumn: true };
  public filterSettings: FilterSettingsModel = { type: 'CheckBox' };

  public render() {
      return (
          <div>
              <GridComponent dataSource={data} allowPaging={true}  allowGrouping={true} allowSorting={true}
                  showColumnMenu={true} allowExcelExport={true}  allowPdfExport={true}  allowFiltering={true} groupSettings={this.groupOptions} filterSettings={this.filterSettings}>
                  <ColumnsDirective>
                      <ColumnDirective field='OrderID' headerText='Order ID' width='140' textAlign='Right' isPrimaryKey={true}/>
                      <ColumnDirective field='CustomerID' headerText='Customer Name'/>
                      <ColumnDirective field='Freight' headerText='Freight' format='C2' textAlign='Right' />
                      <ColumnDirective field='ShipName' headerText='Ship Name' width='200'/>
                  </ColumnsDirective>
                  <Inject services={[Sort, ColumnMenu, Filter, Page, Group, ExcelExport, Edit, PdfExport]} />
                  </GridComponent>
          </div>
      );
  }
};
```

{% endtab %}

> You can disable column menu for a particular column by defining the [`columns.showColumnMenu`](../api/grid/column/#showcolumnmenu) as **false**.
> You can customize the default items by defining the
[`columnMenuItems`](../api/grid/#columnmenuitems) with required items.

### Column menu events

During the resizing action, the grid component triggers the below two events.

1. The [`columnMenuOpen`](../api/grid/#columnmenuopen) event triggers before the column menu opens.
2. The [`columnMenuClick`](../api/grid/#columnmenuclick) event triggers when the user clicks the column menu of the grid.

{% tab template="grid/column", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnMenu, ColumnsDirective, GridComponent, GroupSettingsModel } from '@syncfusion/ej2-react-grids';
import { Edit, ExcelExport } from '@syncfusion/ej2-react-grids';
import { Filter, FilterSettingsModel, Inject, Page, PdfExport, Sort } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public groupOptions: GroupSettingsModel = { showGroupedColumn: true };
  public filterSettings: FilterSettingsModel = { type: 'CheckBox' };
  public columnMenuOpen(){
     alert('columnMenuOpen event is Triggered');
  }
  public columnMenuClick(){
     alert('columnMenuClick event is Triggered');
  }
  public render() {
      return (
          <div>
              <GridComponent dataSource={data} allowPaging={true}  allowGrouping={true} allowSorting={true}
              showColumnMenu={true} allowExcelExport={true}  allowPdfExport={true} allowFiltering={true}
              groupSettings={this.groupOptions} filterSettings={this.filterSettings}
              columnMenuOpen= { this.columnMenuOpen } columnMenuClick= { this.columnMenuClick }>
                  <ColumnsDirective>
                      <ColumnDirective field='OrderID' headerText='Order ID' width='140' textAlign='Right'/>
                      <ColumnDirective field='CustomerID' headerText='Customer Name'/>
                      <ColumnDirective field='Freight' headerText='Freight' format='C2' textAlign='Right' />
                      <ColumnDirective field='ShipName' headerText='Ship Name' width='200'/>
                  </ColumnsDirective>
                  <Inject services={[Sort, ColumnMenu, Filter, Page, ExcelExport, Edit, PdfExport]} />
                  </GridComponent>
          </div>
      );
  }
};
```

{% endtab %}

### Custom Column Menu Item

Custom column menu items can be added by defining the [`columnMenuItems`](../api/grid/#columnmenuitems) as collection of the [`columnMenuItemModel`](../api/grid/columnMenuItemModel).
Actions for this customized items can be defined in the
[`columnMenuClick`](../api/grid/#columnmenuclick) event.

{% tab template="grid/column", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { MenuEventArgs } from '@syncfusion/ej2-navigations';
import { ColumnDirective, ColumnMenu, ColumnsDirective, Grid, GridComponent } from '@syncfusion/ej2-react-grids';
import { ColumnMenuItemModel, Inject, Page, Sort, SortSettingsModel } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public grid: Grid | null;
  public columnMenuItems: ColumnMenuItemModel[] =  [{text:'Clear Sorting', id:'gridclearsorting'}];
  public sortSettings: SortSettingsModel = { columns:[{direction: "Ascending", field: "OrderID"}] };

  public columnMenuClick(args: MenuEventArgs){
      if(this.grid && args.item.id === 'gridclearsorting'){
          this.grid.clearSorting();
      }
  }

  public render() {
      this.columnMenuClick = this.columnMenuClick.bind(this);
      return (
          <div>
              <GridComponent dataSource={data} allowPaging={true} allowSorting={true} showColumnMenu={true} sortSettings={this.sortSettings}
              ref={g=> this.grid = g} columnMenuItems={this.columnMenuItems} columnMenuClick={this.columnMenuClick}>
                  <ColumnsDirective>
                      <ColumnDirective field='OrderID' headerText='Order ID' width='140' textAlign='Right' />
                      <ColumnDirective field='CustomerID' headerText='Customer Name'/>
                      <ColumnDirective field='Freight' headerText='Freight' format='C2' textAlign='Right' />
                      <ColumnDirective field='ShipName' headerText='Ship Name' width='200'/>
                  </ColumnsDirective>
                  <Inject services={[Sort, ColumnMenu, Page]} />
                  </GridComponent>
          </div>
      );
  }
};
```

{% endtab %}

### Customize menu items for particular columns

Sometimes, if you need to hide an item from column menu for particular columns, define the
[`items.hide`](../api/grid/columnMenuItemModel/#items) as **true** of the argument interface [`columnMenuOpenEventArgs`](../api/grid/columnMenuOpenEventArgs) in the
[`columnMenuOpen`](../api/grid/#columnmenuopen) event.

The following sample, **Filter** item was hidden in column menu when opens for the **OrderID** column.

{% tab template="grid/column", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnMenu, ColumnMenuOpenEventArgs, ColumnsDirective, GridComponent } from '@syncfusion/ej2-react-grids';
import { Column, ColumnMenuItemModel, Filter, FilterSettingsModel, Inject, Page, Sort } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public filterOptions: FilterSettingsModel = {type: 'Menu'};

  public columnMenuOpen (args: ColumnMenuOpenEventArgs) {
      for (const item of args.items) {
          if (item.text === 'Filter' && (args.column as Column).field === 'OrderID') {
              (item as ColumnMenuItemModel).hide = true;
          } else {
              (item as ColumnMenuItemModel).hide = false;
          }
      }
  }

  public render() {
      return (
          <div>
              <GridComponent dataSource={data} allowPaging={true}  allowGrouping={true} showColumnMenu={true}
                  allowFiltering={true} allowSorting={true} filterSettings={this.filterOptions}
                  columnMenuOpen={this.columnMenuOpen}>
                  <ColumnsDirective>
                      <ColumnDirective field='OrderID' headerText='Order ID' width='140' textAlign='Right'/>
                      <ColumnDirective field='CustomerID' headerText='Customer Name'/>
                      <ColumnDirective field='Freight' headerText='Freight' format='C2' textAlign='Right' />
                      <ColumnDirective field='ShipName' headerText='Ship Name' width='200'/>
                  </ColumnsDirective>
                  <Inject services={[Sort, ColumnMenu, Page, Filter]} />
                  </GridComponent>
          </div>
      );
  }
};
```

{% endtab %}

## Column Spanning

Grid has option to span the adjacent cells. You need to define
[`colSpan`](../api/grid/queryCellInfoEventArgs/#colspan) attribute to span the cells
in [`queryCellInfo`](../api/grid/queryCellInfoEventArgs/) event.

In the following demo, Employee **Davolio** doing analysis from 9.00 AM to 10.00 AM, so that cells have spanned.

{% tab template="grid/spanning", sourceFiles="app/App.tsx,app/datasource.tsx,app/ColumnSpanDataType.tsx" %}

```typescript
import { Column, ColumnDirective, ColumnsDirective, GridComponent } from '@syncfusion/ej2-react-grids';
import { QueryCellInfoEventArgs } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { IColumnSpanDataType } from './colspanDataType';
import { columnSpanData } from './datasource';

export default class App extends React.Component<{}, {}>{
  public queryCellInfoEvent = (args: QueryCellInfoEventArgs) => {
    const col: Column = args.column as Column;
    const data: IColumnSpanDataType = args.data as IColumnSpanDataType;
    switch (data.EmployeeID) {
        case 10001:
            if (col.field === '9:00' || col.field === '2:30' || col.field === '4:30') {
                args.colSpan = 2;
            } else if (col.field === '11:00') {
                args.colSpan = 3;
            }
            break;
        case 10002:
            if (col.field === '9:30' || col.field === '2:30' ||
                col.field === '4:30') {
                args.colSpan = 3;
            } else if (col.field === '11:00') {
                args.colSpan = 4;
            }
            break;
        case 10003:
            if (col.field === '9:00' || col.field === '11:30') {
                args.colSpan = 3;
            } else if (col.field === '10:30' || col.field === '3:30' ||
                col.field === '4:30' || col.field === '2:30') {
                args.colSpan = 2;
            }
            break;
        case 10004:
            if (col.field === '9:00') {
                args.colSpan = 3;
            } else if (col.field === '11:00') {
                args.colSpan = 4;
            } else if (col.field === '4:00' || col.field === '2:30') {
                args.colSpan = 2;
            }
            break;
        case 10005:
            if (col.field === '9:00') {
                args.colSpan = 4;
            } else if (col.field === '11:30') {
                args.colSpan = 3;
            } else if (col.field === '3:30' || col.field === '4:30' || col.field === '2:30') {
                args.colSpan = 2;
            }
            break;
        case 10006:
            if (col.field === '9:00' || col.field === '4:30' ||
                col.field === '2:30' || col.field === '3:30') {
                args.colSpan = 2;
            } else if (col.field === '10:00' || col.field === '11:30') {
                args.colSpan = 3;
            }
            break;
        case 10007:
            if (col.field === '9:00' || col.field === '3:00' || col.field === '10:30') {
                args.colSpan = 2;
            } else if (col.field === '11:30' || col.field === '4:00') {
                args.colSpan = 3;
            }
            break;
        case 10008:
            if (col.field === '9:00' || col.field === '10:30' || col.field === '2:30') {
                args.colSpan = 3;
            } else if (col.field === '4:00') {
                args.colSpan = 2;
            }
            break;
        case 10009:
            if (col.field === '9:00' || col.field === '11:30') {
                args.colSpan = 3;
            } else if (col.field === '4:30' || col.field === '2:30') {
                args.colSpan = 2;
            }
            break;
        case 100010:
            if (col.field === '9:00' || col.field === '2:30' ||
                col.field === '4:00' || col.field === '11:30') {
                args.colSpan = 3;
            } else if (col.field === '10:30') {
                args.colSpan = 2;
            }
            break;
    }
};
public render() {
    this.queryCellInfoEvent = this.queryCellInfoEvent.bind(this);
    return (
        <div className='control-pane'>
            <div className='control-section'>
                <GridComponent dataSource={columnSpanData} queryCellInfo={this.queryCellInfoEvent} allowTextWrap={true} height='auto' width='auto' gridLines='Both' >
                    <ColumnsDirective>
                        <ColumnDirective field='EmployeeID' headerText='Employee ID' width='150' textAlign='Right'/>
                        <ColumnDirective field='EmployeeName' headerText='Employee Name' width='200' />
                        <ColumnDirective field='9:00' headerText='9:00 AM' width='120'/>
                        <ColumnDirective field='9:30' headerText='9:30 AM' width='120'/>
                        <ColumnDirective field='10:00' headerText='10:00 AM' width='120'/>
                        <ColumnDirective field='10:30' headerText='10:30 AM' width='120'/>
                        <ColumnDirective field='11:00' headerText='11:00 AM' width='120'/>
                        <ColumnDirective field='11:30' headerText='11:30 AM' width='120'/>
                        <ColumnDirective field='12:00' headerText='12:00 PM' width='120'/>
                        <ColumnDirective field='12:30' headerText='12:30 PM' width='120'/>
                        <ColumnDirective field='2:30' headerText='2:30 PM' width='120'/>
                        <ColumnDirective field='3:00' headerText='3:00 PM' width='120'/>
                        <ColumnDirective field='3:30' headerText='3:30 PM' width='120'/>
                        <ColumnDirective field='4:00' headerText='4:00 PM' width='120'/>
                        <ColumnDirective field='4:30' headerText='4:30 PM' width='120'/>
                        <ColumnDirective field='5:00' headerText='5:00 PM' width='120'/>
                    </ColumnsDirective>
                </GridComponent>
            </div>
        </div>
    )
}
};
```

{% endtab %}

## Responsive Columns

You can toggle column visibility based on media queries which are defined at the [`hideAtMedia`](../api/grid/column/#hideatmedia). The [`hideAtMedia`](../api/grid/column/#hideatmedia) accepts valid [`Media Queries`]( http://cssmediaqueries.com/what-are-css-media-queries.html ). In the below sample, for **OrderID** column, [`hideAtMedia`](../api/grid/column/#hideatmedia) property value is set as **(min-width: 700px)** so that **OrderID** column will gets hidden when the browser screen width is **lessthan 700px**.

{% tab template="grid/column", sourceFiles="app/app.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public data: object[] = data;
  public render() {
      return <GridComponent dataSource={this.data} height={315}>
              <ColumnsDirective>
                  /** Column visibility hide when browser screen width lessthan 700px */
                  <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign="Right"
                  hideAtMedia = '(min-width:700px)'/>
                  /** Column Visibility show when browser screen width  500px or less */
                  <ColumnDirective field='CustomerID' headerText='Customer ID' width='150'
                  hideAtMedia = '(max-width:500px)'/>
                  /** Column visibility hide when browser screen width lessthan 700px */
                  <ColumnDirective field='ShipCity' headerText='Ship City' width='150'
                  hideAtMedia = '(min-width:500px)'/>
                  /** It is always shown; */
                 <ColumnDirective field='ShipName' headerText='Ship Name' width='150'/>
              </ColumnsDirective>
             </GridComponent>
  }
};
```

{% endtab %}

## Controlling Grid Actions

You can enable or disable Grid any actions for a particular column by setting the [`allowFiltering`](../api/grid/columnModel/#allowfiltering), [`allowGrouping`](../api/grid/columnModel/#allowgrouping), [`allowSorting`](../api/grid/columnModel/#allowsorting), [`allowEditing`](../api/grid/columnModel/#allowediting) and [`allowReordering`](../api/grid/columnModel/#allowreordering) properties.

{% tab template="grid/column", sourceFiles="app/app.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, EditSettingsModel, GridComponent } from '@syncfusion/ej2-react-grids';
import { Edit, Filter, Group, Inject, Reorder, Sort } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public data: object[] = data;
  public editOptions: EditSettingsModel = { allowEditing: true, allowAdding: true, allowDeleting: true };
  public render() {
      return <GridComponent dataSource={data} allowSorting={true} editSettings={this.editOptions} allowFiltering={true} allowReordering={true} allowGrouping={true} height={230}>
              <ColumnsDirective>
               <ColumnDirective field='OrderID' width='100' textAlign="Right" isPrimaryKey={true} allowGrouping={false}/>
               <ColumnDirective field='CustomerID' width='100'/>
               <ColumnDirective field='Freight' width='100' format="C2" textAlign="Right" allowEditing={false} allowReordering={false} allowFiltering={false}/>
               <ColumnDirective field='OrderDate' width='140' format="yMd" textAlign="Right" allowSorting={false}/>
              </ColumnsDirective>
              <Inject services={[Edit, Sort, Filter, Group, Reorder]} />
             </GridComponent>
  }
};
```

{% endtab %}

## Show/Hide Columns by External Button

You can show or hide the grid columns dynamically through external buttons by invoking the [`showColumns`](../api/grid/#showcolumns) and [`hideColumns`](../api/grid/#hidecolumns)
methods.

{% tab template="grid/column", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { ColumnDirective, ColumnsDirective, Grid, GridComponent } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  private grid: Grid | null;
  public show() {
    if (this.grid) {
      /** show by HeaderText */
      this.grid.showColumns(['Customer ID', 'Freight']);
    }
  }

  public hide(){
    if (this.grid) {
      /** hide by HeaderText */
      this.grid.hideColumns(['Customer ID', 'Freight']);
    }
  }
  public render() {
      this.show = this.show.bind(this);
      this.hide = this.hide.bind(this);
      return (<div>
      <ButtonComponent cssClass= 'e-flat' onClick= { this.show }>Show</ButtonComponent>
      <ButtonComponent cssClass= 'e-flat' onClick= { this.hide }>Hide</ButtonComponent>
      <GridComponent dataSource={data} height={295} ref={g => this.grid = g}>
          <ColumnsDirective>
              <ColumnDirective field='OrderID' headerText='Order ID' width='100' textAlign="Right"/>
              <ColumnDirective field='CustomerID' headerText='Customer ID' width='100'/>
              <ColumnDirective field='EmployeeID' headerText='Employee ID' width='100' textAlign="Right"/>
              <ColumnDirective field='Freight' headerText='Freight' width='100' format="C2" textAlign="Right"/>
              <ColumnDirective field='ShipCountry' headerText='Ship Country' width='100'/>
          </ColumnsDirective>
      </GridComponent>
      </div>)
  }
};
```

{% endtab %}

## ValueAccessor

The [`valueAccessor`](../api/grid/column/#valueaccessor) is used to access/manipulate the value of display data.
You can achieve custom value formatting by using [`valueAccessor`](../api/grid/column/#valueaccessor).

{% tab template="grid/column", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { getValue } from '@syncfusion/ej2-base';
import { Column, ColumnDirective, ColumnsDirective, GridComponent } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data as datasource } from './datasource';

export default class App extends React.Component<{}, {}>{

  public currencyFormatter(field: string, data: object, column: Column){
    return '€' + getValue('Freight', data);
  }

  public valueAccess(field: string, data: object, column: Column){
      return data[field] + '-' + getValue('ShipRegion', data);
  }

  public render() {
    this.valueAccess = this.valueAccess.bind(this);
    this.currencyFormatter = this.currencyFormatter.bind(this);
      return (<div>
      <GridComponent dataSource={datasource} height={315} >
          <ColumnsDirective>
              <ColumnDirective field='OrderID' headerText='Order ID' width='100' textAlign="Right"/>
              <ColumnDirective field='CustomerID' headerText='Customer ID' width='100'/>
              <ColumnDirective field='EmployeeID' headerText='Employee ID' width='100' textAlign="Right"/>
              <ColumnDirective field='Freight' headerText='Freight' width='80' textAlign="Right" valueAccessor={this.currencyFormatter} />
              <ColumnDirective field='ShipCountry' headerText='Ship Country' width='100' valueAccessor={this.valueAccess} />
          </ColumnsDirective>
      </GridComponent>
      </div>)
  }
};
```

{% endtab %}

### Display Array type Columns

You can bind an Array of Objects in a column by using [`valueAccessor`](../api/grid/column/#valueaccessor) property.
In this example, the **Name** field has an **array** of two objects **FirstName** and **LastName**. These two objects are joined and bind to a column using [`valueAccessor`](../api/grid/column/#valueaccessor).

{% tab template="grid/array-of-string", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { Column, ColumnDirective, ColumnsDirective, GridComponent } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { stringData } from './datasource';

export default class App extends React.Component<{}, {}>{
  public valueAccess(field: string, data: object, column: Column){
    return data[field].map((s: any) => {
      return s.LastName || s.FirstName
    }).join(' ');
  }

  public render() {
      this.valueAccess = this.valueAccess.bind(this);
      return (<div>
        <GridComponent dataSource={stringData} height={315} >
            <ColumnsDirective>
                <ColumnDirective field='EmployeeID' headerText='Employee ID' width='120' textAlign="Right"/>
                <ColumnDirective field='Name' headerText='Full Name' width='120' valueAccessor={this.valueAccess}/>
                <ColumnDirective field='Title' headerText='Title' width='160' textAlign="Right"/>
            </ColumnsDirective>
        </GridComponent>
      </div>)
  }
};
```

{% endtab %}

### Expression Column

You can achieve the expression column by using [`valueAccessor`](../api/grid/column/#valueaccessor) property.

{% tab template="grid/expression", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { Column, ColumnDirective, ColumnsDirective, GridComponent } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { foodInformation } from './datasource';

export default class App extends React.Component<{}, {}>{
  public totalCalories (field: string, data: { Protein: number, Fat: number, Carbohydrate: number }, column: Column): number {
    return data.Protein * 4 + data.Fat * 9 + data.Carbohydrate * 4;
  };

  public render() {
    this.totalCalories = this.totalCalories.bind(this);
      return <GridComponent dataSource={foodInformation} height={315}>
              <ColumnsDirective>
                  <ColumnDirective field='FoodName' width='100' />
                  <ColumnDirective field='Protein' width='90' textAlign="Right" />
                  <ColumnDirective field='Fat' width='90' textAlign="Right"/>
                  <ColumnDirective field='Carbohydrate' width='100' textAlign="Right"/>
                  <ColumnDirective headerText='Calories In Take' width='140'  textAlign="Right" valueAccessor= {this.totalCalories}/>
              </ColumnsDirective>
      </GridComponent>
  }
};
```

{% endtab %}

## Render boolean value as checkbox

To render boolean values as checkbox in columns, you need to set [`displayAsCheckBox`](../api/grid/column/#displayascheckbox) property as **true**.

{% tab template="grid/column", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public render() {
    return <GridComponent dataSource={data} height={315}>
        <ColumnsDirective>
            <ColumnDirective field='OrderID' headerText='Order ID' width='100' textAlign="Right"/>
            <ColumnDirective field='CustomerID' headerText='Customer ID' width='120'/>
            <ColumnDirective field='Freight' headerText='Freight' width='120' format="C2" textAlign="Right"/>
            <ColumnDirective field='ShipCountry' headerText='Ship Country' width='150'/>
            <ColumnDirective field='Verified' headerText='Verified' displayAsCheckBox={true} width='150'/>
        </ColumnsDirective>
    </GridComponent>
  }
};
```

{% endtab %}

## See Also

* [How to Change Column Header Text Dynamically](./how-to/change-header-text-dynamically)
* [Customize Column Styles](./how-to/customize-column-styles)
* [Custom Tooltip for Columns](how-to/custom-tool-tip-for-columns)
* [How to Render Other Component in a Column](how-to/render-react-component-in-column)
* [How to change the Orientation of Header Text](./how-to/change-orientation-of-header-text)
* [Group Column by Format](./grouping#group-by-format)
* [How to Use Edit Template in Foreign Key Column](./how-to/use-edit-template-in-foreign-key-column)
* [How to Create and use custom Filter UI in Foreign Key Column](./how-to/customize-filter-ui-in-foreign-key)
* [How to Use Filter Bar Template in Foreign Key Column](./how-to/use-filter-bar-template-in-foreign-key-column)
* [How to Perform aggregation in Foreign Key Column](./how-to/perform-aggregation-in-foreign-key-column)
* [How to set complex column as Foreignkey column](./how-to/complex-column-as-foreign-key-column)
* [Complex Data Binding with list of Array Of Objects](./how-to/list-of-array-of-objects)
* [How to render the color picker component on React Grid](https://www.syncfusion.com/forums/163831/how-to-render-the-color-picker-component-on-react-grid)