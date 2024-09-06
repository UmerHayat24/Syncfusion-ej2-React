---
title: "Customize the icon for column menu"
component: "TreeGrid"
description: "Learn how to customize the icon for column menu."
---

# Customize the icon for column menu

You can customize the column menu icon by overriding the default treegrid class **.e-icons.e-columnmenu** with a custom property **content** as mentioned below,

```css
    .e-treegrid .e-columnheader .e-icons.e-columnmenu::before {
        content: "\e903";
    }
```

In the below sample, treegrid is rendered with a customized column menu icon.

{% tab template="treegrid/custom-column-menu-icon", sourceFiles="app/App.tsx,app/datasource.tsx,app/custom.css", compileJsx=true %}

```typescript

import * as React from 'react';
import { projectData } from './datasource';
import { ColumnsDirective, ColumnDirective, TreeGridComponent, ColumnMenu, Inject } from '@syncfusion/ej2-react-treegrid';

/* tslint:disable */

export default class App extends React.Component {

  public render() {
    return (<div>
      <TreeGridComponent dataSource={projectData} treeColumnIndex={1} idMapping= 'TaskID' parentIdMapping='parentID' showColumnMenu={true} height={315}>
        <ColumnsDirective>
          <ColumnDirective field='TaskID' headerText='Task ID' width='70' textAlign='Right'></ColumnDirective>
          <ColumnDirective field='TaskName' headerText='Task Name' width='100'></ColumnDirective>
          <ColumnDirective field='StartDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' />
          <ColumnDirective field='EndDate' headerText='End Date' width='90' format='yMd' textAlign='Right' />
          <ColumnDirective field='Duration' headerText='Duration' width='90' textAlign='Right' />
          <ColumnDirective field='Priority' headerText='Priority' width='90' textAlign='Right' />
        </ColumnsDirective>
        <Inject services={[ColumnMenu]} />
      </TreeGridComponent>
      </div>
    );
  }
};

```

{% endtab %}