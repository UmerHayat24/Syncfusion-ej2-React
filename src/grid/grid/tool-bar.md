---
title: "ToolBar"
component: "Grid"
description: "Learn how to use the toolbar and add custom toolbar items in the Essential JS 2 DataGrid control."
---

# Toolbar

The Grid provides ToolBar support to handle grid actions. The [`toolbar`](../api/grid/#toolbar)
property accepts either the collection of built-in toolbar items and
[`itemModel`](../api/toolbar/itemModel) objects for custom toolbar items or
HTML element ID for toolbar template.

To use Toolbar, inject **Toolbar** module in Grid.

## Built-in Toolbar Items

Built-in toolbar items execute standard actions of the grid, and it can be added by defining the [`toolbar`](../api/grid/#toolbar)
as a collection of built-in items. It renders the button with icon and text.

The following table shows Built-in toolbar items and its action.

| Built-in Toolbar Items | Actions |
|------------------------|---------|
| Add | Adds a new record.|
| Edit | Edits the selected record.|
| Update | Updates the edited record.|
| Delete | Deletes the selected record.|
| Cancel | Cancels the edit state.|
| Search | Searches the records by the given key.|
| Print | Prints the grid.|
| ExcelExport | Exports the grid to Excel.|
| PdfExport | Exports the grid to PDF.|
| WordExport | Exports the grid to Word.|
| ColumnChooser | Shows column chooser dialog |

{% tab template="grid/toolbar", sourceFiles="app/App.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent, Inject, Toolbar, ToolbarItems } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {
  public toolbarOptions: ToolbarItems[] = ['Search', "Print"];
  public render() {
      return <GridComponent dataSource={data} toolbar={this.toolbarOptions} height={270}>
          <ColumnsDirective>
              <ColumnDirective field='OrderID' width='100' textAlign="Right"/>
              <ColumnDirective field='CustomerID' width='100'/>
              <ColumnDirective field='EmployeeID' width='100' textAlign="Right"/>
              <ColumnDirective field='Freight' width='100' format="C2" textAlign="Right"/>
              <ColumnDirective field='ShipCountry' width='100'/>
          </ColumnsDirective>
          <Inject services={[ Toolbar ]} />
      </GridComponent>
  }
}
```

{% endtab %}

> * The [`toolbar`](../api/grid/#toolbar) has options to define both built-in and custom toolbar items.

## Custom Toolbar Items

Custom toolbar items can be added by defining the [`toolbar`](../api/grid/#toolbar) as a collection of [`itemModel`](../api/toolbar/itemModel).
Actions for this customized toolbar items are defined in the [`toolbarClick`](../api/grid/#toolbarclick) event.

By default, Custom toolbar items are in position **Left**. You can change the position by using the [`align`](../api/toolbar/itemModel/#align) property. In the below sample, we have applied position **Right** for the **Collapse All** toolbar item.

{% tab template="grid/toolbar", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent, Inject } from '@syncfusion/ej2-react-grids';
import { Grid, Group, GroupSettingsModel, Toolbar } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {
  public gridInstance: Grid | null;
  public toolbarOptions: object[] = [
    { text: 'Expand All', tooltipText: 'Expand All', prefixIcon: 'e-expand', id: 'expandall' },
    { text: 'Collapse All', tooltipText: 'Collapse All', prefixIcon: 'e-collapse', id: 'collapseall', align:'Right' }
  ];
  public groupOptions: GroupSettingsModel = {
    columns: ['CustomerID']
  };
  public clickHandler(args: any) {
     if (this.gridInstance && args.item.id === 'expandall') {
      this.gridInstance.groupModule.expandAll();
    }
     if(this.gridInstance && args.item.id === "collapseall"){
      this.gridInstance.groupModule.collapseAll();
    }
  }
  public render() {
    this.clickHandler = this.clickHandler.bind(this);
    return <GridComponent dataSource={data} allowGrouping={true} groupSettings ={this.groupOptions}
          toolbar={this.toolbarOptions} toolbarClick={this.clickHandler}
          ref={g => this.gridInstance = g} height={240}>
        <ColumnsDirective>
          <ColumnDirective field='OrderID' width='100' textAlign="Right"/>
          <ColumnDirective field='CustomerID' width='100'/>
          <ColumnDirective field='EmployeeID' width='100' textAlign="Right"/>
          <ColumnDirective field='Freight' width='100' format="C2" textAlign="Right"/>
          <ColumnDirective field='ShipCountry' width='100'/>
        </ColumnsDirective>
        <Inject services={[ Toolbar, Group ]} />
    </GridComponent>
  }
}
```

{% endtab %}

> * The [`toolbar`](../api/grid/#toolbar) has options to define both built-in and custom toolbar items.
> * If a toolbar item does not match with built-in items, it will be treated as custom toolbar item.

## Built-in and custom items in toolbar

Grid have an option to use both built-in and custom toolbar items at same time.

In the below example, **Add**, **Edit**, **Delete**, **Update**, **Cancel** are built-in toolbar items and **Click** is custom toolbar item.

{% tab template="grid/toolbar", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent, Inject } from '@syncfusion/ej2-react-grids';
import { Toolbar } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {
  public toolbarOptions: object[] = [
    { text: 'Add'}, { text: 'Edit'}, { text: 'Delete'}, { text: 'Update'}, { text: 'Cancel'},
    { text: 'Click', tooltipText: 'Click', prefixIcon: 'e-click', id: 'Click' }
  ];
  public clickHandler(args: any) {
     if (args.item.id === 'Click') {
      alert("Custom toolbar Click...");
    }
  }
  public render() {
    this.clickHandler = this.clickHandler.bind(this);
    return <GridComponent dataSource={data} toolbar={this.toolbarOptions}
        toolbarClick={this.clickHandler}  height={240}>
        <ColumnsDirective>
          <ColumnDirective field='OrderID' width='100' textAlign="Right"/>
          <ColumnDirective field='CustomerID' width='100'/>
          <ColumnDirective field='EmployeeID' width='100' textAlign="Right"/>
          <ColumnDirective field='Freight' width='100' format="C2" textAlign="Right"/>
          <ColumnDirective field='ShipCountry' width='100'/>
        </ColumnsDirective>
        <Inject services={[ Toolbar ]} />
    </GridComponent>
  }
}
```

{% endtab %}

## Enable/Disable Toolbar Items

You can enable/disable toolbar items by using the **enableItems** method.

{% tab template="grid/toolbar", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { ColumnDirective, ColumnsDirective, GridComponent, Inject } from '@syncfusion/ej2-react-grids';
import { Grid, Group, GroupSettingsModel, Toolbar } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {
  public grid: Grid | null;
  public toolbarOptions: string[] = ['Expand', 'Collapse'];
  public groupOptions: GroupSettingsModel = {columns: ['CustomerID']};
  public clickHandler(args: any) {
    if (this.grid) {
      /** Grid_Collapse is component id + '_' + toolbar item name */
      if (args.item.id === 'Grid_Expand') {
        this.grid.groupModule.expandAll();
      } else if(args.item.id === "Grid_Collapse"){
        this.grid.groupModule.collapseAll();
      }
    }
  }
  public enable() {
    /** Enable toolbar items */
    if (this.grid) {
      this.grid.toolbarModule.enableItems(['Grid_Collapse','Grid_Expand'],true);
    }
  }

  public disable() {
    /** Disable toolbar items */
    if (this.grid) {
      this.grid.toolbarModule.enableItems(['Grid_Collapse','Grid_Expand'],false);
    }
  }
  public render() {
    this.enable = this.enable.bind(this);
    this.disable = this.disable.bind(this);
    this.clickHandler = this.clickHandler.bind(this);
    return (<div>
      <ButtonComponent className='e-flat' onClick= { this.enable }>Enable</ButtonComponent>
      <ButtonComponent className='e-flat' onClick= { this.disable }>Disable</ButtonComponent>
      <GridComponent id='Grid' dataSource={data} allowGrouping={true}
          groupSettings ={this.groupOptions} toolbar={this.toolbarOptions}
          toolbarClick={this.clickHandler} ref={g => this.grid = g} height={220}>
        <ColumnsDirective>
            <ColumnDirective field='OrderID' width='100' textAlign="Right"/>
            <ColumnDirective field='CustomerID' width='100'/>
            <ColumnDirective field='EmployeeID' width='100' textAlign="Right"/>
            <ColumnDirective field='Freight' width='100' format="C2" textAlign="Right"/>
            <ColumnDirective field='ShipCountry' width='100'/>
        </ColumnsDirective>
      <Inject services={[ Toolbar, Group ]} />
    </GridComponent>
    </div>)
  }
}
```

{% endtab %}

## See Also

[Toolbar Component](../../toolbar/getting-started)