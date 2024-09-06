---
title: "Cascading DropDownList with TreeGrid editing"
component: "TreeGrid"
description: "Learn how to Cascading DropDownList with TreeGrid editing."
---

# Cascading DropDownList with TreeGrid editing

You can achieve the Cascading DropDownList with treegrid Editing by using the Cell Edit Template feature.

In the below demo, Cascading DropDownList rendered for **Priority** and **Duration** column.

{% tab template="treegrid/cascade-drop", sourceFiles="app/App.tsx,app/datasource.tsx", compileJsx=true %}

```typescript

import * as React from 'react';
import { projectData } from './datasource';
import { DataManager, Query } from '@syncfusion/ej2-data';
import { DropDownList } from '@syncfusion/ej2-dropdowns';
import { ColumnsDirective, ColumnDirective, TreeGridComponent, Inject } from '@syncfusion/ej2-react-treegrid';
import { Edit, Toolbar, ToolbarItems, EditSettingsModel } from '@syncfusion/ej2-react-treegrid';
import { IEditCell } from '@syncfusion/ej2-react-grids';

/* tslint:disable */

export default class App extends React.Component {

  public editOptions: EditSettingsModel = { allowEditing: true, allowAdding: true, allowDeleting: true, mode: 'Row' };
  public toolbarOptions: ToolbarItems[] = ['Add', 'Edit', 'Delete'];
  public treegridObj: TreeGridComponent | null;
  public priorityElem: HTMLElement;
  public priorityObj: DropDownList;
  public durationElem: HTMLElement;
  public durationObj: DropDownList;

  public priority: IEditCell = {
    create:()=>{
      this.priorityElem = document.createElement('input');
      return this.priorityElem;
    },
    destroy:()=>{
      this.priorityObj.destroy();
    },
    read:()=>{
      return this.priorityObj.text;
    },
    write:()=>{
      this.priorityObj = new DropDownList({
        change: () => {
          this.durationObj.enabled = true;
          const tempQuery: Query = new Query().where('priorityId', 'equal', this.priorityObj.value);
          this.durationObj.query = tempQuery;
          this.durationObj.text = '';
          this.durationObj.dataBind();
        },
        dataSource: new DataManager(this.priorityData),
        fields: { value: 'priorityId', text: 'priorityName' },
        floatLabelType: 'Never',
        placeholder: 'Select a Priority'
      });
      this.priorityObj.appendTo(this.priorityElem);
    }
  }

  public duration: IEditCell = {
    create:()=>{
      this.durationElem = document.createElement('input');
      return this.durationElem;
    },
    destroy:()=>{
      this.durationObj.destroy();
    },
    read:()=>{
      return this.durationObj.text;
    },
    write:()=>{
      this.durationObj = new DropDownList({
        dataSource: new DataManager(this.durationData),
        enabled: false,
        fields: { value: 'durationId', text: 'durationValue' },
        floatLabelType: 'Never',
        placeholder: 'Select a duration'
      });
      this.durationObj.appendTo(this.durationElem);
    }
  }

  public priorityData: object[] = [
    { priorityName: 'Normal', priorityId: '1' },
    { priorityName: 'High', priorityId: '2' }
  ];
  public durationData: object[] = [
    { durationValue: 2, priorityId: '1', durationId: 2 },
    { durationValue: 3, priorityId: '1', durationId: 3 },
    { durationValue: 4, priorityId: '1', durationId: 4 },
    { durationValue: 11, priorityId: '2', durationId: 11 },
    { durationValue: 15, priorityId: '2', durationId: 15 },
    { durationValue: 20, priorityId: '2', durationId: 20 }
  ];

  public render() {
    return (
      <TreeGridComponent dataSource={projectData} treeColumnIndex={1} idMapping= 'TaskID' parentIdMapping='parentID' editSettings={this.editOptions} toolbar={this.toolbarOptions}
      ref={g => this.treegridObj = g} height={273}>
        <ColumnsDirective>
          <ColumnDirective field='TaskID' headerText='Task ID' width='70' textAlign='Right' isPrimaryKey={true}></ColumnDirective>
          <ColumnDirective field='TaskName' headerText='Task Name' width='100'></ColumnDirective>
          <ColumnDirective field='StartDate' headerText='Start Date' width='100' format='yMd' textAlign='Right' editType='datepickeredit'></ColumnDirective>
          <ColumnDirective field='EndDate' headerText='End Date' width='100' format='yMd' textAlign='Right' editType='datepickeredit'></ColumnDirective>
          <ColumnDirective field='Priority' headerText='Priority' width='90' textAlign='Right' edit={this.priority} />
          <ColumnDirective field='Duration' headerText='Duration' width='90' textAlign='Right' edit={this.duration} />
          <ColumnDirective field='Progress' headerText='Progress' width='90' textAlign='Right' />
        </ColumnsDirective>
        <Inject services={[Edit, Toolbar]} />
      </TreeGridComponent>
    );
  }
};

```

{% endtab %}
