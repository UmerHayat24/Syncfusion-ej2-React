---
title: "Using Tab Inside the Dialog Editing"
component: "Grid"
description: "Learn how to Using Tab Inside the Dialog Editing."
---

# Using Tab Inside the Dialog Editing

You can use [`tab`](../../../tab) component inside dialog edit UI using dialog template feature. The dialog template feature can be enabled by defining  [`editSettings.mode`](../../api/grid/editSettings/#mode) as `Dialog` and [`editSetting.template`](../../api/grid/editSettings/#template) as a REACT Component.

The following example demonstrate the usage of tab control inside the dialog template.

{% tab template="grid/tabediting", sourceFiles="app/App.tsx,app/wizardTab.tsx,app/orderModel.tsx,app/tabOne.tsx,app/tabTwo.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, Edit } from '@syncfusion/ej2-react-grids';
import { EditSettingsModel, Grid, GridComponent, Inject, Toolbar, ToolbarItems } from '@syncfusion/ej2-react-grids';
import * as React from "react";
import { data } from './datasource';
import { IOrderModel } from './orderModel';
import { DialogFormTemplate} from './wizardTab';

export default class App extends React.Component<{}, {}>{
    public editOptions: EditSettingsModel = { allowEditing: true, allowAdding: true, allowDeleting: true, mode: 'Dialog', template: this.dialogTemplate.bind(this) };
    public toolbarOptions: ToolbarItems[] = ['Add', 'Edit', 'Delete'];
    public grid: Grid | null;

    public dialogTemplate(props: IOrderModel): any {
      const a = [props, this.grid]
      return (<DialogFormTemplate {...a} />);
    }

    public render() {
      return <GridComponent ref={g=> this.grid = g} dataSource={data} editSettings={this.editOptions}
        toolbar={this.toolbarOptions} height={265}>
        <ColumnsDirective>
          <ColumnDirective field='OrderID' headerText='Order ID' width='100' textAlign="Right" isPrimaryKey={true}/>
          <ColumnDirective field='CustomerID' headerText='Customer ID' width='120'/>
          <ColumnDirective field='ShipCountry' headerText='Ship Country' width='150'/>
        </ColumnsDirective>
        <Inject services={[Edit, Toolbar]}/>
      </GridComponent>
    }
};
```

{% endtab %}
