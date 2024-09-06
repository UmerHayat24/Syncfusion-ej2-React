---
title: "Restrict to type decimal points in a NumericTextBox while editing the numeric column"
component: "TreeGrid"
description: "Learn how restrict to type decimal points in a NumericTextBox while editing the numeric column."
---

# Restrict to type decimal points in a NumericTextBox while editing the numeric column

By default, the number of decimal places will be restricted to two in the NumericTextBox while editing the numeric column. We can restrict to type the decimal points in a NumericTextBox by using the **validateDecimalOnType** and **decimals** properties of NumericTextBox.

In the below demo, while editing the row we have restricted to type the decimal point value in the NumericTextBox of **Progress** column.

{% tab template="treegrid/customizedialog", sourceFiles="app/App.tsx,app/datasource.tsx", compileJsx=true %}

```typescript

import * as React from 'react';
import { stackedData } from './datasource';
import { ColumnsDirective, ColumnDirective, TreeGridComponent, Inject } from '@syncfusion/ej2-react-treegrid';
import { Edit, Toolbar, ToolbarItems, EditSettingsModel, Page, TreeGrid } from '@syncfusion/ej2-react-treegrid';
import { IEditCell } from '@syncfusion/ej2-react-grids';

/* tslint:disable */

export default class App extends React.Component {

  public editOptions: EditSettingsModel = { allowEditing: true, allowAdding: true, allowDeleting: true, mode: 'Row' };
  public toolbarOptions: ToolbarItems[] = ['Add', 'Edit', 'Delete'];
  public treegrid: TreeGrid | null;

  public numericParams: IEditCell = {
    params: {
      decimals: 0,
      format: "N",
      validateDecimalOnType: true
    }
  };

  public render() {
    return (
      <TreeGridComponent dataSource={stackedData} treeColumnIndex={1} childMapping='subtasks'
       editSettings={this.editOptions} toolbar={this.toolbarOptions} height={265}
       ref={g => this.treegrid = g}>
        <ColumnsDirective>
          <ColumnDirective field='orderID' headerText='Order ID' width='70' textAlign='Right' isPrimaryKey={true}></ColumnDirective>
          <ColumnDirective field='orderName' headerText='Order Name' width='100'></ColumnDirective>
          <ColumnDirective field='orderDate' headerText='Order Date' width='100' format='yMd' textAlign='Right' editType='datepickeredit'></ColumnDirective>
          <ColumnDirective field='price' headerText='price' edit= {this.numericParams} editType= 'numericedit' width='90' format='c2' textAlign='Right' />
        </ColumnsDirective>
        <Inject services={[Edit, Toolbar, Page]} />
      </TreeGridComponent>
    );
  }
};
```

{% endtab %}