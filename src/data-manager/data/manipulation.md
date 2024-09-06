---
title: "React DataManager | CRUD Data operations | Syncfusion"
component: "DataManager"
description: "Learn how to create, update, and delete (CRUD) records from the data source by using various methods in the DataManager"
---

# CRUD Data operations

In this section, you will see in detail about how to manipulate data using
[`DataManager`](https://ej2.syncfusion.com/documentation/api/data/dataManager/). The [`DataManager`](https://ej2.syncfusion.com/documentation/api/data/dataManager/) can create, update and
delete records either in local data source or remote data source.

Each data sources uses different way in handling the CRUD operations and hence
[`DataManager`](https://ej2.syncfusion.com/documentation/api/data/dataManager/) uses data adaptors to manipulate data that can be understood by a particular data source.

## Insert

The [`insert`](https://ej2.syncfusion.com/documentation/api/data/dataManager/#insert) method of [`DataManager`](https://ej2.syncfusion.com/documentation/api/data/dataManager/) is used to add new record to the data source. For remote data source, the new record will be send along with the request to the server.

{% tab template="data/get-started", sourceFiles="app/App.tsx,app/rowTemplate.tsx" %}

```typescript
import { getValue } from '@syncfusion/ej2-base';
import { DataManager, Query, ReturnOption } from '@syncfusion/ej2-data';
import * as React from 'react';
import { data } from './datasource';
import { Row } from './rowTemplate';

export default class App extends React.Component<{}, {}>{
    public dm: DataManager;
    public style: { [x: string]: string };
    constructor(props: object) {
        super(props);
        this.state = { items: [] };
        this.style = { class: 'e-form' };
        this.dm = new DataManager(data.slice(0, 5));
        this.dm.executeQuery(new Query())
            .then((e: ReturnOption) => {
                this.setState({
                    items: (e.result as object[]).map((row: object) => (<Row {...row}/>))
                });
            });
        this.insertUpdate = this.insertUpdate.bind(this)
    }

    public insertUpdate() {
        const orderid: HTMLInputElement = document.getElementById('OrderID') as HTMLInputElement;
        const cusid: HTMLInputElement = document.getElementById('CustomerID') as HTMLInputElement;
        const empid: HTMLInputElement = document.getElementById('EmployeeID') as HTMLInputElement;
        const rowdata: { OrderID: number, CustomerID: string, EmployeeID: number } = {
            CustomerID: cusid.value,
            EmployeeID: +empid.value,
            OrderID: +orderid.value
        };
        if (!rowdata.OrderID) { return; }
        this.dm.insert(rowdata);
        this.dm.executeQuery(new Query())
            .then((e: ReturnOption) => {
                this.setState({
                    items: (e.result as object[]).map((row: object) => (<Row {...row}/>))
                });
            });
    }

    public render() {
        return (<div><div style={this.style}>
            <input type="number" id='OrderID' placeholder="Order ID" />
            <input type="text" id="CustomerID" placeholder="Customer ID" />
            <input type="number" id="EmployeeID" placeholder="Employee ID" />
            <input type="button" value="Insert" id="manipulate" onClick={this.insertUpdate} /></div>
            <div><table id='datatable' className='e-table'>
                <thead>
                    <tr><th>Order ID</th><th>Customer ID</th><th>Employee ID</th></tr>
                </thead>
                <tbody>{ getValue('items', this.state) }</tbody>
            </table>
            </div></div>)
    }
}
```

{% endtab %}

> In remote data sources, when the primary key field is an identity field, then it is advised to
return the created data in the response.

## Update

The [`update`](https://ej2.syncfusion.com/documentation/api/data/dataManager/#update) method of [`DataManager`](https://ej2.syncfusion.com/documentation/api/data/dataManager) is used to modify/update a record in the data source. For remote data source, the modified
record will be send along with the request to the server.

{% tab template="data/get-started", sourceFiles="app/App.tsx,app/rowTemplate.tsx" %}

```typescript
import { getValue } from '@syncfusion/ej2-base';
import { DataManager, Query, ReturnOption } from '@syncfusion/ej2-data';
import * as React from 'react';
import { data } from './datasource';
import { Row } from './rowTemplate';

export default class App extends React.Component<{}, {}>{
    public dm: DataManager;
    public style: { [x: string]: string };
    constructor(props: object) {
        super(props);
        this.state = { items: [] };
        this.style = { class: 'e-form' };
        this.dm = new DataManager(data.slice(0, 5));
        this.dm.executeQuery(new Query())
            .then((e: ReturnOption) => {
                this.setState({
                    items: (e.result as object[]).map((row: object) => (<Row {...row}/>))
                });
            });
        this.insertUpdate = this.insertUpdate.bind(this)
    }

    public insertUpdate() {
        const orderid: HTMLInputElement = document.getElementById('OrderID') as HTMLInputElement;
        const cusid: HTMLInputElement = document.getElementById('CustomerID') as HTMLInputElement;
        const empid: HTMLInputElement = document.getElementById('EmployeeID') as HTMLInputElement;
        const rowdata: { OrderID: number, CustomerID: string, EmployeeID: number } = {
            CustomerID: cusid.value,
            EmployeeID: +empid.value,
            OrderID: +orderid.value
        };
        if (!rowdata.OrderID) { return; }
        this.dm.update('OrderID', rowdata);
        this.dm.executeQuery(new Query())
            .then((e: ReturnOption) => {
                this.setState({
                    items: (e.result as object[]).map((row: object) => (<Row {...row}/>))
                });
            });
    }

    public render() {
        return (<div><div style={this.style}>
            <input type="number" id='OrderID' placeholder="Order ID" />
            <input type="text" id="CustomerID" placeholder="Customer ID" />
            <input type="number" id="EmployeeID" placeholder="Employee ID" />
            <input type="button" value="Update" id="manipulate" onClick={this.insertUpdate} /></div>
            <div><table id='datatable' className='e-table'>
                <thead>
                    <tr><th>Order ID</th><th>Customer ID</th><th>Employee ID</th></tr>
                </thead>
                <tbody>{ getValue('items', this.state) }</tbody>
            </table>
            </div></div>)
    }
}
```

{% endtab %}

> Primary key name is required by the `update` method to find the record to be updated.

## Remove

The [`remove`](https://ej2.syncfusion.com/documentation/api/data/dataManager/#remove) method of [`DataManager`](https://ej2.syncfusion.com/documentation/api/data/dataManager) is used to remove a record from the data source. For remote data source, the record details such as primary key and data will be send along with the request to the server.

{% tab template="data/get-started", sourceFiles="app/App.tsx,app/rowTemplate.tsx" %}

```typescript
import { getValue } from '@syncfusion/ej2-base';
import { DataManager, Query, ReturnOption } from '@syncfusion/ej2-data';
import * as React from 'react';
import { data } from './datasource';
import { Row } from './rowTemplate';

export default class App extends React.Component<{}, {}>{
    public dm: DataManager;
    public style: { [x: string]: string };
    constructor(props: object) {
        super(props);
        this.state = { items: [] };
        this.style = { class: 'e-form' };
        this.dm = new DataManager(data.slice(0, 5));
        this.dm.executeQuery(new Query())
            .then((e: ReturnOption) => {
                this.setState({
                    items: (e.result as object[]).map((row: object) => (<Row {...row}/>))
                });
            });
        this.insertUpdate = this.insertUpdate.bind(this)
    }

    public insertUpdate() {
        const orderid: HTMLInputElement = document.getElementById('OrderID') as HTMLInputElement;
        const rowdata: { OrderID: number } = {
            OrderID: +orderid.value,
        };
        if(!rowdata.OrderID) { return; }
        this.dm.remove('OrderID', rowdata);
        this.dm.executeQuery(new Query())
            .then((e: ReturnOption) => {
                this.setState({
                    items: (e.result as object[]).map((row: object) => (<Row {...row}/>))
                });
            });
    }

    public render() {
        return (<div><div style={this.style}>
            <input type="number" id='OrderID' placeholder="Order ID"/>
            <input type="button" value="Remove" id="manipulate" onClick={this.insertUpdate} /></div>
            <table id='datatable' className='e-table'>
                <thead>
                    <tr><th>Order ID</th><th>Customer ID</th><th>Employee ID</th></tr>
                </thead>
                <tbody>{ getValue('items', this.state) }</tbody>
            </table>
            </div>)
    }
}
```

{% endtab %}

> Primary key name and its value are required to find the record to be removed.

## Batch Edit Operation

[`DataManager`](https://ej2.syncfusion.com/documentation/api/data/dataManager) supports batch processing for the CRUD operations. You
can use the [`saveChanges`](https://ej2.syncfusion.com/documentation/api/data/dataManager/#savechanges) method to batch the edit operation. For remote data source, requests to add, remove and change are handled altogether at
a time rather than passing the request separately for each operation.

{% tab template="data/get-started", sourceFiles="app/App.tsx,app/rowTemplate.tsx" %}

```typescript
import { getValue } from '@syncfusion/ej2-base';
import { DataManager, Query, ReturnOption } from '@syncfusion/ej2-data';
import * as React from 'react';
import { data } from './datasource';
import { Row } from './rowTemplate';

export default class App extends React.Component<{}, {}>{
    public dm: DataManager;
    public style: { [x: string]: string };
    public changes: {
        addedRecords: object[],
        changedRecords: object[],  
        deletedRecords: object[]
    };
    constructor(props: object) {
        super(props);
        this.state = { items: [] };
        this.style = { class: 'e-form' };
        this.changes = { changedRecords: [], addedRecords: [], deletedRecords: [] };
        this.dm = new DataManager(data.slice(0, 5));
        this.dm.executeQuery(new Query())
            .then((e: ReturnOption) => {
                this.setState({
                    items: (e.result as object[]).map((row: object) => (<Row {...row}/>))
                });
            });
        this.action = this.action.bind(this);
        this.saveChanges = this.saveChanges.bind(this);
    }

    public action(event: React.MouseEvent) {
        let action: string = event.currentTarget.getAttribute('value') as string;
        action = (action === 'Update' ? 'changed' : action === 'Insert' ? 'added' : 'deleted') + 'Records';
        const orderid: HTMLInputElement = document.getElementById('OrderID') as HTMLInputElement;
        const cusid: HTMLInputElement = document.getElementById('CustomerID') as HTMLInputElement;
        const empid: HTMLInputElement = document.getElementById('EmployeeID') as HTMLInputElement;
        const rowdata: { OrderID: number, CustomerID: string, EmployeeID: number } = {
            CustomerID: cusid.value,
            EmployeeID: +empid.value,
            OrderID: +orderid.value
        };
        if (!rowdata.OrderID) { return; }
        this.changes[action].push(rowdata);
        orderid.value = cusid.value = empid.value = '';
    }

    public saveChanges(): void {
        this.dm.saveChanges(this.changes);
        this.dm.executeQuery(new Query())
            .then((e: ReturnOption) => {
                this.setState({
                    items: (e.result as object[]).map((row: object) => (<Row {...row}/>))
                });
            });
        this.changes = { changedRecords: [], addedRecords: [], deletedRecords: [] };
    }

    public render() {
        return (<div><div style={this.style}>
            <input type="number" id='OrderID' placeholder="Order ID" />
            <input type="text" id="CustomerID" placeholder="Customer ID" />
            <input type="number" id="EmployeeID" placeholder="Employee ID" />
            <input type="button" value="Insert" onClick={this.action} />
            <input type="button" value="Update" onClick={this.action} />
            <input type="button" value="Remove" onClick={this.action} /></div>
            <div style={this.style}>
                <label>Click to Save changes:</label>
                <input type="button" value="Save Changes" onClick={this.saveChanges} /></div>
            <div><table id='datatable' className='e-table'>
                <thead>
                    <tr><th>Order ID</th><th>Customer ID</th><th>Employee ID</th></tr>
                </thead>
                <tbody>{getValue('items', this.state)}</tbody>
            </table></div></div>)
    }
}
```

{% endtab %}
