---
title: "Customize the icon for column menu"
component: "Grid"
description: "Learn how to customize the icon for column menu."
---

# Customize the icon for column menu

You can customize the column menu icon by overriding the default grid class **.e-icons.e-columnmenu** with a custom property **content** as mentioned below,

```css
    .e-grid .e-columnheader .e-icons.e-columnmenu::before {
        content: "\e903";
    }
```

In the below sample, grid is rendered with a customized column menu icon.

{% tab template="grid/custom-column-menu-icon", sourceFiles="app/App.tsx,app/css/custom.css,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnMenu, ColumnsDirective, GridComponent, Inject } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import './custom.css';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {

  public render() {
    return (<div>
    <GridComponent dataSource={data} height={315} showColumnMenu={true} >
      <ColumnsDirective>
        <ColumnDirective field='OrderID' headerText='Order ID' width='100'/>
        <ColumnDirective field='CustomerID' headerText='Customer ID' width='100'/>
        <ColumnDirective field='EmployeeID' headerText='Employee ID' width='100'/>
        <ColumnDirective field='Freight' headerText='Freight' width='100' format="C2"/>
        <ColumnDirective field='ShipCountry' headerText='Ship Country' width='100'/>
      </ColumnsDirective>
      <Inject services={[ColumnMenu]} />
    </GridComponent>
    </div>)
  }
};
```

{% endtab %}