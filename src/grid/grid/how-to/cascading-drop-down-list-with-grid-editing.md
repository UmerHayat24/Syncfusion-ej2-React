---
title: "Cascading DropDownList with Grid editing"
component: "Grid"
description: "Learn how to Cascading DropDownList with Grid editing."
---

# Cascading DropDownList with Grid editing

You can achieve the Cascading DropDownList with grid Editing by using the Cell Edit Template feature.

In the below demo, Cascading DropDownList rendered for **ShipCountry** and **ShipState** column.

{% tab template="grid/cascade-drop", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { DataManager, Query } from '@syncfusion/ej2-data';
import { DropDownList } from '@syncfusion/ej2-dropdowns';
import { ColumnDirective, ColumnsDirective, EditSettingsModel, GridComponent } from '@syncfusion/ej2-react-grids';
import { Edit, IEditCell, Inject, Toolbar, ToolbarItems } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { cascadeData } from './datasource';

export default class App extends React.Component<{}, {}> {
  public editOptions: EditSettingsModel = { allowEditing: true, allowAdding: true, allowDeleting: true };
  public toolbarOptions: ToolbarItems[] = ['Add', 'Edit', 'Delete', 'Update', 'Cancel'];
  public countryParams : IEditCell = {
    create:()=>{
      this.countryElem = document.createElement('input');
      return this.countryElem;
    },
    destroy:()=>{
        this.countryObj.destroy();
    },
    read:()=>{
        return this.countryObj.text;
    },
    write:()=>{
      this.countryObj = new DropDownList({
        change: () => {
          this.stateObj.enabled = true;
          const tempQuery: Query = new Query().where('countryId', 'equal', this.countryObj.value);
          this.stateObj.query = tempQuery;
          this.stateObj.text = '';
          this.stateObj.dataBind();
        },
        dataSource: new DataManager(this.country),
        fields: { value: 'countryId', text: 'countryName' },
        floatLabelType: 'Never',
        placeholder: 'Select a country'
      });
      this.countryObj.appendTo(this.countryElem);
    }
  };
  public stateParams : object = {
    create:()=>{
        this.stateElem = document.createElement('input');
        return this.stateElem;
    },
    destroy:()=>{
        this.stateObj.destroy();
    },
    read:()=>{
        return this.stateObj.text;
    },
    write:()=>{
      this.stateObj = new DropDownList({
        dataSource: new DataManager(this.stateColl),
        enabled: false,
        fields: { value: 'stateId', text: 'stateName' },
        floatLabelType: 'Never',
        placeholder: 'Select a state'
      });
      this.stateObj.appendTo(this.stateElem);
    }
  };

  public countryElem : HTMLElement;
  public countryObj : DropDownList;

  public stateElem : HTMLElement;
  public stateObj : DropDownList;

  public country: object[] = [
      { countryName: 'United States', countryId: '1' },
      { countryName: 'Australia', countryId: '2' }
  ];
  public stateColl: object[] = [
      { stateName: 'New York', countryId: '1', stateId: '101' },
      { stateName: 'Virginia ', countryId: '1', stateId: '102' },
      { stateName: 'Washington', countryId: '1', stateId: '103' },
      { stateName: 'Queensland', countryId: '2', stateId: '104' },
      { stateName: 'Tasmania ', countryId: '2', stateId: '105' },
      { stateName: 'Victoria', countryId: '2', stateId: '106' }
  ];

  public render() {
    return <GridComponent dataSource={cascadeData} editSettings={this.editOptions}
        toolbar={this.toolbarOptions} height={273}>
        <ColumnsDirective>
          <ColumnDirective field='OrderID' headerText='Order ID' width='100' textAlign="Right" isPrimaryKey={true}/>
          <ColumnDirective field='CustomerID' headerText='Customer ID' width='120'/>
          <ColumnDirective field='ShipCountry' headerText='Ship Country' width='150' editType= 'dropdownedit' edit={this.countryParams} textAlign="Right"/>
          <ColumnDirective field='ShipState' headerText='Ship State' editType= 'dropdownedit' edit={this.stateParams} width='150'/>
        </ColumnsDirective>
        <Inject services={[Edit, Toolbar]} />
    </GridComponent>
  }
};
```

{% endtab %}
