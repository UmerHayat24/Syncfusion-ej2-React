---
title: "Collaborative Editing in Spreadsheet"
component: "Spreadsheet"
description: "This section helps to learn how to collaborative editing in Spreadsheet control"
---

# Collaborative Editing

The collaborative editing support allows you to work at a spreadsheet collaboratively with other users. Multiple users can access to the the same spreadsheet simultaneously.

> * To use Collaborative editing, inject the `CollaborativeEditing` module in the spreadsheet.

## Dependencies

The following list of dependencies are required to use the collaborative editing support in spreadsheet.

```tsx
|-- @aspnet/signalr
   |-- eventsource
   |-- request
   |-- ws

```

> * Run the command `npm i @aspnet/signalr` to install `@aspnet/signalr` packages in your application.

## Client configuration

To broadcast the data for every action is spreadsheet, you need to transfer the data to the server through `send` method in `actionComplete` event and receive the same data by using the `dataReceived` method. In the `dataReceived` method, you need to update the action to the connected clients through `updateAction` method.

The following code example shows `Collaborative Editing` support in the Spreadsheet control.

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { Spreadsheet, CollaborativeEditing } from '@syncfusion/ej2-spreadsheet';
import { SpreadsheetComponent, SheetsDirective, SheetDirective, RangesDirective } from '@syncfusion/ej2-react-spreadsheet';
import { RangeDirective, ColumnsDirective, ColumnDirective } from '@syncfusion/ej2-react-spreadsheet';
import { defaultData } from './datasource';
import * as signalR from '@aspnet/signalr';

// To Inject CollaborativeEditing module.
Spreadsheet.Inject(CollaborativeEditing);

export default class App extends React.Component<{}, {}> {
    spreadsheet: SpreadsheetComponent;
    // For signalR Hub connection
    public connection = new signalR.HubConnectionBuilder().withUrl('https://localhost:44385/hubs/spreadsheethub', { // localhost from AspNetCore service
        skipNegotiation: true,
        transport: signalR.HttpTransportType.WebSockets
    }).build();

    public onActionComplete(args): void {
        this.connection.send('BroadcastData', JSON.stringify(args)); // send the action data to the server
    }
    componentDidMount = () => {
        this.connection.on('dataReceived', (data: string) => {
            let model: CollaborativeEditArgs = JSON.parse(data) as CollaborativeEditArgs;
            this.spreadsheet.updateAction({ action: model.action, eventArgs: model.eventArgs }); // update the action to the connected clients
        });
        this.connection.start().then(() => { // to start the server
            console.log('server connected!!!');
        }).catch(err => console.log(err));
    }
    render() {
        return (<SpreadsheetComponent ref={(ssObj) => { this.spreadsheet = ssObj }} actionComplete={this.onActionComplete.bind(this)}>
            <SheetsDirective>
                <SheetDirective>
                    <RangesDirective>
                        <RangeDirective dataSource={defaultData}></RangeDirective>
                    </RangesDirective>
                    <ColumnsDirective>
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

## Server configuration

To make the communication between the server to the connected clients and from clients to the server, you need to configure the signalR Hubs using the following code.

```tsx
import * as signalR from '@aspnet/signalr';

// For signalR Hub connection
    public connection = new signalR.HubConnectionBuilder().withUrl('https://localhost:44385/hubs/spreadsheethub', { // localhost from AspNetCore service
        skipNegotiation: true,
        transport: signalR.HttpTransportType.WebSockets
    }).build();
```

## Hub configuration

Initially create a AspNetCore project and add the hub file for sending and receiving the data between server and clients.

```tsx
using Microsoft.AspNetCore.SignalR;
using System.Threading.Tasks;

namespace WebApplication.Hubs
{
    public class SpreadsheetHub : Hub
    {
        public async Task BroadcastData(string data)
        {
            await Clients.All.SendAsync("dataReceived", data);
        }
    }
}
```

To configure the SignalR middleware by registering the following service in the `ConfigureServices` method of the `Startup` class.

```tsx
    services.AddSignalR();
```

To set up the SignalR routes by calling MapHub in the `Configure` method of the `Startup` class.

```tsx
    app.UseEndpoints(endpoints =>

    {

        endpoints.MapRazorPages();

        endpoints.MapHub<SpreadsheetHub>("/spreadsheetHub");

    });
```

For hosting the service, you may use the above code snippet or download and run the [local service](https://www.syncfusion.com/downloads/support/directtrac/general/ze/WebApplication1377017438).

## Prevent the particular action update for collaborative client

Using the `action` argument from the `actionComplete` event, you can prevent the particular action update for collaborative client.

The following code example shows how to prevent collaborative client from updating the `format` action.

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { Spreadsheet, CollaborativeEditing } from '@syncfusion/ej2-spreadsheet';
import { SpreadsheetComponent, SheetsDirective, SheetDirective, RangesDirective } from '@syncfusion/ej2-react-spreadsheet';
import { RangeDirective, ColumnsDirective, ColumnDirective } from '@syncfusion/ej2-react-spreadsheet';
import { defaultData } from './datasource';
import * as signalR from '@aspnet/signalr';

// To Inject CollaborativeEditing module.
Spreadsheet.Inject(CollaborativeEditing);

export default class App extends React.Component<{}, {}> {
    spreadsheet: SpreadsheetComponent;
    // For signalR Hub connection
    public connection = new signalR.HubConnectionBuilder().withUrl('https://localhost:44385/hubs/spreadsheethub', {// localhost from AspNetCore service
        skipNegotiation: true,
        transport: signalR.HttpTransportType.WebSockets
    }).build();

    public onActionComplete(args): void {
        if (args.action != 'format') {  // prevent the format action
            this.connection.send('BroadcastData', JSON.stringify(args)); // send the action data to the server
        }
    }
    componentDidMount = () => {
        this.connection.on('dataReceived', (data: string) => {
            let model: CollaborativeEditArgs = JSON.parse(data) as CollaborativeEditArgs;
            this.spreadsheet.updateAction({ action: model.action, eventArgs: model.eventArgs }); // update the action to the connected clients
        });
        this.connection.start().then(() => { // to start the server
            console.log('server connected!!!');
        }).catch(err => console.log(err));
    }
    render() {
        return (<SpreadsheetComponent ref={(ssObj) => { this.spreadsheet = ssObj }} actionComplete={this.onActionComplete.bind(this)}>
            <SheetsDirective>
                <SheetDirective>
                    <RangesDirective>
                        <RangeDirective dataSource={defaultData}></RangeDirective>
                    </RangesDirective>
                    <ColumnsDirective>
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

* [Filtering](./filter)
* [Sorting](./sort)
* [Hyperlink](./link)