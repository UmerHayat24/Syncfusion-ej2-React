---
title: "Customizing Filter Dialog by using additional Parameter"
component: "Grid"
description: "Learn how to customize the filter dialog in Grid by using an additional Parameter."
---

# Customizing Filter Dialog by using an additional Parameter

You can customize the default settings of the components which are used in Menu filter by using params of filter property in column definition.
In the below sample, OrderID and Freight Columns are numeric columns, while open the filter dialog then you can see that NumericTextBox with spin button is displayed to change/set the filter value. Now using the params option we hide the spin button in NumericTextBox for OrderID Column.

{% tab template="grid/column", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent } from '@syncfusion/ej2-react-grids';
import { Filter, FilterSettingsModel, Grid, IFilter, Inject } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {
  public grid: Grid | null;
  public FilterOptions: FilterSettingsModel = {
     type: 'Menu'
  };
  public ifilter: IFilter = { params: {showSpinButton: false}};
  public render() {
     return <GridComponent ref={g => this.grid = g} dataSource={data} allowFiltering={true}  
          filterSettings={this.FilterOptions} height='315'>
         <ColumnsDirective>
             <ColumnDirective field='OrderID' width='100' filter={this.ifilter} textAlign="Right"/>
             <ColumnDirective field='CustomerID' width='100'/>
             <ColumnDirective field='EmployeeID' width='100' textAlign="Right"/>
             <ColumnDirective field='Freight' width='100' format="C2" textAlign="Right"/>
             <ColumnDirective field='ShipCountry' width='100'/>
         </ColumnsDirective>
         <Inject services={[Filter]} />
     </GridComponent>
 }
};
```

{% endtab %}