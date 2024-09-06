---
title: "Immutable"
component: "Grid"
description: "Learn how to use immutable data in the Essential JS 2 DataGrid control. Also learn about the limitations of this feature."
---

# Immutable Mode

The immutable mode optimizes the Grid re-rendering performance by using the object reference and [`deep compare`](https://dmitripavlutin.com/how-to-compare-objects-in-javascript/#4-deep-equality) concept. When performing the Grid actions, it will only re-render the modified or newly added rows and prevent the re-rendering of the unchanged rows.

To enable this feature, you have to set the [`enableImmutableMode`](../api/grid/#enableImmutableMode) property as **true**.

>* This feature uses the primary key value for data comparison. So, you need to provide the [`isPrimaryKey`](../api/grid/column/#isprimarykey) column.

{% tab template="grid/immutable-mode", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent, Inject, Page } from '@syncfusion/ej2-react-grids';
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
    public pageSettings: object = { pageSize: 50 };
    public immutableInit: boolean = true;
    public init: boolean = true;
    public primaryKey: number = 0;
    public normalStart: number;
    public immutableStart: number;
    public immutableGrid: GridComponent;
    public normalGrid: GridComponent;
    public topBtn: ButtonComponent;
    public bottomBtn: ButtonComponent;
    public deleteBtn: ButtonComponent;
    public sortBtn: ButtonComponent;
    public pageBtn: ButtonComponent;
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
        let addedRecords: object[] = [
            { 'OrderID': ++this.primaryKey, 'ProductName': 'Chai', 'ProductID': 'Sasquatch Ale', 'CustomerID': 'QUEDE', 'CustomerName': 'Yoshi Tannamuri' },
            { 'OrderID': ++this.primaryKey, 'ProductName': 'Georg Pipps', 'ProductID': 'Valkoinen suklaa', 'CustomerID': 'RATTC', 'CustomerName': 'Martín Sommer' },
            { 'OrderID': ++this.primaryKey, 'ProductName': 'Yoshi Tannamuri', 'ProductID': 'Gula Malacca', 'CustomerID': 'COMMI', 'CustomerName': 'Ann Devon' },
            { 'OrderID': ++this.primaryKey, 'ProductName': 'Palle Ibsen', 'ProductID': 'Rogede sild', 'CustomerID': 'RATTC', 'CustomerName': 'Paula Wilson' },
            { 'OrderID': ++this.primaryKey, 'ProductName': 'Francisco Chang', 'ProductID': 'Mascarpone Fabioli', 'CustomerID': 'ROMEY', 'CustomerName': 'Jose Pavarotti' }
        ];
        let aData: object[] = addedRecords.concat(this.immutableGrid.dataSource as object[]);
        this.normalGrid.setProperties({ dataSource: aData });
        this.immutableGrid.setProperties({ dataSource: aData });
    }
    public addBottomEvent() {
        let addedRecords: object[] = [
            { 'OrderID': ++this.primaryKey, 'ProductName': 'Chai', 'ProductID': 'Sasquatch Ale', 'CustomerID': 'QUEDE', 'CustomerName': 'Yoshi Tannamuri' },
            { 'OrderID': ++this.primaryKey, 'ProductName': 'Georg Pipps', 'ProductID': 'Valkoinen suklaa', 'CustomerID': 'RATTC', 'CustomerName': 'Martín Sommer' },
            { 'OrderID': ++this.primaryKey, 'ProductName': 'Yoshi Tannamuri', 'ProductID': 'Gula Malacca', 'CustomerID': 'COMMI', 'CustomerName': 'Ann Devon' },
            { 'OrderID': ++this.primaryKey, 'ProductName': 'Palle Ibsen', 'ProductID': 'Rogede sild', 'CustomerID': 'RATTC', 'CustomerName': 'Paula Wilson' },
            { 'OrderID': ++this.primaryKey, 'ProductName': 'Francisco Chang', 'ProductID': 'Mascarpone Fabioli', 'CustomerID': 'ROMEY', 'CustomerName': 'Jose Pavarotti' }
        ]
        let aData: object[] = (this.immutableGrid.dataSource as object[]).concat(addedRecords);
        this.normalGrid.setProperties({ dataSource: aData });
        this.immutableGrid.setProperties({ dataSource: aData });
    }
    public deleteEvent() {
        (this.immutableGrid.dataSource as object[]).splice(0, 5);
        this.normalGrid.setProperties({ dataSource: this.immutableGrid.dataSource });
        this.immutableGrid.setProperties({ dataSource: this.immutableGrid.dataSource });
    }
    public sortEvent() {
        let aData: object[] = (this.immutableGrid.dataSource as object[]).reverse();
        this.normalGrid.setProperties({ dataSource: aData });
        this.immutableGrid.setProperties({ dataSource: aData });
    }
    public pageEvent() {
        let totalPage: number = (this.immutableGrid.dataSource as object[]).length / this.immutableGrid.pageSettings.pageSize;
        let page: number = Math.floor(Math.random() * totalPage) + 1;
        this.normalGrid.setProperties({ pageSettings: { currentPage: page } });
        this.immutableGrid.setProperties({ pageSettings: { currentPage: page } });
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
                  <ButtonComponent ref={topInfo => { this.topBtn = topInfo }} cssClass='e-info' onClick={this.addTopEvent.bind(this)}>Add 5 rows at top</ButtonComponent>
                  <ButtonComponent ref={bottomInfo => { this.bottomBtn = bottomInfo }} cssClass='e-info' onClick={this.addBottomEvent.bind(this)}>Add 5 rows at bottom</ButtonComponent>
                  <ButtonComponent ref={deleteInfo => { this.deleteBtn = deleteInfo }} cssClass='e-info' onClick={this.deleteEvent.bind(this)}>Delete 5 rows</ButtonComponent>
                  <ButtonComponent ref={sortInfo => { this.sortBtn = sortInfo }} cssClass='e-info' onClick={this.sortEvent.bind(this)}>Sort Order ID</ButtonComponent>
                  <ButtonComponent ref={pageInfo => { this.pageBtn = pageInfo }} cssClass='e-info' onClick={this.pageEvent.bind(this)}>Paging</ButtonComponent>
                </div>
              </td>
            </tr>
            <tr>
              <td>
                <span><b>Immutable Grid</b></span>
                <GridComponent ref={immutable => { this.immutableGrid = immutable }} dataSource={data} height='250' enableImmutableMode={true} allowPaging={true} pageSettings={this.pageSettings} beforeDataBound={this.immutableBeforeDataBound.bind(this)} dataBound={this.immutableDataBound.bind(this)}>
                  <ColumnsDirective>
                    <ColumnDirective field='OrderID' headerText='Order ID' isPrimaryKey="true" width='120' textAlign='Right'></ColumnDirective>
                    <ColumnDirective field='ProductName' headerText='Product Name' width='160'></ColumnDirective>
                    <ColumnDirective field='ProductID' headerText='Product ID' width='130' textAlign='Right' />
                    <ColumnDirective field='CustomerID' headerText='Customer ID' width='120' />
                    <ColumnDirective field='CustomerName' headerText='Customer Name' width='160'></ColumnDirective>
                  </ColumnsDirective>
                   <Inject services={[Page]} />
                </GridComponent>
              </td>
            </tr>
            <tr>
              <td>
                <span><b>Normal Grid</b></span>
                <GridComponent ref={normal => { this.normalGrid = normal }} dataSource={data} height='250' allowPaging={true} pageSettings={this.pageSettings} beforeDataBound={this.beforeDataBound.bind(this)} dataBound={this.dataBound.bind(this)}>
                  <ColumnsDirective>
                    <ColumnDirective field='OrderID' headerText='Order ID' isPrimaryKey="true" width='120' textAlign='Right'></ColumnDirective>
                    <ColumnDirective field='ProductName' headerText='Product Name' width='160'></ColumnDirective>
                    <ColumnDirective field='ProductID' headerText='Product ID' width='130' textAlign='Right' />
                    <ColumnDirective field='CustomerID' headerText='Customer ID' width='120' />
                    <ColumnDirective field='CustomerName' headerText='Customer Name' width='160'></ColumnDirective>
                  </ColumnsDirective>
                   <Inject services={[Page]} />
                </GridComponent>
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
* Hierarchy Grid
* Column reorder
* Virtualization
* Infinite scroll
* Grouping
