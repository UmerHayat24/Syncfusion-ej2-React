---
title: "Search"
component: "Grid"
description: "Learn how to search DataGrid content, change search operators, perform searches using external buttons, and search particular fields."
---

# Search

You can search records in a Grid, by using the [`search`](../api/grid/#search) method with search key as a parameter.
This also provides an option to integrate search text box in Grid's toolbar by adding **Search** item to the
[`toolbar`](../api/grid/#toolbar).

To search records, inject the **Search** module in the grid.

{% tab template="grid/searching", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent } from '@syncfusion/ej2-react-grids';
import { Inject, Search, Toolbar, ToolbarItems } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public toolbarOptions: ToolbarItems[] = ['Search'];
  public render() {
      return <GridComponent dataSource={data} toolbar={this.toolbarOptions}
            height={272}>
          <ColumnsDirective>
              <ColumnDirective field='OrderID' width='100' textAlign="Right"/>
              <ColumnDirective field='CustomerID' width='100'/>
              <ColumnDirective field='EmployeeID' width='100' textAlign="Right"/>
              <ColumnDirective field='Freight' width='100' format="C2" textAlign="Right"/>
              <ColumnDirective field='ShipCountry' width='100'/>
          </ColumnsDirective>
          <Inject services={[Search, Toolbar]} />
      </GridComponent>
  }
};
```

{% endtab %}

## Initial search

To apply search at initial rendering, set the [`fields`](../api/grid/searchSettings/#fields), [`operator`](../api/grid/searchSettings/#operator), [`key`](../api/grid/searchSettings/#key), and [`ignoreCase`](../api/grid/searchSettings/#ignorecase) in the [`searchSettings`](../api/grid/#searchsettings).

{% tab template="grid/searching", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent, SearchSettingsModel} from '@syncfusion/ej2-react-grids';
import { Inject, Search, Toolbar, ToolbarItems } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public toolbarOptions: ToolbarItems[] = ['Search'];
  public searchOptions: SearchSettingsModel = {
    fields: ['CustomerID'],
    ignoreCase: true,
    key: 'Ha',
    operator: 'contains'
  };
  public render() {
      return <GridComponent dataSource={data} toolbar={this.toolbarOptions} searchSettings={this.searchOptions}
            height={272}>
          <ColumnsDirective>
              <ColumnDirective field='OrderID' width='100' textAlign="Right"/>
              <ColumnDirective field='CustomerID' width='100'/>
              <ColumnDirective field='EmployeeID' width='100' textAlign="Right"/>
              <ColumnDirective field='Freight' width='100' format="C2" textAlign="Right"/>
              <ColumnDirective field='ShipCountry' width='100'/>
          </ColumnsDirective>
          <Inject services={[Search, Toolbar]} />
      </GridComponent>
  }
};
```

{% endtab %}

> By default, Grid searches all the bound column values. To customize this behavior define the
[`searchSettings.fields`](../api/grid/searchSettings/#fields) property.

## Search operators

The search operator can be defined in the [`searchSettings.operator`](../api/grid/searchSettings/#operator) property to configure specific searching.

The following operators are supported in searching:

Operator |Description
-----|-----
startswith |Checks whether a value begins with the specified value.
endswith |Checks whether a value ends with specified value.
contains |Checks whether a value contains with specified value.
equal |Checks whether a value equal to specified value.
notequal |Checks whether a value not equal to specified value.

## Search by external button

To search grid records from an external button, invoke the [`search`](../api/grid/#search) method.

{% tab template="grid/searching", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { ColumnDirective, ColumnsDirective, Grid, GridComponent } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { employeeData } from './datasource';

export default class App extends React.Component<{}, {}>{
  public grid: Grid | null;
  public inputStyle : object = {width:'200px', display: 'inline-block'};
  public clickHandler() {
    const searchText: string =
      (document.getElementsByClassName('searchtext')[0] as HTMLInputElement).value;
    if (this.grid) {
      this.grid.search(searchText);
    }
  }
  public render() {
      this.clickHandler = this.clickHandler.bind(this);
      return (<div>
                <div className='e-float-input' style={this.inputStyle}>
                    <input type="text" className="searchtext" />
                    <span className="e-float-line"/>
                    <label className="e-float-text">Search text</label>
                </div>
                <ButtonComponent onClick= { this.clickHandler }>Search</ButtonComponent>
                <GridComponent  dataSource={employeeData} height={260} ref={g => this.grid = g}>
                  <ColumnsDirective>
                    <ColumnDirective field='EmployeeID' headerText='Employee ID' width='120' textAlign='Right'/>
                    <ColumnDirective field='FirstName' headerText='First Name' width='150'/>
                    <ColumnDirective field='City' headerText='City' width='150'/>
                    <ColumnDirective field='Country' headerText='Country' width='150'/>
                  </ColumnsDirective>
                </GridComponent>
              </div>)
  }
};
```

{% endtab %}

## Search Specific Columns

By default, grid searches all visible columns. You can search specific columns by defining the specific column's field names in the [`searchSettings.fields`](../api/grid/searchSettings/#fields) property.

{% tab template="grid/searching", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent } from '@syncfusion/ej2-react-grids';
import { Inject, SearchSettingsModel, Toolbar } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public searchSettings: SearchSettingsModel = {
    fields: ['CustomerID', 'EmployeeID', 'ShipCountry']
  };
  public render() {
      return (<div>
      <GridComponent dataSource={data} height={280} toolbar= {['Search']}
          searchSettings={this.searchSettings}>
          <ColumnsDirective>
              <ColumnDirective field='OrderID' headerText='Order ID' width='100' textAlign="Right"/>
              <ColumnDirective field='CustomerID' headerText='Customer ID' width='100'/>
              <ColumnDirective field='EmployeeID' headerText='Employee ID' width='100' textAlign="Right"/>
              <ColumnDirective field='ShipCountry' headerText='Ship Country' width='100'/>
          </ColumnsDirective>
          <Inject services={[Toolbar]} />
      </GridComponent>
      </div>)
  }
};
```

{% endtab %}

## Clear search by external button

To clear the searched grid records from the external button, set [`searchSettings.key`](../api/grid/searchSettings/#key) property as **empty** string.

{% tab template="grid/searching", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { ColumnDirective, ColumnsDirective, Grid, GridComponent } from '@syncfusion/ej2-react-grids';
import { Inject, Search, SearchSettingsModel, Toolbar, ToolbarItems } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public grid: Grid | null;
  public toolbarOptions: ToolbarItems[] = ['Search'];
  public searchOptions: SearchSettingsModel = {
    fields: ['CustomerID'],
    ignoreCase: true,
    key: 'Ha',
    operator: 'contains'
  };
  public clickHandler(){
    if (this.grid) {
      this.grid.searchSettings.key = '';
    }
  }

  public render(){
    this.clickHandler = this.clickHandler.bind(this);
    return (<div>
    <ButtonComponent onClick= { this.clickHandler }>Clear Search</ButtonComponent>
    <GridComponent  dataSource={data} toolbar={this.toolbarOptions}
          searchSettings={this.searchOptions} height={260} ref={g => this.grid = g}>
        <ColumnsDirective>
            <ColumnDirective field='OrderID' width='100' textAlign="Right"/>
            <ColumnDirective field='CustomerID' width='100'/>
            <ColumnDirective field='EmployeeID' width='100' textAlign="Right"/>
            <ColumnDirective field='ShipCountry' width='100'/>
        </ColumnsDirective>
        <Inject services={[Search, Toolbar]} />
    </GridComponent></div>)
  }
};
```

{% endtab %}

## Search on each key stroke

You can search the Grid data on each key stroke by binding the `keyup` event for the search input element inside the [`created`](../api/grid/#created) event. Inside the `keyup` handler you can search the Grid by invoking the [`search`](../api/grid/#search) method of the Grid component.

{% tab template="grid/searching", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent } from '@syncfusion/ej2-react-grids';
import { Inject, Toolbar } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public grid: Grid | null;
  public created = () => {
        document.getElementById(this.grid.element.id + "_searchbar").addEventListener('keyup', () => {
          this.grid.search((event.target as HTMLInputElement).value)
        });
    }
  public render() {
      return (<div>
      <GridComponent dataSource={data} height={280} toolbar= {['Search']}
          ref={g => this.grid = g} created={this.created}>
          <ColumnsDirective>
              <ColumnDirective field='OrderID' headerText='Order ID' width='100' textAlign="Right"/>
              <ColumnDirective field='CustomerID' headerText='Customer ID' width='100'/>
              <ColumnDirective field='EmployeeID' headerText='Employee ID' width='100' textAlign="Right"/>
              <ColumnDirective field='ShipCountry' headerText='Ship Country' width='100'/>
          </ColumnsDirective>
          <Inject services={[Toolbar]} />
      </GridComponent>
      </div>)
  }
};
```

{% endtab %}
