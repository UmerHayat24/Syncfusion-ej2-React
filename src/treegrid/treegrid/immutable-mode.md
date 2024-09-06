---
title: "Immutable"
component: "TreeGrid"
description: "Learn how to use immutable data in the Essential JS 2 Tree Grid control. Also learn about the limitations of this feature."
---

# Immutable Mode

The immutable mode optimizes the Tree Grid re-rendering performance by using the object reference and [`deep compare`](https://dmitripavlutin.com/how-to-compare-objects-in-javascript/#4-deep-equality) concept. When performing the Grid actions, it will only re-render the modified or newly added rows and prevent the re-rendering of the unchanged rows.

To enable this feature, you have to set the [`enableImmutableMode`](../api/treegrid/#enableImmutableMode) property as **true**.

>* This feature uses the primary key value for data comparison. So, you need to provide the [`isPrimaryKey`](../api/treegrid/column/#isprimarykey) column.

{% tab template="treegrid/immutable-mode", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, TreeGridComponent, Inject, Page } from '@syncfusion/ej2-react-treegrid';
import { Page, Edit, SelectionSettingsModel, EditSettingsModel } from '@syncfusion/ej2-react-treegrid';
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import * as React from 'react';
import { sampleData2, dataSource1, sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public pageSettings: object = { pageSize: 50 };
    public settings: SelectionSettingsModel = { type: 'Multiple' };
    public immutableInit: boolean = true;
    public init: boolean = true;
    public normalStart: number;
    public immutableStart: number;
    public immutableGrid: GridComponent;
    public normalGrid: GridComponent;
    public topBtn: ButtonComponent;
    public bottomBtn: ButtonComponent;
    public deleteBtn: ButtonComponent;
    public sortBtn: ButtonComponent;
    public pageBtn: ButtonComponent;
    public editOptions: EditSettingsModel = {
        allowAdding: true,
        allowDeleting: true,
        allowEditing: true,
        mode: 'Cell'
    };
     public immutableBeforeDataBound() {
        this.immutableStart = new Date().getTime();
    }
    public immutableDataBound() {
        let val: number | string = this.immutableInit ? '' : new Date().getTime() - this.immutableStart;
        document.getElementById("immutableDelete").innerHTML =
            "Immutable rendering Time: " + "<b>" + val + "</b>" + "<b>ms</b>";
        this.immutableStart = 0; this.immutableInit = false;
    }
    public addTopEvent() {
        this.normalGrid.addRecord(sampleData[0], 0, "Top");
        this.immutableGrid.addRecord(sampleData[0], 0, "Top");
    }
    public addBottomEvent() {
        this.normalGrid.addRecord(sampleData[0], 0, "Bottom");
        this.immutableGrid.addRecord(sampleData[0], 0, "Bottom");
    }
    public deleteEvent() {
        this.normalGrid.selectRows([0, 2, 4]);
        this.immutableGrid.selectRows([0, 2, 4]);
        this.normalGrid.deleteRecord();
        this.immutableGrid.deleteRecord();
    }
    public sortEvent() {
        let aData: object[] = (this.immutableGrid.dataSource as object[]).reverse();
        this.normalGrid.setProperties({ dataSource: aData });
        this.immutableGrid.setProperties({ dataSource: aData });
    }
    public pageEvent() {
        let page: number = this.normalGrid.pageSettings.currentPage + 1;
        this.normalGrid.goToPage(page);
        this.immutableGrid.goToPage(page);
    }
    public beforeDataBound() {
        this.normalStart = new Date().getTime();
    }
    public dataBound() {
        let val: number | string = this.init ? '' : new Date().getTime() - this.normalStart;
        document.getElementById("normalDelete").innerHTML =
        "Normal rendering Time: " + "<b>" + val + "</b>" + "<b>ms</b>";
        this.normalStart = 0; this.init = false;
    }

    public render() {
    if(sampleData2.length == 0){
        dataSource1();
    }
    return (<div>
      <table>
          <tbody>
            <tr>
              <td>
                <span id="immutableDelete"></span>
              </td>
            </tr>
            <tr>
              <td>
                <span id="normalDelete"></span>
              </td>
            </tr>
            <tr>
              <td>
                <div>
                  <ButtonComponent ref={topInfo => { this.topBtn = topInfo }} cssClass='e-info' onClick={this.addTopEvent.bind(this)}>Add row at top</ButtonComponent>
                  <ButtonComponent ref={bottomInfo => { this.bottomBtn = bottomInfo }} cssClass='e-info' onClick={this.addBottomEvent.bind(this)}>Add row at bottom</ButtonComponent>
                  <ButtonComponent ref={deleteInfo => { this.deleteBtn = deleteInfo }} cssClass='e-info' onClick={this.deleteEvent.bind(this)}>Delete 5 rows</ButtonComponent>
                  <ButtonComponent ref={sortInfo => { this.sortBtn = sortInfo }} cssClass='e-info' onClick={this.sortEvent.bind(this)}>Sort Task ID</ButtonComponent>
                  <ButtonComponent ref={pageInfo => { this.pageBtn = pageInfo }} cssClass='e-info' onClick={this.pageEvent.bind(this)}>Paging</ButtonComponent>
                </div>
              </td>
            </tr>
            <tr>
              <td>
                <span><b>Immutable Grid</b></span>
                <TreeGridComponent ref={immutable => { this.immutableGrid = immutable }} treeColumnIndex={1} childMapping='subtasks' dataSource={sampleData2} height='350' selectionSettings={this.settings} enableImmutableMode={true} allowPaging={true} pageSettings={this.pageSettings} beforeDataBound={this.immutableBeforeDataBound.bind(this)} dataBound={this.immutableDataBound.bind(this)} editSettings={this.editOptions}>
                <ColumnsDirective>
                    <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right' isPrimaryKey={true}/>
                    <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
                    <ColumnDirective field='priority' headerText='Priority' width='90' />
                    <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
                </ColumnsDirective>
                   <Inject services={[Page, Edit]} />
                </TreeGridComponent>
              </td>
              <td>
                <span><b>Normal Grid</b></span>
                <TreeGridComponent ref={normal => { this.normalGrid = normal }} treeColumnIndex={1} childMapping='subtasks' dataSource={sampleData2} allowPaging={true} height='350' pageSettings={this.pageSettings} selectionSettings={this.settings} beforeDataBound={this.beforeDataBound.bind(this)} editSettings={this.editOptions} dataBound={this.dataBound.bind(this)}>
                <ColumnsDirective>
                    <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right' isPrimaryKey={true}/>
                    <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
                    <ColumnDirective field='priority' headerText='Priority' width='90' />
                    <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
                </ColumnsDirective>
                   <Inject services={[Page, Edit]} />
                </TreeGridComponent>
              </td>
            </tr>
          </tbody>
        </table></div>)
  }
};
```

{% endtab %}

## Limitations

The following features are not supported in the immutable mode:

* Frozen rows and columns
* Row Template
* Detail Template
* Column reorder
* Virtualization
* Infinite scroll