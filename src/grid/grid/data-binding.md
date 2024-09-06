---
title: "Data Binding"
component: "Grid"
description: "Learn how to bind local and remote data in the Essential JS 2 DataGrid control."
---

# Data Binding

The Grid uses **DataManager** which supports both RESTful JSON data services binding and local JavaScript object array binding.
The [`dataSource`](../api/grid/#datasource) property can be assigned either with the instance of [`DataManager`](https://ej2.syncfusion.com/react/documentation/data/getting-started/) or JavaScript object collection.
It supports two kind of data binding method they are,
* Local data
* Remote data

To get start quickly with Data Binding, you can check on this video:

`youtube:UgeX6JMoqfs`

## Local Data

To bind local data to the grid, you can assign a JavaScript object array to the
 [`dataSource`](../api/grid/#datasource) property.
 The local data source can also be provided as an instance of the [`DataManager`](https://ej2.syncfusion.com/react/documentation/data/getting-started/).

{% tab template="grid/data-binding", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
    public data: object[] = data.slice(0, 7);
    public render() {
        return <GridComponent dataSource={this.data}>
                <ColumnsDirective>
                    <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign="Right"/>
                    <ColumnDirective field='CustomerID' headerText='Customer ID' width='150'/>
                    <ColumnDirective field='ShipCity' headerText='Ship City' width='150'/>
                    <ColumnDirective field='ShipName' headerText='Ship Name' width='150'/>
                </ColumnsDirective>
               </GridComponent>
    }
};
```

{% endtab %}

> By default **DataManager** uses [`JsonAdaptor`](https://ej2.syncfusion.com/react/documentation/data/adaptors/#json-adaptor) for local data-binding.

## Remote Data

To bind remote data to grid component, assign service data as an instance of **DataManager** to the
[`dataSource`](../api/grid/#datasource) property. To interact with remote data source, provide the endpoint **url**.

{% tab template="grid/data-binding", sourceFiles="app/App.tsx" %}

```typescript
import { DataManager } from '@syncfusion/ej2-data';
import { ColumnDirective, ColumnsDirective, GridComponent } from '@syncfusion/ej2-react-grids';
import * as React from 'react';

export default class App extends React.Component<{}, {}>{
    public data = new DataManager({
                      url: 'https://js.syncfusion.com/demos/ejServices/Wcf/Northwind.svc/Orders/'s
                    });
    public render() {
        return <GridComponent dataSource={this.data} height={315}>
                <ColumnsDirective>
                    <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign="Right"/>
                    <ColumnDirective field='CustomerID' headerText='Customer ID' width='150'/>
                    <ColumnDirective field='ShipCity' headerText='Ship City' width='150'/>
                    <ColumnDirective field='ShipName' headerText='Ship Name' width='150'/>
                </ColumnsDirective>
               </GridComponent>
    }
}
```

{% endtab %}

> By default **DataManager** uses [`ODataAdaptor`](https://ej2.syncfusion.com/react/documentation/data/adaptors/#odata-adaptor) for remote data-binding.

### Binding with OData Services

[OData](http://www.odata.org/documentation/odata-version-3-0/) is standardized protocol for creating and consuming data.
You can retrieve data from OData service using DataManager. You can refer to the following code example of remote Data binding using OData service.

{% tab template="grid/data-binding", sourceFiles="app/App.tsx" %}

```typescript
import { DataManager, ODataAdaptor } from '@syncfusion/ej2-data';
import { ColumnDirective, ColumnsDirective, GridComponent } from '@syncfusion/ej2-react-grids';
import * as React from 'react';

export default class App extends React.Component<{}, {}>{
    public data = new DataManager({
                    adaptor: new ODataAdaptor,
                    url: 'https://js.syncfusion.com/demos/ejServices/Wcf/Northwind.svc/Orders/'
                });
    public render() {
        return <GridComponent dataSource={this.data} height={315}>
                <ColumnsDirective>
                    <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign="Right"/>
                    <ColumnDirective field='CustomerID' headerText='Customer ID' width='150'/>
                    <ColumnDirective field='ShipCity' headerText='Ship City' width='150'/>
                    <ColumnDirective field='ShipName' headerText='Ship Name' width='150'/>
                </ColumnsDirective>
               </GridComponent>
    }
}
```

{% endtab %}

### Binding with OData v4 services

The ODataV4 is an improved version of OData protocols, and the **DataManager** can also retrieve and consume OData v4 services.
 For more details on OData v4 services, refer to the
 [odata documentation](http://docs.oasis-open.org/odata/odata/v4.0/errata03/os/complete/part1-protocol/odata-v4.0-errata03-os-part1-protocol-complete.html#_Toc453752197).
To bind OData v4 service, use the [`ODataV4Adaptor`](https://ej2.syncfusion.com/react/documentation/data/adaptors/#odatav4-adaptor).

{% tab template="grid/data-binding", sourceFiles="app/App.tsx" %}

```typescript
import { DataManager, ODataV4Adaptor } from '@syncfusion/ej2-data';
import { ColumnDirective, ColumnsDirective, GridComponent } from '@syncfusion/ej2-react-grids';
import * as React from 'react';

export default class App extends React.Component<{}, {}>{
    public data = new DataManager({
                    adaptor: new ODataV4Adaptor,
                    url: 'https://services.odata.org/V4/Northwind/Northwind.svc/Orders/?$top=7'
                });
    public render() {
        return <GridComponent dataSource={this.data}>
                <ColumnsDirective>
                    <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign="Right"/>
                    <ColumnDirective field='CustomerID' headerText='Customer ID' width='150'/>
                    <ColumnDirective field='ShipCity' headerText='Ship City' width='150'/>
                    <ColumnDirective field='ShipName' headerText='Ship Name' width='150'/>
                </ColumnsDirective>
               </GridComponent>
    }
}
```

{% endtab %}

### Web API

You can use [`WebApiAdaptor`](https://ej2.syncfusion.com/react/documentation/data/adaptors/#web-api-adaptor) to bind grid with Web API created using OData endpoint.

```typescript
import { DataManager, WebApiAdaptor } from '@syncfusion/ej2-data';
import { ColumnDirective, ColumnsDirective, GridComponent } from '@syncfusion/ej2-react-grids';
import * as React from 'react';

export default class App extends React.Component<{}, {}>{
    public data = new DataManager({
                    adaptor: new WebApiAdaptor,
                    url: '/api/OrderApi'
                });
    public render() {
        return <GridComponent dataSource={this.data}>
                <ColumnsDirective>
                    <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign="Right"/>
                    <ColumnDirective field='CustomerID' headerText='Customer ID' width='150'/>
                    <ColumnDirective field='ShipCity' headerText='Ship City' width='150' />
                    <ColumnDirective field='ShipName' headerText='Ship Name' width='150'/>
                </ColumnsDirective>
               </GridComponent>
    }
};
```

The response object should contain properties **Items** and **Count** whose values are collection of entities and total count of the entities respectively.

The sample response object should look like below.

```json
{
    Items: [{..}, {..}, {..}, ...],
    Count: 830
}
```

### Remote Save Adaptor

You may need to perform all Grid Actions in client-side except the CRUD operations, that should be interacted with server-side to persist data. It can be achieved in Grid by using **RemoteSaveAdaptor**.

Datasource must be set to **json** property and set **RemoteSaveAdaptor** to the **adaptor** property. CRUD operations can be mapped to server-side using **updateUrl**, **insertUrl**, **removeUrl**, **batchUrl**, **crudUrl** properties.

You can use the following code example to use **RemoteSaveAdaptor** in Grid.

```typescript
import { DataManager, RemoteSaveAdaptor } from '@syncfusion/ej2-data';
import { ColumnDirective, ColumnsDirective, Edit,  EditSettingsModel } from '@syncfusion/ej2-react-grids';
import { GridComponent, Inject, Toolbar, ToolbarItems } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
    public dataSource = new DataManager({
                        adaptor: new RemoteSaveAdaptor,
                        insertUrl: '/Home/Insert',
                        json: data,
                        removeUrl: '/Home/Delete',
                        updateUrl: '/Home/Update'
                    });
    public toolbarOptions: ToolbarItems[] = ['Add', 'Edit', 'Delete', 'Update', 'Cancel'];
    public editSettings: EditSettingsModel = { allowEditing: true, allowAdding: true, allowDeleting: true };

    public render() {
        return <GridComponent dataSource={this.dataSource} editSettings={this.editSettings} toolbar={this.toolbarOptions}>
                    <ColumnsDirective>
                        <ColumnDirective field='OrderID' headerText='Order ID' isPrimaryKey={true} width='120' textAlign="Right"/>
                        <ColumnDirective field='CustomerID' headerText='Customer ID' width='150'/>
                        <ColumnDirective field='ShipCity' headerText='Ship City' width='150'/>
                        <ColumnDirective field='ShipName' headerText='Ship Name' width='150'/>
                    </ColumnsDirective>
                    <Inject services={[Edit, Toolbar]} />
               </GridComponent>
    }
}
```

The following code example describes the CRUD operations handled at server-side.

```json
    public ActionResult Update(OrdersDetails value)
    {
        ...
        return Json(value);
    }
    public ActionResult Insert(OrdersDetails value)
    {
        ...
        return Json(value);
    }
    public ActionResult Delete(int key)
    {
        ...
        return Json(data);
    }
```

### Custom Adaptor

You can create your own adaptor by extending the built-in adaptors. For the sake of demonstrating custom adaptor approach,
we are going to see how to add serial number for the records
by overriding the built-in response processing using **processResponse** method of the [`ODataAdaptor`](https://ej2.syncfusion.com/react/documentation/data/adaptors/#odata-adaptor).

{% tab template="grid/data-binding", sourceFiles="app/App.tsx,app/SerialNoAdaptor.tsx" %}

```typescript
import { DataManager } from '@syncfusion/ej2-data';
import { ColumnDirective, ColumnsDirective, GridComponent } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { SerialNoAdaptor } from './SerialNoAdaptor';

export default class App extends React.Component<{}, {}>{
    public data = new DataManager({
                    adaptor: new SerialNoAdaptor,
                    url: 'https://js.syncfusion.com/demos/ejServices/Wcf/Northwind.svc/Orders/'
                });
    public render() {
        return <GridComponent dataSource={this.data} height={315}>
                <ColumnsDirective>
                    <ColumnDirective field='Sno' headerText='SNO' width='120' textAlign="Right"/>
                    <ColumnDirective field='CustomerID' headerText='Customer ID' width='150'/>
                    <ColumnDirective field='ShipCity' headerText='Ship City' width='150'/>
                    <ColumnDirective field='ShipName' headerText='Ship Name' width='150'/>
                </ColumnsDirective>
               </GridComponent>
    }
};
```

{% endtab %}

### Offline mode

On remote data binding, all grid actions such as paging, sorting, editing, grouping, filtering, etc, will be processed on server-side.
 To avoid post back for every action, set the grid to load all data on initialization and make the actions process in client-side.
 To enable this behavior, use the **offline** property of **DataManager**.

{% tab template="grid/data-binding", sourceFiles="app/App.tsx" %}

```typescript
import { DataManager, ODataAdaptor } from '@syncfusion/ej2-data';
import { ColumnDirective, ColumnsDirective, GridComponent, Group } from '@syncfusion/ej2-react-grids';
import { Inject, Page, PageSettingsModel, Sort } from '@syncfusion/ej2-react-grids';
import * as React from 'react';

export default class App extends React.Component<{}, {}>{
    public data = new DataManager({
                    adaptor: new ODataAdaptor,
                    offline: true,
                    url: 'https://js.syncfusion.com/demos/ejServices/Wcf/Northwind.svc/Orders/'
                });
    public page: PageSettingsModel = {pageSize:7};
    public render() {
        return <GridComponent dataSource={this.data} allowPaging={true} allowGrouping={true} allowSorting={true} pageSettings={this.page}>
                <Inject services={[Page, Group, Sort]}/>
                <ColumnsDirective>
                    <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign="Right"/>
                    <ColumnDirective field='CustomerID' headerText='Customer ID' width='150'/>
                    <ColumnDirective field='ShipCity' headerText='Ship City' width='150'/>
                    <ColumnDirective field='ShipName' headerText='Ship Name' width='150'/>
                </ColumnsDirective>
               </GridComponent>
    }
}
```

{% endtab %}

### Sending additional parameters to server

To add a custom parameter to the data request, use the [`addParams`](https://ej2.syncfusion.com/documentation/api/data/query/#addparams) method of [`Query`](https://ej2.syncfusion.com/documentation/api/data/query/#query) class.
Assign the [`Query`](https://ej2.syncfusion.com/documentation/api/data/query/#query) object with additional parameters to the grid [`query`](../api/grid/#query) property.

{% tab template="grid/data-binding", sourceFiles="app/App.tsx" %}

```typescript
import { DataManager, ODataAdaptor, Query } from '@syncfusion/ej2-data';
import { ColumnDirective, ColumnsDirective, GridComponent } from '@syncfusion/ej2-react-grids';
import * as React from 'react';

export default class App extends React.Component<{}, {}>{
    public data = new DataManager({
        adaptor: new ODataAdaptor,
        url: 'https://js.syncfusion.com/demos/ejServices/Wcf/Northwind.svc/Orders/'
    });
    public query = new Query().addParams('ej2grid', 'true');
    public render() {
        return <GridComponent dataSource={this.data} query={this.query}>
                <ColumnsDirective>
                    <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign="Right"/>
                    <ColumnDirective field='CustomerID' headerText='Customer ID' width='150'/>
                    <ColumnDirective field='ShipCity' headerText='Ship City' width='150'/>
                    <ColumnDirective field='ShipName' headerText='Ship Name' width='150'/>
                </ColumnsDirective>
               </GridComponent>
    }
}
```

{% endtab %}

> The parameters added using the [`query`](../api/grid/#query) property will be sent along with the data request for every grid action.

### Handle Http Error

During server interaction from the grid, some server-side exceptions may occur, and you can acquire those error messages or exception details
in client-side using the [`actionFailure`](../api/grid/#actionfailure) event.

The argument passed to the [`actionFailure`](../api/grid/#actionfailure) Grid event contains the error details returned from server.

{% tab template="grid/data-binding", sourceFiles="app/App.tsx" %}

```typescript
import { DataManager } from '@syncfusion/ej2-data';
import { ColumnDirective, ColumnsDirective, FailureEventArgs, Grid, GridComponent } from '@syncfusion/ej2-react-grids';
import * as React from 'react';

export default class App extends React.Component<{}, {}>{
    public data = new DataManager({
                      url: 'http://services.odata.org/invalidurl'
                    });
    public grid: Grid | null;
    public render() {
        this.onActionFailure = this.onActionFailure.bind(this);
        return <GridComponent dataSource={this.data} ref={g => this.grid = g} actionFailure={this.onActionFailure}>
                <ColumnsDirective>
                    <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign="Right"/>
                    <ColumnDirective field='CustomerID' headerText='Customer ID' width='150'/>
                    <ColumnDirective field='ShipCity' headerText='Ship City' width='150'/>
                    <ColumnDirective field='ShipName' headerText='Ship Name' width='150'/>
                </ColumnsDirective>
               </GridComponent>
    }

    public onActionFailure = (e: FailureEventArgs) => {
        const span: HTMLElement = document.createElement('span');
        if (this.grid) {
            (this.grid.element.parentNode as HTMLElement).insertBefore(span, this.grid.element);
            span.style.color = "#FF0000";
            span.innerHTML = "Server exception: 404 Not found";
        }
    }
}
```

{% endtab %}

> The [`actionFailure`](../api/grid/#actionfailure) event will be triggered not only for the server errors, but
also when there is an exception while processing the Grid actions.

## Custom Binding

It is possible to handle data processing externally and bind the result to the Grid. This help you to provide your own custom data logic. Grid expects an object as the result of the custom logic and the emitted value should be an object with properties **result** and **count**.

> In this context, we are going to use [`Ajax`](https://ej2.syncfusion.com/documentation/api/base/ajax/) from our **@syncfusion/ej2-base** library for handling remote interaction, you can choose any HTTP client as per your choice.

```typescript
import { Ajax, getValue } from '@syncfusion/ej2-base';
import { ColumnDirective, ColumnsDirective, DataStateChangeEventArgs, Grid, GridComponent } from '@syncfusion/ej2-react-grids';
import { Inject, Page, PageSettingsModel } from '@syncfusion/ej2-react-grids';
import { DataResult } from '@syncfusion/ej2-react-grids';
import * as React from 'react';

export default class App extends React.Component<{}, {}> {
    public orderService: OrderService = new OrderService();
    public grid: Grid | null;
    public data: any;
    public pageSettings: PageSettingsModel = { pageSize: 10 };
    public renderComplete() {
        if(this.grid && (this.grid.dataSource instanceof Array
            && !(this.grid.dataSource as object[]).length)) {
            const state = { skip: 0, take: 10 };
            this.dataStateChange(state);
        }
    }
    public dataStateChange(state : DataStateChangeEventArgs) {
      this.orderService.execute(state).then(( gridData ) => {
          if(this.grid) {
            this.grid.dataSource = gridData
          }
        });
    }
    public render() {
      this.renderComplete = this.renderComplete.bind(this);
      this.dataStateChange = this.dataStateChange.bind(this);
      return (
        <div className='control-pane'>
          <div className='control-section'>
            <GridComponent dataSource={this.data} ref={g => this.grid = g} pageSettings={this.pageSettings}
              dataBound={this.renderComplete} dataStateChange={this.dataStateChange} allowPaging={true}>
              <ColumnsDirective>
                <ColumnDirective field='OrderID' headerText='Order ID' width='120'/>
                <ColumnDirective field='CustomerID' headerText='Customer Name' width='150'/>
                <ColumnDirective field='ShipName' headerText='Ship Name' width='120' />
                <ColumnDirective field='ShipCity' headerText='Ship City' width='150'/>
              </ColumnsDirective>
              <Inject services={[Page]} />
            </GridComponent>
          </div>
        </div>)
    }
  };

  export class OrderService {
    public ajax: Ajax = new Ajax({
        mode: true,
        onFailure: (e: Error) => false,
        type: 'GET'
    });
    private BASE_URL: string = 'https://js.syncfusion.com/demos/ejServices/Wcf/Northwind.svc/Orders';
  
    public execute(state: DataStateChangeEventArgs): Promise<DataResult> {
        return this.getData(state);
    }
  
    private getData(state: DataStateChangeEventArgs): Promise<DataResult> {
        const pageQuery = `$skip=${state.skip}&$top=${state.take}`;
        this.ajax.url = `${this.BASE_URL}?${pageQuery}&$inlinecount=allpages&$format=json`;

        return this.ajax.send().then((response: any) => {
            const data: any = JSON.parse(response);
            return {
                count:  parseInt(getValue('d.__count', data), 10),
                result: getValue('d.results', data)
            };
        });
    }
  };
```

### Handling Grid actions

For grid actions such as **paging**, **grouping**, **sorting** etc, the [`dataStateChange`](https://ej2.syncfusion.com/react/documentation/api/grid/#datastatechange) event will be invoked. You have to query and resolve data using [`Ajax`](https://ej2.syncfusion.com/documentation/api/base/ajax/) in this event based on the state arguments.

```typescript
import { Ajax, getValue } from '@syncfusion/ej2-base';
import { ColumnDirective, ColumnsDirective, DataStateChangeEventArgs, Grid, GridComponent } from '@syncfusion/ej2-react-grids';
import { Group, Inject, Page, PageSettingsModel, Sort } from '@syncfusion/ej2-react-grids';
import { DataResult, Sorts } from '@syncfusion/ej2-react-grids';
import * as React from 'react';


export default class App extends React.Component<{}, {}> {
    public orderService: OrderService = new OrderService();
    public grid: Grid | null;
    public data: any;
    public pageSettings: PageSettingsModel = { pageSize: 10 };
    public renderComplete() {
        if(this.grid && (this.grid.dataSource instanceof Array
            && !(this.grid.dataSource as object[]).length)) {
            const state = { skip: 0, take: 10 };
            this.dataStateChange(state);
        }
    }
    public dataStateChange(state : DataStateChangeEventArgs) {
      this.orderService.execute(state).then(( gridData ) => {
          if(this.grid) {
            this.grid.dataSource = gridData
          }
        });
    }
    public render() {
      this.renderComplete = this.renderComplete.bind(this);
      this.dataStateChange = this.dataStateChange.bind(this);
      return (
        <div className='control-pane'>
          <div className='control-section'>
            <GridComponent dataSource={this.data} ref={g => this.grid = g} pageSettings={this.pageSettings}
              dataBound={this.renderComplete} dataStateChange={this.dataStateChange} allowPaging={true}
              allowGrouping={true} allowSorting={true}>
              <ColumnsDirective>
                <ColumnDirective field='OrderID' headerText='Order ID' width='120'/>
                <ColumnDirective field='CustomerID' headerText='Customer Name' width='150'/>
                <ColumnDirective field='ShipName' headerText='Ship Name' width='120' />
                <ColumnDirective field='ShipCity' headerText='Ship City' width='150'/>
              </ColumnsDirective>
              <Inject services={[Page, Sort, Group]} />
            </GridComponent>
          </div>
        </div>)
    }
  };

export class OrderService {
    public ajax: Ajax = new Ajax({
        mode: true,
        onFailure: (e: Error) => false,
        type: 'GET'
    });
    private BASE_URL: string = 'https://js.syncfusion.com/demos/ejServices/Wcf/Northwind.svc/Orders';
  
    public execute(state: DataStateChangeEventArgs): Promise<DataResult> {
        return this.getData(state);
    }
  
    private getData(state: DataStateChangeEventArgs): Promise<DataResult> {
        const pageQuery = `$skip=${state.skip}&$top=${state.take}`;
        let sortQuery: string = '';
  
        if (state && (state.sorted || []).length) {
            sortQuery = `&$orderby=` + ((state).sorted as Sorts[]).map((obj: Sorts) => {
                return obj.direction === 'descending' ? `${obj.name} desc` : obj.name;
            }).reverse().join(',');
        }
  
        this.ajax.url = `${this.BASE_URL}?${pageQuery}${sortQuery}&$inlinecount=allpages&$format=json`;
  
        return this.ajax.send().then((response: any) => {
            const data: any = JSON.parse(response);
            return {
                count:  parseInt(getValue('d.__count', data), 10),
                result: getValue('d.results', data)
            };
        });
    }
  };
```

> While initial rendering, the [`dataStateChange`](https://ej2.syncfusion.com/react/documentation/api/grid/#datastatechange) event will not be triggered. You can perform the operation in the **componentDidMount** or when you want the grid to show record.

### Perform CRUD operations

The [`dataSourceChanged`](https://ej2.syncfusion.com/react/documentation/api/grid/#datasourcechanged) event will be triggered for updating the grid data. You can perform the save operation based on the event arguments and call the [`endEdit`](https://ej2.syncfusion.com/react/documentation/api/grid/#endedit) method to indicate the completion of save operation.

```typescript
import { Ajax, getValue } from '@syncfusion/ej2-base';
import { ColumnDirective, ColumnsDirective, DataStateChangeEventArgs, Grid, GridComponent } from '@syncfusion/ej2-react-grids';
import { DataResult, DataSourceChangedEventArgs, Edit, Inject, Page, PageSettingsModel, Toolbar } from '@syncfusion/ej2-react-grids';
import * as React from 'react';

export default class App extends React.Component<{}, {}> {
    public orderService: OrderService = new OrderService();
    public grid: Grid | null;
    public data: any;  
    public toolbarOptions: any = ['Add', 'Edit', 'Delete', 'Update', 'Cancel'];
    public editSettings: any = { allowEditing: true, allowAdding: true, allowDeleting: true };
  
    public pageSettings: PageSettingsModel = { pageSize: 10 };
    public renderComplete() {
        if(this.grid && (this.grid.dataSource instanceof Array
            && !(this.grid.dataSource as object[]).length)) {
            const state = { skip: 0, take: 10 };
            this.dataStateChange(state);
        }
    }
    public dataStateChange(state : DataStateChangeEventArgs) {
      this.orderService.execute(state).then(( gridData ) => {
        if (this.grid) {
            this.grid.dataSource = gridData
        }
      });
    }
    public dataSourceChanged(state: DataSourceChangedEventArgs): void {
      if (state.action === 'add') {
        this.orderService.addRecord(state).then(() => state.endEdit());
      } else if (state.action === 'edit') {
        this.orderService.updateRecord(state).then(() => state.endEdit());
      } else if (state.requestType === 'delete') {
        this.orderService.deleteRecord(state).then(() => state.endEdit());
      }
    }
  
    public render() {
      this.dataStateChange = this.dataStateChange.bind(this);
      this.dataSourceChanged = this.dataSourceChanged.bind(this);
      this.renderComplete = this.renderComplete.bind(this);
      return (
        <div className='control-pane'>
          <div className='control-section'>
            <GridComponent dataSource={this.data} ref={g => this.grid = g} editSettings={this.editSettings}
              toolbar={this.toolbarOptions} allowPaging={true} allowSorting={true} pageSettings={this.pageSettings}
              allowGrouping={true} dataStateChange={this.dataStateChange}
              dataSourceChanged={this.dataSourceChanged} dataBound={this.renderComplete}>
              <ColumnsDirective>
                <ColumnDirective field='OrderID' headerText='Order ID' width='120'/>
                <ColumnDirective field='CustomerID' headerText='Customer Name' width='150'/>
                <ColumnDirective field='ShipName' headerText='Ship Name' width='120' />
                <ColumnDirective field='ShipCity' headerText='Ship City' width='150'/>
              </ColumnsDirective>
              <Inject services={[Page, Edit, Toolbar]} />
            </GridComponent>
          </div>
        </div>
      )
    }
  };
  
export class OrderService {
    public ajax: Ajax = new Ajax({
        mode: true,
        onFailure: (e: Error) => false,
        type: 'GET'
    });
    private BASE_URL: string = '/api/Orders';
  
    public execute(state: DataStateChangeEventArgs): Promise<DataResult> {
        return this.getData(state);
    }
    public addRecord(state: DataSourceChangedEventArgs) : Promise<DataResult> {
        const add: Ajax = new Ajax({
            mode: true,
            onFailure: (e: Error) => false,
            type: 'POST'
        });
        return add.send(JSON.stringify(state.data)).then((response: any) => {
            const data: any = JSON.parse(response);
            return data;
        });
    }
    public updateRecord(state: DataSourceChangedEventArgs) : Promise<DataResult> {
        const update: Ajax = new Ajax({
            mode: true,
            onFailure: (e: Error) => false,
            type: 'PUT'
        });
        return update.send(JSON.stringify(state.data)).then((response: any) => {
            const data: any = JSON.parse(response);
            return data;
        });
    }
    public deleteRecord(state: DataSourceChangedEventArgs) : Promise<DataResult> {
        const remove: Ajax = new Ajax({
            mode: true,
            onFailure: (e: Error) => false,
            type: 'DELETE'
        });
        return remove.send(JSON.stringify((state.data && state.data[0]))).then((response: any) => {
            const data: any = JSON.parse(response);
            return data;
        });
    }
    private getData(state: DataStateChangeEventArgs): Promise<DataResult> {
        const pageQuery = state.skip ? `$skip=${state.skip}&$top=${state.take}` : `$top=${state.take}`;
        this.ajax.url = `${this.BASE_URL}?${pageQuery}&$inlinecount=allpages&$format=json`;
  
        return this.ajax.send().then((response: any) => {
            const data: any = JSON.parse(response);
            return {
                count:  parseInt(getValue('d.__count', data), 10),
                result: getValue('d.results', data)
            };
        });
    }
  };
```

### Calculate aggregates

The footer aggregate values  should be calculated and send along with the **dataSource** property as follows. The aggregate property of the data source should contain the aggregate value assigned to the property named in the **field – type** format. For example, the **Sum** aggregate value for the **Freight** field should be assigned to the property named as **Freight - sum**.

```json
{
    result: [{..}, {..}, {..}, ...],
    count: 830,
    aggregates: { 'Freight - sum' : 450,'EmployeeID - min': 1 }
}
```

> The group footer and caption aggregate values will be calculated by the Grid itself.

### Provide Excel filter data source

The [`dataStateChange`](https://ej2.syncfusion.com/react/documentation/api/grid/#datastatechange) event will be triggered with appropriate arguments when the excel filter requests the filter choice data source. You need to resolve the excel filter data source using the **dataSource** resolver function from the state argument as follows.

```typescript
import { ColumnDirective, ColumnsDirective, DataStateChangeEventArgs, Grid, GridComponent } from '@syncfusion/ej2-react-grids';
import { Filter, FilterSettingsModel, Inject, Page, PageSettingsModel } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { OrderService } from './OrderService';

export default class App extends React.Component<{}, {}> {
    public orderService: OrderService = new OrderService();
    public grid: Grid | null;
    public data: any;
    public filterSettings: FilterSettingsModel = { type: 'Excel' }
    public pageSettings: PageSettingsModel = { pageSize: 10 };
    public renderComplete() {
        if(this.grid && (this.grid.dataSource instanceof Array
            && !(this.grid.dataSource as object[]).length)) {
            const state = { skip: 0, take: 10 };
            this.dataStateChange(state);
        }
    }
    public dataStateChange(state : DataStateChangeEventArgs) {
        if (state.action && (state.action.requestType === 'filterchoicerequest'
            || state.action.requestType ==='filtersearchbegin')) {
          this.orderService.execute(state).then((e) => state.dataSource && state.dataSource(e));
        } else {
          this.orderService.execute(state).then(( gridData ) => {
            if (this.grid) {
                this.grid.dataSource = gridData
            }
          });
        }
    }
    public render() {
      this.renderComplete = this.renderComplete.bind(this);
      this.dataStateChange = this.dataStateChange.bind(this);
      return (
        <div className='control-pane'>
          <div className='control-section'>
            <GridComponent dataSource={this.data} ref={g => this.grid = g} allowFiltering={true} allowPaging={true}
                pageSettings={{ pageCount: 4, pageSize: 10 }} dataStateChange={this.dataStateChange}
                dataBound={this.renderComplete} filterSettings={this.filterSettings}>
              <ColumnsDirective>
                <ColumnDirective field='OrderID' headerText='Order ID' width='120'/>
                <ColumnDirective field='CustomerID' headerText='Customer Name' width='150'/>
                <ColumnDirective field='ShipName' headerText='Ship Name' width='120' />
                <ColumnDirective field='ShipCity' headerText='Ship City' width='150'/>
              </ColumnsDirective>
              <Inject services={[Page, Filter]} />
            </GridComponent>
          </div>
        </div>)
    }
  };
```

## Binding with ajax

You can use Grid [`dataSource`](../api/grid/#datasource) property to bind the datasource to Grid from external ajax request. In the below code we have fetched the datasource from the server with the help of ajax request and provided that to [`dataSource`](../api/grid/#datasource) property by using **onSuccess** event of the ajax.

```typescript
import { Ajax } from '@syncfusion/ej2-base';
import { ColumnDirective, ColumnsDirective, Grid, GridComponent } from '@syncfusion/ej2-react-grids';
import * as React from 'react';

export default class App extends React.Component<{}, {}> {
  public grid: Grid | null;
  public componentDidMount(){
    const ajax = new Ajax("https://ej2services.syncfusion.com/production/web-services/api/Orders", "GET");
    ajax.send();
    ajax.onSuccess = (data: any) => {
      if (this.grid) {
        this.grid.dataSource = JSON.parse(data);
      }
    }
  }
    public render() {
        return (<div className='control-pane'>
        <div className='control-section'>
          <GridComponent ref={g => this.grid = g}>
            <ColumnsDirective>
              <ColumnDirective field='OrderID' headerText='Order ID'  textAlign='Right' width='120'/>
              <ColumnDirective field='CustomerID' headerText='Customer ID'  textAlign='Right'  width='120'/>
              <ColumnDirective field='EmployeeID' headerText='Employee ID'  textAlign='Right'  width='120'/>
              <ColumnDirective field='ShipCountry' headerText='Ship Country'  textAlign='Right'  width='120'/>
            </ColumnsDirective>
          </GridComponent>
        </div>
      </div>);
    }  
};
```

> If you bind the dataSource from this way, then it acts like a local dataSource. So you cannot perform any server side crud actions.

## See Also

* [How to perform filtering, sorting operation using custom service in React Grid](https://www.syncfusion.com/forums/166390/how-to-perform-filtering-sorting-operation-using-custom-service-in-react-grid)
* [Custom binding approach to bind data in React Grid](https://www.syncfusion.com/forums/159221/custom-binding-approach-to-bind-data-in-react-grid)
* [How to customize query parameters while performing sorting and filtering in React Grid](https://www.syncfusion.com/forums/158697/how-to-customize-query-parameters-while-performing-sorting-and-filtering-in-react-grid)
* [How to bind SQL Server data in React DataGrid using SqlClient data provider](https://www.syncfusion.com/kb/11449/how-to-bind-sql-server-data-in-react-datagrid-using-sqlclient-data-provider)
* [How to show the spinner in React Grid while binding custom data source](https://www.syncfusion.com/kb/11226/how-to-show-the-spinner-in-react-grid-while-binding-custom-data-source)