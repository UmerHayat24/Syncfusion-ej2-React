---
title: "Change Change Column Header Text Dynamically"
component: "TreeGrid"
description: "Learn how to change column header text dynamically."
---

# Change Column Header Text Dynamically

You can change the column [`headerText`](https://ej2.syncfusion.com/react/documentation/api/treegrid/column/#headertext) dynamically through an external button.

Follow the given steps to change the header text dynamically:

**Step 1**:

Get the column object corresponding to the field name by using the [`getColumnByField`](https://ej2.syncfusion.com/react/documentation/api/treegrid#getcolumnbyfield) method.
Then change the header Text value.

```typescript
      /** get the JSON object of the column corresponding to the field name */
      const column = this.treegridObj.getColumnByField("Duration");
      /** assign a new header text to the column */
      column.headerText = "Changed Text";
```

**Step 2**:

To reflect the changes in the grid header, invoke the [`refreshColumns`](https://ej2.syncfusion.com/react/documentation/api/treegrid#refreshcolumns) method.

```typescript

      this.treegridObj.refreshColumns();

```

{% tab template="treegrid/change-headertext", sourceFiles="app/App.tsx,app/datasource.tsx", compileJsx=true %}

```typescript

import * as React from 'react';
import { projectData } from './datasource';
import { ColumnsDirective, ColumnDirective, TreeGridComponent, EditSettingsModel } from '@syncfusion/ej2-react-treegrid';
import { Inject, Page, Edit, Toolbar, ToolbarItems } from '@syncfusion/ej2-react-treegrid';
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';

/* tslint:disable */

export default class App extends React.Component {
  public editOptions: EditSettingsModel = { allowAdding:true, allowEditing: true, allowDeleting:true };
  public toolbarOptions: ToolbarItems[] = ['Add', 'Edit', 'Delete', 'Update', 'Cancel'];

  public treegridObj: TreeGridComponent | null;

  public click() {
    if (this.treegridObj) {
      /** get the JSON object of the column corresponding to the field name */
      const column = this.treegridObj.getColumnByField("Duration");
      /** assign a new header text to the column */
      column.headerText = "Changed Text";
      this.treegridObj.refreshColumns();
    }
  }
  public render() {
    this.click = this.click.bind(this);
    return (<div>
      <ButtonComponent cssClass= 'e-flat' isToggle onClick= { this.click }>Change Header Text</ButtonComponent>
      <TreeGridComponent dataSource={projectData} treeColumnIndex={1} idMapping= 'TaskID' parentIdMapping='parentID' height={210} toolbar={this.toolbarOptions}
      ref={g=> this.treegridObj = g} editSettings={this.editOptions}>
        <ColumnsDirective>
          <ColumnDirective field='TaskID' headerText='Task ID' width='70' textAlign='Right'></ColumnDirective>
          <ColumnDirective field='TaskName' headerText='Task Name' width='100'></ColumnDirective>
          <ColumnDirective field='StartDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' />
          <ColumnDirective field='Duration' headerText='Duration' width='90' textAlign='Right' />
        </ColumnsDirective>
        <Inject services={[Page, Edit, Toolbar]} />
      </TreeGridComponent>
    </div>  
    );
  }
};

```

{% endtab %}
