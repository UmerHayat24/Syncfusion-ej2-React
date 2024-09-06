---
title: "React DataManager | Getting started | Syncfusion"
component: "DataManager"
description: "Learn how to connect the React DataManager to a data source and perform queries against it. Also learn how to use DataManager with the React Data Grid Component"
---

# Getting started

## Dependencies

Below is the list of minimum dependencies required to use the DataManager.

```javascript
|-- @syncfusion/ej2-data
    |-- @syncfusion/ej2-base
    |-- es6-promise (Required when window.Promise is not available)
```

> **@syncfusion/ej2-data** requires the presence of a Promise feature in global environment. In the browser, window.Promise must be available.

## Installation and configuration

You can use [`create-react-app`](https://github.com/facebookincubator/create-react-app) to setup the applications.
To install **create-react-app** run the following command.

```sh
npm install -g create-react-app
```

* To setup basic **React** sample use following commands.

```sh
create-react-app quickstart --scripts-version=react-scripts-ts
cd quickstart
npm install
```

* Install Syncfusion packages using below command.

```sh
npm install @syncfusion/ej2-data --save
```

## Connection to a data source

The DataManager can act as gateway for both local and remote data source which will uses the query to interact with the data source.

### Binding to JSON data

[`DataManager`](https://ej2.syncfusion.com/documentation/api/data/dataManager/) can be bound to local data source by assigning the array of JavaScript objects to the **json** property or simply passing them
to the constructor while instantiating.

{% tab template="data/get-started", sourceFiles="app/App.tsx,app/rowTemplate.tsx,app/orders.tsx" %}

```typescript
import { DataManager, Query } from '@syncfusion/ej2-data';
import * as React from 'react';
import { data } from './datasource';
import { IOrders } from './orders';
import { Row } from './rowTemplate';

export default class App extends React.Component<{}, {}>{

    public result: object[] = new DataManager(data).executeLocal(new Query().take(8));

    public items: object[] = this.result.map((row: IOrders) => (<Row {...row}/>));
    public render() {
    return (<table id='datatable' className='e-table'>
            <thead>
             <tr><th>Order ID</th><th>Customer ID</th><th>Employee ID</th></tr>
            </thead>
            <tbody>{this.items}</tbody>
           </table>);
    }

}
```

{% endtab %}

### Binding to OData

[`DataManager`](https://ej2.syncfusion.com/documentation/api/data/dataManager/)  can be bound to remote data source by assigning service end point URL to the **url** property.
Now all [`DataManager`](https://ej2.syncfusion.com/documentation/api/data/dataManager/)  operations will address the provided service end point.

{% tab template="data/get-started", sourceFiles="app/App.tsx,app/rowTemplate.tsx,app/orders.tsx" %}

```typescript
import { getValue } from '@syncfusion/ej2-base';
import { DataManager, Query, ReturnOption } from '@syncfusion/ej2-data';
import * as React from 'react';
import { IOrders } from './orders';
import { Row } from './rowTemplate';


const SERVICE_URI: string = 'https://js.syncfusion.com/demos/ejServices/Wcf/Northwind.svc/Orders';

export default class App extends React.Component<{}, {}>{
    constructor(props: object) {
        super(props);
        this.state = { items: [] };
        new DataManager({ url: SERVICE_URI }).executeQuery(new Query().take(8))
        .then((e: ReturnOption) => {
            const res = (e.result as IOrders[]).map((row: IOrders) => (<Row {...row}/>));
            this.setState({
                items: res
            });
        });
     }

    public render() {
        return (<table id='datatable' className='e-table'>
                <thead>
                    <tr><th>Order ID</th><th>Customer ID</th><th>Employee ID</th></tr>
                </thead>
                <tbody>{ getValue('items', this.state) }</tbody>
            </table>)
    }

}
```

{% endtab %}

## Filter

The data filtering is a trivial operation which will let us to get reduced view of data based on filter criteria.
The filter expression can be built easily using [`where`](https://ej2.syncfusion.com/documentation/api/data/query/#where) method of [`Query`](https://ej2.syncfusion.com/documentation/api/data/query/) class.

{% tab template="data/get-started", sourceFiles="app/App.tsx,app/rowTemplate.tsx,app/orders.tsx" %}

```typescript
import { DataManager, Query } from '@syncfusion/ej2-data';
import * as React from 'react';
import { data } from './datasource';
import { IOrders } from './orders';
import { Row } from './rowTemplate';

export default class App extends React.Component<{}, {}>{

    public result: object[] = new DataManager(data).executeLocal(new Query()
        .where('EmployeeID', 'equal', 3));

    public items: object[] = this.result.map((row: IOrders) => (<Row {...row}/>));
    public render() {
    return (<table id='datatable' className='e-table'>
            <thead>
             <tr><th>Order ID</th><th>Customer ID</th><th>Employee ID</th></tr>
            </thead>
            <tbody>{this.items}</tbody>
           </table>);
    }

}
```

{% endtab %}

## Sort

The data can be ordered either in ascending or descending using [`sortBy`](https://ej2.syncfusion.com/documentation/api/data/query/#sortby) method of [`Query`](https://ej2.syncfusion.com/documentation/api/data/query/) class.

{% tab template="data/get-started", sourceFiles="app/App.tsx,app/rowTemplate.tsx,app/orders.tsx" %}

```typescript
import { DataManager, Query } from '@syncfusion/ej2-data';
import * as React from 'react';
import { data } from './datasource';
import { IOrders } from './orders';
import { Row } from './rowTemplate';

export default class App extends React.Component<{}, {}>{

    public result: object[] = new DataManager(data).executeLocal(new Query()
        .sortBy('CustomerID').take(8));

    public items: object[] = this.result.map((row: IOrders) => (<Row {...row}/>));
    public render() {
        return (<table id='datatable' className='e-table'>
                <thead>
                <tr><th>Order ID</th><th>Customer ID</th><th>Employee ID</th></tr>
                </thead>
                <tbody>{this.items}</tbody>
            </table>);
    }

}
```

{% endtab %}

## Page

The [`page`](https://ej2.syncfusion.com/documentation/api/data/query/#page) method of the Query class is used to get range of data based on the page number and the total page size.

{% tab template="data/get-started", sourceFiles="app/App.tsx,app/rowTemplate.tsx,app/orders.tsx" %}

```typescript
import { DataManager, Query } from '@syncfusion/ej2-data';
import * as React from 'react';
import { data } from './datasource';
import { IOrders } from './orders';
import { Row } from './rowTemplate';

export default class App extends React.Component<{}, {}>{

    public result: object[] = new DataManager(data).executeLocal(new Query()
        .page(1, 8));

    public items: object[] = this.result.map((row: IOrders) => (<Row {...row}/>));
    public render() {
        return (<table id='datatable' className='e-table'>
                <thead>
                <tr><th>Order ID</th><th>Customer ID</th><th>Employee ID</th></tr>
                </thead>
                <tbody>{this.items}</tbody>
            </table>);
    }

}
```

{% endtab %}

## Component binding

DataManager component can be used with Syncfusion components which supports data binding.

### Local data binding

A DataSource can be created in-line with other Syncfusion component configuration settings.

{% tab template="data/component-binding", sourceFiles="app/App.tsx" %}

```typescript
import { DataManager } from '@syncfusion/ej2-data';
import { ColumnDirective, ColumnsDirective, GridComponent} from '@syncfusion/ej2-react-grids';
import * as React from "react";
import './App.css';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
    public data: DataManager = new DataManager(data);
    public render(){
        return <GridComponent  dataSource={this.data}>
                <ColumnsDirective>
                 <ColumnDirective field='OrderID' width='100' textAlign="Right"/>
                 <ColumnDirective field='CustomerID' width='100'/>
                 <ColumnDirective field='EmployeeID' width='100' textAlign="Right"/>
                 <ColumnDirective field='Freight' width='100' format="C2" textAlign="Right"/>
                 <ColumnDirective field='ShipCountry' width='100'/>
               </ColumnsDirective>
              </GridComponent>
    }
};
```

{% endtab %}

### Remote data binding

To bind remote data to Syncfusion component, you can assign a service data as an instance of [`DataManager`](https://ej2.syncfusion.com/documentation/api/data/dataManager/) to the **dataSource** property.

{% tab template="data/component-binding", sourceFiles="app/App.tsx" %}

```typescript
import { DataManager } from '@syncfusion/ej2-data';
import { ColumnDirective, ColumnsDirective, GridComponent} from '@syncfusion/ej2-react-grids';
import * as React from "react";
import './App.css';

const SERVICE_URI = 'http://js.syncfusion.com/demos/ejServices/Wcf/Northwind.svc/Orders/?$top=20';

export default class App extends React.Component<{}, {}>{
    public data: DataManager = new DataManager({ url: SERVICE_URI });
    public render(){
        return <GridComponent  dataSource={this.data}>
                <ColumnsDirective>
                 <ColumnDirective field='OrderID' width='100' textAlign="Right"/>
                 <ColumnDirective field='CustomerID' width='100'/>
                 <ColumnDirective field='EmployeeID' width='100' textAlign="Right"/>
                 <ColumnDirective field='Freight' width='100' format="C2" textAlign="Right"/>
                 <ColumnDirective field='ShipCountry' width='100'/>
               </ColumnsDirective>
              </GridComponent>
    }
};
```

{% endtab %}
