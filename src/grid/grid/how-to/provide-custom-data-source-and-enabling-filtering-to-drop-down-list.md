---
title: "Provide custom data source and enabling filtering to DropDownList"
component: "Grid"
description: "Learn how to Provide custom data source and enabling filtering to DropDownList."
---

# Provide custom data source and enabling filtering to DropDownList

You can provide data source to the DropDownList by using the **params** of [`columns.edit`](../../api/grid/column/#edit) property.

While setting new data source using edit params, you must specify a new **query** property for the DropDownList as follows,

```typescript
  public countryParams : IEditCell = {
    params:   {
      actionComplete: () => false,
      allowFiltering: true,
      dataSource: new DataManager(this.country),
      fields: { text: "countryName", value: "countryName"},
      query: new Query()
    }
  };
```

You can also enable filtering for the DropDownList by passing the [`allowFiltering`](../../api/drop-down-list/#allowfiltering) as **true** to the edit params.

In the below demo, DropDownList is rendered with custom [`dataSource`](../../api/drop-down-list/#datasource) for the *ShipCountry* column and enabled filtering to search DropDownList items.

{% tab template="grid/cascade-drop", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { DataManager, Query } from '@syncfusion/ej2-data';
import { ColumnDirective, ColumnsDirective, EditSettingsModel, GridComponent, Inject } from '@syncfusion/ej2-react-grids';
import { Edit, IEditCell, Toolbar, ToolbarItems } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { cascadeData } from './datasource';

export default class App extends React.Component<{}, {}> {
  public editOptions: EditSettingsModel = { allowAdding: true, allowDeleting: true, allowEditing: true  };
  public toolbarOptions: ToolbarItems[] = ['Add', 'Edit', 'Delete', 'Update', 'Cancel'];
  public country: object[] = [
    { countryName: 'United States', countryId: '1' },
    { countryName: 'Australia', countryId: '2' },
    { countryName: 'India', countryId: '3' }
  ];
  public countryParams : IEditCell = {
    params:   {
      actionComplete: () => false,
      allowFiltering: true,
      dataSource: new DataManager(this.country),
      fields: { text: "countryName", value: "countryName"},
      query: new Query()
    }
  };

  public render() {
    return <GridComponent dataSource={cascadeData} editSettings={this.editOptions}
      toolbar={this.toolbarOptions} height={273}>
      <ColumnsDirective>
          <ColumnDirective field='OrderID' headerText='Order ID' width='100' textAlign='Right' isPrimaryKey={true}/>
          <ColumnDirective field='CustomerID' headerText='Customer ID' width='120'/>
          <ColumnDirective field='ShipCountry' headerText='Ship Country' width='150' editType= 'dropdownedit' edit={this.countryParams} textAlign='Right'/>
      </ColumnsDirective>
      <Inject services={[Edit, Toolbar]} />
    </GridComponent>
  }
};
```

{% endtab %}
