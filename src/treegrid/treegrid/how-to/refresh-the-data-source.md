---
title: "How To"
component: "TreeGrid"
description: "Learn how to customize the Essential JS 2 TreeGrid."
---

# How To

## How to Refresh the Datasource

You can add/delete the datasource records through an external button. To reflect the datasource changes in treegrid, you need to assign the modified data to dataSource property.

Please follow the below steps to refresh the treegrid after datasource change.

**Step 1**:

Add/delete the datasource record by using the following code.

```typescript

    const dataSource: object = extendArray((this.treegridObj as TreeGridComponent).dataSource as object[]);

    // Added New Record.
    (dataSource as object[]).unshift({ TaskID: 99, TaskName: "New Data", StartDate: new Date('02/03/2017'), Duration: 10 });

    // Delete record.
    (dataSource as object[]).splice(selectedRow, 1);

```

**Step 2**:

Refresh the treegrid after the datasource change by assign the modified data to dataSource property.

```typescript
    (this.treegridObj as TreeGridComponent).dataSource = dataSource; // Refresh the TreeGrid.

```

{% tab template="treegrid/refresh", sourceFiles="app/App.tsx,app/datasource.tsx", compileJsx=true %}

```typescript

import * as React from 'react';
import { projectData } from './datasource';
import { ColumnsDirective, ColumnDirective, TreeGridComponent, extendArray } from '@syncfusion/ej2-react-treegrid';
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';

/* tslint:disable */

export default class App extends React.Component {
    public treegridObj: TreeGridComponent | null;
    public treegridData: object[] = projectData;
    public add() {
      const dataSource: object = extendArray((this.treegridObj as TreeGridComponent).dataSource as object[]);
      (dataSource as object[]).unshift({ TaskID: 99, TaskName: "New Data", StartDate: new Date('02/03/2017'), Duration: 10 });
      (this.treegridObj as TreeGridComponent).dataSource = dataSource;
    }
    public delete() {
        const selectedRow: number = (this.treegridObj as TreeGridComponent).getSelectedRowIndexes()[0];
        const dataSource: object = extendArray((this.treegridObj as TreeGridComponent).dataSource as object[]);
        if (selectedRow.length > 0){
          (dataSource as object[]).splice(selectedRow, 1); // Delete record.
        }
        else {
            alert("No records selected for delete operation");
        }
        (this.treegridObj as TreeGridComponent).dataSource = dataSource; // Refresh the TreeGrid.
    }
  public render() {
    return (<div>
      <ButtonComponent cssClass= 'e-flat' isToggle onClick={ this.add.bind(this) }>Add</ButtonComponent>
      <ButtonComponent cssClass= 'e-flat' isToggle onClick= { this.delete.bind(this)} >Delete</ButtonComponent>
      <TreeGridComponent dataSource={this.treegridData} treeColumnIndex={1} idMapping= 'TaskID' parentIdMapping='parentID' height={280} ref={g=> this.treegridObj = g}>
        <ColumnsDirective>
            <ColumnDirective field='TaskID' headerText='Task ID' width='70' textAlign='Right'></ColumnDirective>
            <ColumnDirective field='TaskName' headerText='Task Name' width='100'></ColumnDirective>
            <ColumnDirective field='StartDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' />
            <ColumnDirective field='Duration' headerText='Duration' width='90' textAlign='Right' />
        </ColumnsDirective>
      </TreeGridComponent>
    </div>  
    );
  }
};

```

{% endtab %}
