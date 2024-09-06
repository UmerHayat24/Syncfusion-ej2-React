---
title: "Hierarchical Binding"
component: "Grid"
description: "Learn how to display master-detail data in the Essential JS 2 DataGrid control in a hierarchical manner."
---

# Hierarchical Binding

The Grid allows display of table data in a hierarchical structure to visualize relations between parent and child records.
This feature is enabled by defining the [`childGrid`](../api/grid/#childgrid) and
[`childGrid.queryString`](../api/grid/#querystring). The [`childGrid`](../api/grid/#childgrid)
describes the options of grid and the [`childGrid.queryString`](../api/grid/#querystring)
describes the relation between parent and child grids.

To use hierarchical binding, inject the [`DetailRow`](../api/grid/detailRow/) module in the grid.

{% tab template="grid/hierarchy-grid", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent } from '@syncfusion/ej2-react-grids';
import { DetailRow, GridModel, Inject } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data, employeeData } from './datasource';

export default class App extends React.Component<{}, {}>{
  public childGridOptions : GridModel = {
    columns: [
      { field: 'OrderID', headerText: 'Order ID', textAlign: 'Right', width: 120 },
      { field: 'CustomerID', headerText: 'Customer ID', width: 150 },
      { field: 'ShipCity', headerText: 'Ship City', width: 150 },
      { field: 'ShipName', headerText: 'Ship Name', width: 150 }
    ],
    dataSource: data,
    queryString: 'EmployeeID'
  };

  public render(){
    return <GridComponent  dataSource={employeeData} childGrid={this.childGridOptions} height={315}>
              <ColumnsDirective>
                <ColumnDirective field='EmployeeID' headerText='Employee ID' width='120' textAlign='Right'/>
                <ColumnDirective field='FirstName' headerText='First Name' width='150'/>
                <ColumnDirective field='City' headerText='City' width='150'/>
                <ColumnDirective field='Country' headerText='Country' width='150'/>
            </ColumnsDirective>
            <Inject services={[DetailRow]}/>
          </GridComponent >
  }
};
```

{% endtab %}

> * Grid supports n levels of child grids.
> * Hierarchical Binding is not supported when [`DetailTemplate`](../api/grid/#detailtemplate) is enabled.

## ExpandAll by external Button

By default, grid renders in collapsed state.
You can expand all child grid rows by invoking the [`expandAll`](../api/grid/detailRow/#expandall) method and collapse all grid rows by invoking
the [`collapseAll`](../api/grid/detailRow/#collapseall) through an external button.

{% tab template="grid/hierarchy-grid", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { ColumnDirective, ColumnsDirective, GridComponent } from '@syncfusion/ej2-react-grids';
import { DetailRow, Grid, GridModel, Inject } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data, employeeData } from './datasource';

export default class App extends React.Component<{}, {}>{
  public grid: Grid | null;
  public inputStyle : object = {
    display: 'inline-block',
    width:'200px'
  };
  public childGridOptions : GridModel = {
    columns: [
        { field: 'OrderID', headerText: 'Order ID', textAlign: 'Right', width: 120 },
        { field: 'CustomerID', headerText: 'Customer ID', width: 150 },
        { field: 'ShipCity', headerText: 'Ship City', width: 150 },
        { field: 'ShipName', headerText: 'Ship Name', width: 150 }
    ],
    dataSource: data,
    queryString: 'EmployeeID'
  };

  public collapseHandler(){
    if (this.grid) {
      this.grid.detailRowModule.collapseAll();
    }
  }

  public expandHandler(){
    if (this.grid) {
      this.grid.detailRowModule.expandAll();
    }
  }
  public render(){
      this.expandHandler = this.expandHandler.bind(this);
      this.collapseHandler = this.collapseHandler.bind(this);
      return (<div>
      <ButtonComponent onClick= { this.expandHandler }>ExpandAll</ButtonComponent>
      <ButtonComponent onClick= { this.collapseHandler }>CollapseAll</ButtonComponent>
      <GridComponent  dataSource={employeeData} childGrid={this.childGridOptions} height={265}
          ref={g => this.grid = g}>
        <ColumnsDirective>
          <ColumnDirective field='EmployeeID' headerText='Employee ID' width='120' textAlign="Right"/>
          <ColumnDirective field='FirstName' headerText='First Name' width='150'/>
          <ColumnDirective field='City' headerText='City' width='150'/>
          <ColumnDirective field='Country' headerText='Country' width='150'/>
        </ColumnsDirective>
        <Inject services={[DetailRow]}/>
      </GridComponent></div>)
  }
};
```

{% endtab %}

## Expand Child Grid Initially

You can expand a particular Child Grid at initial rendering by invoking the [`expand`](../api/grid/detailRow/#expand) method in [`dataBound`](../api/grid/#databound) event.

{% tab template="grid/hierarchy-grid", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent } from '@syncfusion/ej2-react-grids';
import { DetailRow, Grid, GridModel, Inject } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data, employeeData } from './datasource';

export default class App extends React.Component<{}, {}>{
  public grid: Grid | null;
  public childGridOptions : GridModel = {
    columns: [
        { field: 'OrderID', headerText: 'Order ID', textAlign: 'Right', width: 120 },
        { field: 'CustomerID', headerText: 'Customer ID', width: 150 },
        { field: 'ShipCity', headerText: 'Ship City', width: 150 },
        { field: 'ShipName', headerText: 'Ship Name', width: 150 }
    ],
    dataSource: data,
    queryString: 'EmployeeID'
  };
  
  public onDataBound() {
    if (this.grid) {
      /** Initially expand first chid Grid. */
      this.grid.detailRowModule.expand(0);
    }
  }

  public render(){
      this.onDataBound = this.onDataBound.bind(this);
      return (<div>
      <GridComponent  dataSource={employeeData} childGrid={this.childGridOptions} height={265}
          ref={g => this.grid = g} dataBound={this.onDataBound}>
        <ColumnsDirective>
          <ColumnDirective field='EmployeeID' headerText='Employee ID' width='120' textAlign="Right"/>
          <ColumnDirective field='FirstName' headerText='First Name' width='150'/>
          <ColumnDirective field='City' headerText='City' width='150'/>
          <ColumnDirective field='Country' headerText='Country' width='150'/>
        </ColumnsDirective>
        <Inject services={[DetailRow]}/>
      </GridComponent></div>)
  }
};
```

{% endtab %}

## Dynamically Load Child Grid Data

You can Dynamically load child Grid dataSource by using [`load`](../api/grid/#load) event. This [`load`](../api/grid/#load) event triggers while expand the child Grid at first time.

{% tab template="grid/hierarchy-grid", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent } from '@syncfusion/ej2-react-grids';
import { DetailRow, Grid, GridModel, Inject } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data, employeeData } from './datasource';

export default class App extends React.Component<{}, {}>{
  public grid: Grid | null;
  public childGridOptions : GridModel = {
    columns: [
        { field: 'OrderID', headerText: 'Order ID', textAlign: 'Right', width: 120 },
        { field: 'CustomerID', headerText: 'Customer ID', width: 150 },
        { field: 'ShipCity', headerText: 'Ship City', width: 150 },
        { field: 'ShipName', headerText: 'Ship Name', width: 150 }
    ],
    queryString: 'EmployeeID'
  };
  

  public onLoad() {
    /** Assigning data source for child Grid */
    this.childGridOptions.dataSource = data;
  }

  public render(){
      this.onLoad = this.onLoad.bind(this);
      return (<div>
      <GridComponent  dataSource={employeeData} childGrid={this.childGridOptions} height={265}
          ref={g => this.grid = g} load={this.onLoad}>
        <ColumnsDirective>
          <ColumnDirective field='EmployeeID' headerText='Employee ID' width='120' textAlign="Right"/>
          <ColumnDirective field='FirstName' headerText='First Name' width='150'/>
          <ColumnDirective field='City' headerText='City' width='150'/>
          <ColumnDirective field='Country' headerText='Country' width='150'/>
        </ColumnsDirective>
        <Inject services={[DetailRow]}/>
      </GridComponent></div>)
  }
};
```

{% endtab %}

## Bind hierarchy grid with different field

By default, Parent and child grid relation will be maintained by **queryString** property. We should use the same field name to map both parent and child grid. To achieve parent and child relation with different fields, we need to change the mapping value in the child grid [`load`](../api/grid/#load) event.

In the below sample, we have bound the child and parent grid with different fields. Parent grid field name as **EmployeeID** and the child grid field name as **ID**. We need to define the mapping value of **parentKeyFieldValue** from the parent row data in the child grid **load** event.

{% tab template="grid/hierarchy-grid", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent } from '@syncfusion/ej2-react-grids';
import { DetailRow, Grid, GridModel, Inject } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { childdata, employeeData } from './datasource';

export default class App extends React.Component<{}, {}>{
  public grid: Grid | null;
  public childGridOptions : GridModel = {
    columns: [
      { field: 'OrderID', headerText: 'Order ID', textAlign: 'Right', width: 120 },
      { field: 'CustomerID', headerText: 'Customer ID', width: 150 },
      { field: 'ShipCity', headerText: 'Ship City', width: 150 },
      { field: 'ShipName', headerText: 'Ship Name', width: 150 }
    ],
    dataSource: childdata,
    load() {
      const str: string = 'EmployeeID';
      (this as any).parentDetails.parentKeyFieldValue =
        (this as any).parentDetails.parentRowData[str];
    },
    queryString: 'ID'
  };

  public render(){
      return (<div>
      <GridComponent  dataSource={employeeData} childGrid={this.childGridOptions} height={265}
          ref={g => this.grid = g} >
        <ColumnsDirective>
          <ColumnDirective field='EmployeeID' headerText='Employee ID' width='120' textAlign='Right'/>
          <ColumnDirective field='FirstName' headerText='First Name' width='150'/>
          <ColumnDirective field='City' headerText='City' width='150'/>
          <ColumnDirective field='Country' headerText='Country' width='150'/>
        </ColumnsDirective>
        <Inject services={[DetailRow]}/>
      </GridComponent></div>)
  }
};
```

{% endtab %}

## Adding Record in ChildGrid

Parent and child grid are related by [`queryString`](../api/grid/#querystring) field value.
To maintain this relation in newly added record, You need to set value for [`queryString`](../api/grid/#querystring) field in the added data by the [`actionBegin`](../api/grid/#actionbegin) event.

In the below demo, **EmployeeID** field relates the parent and child grids. To add a new record in child grid, We have to set the **EmployeeID** field with parent record's [`queryString`](../api/grid/#querystring) field value in the [`actionBegin`](../api/grid/#actionbegin) event.

{% tab template="grid/hierarchy-grid", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { setValue } from '@syncfusion/ej2-base';
import { ColumnDirective, ColumnsDirective, GridComponent } from '@syncfusion/ej2-react-grids';
import { AddEventArgs, DetailRow, Edit, GridModel, Inject, Toolbar } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data, employeeData } from './datasource';

export default class App extends React.Component<{}, {}>{
  public childGridOptions : GridModel = {
    actionBegin(args: AddEventArgs) {
      if (args.requestType === "add") {
        /** parentKeyFieldValue refers to the queryString field value of the parent record. */
        setValue('EmployeeID', (this as any).parentDetails.parentKeyFieldValue, (args.data as object));
       }
    },
    columns: [
        { field: 'OrderID', headerText: 'Order ID', isPrimaryKey:true, textAlign: 'Right', width: 120 },
        { field: 'EmployeeID', headerText: 'Employee ID', textAlign: 'Right', allowEditing:false, width: 120 },
        { field: 'ShipCity', headerText: 'Ship City', width: 150 },
        { field: 'ShipName', headerText: 'Ship Name', width: 150 }
    ],
    dataSource: data,
    editSettings: { allowEditing: true, allowAdding: true, allowDeleting: true },
    queryString: 'EmployeeID',
    toolbar: ['Add', 'Edit', 'Delete', 'Update', 'Cancel'],
  };

  public render(){
    return <GridComponent dataSource={employeeData} childGrid={this.childGridOptions} height={315}>
              <ColumnsDirective>
                <ColumnDirective field='EmployeeID' headerText='Employee ID' width='120' textAlign="Right"/>
                <ColumnDirective field='FirstName' headerText='First Name' width='150'/>
                <ColumnDirective field='City' headerText='City' width='150'/>
                <ColumnDirective field='Country' headerText='Country' width='150'/>
            </ColumnsDirective>
            <Inject services={[DetailRow, Edit, Toolbar]}/>
        </GridComponent >
  }
};
```

{% endtab %}
