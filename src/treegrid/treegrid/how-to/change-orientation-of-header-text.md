---
title: "Change the Orientation of Header Text"
component: "TreeGrid"
description: "Learn how to Change the Orientation of Header Text."
---

# Change the Orientation of Header Text

You can change the orientation of the header text by using the [`customAttributes`](../api/treegrid/column/#customattributes) property.

Ensure the following steps:

**Step 1**:

Create a css class with orientation style for treegrid header cell.

```css
.orientationcss .e-headercelldiv {
    transform: rotate(90deg);
}

```

**Step 2**:

Add the custom css class to particular column by using [`customAttributes`](../api/treegrid/column/#customattributes) property.

```typescript
    <ColumnDirective field='EndDate' headerText='End Date' width='90' format='yMd' customAttributes={this.customAttributes} textAlign='Center' />

```

**Step 3**:

Resize the header cell height in [`create`](../api/treegrid/#create) event by using the following code.

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

{% tab template="treegrid/header-orientation", sourceFiles="app/App.tsx,app/datasource.tsx,app/custom.css", compileJsx=true %}

```typescript

import * as React from 'react';
import { projectData } from './datasource';
import { ColumnsDirective, ColumnDirective, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';

/* tslint:disable */

export default class App extends React.Component {

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
      <TreeGridComponent dataSource={projectData} treeColumnIndex={1} idMapping= 'TaskID' parentIdMapping='parentID' created={this.setHeaderHeight} height={230}>
        <ColumnsDirective>
          <ColumnDirective field='TaskID' headerText='Task ID' width='70' textAlign='Right'></ColumnDirective>
          <ColumnDirective field='TaskName' headerText='Task Name' width='100'></ColumnDirective>
          <ColumnDirective field='StartDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' />
          <ColumnDirective field='EndDate' headerText='End Date' width='90' format='yMd' customAttributes={this.customAttributes} textAlign='Center' />
          <ColumnDirective field='Duration' headerText='Duration' width='90' textAlign='Right' />
          <ColumnDirective field='Progress' headerText='Progress' width='90' textAlign='Right' />
        </ColumnsDirective>
      </TreeGridComponent>
      </div>
    );
  }
};

```

{% endtab %}