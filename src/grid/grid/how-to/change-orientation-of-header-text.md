---
title: "Change the Orientation of Header Text"
component: "Grid"
description: "Learn how to Change the Orientation of Header Text."
---

# Change the Orientation of Header Text

You can change the orientation of the header text by using the [`customAttributes`](../../api/grid/column/#customattributes) property.

Ensure the following steps:

**Step 1**:

Create a css class with orientation style for grid header cell.

```css
.orientationcss .e-headercelldiv {
    transform: rotate(90deg);
}

```

**Step 2**:

Add the custom css class to particular column by using [`customAttributes`](../../api/grid/column/#customattributes) property.

```typescript
    <ColumnDirective field='Freight' headerText='Freight' customAttributes={this.customAttributes} width='80' format="C2" textAlign="Center"/>

```

**Step 3**:

Resize the header cell height by using the following code.

```typescript
  public setHeaderHeight() {
    /** Obtain the width of the headerText content */
    const textWidth: number = (document.querySelector(".orientationcss > div") as HTMLElement).scrollWidth;
    const headerCell: NodeList = document.querySelectorAll(".e-headercell");
    for(let i: number = 0; i < headerCell.length; i++) {
      /** Assign the obtained textWidth as the height of the headerCell */
      ((headerCell as any).item(i)).style.height = textWidth + 'px';
    }
  }

```

{% tab template="grid/header-orientation", sourceFiles="app/App.tsx,app/css/custom.css,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import './custom.css';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {
  private customAttributes: any = { class: 'orientationcss'};
  public setHeaderHeight() {
    /** Obtain the width of the headerText content */
    const textWidth: number = (document.querySelector(".orientationcss > div") as HTMLElement).scrollWidth;
    const headerCell: NodeList = document.querySelectorAll(".e-headercell");
    for(let i: number = 0; i < headerCell.length; i++) {
      /** Assign the obtained textWidth as the height of the headerCell */
      ((headerCell as any).item(i)).style.height = textWidth + 'px';
    }
  }

  public render() {
    this.setHeaderHeight = this.setHeaderHeight.bind(this);
    return (<div>
    <GridComponent dataSource={data} height={260} created={this.setHeaderHeight} >
      <ColumnsDirective>
        <ColumnDirective field='OrderID' headerText='Order ID' width='100' textAlign="Right"/>
        <ColumnDirective field='CustomerID' headerText='Customer ID' width='100'/>
        <ColumnDirective field='EmployeeID' headerText='Employee ID' width='100' textAlign="Right"/>
        <ColumnDirective field='Freight' headerText='Freight' customAttributes={this.customAttributes} width='80' format="C2" textAlign="Center"/>
        <ColumnDirective field='ShipCountry' headerText='Ship Country' width='100'/>
      </ColumnsDirective>
    </GridComponent>
    </div>)
  }
};
```

{% endtab %}
