---
title: "Customize Column Styles"
component: "TreeGrid"
description: "Learn how to Customize Column Styles."
---

# Customize Column Styles

You can customise the appearance of header and content of the particular column using the
[`customAttributes`](../../api/treegrid/column/#customattributes) property.

To customize the treegrid column, follow the given steps:

**Step 1**:

Create a css class with custom style to override the default style for rowcell and headercell.

```css

.e-treegrid .e-rowcell.customcss{
    background-color: #ecedee;
    font-family: 'Bell MT';
    color: 'red';
    font-size: '20px';
}

.e-treegrid .e-headercell.customcss{
    background-color: #2382c3;
    color: white;
    font-family: 'Bell MT';
    font-size: '20px';
}

```

**Step 2**:

Add the custom css class to particular column by using [`customAttributes`](../api/treegrid/column/#customattributes) property.

```typescript
<ColumnDirective field='TaskName' headerText='Task Name' width='100' customAttributes={this.customAttributes}></ColumnDirective>

```

{% tab template="treegrid/custom-column", sourceFiles="app/App.tsx,app/datasource.tsx,app/custom.css" %}

```typescript

import * as React from 'react';
import { projectData } from './datasource';
import { ColumnsDirective, ColumnDirective, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';

/* tslint:disable */

export default class App extends React.Component {

  public customAttributes: any = {class: 'customcss'};
  public render() {
    return (
      <TreeGridComponent dataSource={projectData} treeColumnIndex={1} idMapping= 'TaskID' parentIdMapping='parentID' height={320}>
        <ColumnsDirective>
          <ColumnDirective field='TaskID' headerText='Task ID' width='70' textAlign='Right'></ColumnDirective>
          <ColumnDirective field='TaskName' headerText='Task Name' width='100' customAttributes={this.customAttributes}></ColumnDirective>
          <ColumnDirective field='StartDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' />
          <ColumnDirective field='Duration' headerText='Duration' width='90' textAlign='Right' />
        </ColumnsDirective>
      </TreeGridComponent>
    );
  }
};

```

{% endtab %}