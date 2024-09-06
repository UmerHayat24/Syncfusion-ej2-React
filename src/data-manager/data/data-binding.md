---
title: "React DataManager | Data Binding | Syncfusion"
component: "DataManager"
description: "Learn how to consume local and remote data sources using the React DataManager."
---

# Data Binding

[`DataManager`](https://ej2.syncfusion.com/documentation/api/data/dataManager/) supports both RESTful JSON data services binding and local JavaScript object array binding.

## Local data binding

[`DataManager`](https://ej2.syncfusion.com/documentation/api/data/dataManager/) can be bound to local data source by assigning the
array of JavaScript objects to the `json` property or simply passing them
to the constructor while instantiating. Now the JavaScript object array can be queried and manipulated.

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

## Remote data binding

[`DataManager`](https://ej2.syncfusion.com/documentation/api/data/dataManager/) can be bound to remote data source by assigning service end point URL to the `url` property. With the
provided **url**, the [`DataManager`](https://ej2.syncfusion.com/documentation/api/data/dataManager/) handles all communication with the
data server with help of queries.

When querying data, the [`DataManager`](https://ej2.syncfusion.com/documentation/api/data/dataManager/) will convert the query object, [`Query`](https://ej2.syncfusion.com/documentation/api/data/query/) into server request after calling
**executeQuery** and waits for the server response(`JSON` format).

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
> The queried data will not be cached locally unless offline mode is enabled.

## See Also

* [Binding with OData service](./adaptors/#odata-adaptor)
* [Binding with ODataV4 service](./adaptors/#odatav4-adaptor)
* [Binding with Web API](./adaptors/#web-api-adaptor)
* [How to write custom adaptor](./adaptors/#writing-custom-adaptor)
* [How to work in offline mode](./how-to/#work-in-offline-mode)
* [How to send additional parameters](./how-to/#sending-additional-parameters-to-server)
* [How to add custom request headers](./how-to/#adding-custom-headers)