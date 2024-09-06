---
title: "Custom Tooltip for columns"
component: "Grid"
description: "Learn how to Custom Tooltip for columns."
---

# Custom Tooltip for columns

To display a custom ToolTip ([`EJ2 Tooltip`](../../../tooltip/getting-started)), you can render the Grid control inside the Tooltip component and set the target as “.e-rowcell”. The tooltip is displayed when hovering the grid cells.

Change the tooltip content for the grid cells by using the following code in the [`beforeRender`](../../../api/tooltip/#beforerender) event.

```typescript

public beforeRender(args) {
  // event triggered before render the tooltip on target element.
  this.tooltip.content = args.target.closest("td").innerText;
}

```

{% tab template="grid/custom-tooltip", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { getValue } from '@syncfusion/ej2-base';
import { Column, ColumnDirective, ColumnsDirective, GridComponent } from '@syncfusion/ej2-react-grids';
import { TooltipComponent } from '@syncfusion/ej2-react-popups';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {
  public tooltip;  
  public beforeRender(args) {
  // event triggered before render the tooltip on target element.
  this.tooltip.content = args.target.closest("td").innerText;
  }
  public render() {
    return <div>
    <TooltipComponent ref={t => this.tooltip = t} target='.e-rowcell' beforeRender={this.beforeRender.bind(this)}>
      <GridComponent dataSource={data} height={320} ref={g => this.grid = g}>
        <ColumnsDirective>
          <ColumnDirective field='OrderID' headerText='Order ID' width='100' textAlign="Right"/>
          <ColumnDirective field='CustomerID' headerText='Customer ID' width='100'/>
          <ColumnDirective field='EmployeeID' headerText='Employee ID' width='100' textAlign="Right"/>
          <ColumnDirective field='Freight' headerText='Freight' width='100' format="C2" textAlign="Right"/>
          <ColumnDirective field='ShipCountry' headerText='Ship Country' width='100'/>
        </ColumnsDirective>
      </GridComponent>
    </TooltipComponent></div>
  }
};
```

{% endtab %}
