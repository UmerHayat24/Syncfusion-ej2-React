---
title: "Data Binding"
component: "Spreadsheet"
description: "Learn how to bind local and remote data in the Essential JS 2 Spreadsheet control."
---

# Data Binding

The Spreadsheet uses [`DataManager`](../data), which supports both RESTful JSON data services and local JavaScript object array binding to a range. The `dataSource` property can be assigned either with the instance of [`DataManager`](../data) or JavaScript object array collection.

> To bind data to a cell, use `cell data binding` support.

## Local data

To bind local data to the Spreadsheet, you can assign a JavaScript object array to the `dataSource` property.

Refer to the following code example for local data binding.

{% tab template="spreadsheet/local-data-binding", sourceFiles="app/**/*.tsx,index.html", iframeHeight="450px", isDefaultActive=true, compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { SpreadsheetComponent, SheetsDirective, SheetDirective, RangesDirective } from '@syncfusion/ej2-react-spreadsheet';
import { data } from './datasource';
import { RangeDirective, ColumnsDirective, ColumnDirective } from '@syncfusion/ej2-react-spreadsheet';
export default class App extends React.Component<{}, {}> {
    spreadsheet: SpreadsheetComponent;
     render() {
        return  (<SpreadsheetComponent ref={(ssObj) => { this.spreadsheet = ssObj }}>
                        <SheetsDirective>
                            <SheetDirective>
                                <RangesDirective>
                                    <RangeDirective dataSource={data}></RangeDirective>
                                </RangesDirective>
                                <ColumnsDirective>
                                    <ColumnDirective width={100}></ColumnDirective>
                                    <ColumnDirective width={110}></ColumnDirective>
                                    <ColumnDirective width={100}></ColumnDirective>
                                    <ColumnDirective width={180}></ColumnDirective>
                                    <ColumnDirective width={130}></ColumnDirective>
                                    <ColumnDirective width={130}></ColumnDirective>
                                </ColumnsDirective>
                            </SheetDirective>
                        </SheetsDirective>
                    </SpreadsheetComponent>);
    }
}
ReactDOM.render(<App />, document.getElementById('root'));
```

{% endtab %}

> The local data source can also be provided as an instance of the [`DataManager`](../data). By default, [`DataManager`](../data) uses **JsonAdaptor** for local data-binding.

## Remote data

To bind remote data to the Spreadsheet control, assign service data as an instance of [`DataManager`](../data) to the `dataSource` property. To interact with remote data source, provide the service endpoint `url`.

Refer to the following code example for remote data binding.

{% tab template="spreadsheet/remote-data-binding", sourceFiles="app/**/*.tsx,index.html", iframeHeight="450px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { DataManager, Query } from '@syncfusion/ej2-data';
import { SpreadsheetComponent, SheetsDirective, SheetDirective, RangesDirective } from '@syncfusion/ej2-react-spreadsheet';
import { RangeDirective, ColumnsDirective, ColumnDirective } from '@syncfusion/ej2-react-spreadsheet';

export default class App extends React.Component<{}, {}> {
    public query: Query = new Query().select(['OrderID', 'CustomerID', 'ShipName', 'ShipCity', 'ShipCountry', 'Freight']).take(200);
    public data: DataManager = new DataManager({
        url: 'https://js.syncfusion.com/demos/ejServices//wcf/Northwind.svc/Orders',
        crossDomain: true
    });
    spreadsheet: SpreadsheetComponent;
     render() {
        return  (<SpreadsheetComponent ref={(ssObj) => { this.spreadsheet = ssObj }}>
                        <SheetsDirective>
                            <SheetDirective name= 'Shipment Details'>
                                <RangesDirective>
                                    <RangeDirective dataSource={this.data} query={this.query}></RangeDirective>
                                </RangesDirective>
                                <ColumnsDirective>
                                    <ColumnDirective width={100}></ColumnDirective>
                                    <ColumnDirective width={110}></ColumnDirective>
                                    <ColumnDirective width={100}></ColumnDirective>
                                    <ColumnDirective width={180}></ColumnDirective>
                                    <ColumnDirective width={130}></ColumnDirective>
                                    <ColumnDirective width={130}></ColumnDirective>
                                </ColumnsDirective>
                            </SheetDirective>
                        </SheetsDirective>
                    </SpreadsheetComponent>);
    }
}
ReactDOM.render(<App />, document.getElementById('root'));
```

{% endtab %}

> By default, `DataManager` uses **ODataAdaptor** for remote data-binding.

### Binding with OData services

`OData` is a standardized protocol for creating and consuming data. You can retrieve data from OData service using the DataManager. Refer to the following code example for remote Data binding using OData service.

{% tab template="spreadsheet/remote-data-binding", sourceFiles="app/**/*.tsx,index.html", iframeHeight="450px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { DataManager, ODataAdaptor } from '@syncfusion/ej2-data';
import { SpreadsheetComponent, SheetsDirective, SheetDirective, RangesDirective } from '@syncfusion/ej2-react-spreadsheet';
import { RangeDirective, ColumnsDirective, ColumnDirective } from '@syncfusion/ej2-react-spreadsheet';

export default class App extends React.Component<{}, {}> {
            public data = new DataManager({
                adaptor: new ODataAdaptor,
                url: 'https://ej2services.syncfusion.com/production/web-services/api/Orders'
            });
    spreadsheet: SpreadsheetComponent;
     public created(): void {
         //Applies cell and number formatting to specified range of the active sheet
        this.spreadsheet.cellFormat({ fontWeight: 'bold', textAlign: 'center', verticalAlign: 'middle' },
        'A1:K1');
    }
     render() {
        return  (<SpreadsheetComponent ref={(ssObj) => { this.spreadsheet = ssObj }} created={this.created.bind(this)}>
                        <SheetsDirective>
                            <SheetDirective name= 'Order Details'>
                                <RangesDirective>
                                    <RangeDirective dataSource={this.data}></RangeDirective>
                                </RangesDirective>
                                <ColumnsDirective>
                                    <ColumnDirective width={80}></ColumnDirective>
                                    <ColumnDirective width={80}></ColumnDirective>
                                    <ColumnDirective width={80}></ColumnDirective>
                                    <ColumnDirective width={80}></ColumnDirective>
                                    <ColumnDirective width={80}></ColumnDirective>
                                    <ColumnDirective width={80}></ColumnDirective>
                                    <ColumnDirective width={280}></ColumnDirective>
                                    <ColumnDirective width={180}></ColumnDirective>
                                    <ColumnDirective width={80}></ColumnDirective>
                                    <ColumnDirective width={180}></ColumnDirective>
                                    <ColumnDirective width={180}></ColumnDirective>
                                </ColumnsDirective>
                            </SheetDirective>
                        </SheetsDirective>
                    </SpreadsheetComponent>);
    }
}
ReactDOM.render(<App />, document.getElementById('root'));
```

{% endtab %}

### Web API

You can use WebApiAdaptor to bind spreadsheet with Web API created using OData endpoint.

{% tab template="spreadsheet/remote-data-binding", sourceFiles="app/**/*.tsx,index.html", iframeHeight="450px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { DataManager, WebApiAdaptor } from '@syncfusion/ej2-data';
import { SpreadsheetComponent, SheetsDirective, SheetDirective, RangesDirective } from '@syncfusion/ej2-react-spreadsheet';
import { RangeDirective, ColumnsDirective, ColumnDirective } from '@syncfusion/ej2-react-spreadsheet';

export default class App extends React.Component<{}, {}> {
            public data = new DataManager({
                adaptor: new WebApiAdaptor,
                url: 'https://ej2services.syncfusion.com/production/web-services/api/Orders'
            });
    spreadsheet: SpreadsheetComponent;
     public created(): void {
         //Applies cell and number formatting to specified range of the active sheet
        this.spreadsheet.cellFormat({ fontWeight: 'bold', textAlign: 'center', verticalAlign: 'middle' },
        'A1:K1');
    }
     render() {
        return  (<SpreadsheetComponent ref={(ssObj) => { this.spreadsheet = ssObj }} created={this.created.bind(this)}>
                        <SheetsDirective>
                            <SheetDirective name= 'Order Details'>
                                <RangesDirective>
                                    <RangeDirective dataSource={this.data}></RangeDirective>
                                </RangesDirective>
                                <ColumnsDirective>
                                    <ColumnDirective width={80}></ColumnDirective>
                                    <ColumnDirective width={80}></ColumnDirective>
                                    <ColumnDirective width={80}></ColumnDirective>
                                    <ColumnDirective width={80}></ColumnDirective>
                                    <ColumnDirective width={80}></ColumnDirective>
                                    <ColumnDirective width={80}></ColumnDirective>
                                    <ColumnDirective width={280}></ColumnDirective>
                                    <ColumnDirective width={180}></ColumnDirective>
                                    <ColumnDirective width={80}></ColumnDirective>
                                    <ColumnDirective width={180}></ColumnDirective>
                                    <ColumnDirective width={180}></ColumnDirective>
                                </ColumnsDirective>
                            </SheetDirective>
                        </SheetsDirective>
                    </SpreadsheetComponent>);
    }
}
ReactDOM.render(<App />, document.getElementById('root'));
```

{% endtab %}

## Cell data binding

The Spreadsheet control can bind the data to individual cell in a sheet . To achive this you can use the
`value` property.

Refer to the following code example for cell data binding.

{% tab template="spreadsheet/cell-data-binding", sourceFiles="app/**/*.tsx,index.html", iframeHeight="450px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { SpreadsheetComponent, SheetsDirective, SheetDirective, RowsDirective, CellsDirective, RowDirective, CellDirective } from '@syncfusion/ej2-react-spreadsheet';
import { ColumnsDirective, ColumnDirective } from '@syncfusion/ej2-react-spreadsheet';

export default class App extends React.Component<{}, {}> {
    spreadsheet: SpreadsheetComponent;
     render() {
        return  (<SpreadsheetComponent ref={(ssObj) => { this.spreadsheet = ssObj }}>
        <SheetsDirective>
            <SheetDirective selectedRange='D13' name='PriceDetails'>
                <RowsDirective>
                    <RowDirective>
                        <CellsDirective>
                            <CellDirective value='Item Name' ></CellDirective>
                            <CellDirective value='Quantity' ></CellDirective>
                            <CellDirective value='Price' ></CellDirective>
                            <CellDirective value='Amount' ></CellDirective>
                            <CellDirective value='Stock Detail' ></CellDirective>
                            <CellDirective value='Website' ></CellDirective>
                        </CellsDirective>
                    </RowDirective>
                    <RowDirective>
                        <CellsDirective>
                            <CellDirective value='Casual Shoes' ></CellDirective>
                            <CellDirective value='10' ></CellDirective>
                            <CellDirective value='$20' ></CellDirective>
                            <CellDirective value='$200' ></CellDirective>
                            <CellDirective value='OUT OF STOCK' ></CellDirective>
                            <CellDirective value='Amazon'></CellDirective>
                        </CellsDirective>
                    </RowDirective>
                    <RowDirective>
                        <CellsDirective>
                            <CellDirective value='Sports Shoes' ></CellDirective>
                            <CellDirective value='20' ></CellDirective>
                            <CellDirective value='$30' ></CellDirective>
                            <CellDirective value='$600'></CellDirective>
                            <CellDirective value='IN STOCK'></CellDirective>
                            <CellDirective value='Overstack'></CellDirective>
                        </CellsDirective>
                    </RowDirective>
                    <RowDirective>
                        <CellsDirective>
                            <CellDirective value='Formal Shoes' ></CellDirective>
                            <CellDirective value='20' ></CellDirective>
                            <CellDirective value='$15' ></CellDirective>
                            <CellDirective value='$300'></CellDirective>
                            <CellDirective value='IN STOCK'></CellDirective>
                            <CellDirective value='AliExpress'></CellDirective>
                        </CellsDirective>
                    </RowDirective>
                    <RowDirective>
                        <CellsDirective>
                            <CellDirective value='Sandals & Floaters' ></CellDirective>
                            <CellDirective value='15' ></CellDirective>
                            <CellDirective value='$20' ></CellDirective>
                            <CellDirective value='$300' ></CellDirective>
                            <CellDirective value='OUT OF STOCK' ></CellDirective>
                            <CellDirective value='AliBaba'></CellDirective>
                        </CellsDirective>
                    </RowDirective>
                    <RowDirective>
                        <CellsDirective>
                            <CellDirective value='Flip-Flops & Slippers' ></CellDirective>
                            <CellDirective value='30' ></CellDirective>
                            <CellDirective value='$10' ></CellDirective>
                            <CellDirective value='$300'></CellDirective>
                            <CellDirective value='IN STOCK' ></CellDirective>
                            <CellDirective value='Taobao'></CellDirective>
                        </CellsDirective>
                    </RowDirective>
                </RowsDirective>
                <ColumnsDirective>
                    <ColumnDirective width={110}></ColumnDirective>
                    <ColumnDirective width={115}></ColumnDirective>
                    <ColumnDirective width={110}></ColumnDirective>
                    <ColumnDirective width={100}></ColumnDirective>
                    <ColumnDirective width={110}></ColumnDirective>
                    <ColumnDirective width={100}></ColumnDirective>
                </ColumnsDirective>
            </SheetDirective>
        </SheetsDirective>
    </SpreadsheetComponent>);
    }
}
ReactDOM.render(<App />, document.getElementById('root'));
```

{% endtab %}

> The cell data binding also supports formula, style, number format, and more.

## Dynamic data binding and Datasource change event

You can dynamically change the datasource of the spreadsheet by changing the `dataSource` property of the `range` object of the `sheet`. The `dataSourceChanged` event handler will be triggered when editing, inserting, and deleting a row in the datasource range. This event will be triggered with a parameter named `action` which indicates the `edit`, `add` and `delete` actions for the respective ones.

The following table defines the arguments of the `dataSourceChanged` event.

| Property | Type | Description |
|-----|-----|-------|
| action | string | Indicates the type of action such as `edit`, `add`, and `delete` performed in the datasource range. |
| data | object[] | Modified data for `edit` action; New data for `add` action; Deleted data for `delete` action. |
| rangeIndex | number | Specifies the range index of the datasource. |
| sheetIndex | number | Specifies the sheet index of the datasource. |

> For `add` action, the value for all the fields will be `null` in the data. In the case that you do not want the primary key field to be null which needs to be updated in the backend service, you can use `edit` action after updating the primary key field to update in the backend service. <br><br>
> For inserting a row at the end of the datasource range, you should insert a row below at the end of the range to trigger the `dataSourceChanged` event with action `add`.

{% tab template="spreadsheet/dynamic-data-binding", sourceFiles="app/**/*.tsx,index.html", iframeHeight="750px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { SpreadsheetComponent, SheetsDirective, SheetDirective, RangesDirective } from '@syncfusion/ej2-react-spreadsheet';
import { defaultData, itemData } from './datasource';
import { RangeDirective, ColumnsDirective, ColumnDirective } from '@syncfusion/ej2-react-spreadsheet';
export default class App extends React.Component<{}, {}> {
    spreadsheet: SpreadsheetComponent;
    dataSourceChanged(args) {
        this.appendElement("Data source changed with" + "<b>&nbsp;" + args.action + "</b> action<hr>");
    }

    btnClick() {
        this.spreadsheet.sheets[0].ranges[0].dataSource = itemData;
    }

    clearBtnClick() {
        document.getElementById('EventLog').innerHTML = "";
    }

    appendElement(html) {
        var span = document.createElement("span");
        span.innerHTML = html;
        var log = document.getElementById('EventLog');
        log.insertBefore(span, log.firstChild);
    }
     render() {
        return  (<div>
              <div>
                <button id="changeDataBtn" className='e-btn' onClick={this.btnClick.bind(this)}>Change Datasource</button>
              <SpreadsheetComponent ref={(ssObj) => { this.spreadsheet = ssObj; }} dataSourceChanged={this.dataSourceChanged.bind(this)}>
                <SheetsDirective>
                  <SheetDirective>
                    <RangesDirective>
                      <RangeDirective dataSource={defaultData}></RangeDirective>
                    </RangesDirective>

                    <ColumnsDirective>
                      <ColumnDirective width={180}></ColumnDirective>
                      <ColumnDirective width={130}></ColumnDirective>
                      <ColumnDirective width={130}></ColumnDirective>
                      <ColumnDirective width={180}></ColumnDirective>
                      <ColumnDirective width={130}></ColumnDirective>
                      <ColumnDirective width={120}></ColumnDirective>
                    </ColumnsDirective>
                  </SheetDirective>
                </SheetsDirective>
              </SpreadsheetComponent>
              </div>
              <div>
                <h4><b>Event Trace</b></h4>
                <div id="evt">
                  <div style={{ height: "173px", overflow: "auto", width: "250px" }}>
                    <span id="EventLog" ></span>
                  </div>
                  <button id="clearBtn" className='e-btn' onClick={this.clearBtnClick.bind(this)}>Clear</button>
                </div>
              </div>
            </div>);
    }
}
ReactDOM.render(<App />, document.getElementById('root'));
```

{% endtab %}

## Note

You can refer to our [React Spreadsheet](https://www.syncfusion.com/react-ui-components/react-spreadsheet) feature tour page for its groundbreaking feature representations. You can also explore our [React Spreadsheet example](https://ej2.syncfusion.com/react/demos/#/material/spreadsheet/default) to knows how to present and manipulate data.

## See Also

* [Filtering](./filter)
* [Sorting](./sort)
* [Hyperlink](./link)
* [`Collaborative Editing`](use-cases/collaborative-editing)