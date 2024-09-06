---
title: "State Persistence"
component: "Grid"
description: "Learn how to persist the DataGrid state and model in the browser’s local storage."
---

# State Persistence

State persistence refers to the Grid's state maintained in the browser's [`localStorage`](https://www.w3schools.com/html/html5_webstorage.asp#) even if the browser is refreshed or if you move to the next page within the browser.
State persistence stores grid’s model object in the local storage when the [`enablePersistence`](../api/grid/#enablepersistence) is defined as true.

## Maintaining Custom Query in State Persistence

The grid does not maintain the query params after page load event when the [`enablePersistence`](../api/grid/#enablepersistence) is set to true.
This is because the grid refreshes its query params for every page load. You can maintain the custom query params by resetting the [`addParams`](https://ej2.syncfusion.com/documentation/api/data/query/#addparams) method of Grid [`query`](../api/grid/#query) in the [`actionBegin`](../api/grid/#actionbegin) event.

{% tab template="grid/column", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent } from '@syncfusion/ej2-react-grids';
import { ActionEventArgs, Filter, Grid, Inject, Page  } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  private grid: Grid | null;
  public actionHandler(args: ActionEventArgs){
    if (this.grid) {
      this.grid.query.addParams('$filter', 'EmployeeID eq 1');
    }
  }

  public render() {
      this.actionHandler = this.actionHandler.bind(this);
      return <GridComponent dataSource={data} allowFiltering={true} allowPaging={true} enablePersistence={true} height={230}
      actionBegin={this.actionHandler} ref={g => this.grid = g}>
          <ColumnsDirective>
              <ColumnDirective field='OrderID' width='100' textAlign="Right"/>
              <ColumnDirective field='CustomerID' width='100'/>
              <ColumnDirective field='EmployeeID' width='100' textAlign="Right"/>
              <ColumnDirective field='Freight' width='100' format="C2" textAlign="Right"/>
              <ColumnDirective field='ShipCountry' width='100'/>
          </ColumnsDirective>
          <Inject services={[Filter, Page]} />
      </GridComponent>
  }
};
```

{% endtab %}

## How to get or set localStorage value

If the [`enablePersistence`](../api/grid/#enablepersistence) property is set to **true**, the grid property value is saved in the **window.localStorage** for reference.
You can get/set the localStorage value by using the **getItem/setItem** method in the **window.localStorage**.

```typescript
    /** get the Grid model
     * "gridGrid" is component name + component id
     */
    const value: string = window.localStorage.getItem('gridGrid');
    const model: object = JSON.parse(value);
```

```typescript
  /** set the Grid model
   * "gridGrid" is component name + component id
   */
  window.localStorage.setItem('gridGrid', JSON.stringify(model));
```

## Restore initial Grid state

When the [`enablePersistence`](../api/grid/#enablepersistence) property is set to **true**, the Grid will keep its state even if the page is reloaded. In some cases, you may be required to retain the Grid in its initial state. The Grid will not retain its initial state now since the [`enablePersistence`](../api/grid/#enablepersistence) property has been enabled.

You can achieve this by destroying the grid after disabling the [`enablePersistence`](../api/grid/#enablepersistence) property and clearing the local storage data, as shown in the sample below.

{% tab template="grid/column", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent } from '@syncfusion/ej2-react-grids';
import { ActionEventArgs, Filter, Grid, Inject, Page  } from '@syncfusion/ej2-react-grids';
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  private grid: Grid | null;
  public clickHandler(){
      this.grid.enablePersistence = false;
      window.localStorage.setItem("gridGrid", "");
      this.grid.destroy();
      //reloads the page
      location.reload();
  }
  public render() {
      this.clickHandler = this.clickHandler.bind(this);
      return( <div> <ButtonComponent onClick= { this.clickHandler }>Restore to initial state</ButtonComponent> <GridComponent id="Grid" dataSource={data} allowFiltering={true} allowPaging={true} enablePersistence={true} height={230}
      ref={g => this.grid = g}>
          <ColumnsDirective>
              <ColumnDirective field='OrderID' width='100' textAlign="Right"/>
              <ColumnDirective field='CustomerID' width='100'/>
              <ColumnDirective field='EmployeeID' width='100' textAlign="Right"/>
              <ColumnDirective field='Freight' width='100' format="C2" textAlign="Right"/>
              <ColumnDirective field='ShipCountry' width='100'/>
          </ColumnsDirective>
          <Inject services={[Filter, Page]} />
      </GridComponent></div>)
  }
};
```

{% endtab %}

## How to add a new column while using enablePersistence

The Grid columns can be persisted when the [enablePersistence](../api/grid/#enablepersistence) property is set to true. If you want to add the new columns with the existing persist state, you can use the Grid inbuilt method such as `column.push` and call the [refreshColumns()](../api/grid/#refreshcolumns) method for UI changes. Please refer to the following sample for more information.

{% tab template="grid/column", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent } from '@syncfusion/ej2-react-grids';
import { Grid, Inject, Page  } from '@syncfusion/ej2-react-grids';
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  private grid: Grid | null;
  public addColumn(){
    let obj = { field: "Freight", headerText: 'Freight', width: 120 };
    this.grid.columns.push(obj as any); //you can add the columns by using the Grid columns method
    this.grid.refreshColumns();
  }
  public render() {
      this.addColumn = this.addColumn.bind(this);
      return( <div> <ButtonComponent onClick= { this.addColumn }>Add Columns</ButtonComponent>
      <GridComponent id="Grid" dataSource={data} allowPaging={true} enablePersistence={true} height={230}
      ref={g => this.grid = g}>
          <ColumnsDirective>
              <ColumnDirective field='OrderID' width='100' textAlign="Right"/>
              <ColumnDirective field='CustomerID' width='100'/>
              <ColumnDirective field='EmployeeID' width='100' textAlign="Right"/>
              <ColumnDirective field='Freight' width='100' format="C2" textAlign="Right"/>
              <ColumnDirective field='ShipCountry' width='100'/>
          </ColumnsDirective>
          <Inject services={[Page]} />
      </GridComponent></div>)
  }
};
```

{% endtab %}

## How to prevent columns from persisting

When the [enablePersistence](../api/grid/#enablepersistence) property is set to true, the Grid properties such as [Grouping](../api/grid/groupSettingsModel/), [Paging](../api/grid/pageSettingsModel/), [Filtering](../api/grid/pageSettingsModel/), [Sorting](../api/grid/sortSettingsModel/), and [Columns](../api/grid/columnModel/) will persist. You can use the `addOnPersist` method to prevent these Grid properties from persisting.

The following example demonstrates how to prevent Grid columns from persisting. In the [dataBound](../api/grid/#databound) event of the Grid, you can override the `addOnPersist` method and remove the columns from the key list given for persistence.

>**Note:** When the [enablePersistence](../api/grid/#enablepersistence) property is set to true, the Grid properties such as column template, column formatter, header text, and value accessor will not persist.

{% tab template="grid/column", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent } from '@syncfusion/ej2-react-grids';
import { Grid, Inject, Page  } from '@syncfusion/ej2-react-grids';
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  private grid: Grid | null;
  public dataBound(){
    let cloned =  this.grid.addOnPersist;
    this.grid.addOnPersist = function (key: any) {
        key = key.filter((item: string)  => item !== "columns");
        return cloned.call(this, key);
    };
  }
  public addColumn(){
    let obj = { field: "Freight", headerText: 'Freight', width: 120 };
    this.grid.columns.push(obj as any); //you can add the columns by using the Grid columns method
    this.grid.refreshColumns();
  }
  public removeColumn(){
    this.grid.columns.pop();
    this.grid.refreshColumns();
  }
  public render() {
      this.dataBound = this.dataBound.bind(this);
      this.addColumn = this.addColumn.bind(this);
      this.removeColumn = this.removeColumn.bind(this);
      return( <div> <ButtonComponent onClick= { this.addColumn }>Add Columns</ButtonComponent>
      <ButtonComponent onClick= { this.removeColumn }>Remove Columns</ButtonComponent><GridComponent id="Grid" dataSource={data} allowPaging={true} enablePersistence={true} dataBound={this.dataBound} height={230}
      ref={g => this.grid = g}>
          <ColumnsDirective>
              <ColumnDirective field='OrderID' width='100' textAlign="Right"/>
              <ColumnDirective field='CustomerID' width='100'/>
              <ColumnDirective field='EmployeeID' width='100' textAlign="Right"/>
              <ColumnDirective field='Freight' width='100' format="C2" textAlign="Right"/>
              <ColumnDirective field='ShipCountry' width='100'/>
          </ColumnsDirective>
          <Inject services={[Page]} />
      </GridComponent></div>)
  }
};
```

{% endtab %}

## Persist the Grid column template, header template, and headerText

By default, the Grid properties such as column template, header text, header template, column formatter, and value accessor will not persist when [enablePersistence](../api/grid/#enablepersistence) is set to true. Because the column template and header text can be customized at the application level.

If you wish to restore all these column properties, then you can achieve it by cloning the grid’s columns property using JavaScript Object’s assign method and storing this along with the persist data manually. While restoring the settings, this column object must be assigned to the grid’s columns property to restore the column settings as demonstrated in the following sample.

{% tab template="grid/column", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent } from '@syncfusion/ej2-react-grids';
import { ActionEventArgs, Filter, Grid, Inject, Page  } from '@syncfusion/ej2-react-grids';
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  private grid: Grid | null;
  public clickHandler(){
    let savedProperties = JSON.parse(this.grid.getPersistData());
    let gridColumnsState = Object.assign([], this.grid.getColumns());
    savedProperties.columns.forEach((col: {
        field: any;
        headerText: any;
        template: any;
        headerTemplate: any;
    }) => {
        let headerText = gridColumnsState.find((colColumnsState) => colColumnsState.field === col.field)['headerText'];
        let colTemplate = gridColumnsState.find((colColumnsState) => colColumnsState.field === col.field)['template'];
        let headerTemplate = gridColumnsState.find((colColumnsState) => colColumnsState.field === col.field)['headerTemplate'];
        col.headerText = 'Text Changed';
        col.template = colTemplate;
        col.headerTemplate = headerTemplate; //likewise you can restore required column properties as per your wants.
    }
  );
    console.log(savedProperties);
    this.grid.setProperties(savedProperties);
  }
  public headerTemplate: any = this.customerTemplate;
  public customerTemplate(props: any): any {
     return (<div>
          <span className="e-icons e-header" ></span>Customer ID
       </div>);
  }
  public columnTemplate: any = this.gridTemplate;
  public gridTemplate(props: any): any {
      return (<div>
          <a rel='nofollow' href="https://en.wikipedia.org/wiki/${ShipCountry}"><span className="e-icons e-column"></span></a>
        </div>);
  }
  public render() {
      this.clickHandler = this.clickHandler.bind(this);
      return( <div> <ButtonComponent onClick= { this.clickHandler }>Restore</ButtonComponent> <GridComponent id="Grid" dataSource={data} allowFiltering={true} allowPaging={true} enablePersistence={true} height={230}
      ref={g => this.grid = g}>
          <ColumnsDirective>
              <ColumnDirective field='OrderID' width='100' textAlign="Right"/>
              <ColumnDirective field='CustomerID' width='100'  headerTemplate={this.headerTemplate}/>
              <ColumnDirective field='EmployeeID' width='100' textAlign="Right"/>
              <ColumnDirective field='Freight' width='100' format="C2" textAlign="Right"/>
              <ColumnDirective field='ShipCountry' width='100' template={this.columnTemplate} />
          </ColumnsDirective>
          <Inject services={[Filter, Page]} />
      </GridComponent></div>)
  }
};
```

{% endtab %}

## See Also

* [How to get persisted data in React Grid](https://www.syncfusion.com/forums/145524/how-to-get-persisted-data-in-react-grid)
* [How to get the Grid settings in React Grid](https://www.syncfusion.com/forums/155698/how-to-get-the-grid-settings-in-react-grid)