---
title: "React DataManager | How To | Syncfusion"
component: "DataManager"
description: "Documentation on working in offline mode, sending additional parameters, and adding custom headers in the React DataManager"
---

# How To

## Work in offline mode

On remote data binding,
every time invoking **executeQuery** will send request to the server and the query will be
processed on server-side.
To avoid post back to server on calling **executeQuery**
to load all the data on initialization time and make the query processing in client-side.
To enable this behavior, you can use **offline** property of
[`DataManager`](https://ej2.syncfusion.com/documentation/api/data/dataManager/).

{% tab template="data/get-started", sourceFiles="app/App.tsx,app/rowTemplate.tsx,app/orders.tsx" %}

```typescript
import { getValue } from '@syncfusion/ej2-base';
import { DataManager, ODataAdaptor, Predicate, Query, ReturnOption } from '@syncfusion/ej2-data';
import * as React from 'react';
import { IOrders } from './orders';
import { Row } from './rowTemplate';

const SERVICE_URI: string = 'https://js.syncfusion.com/demos/ejServices/Wcf/Northwind.svc/Orders';

export default class App extends React.Component<{}, {}>{
    constructor(props: object) {
        super(props);
        this.state = { items: [] };
        const dm: DataManager = new DataManager({ url: SERVICE_URI, adaptor: new ODataAdaptor, offline: true }, new Query().take(8));
            dm.ready.then((e: ReturnOption) => {
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

> The loaded data will be cached in the **json** property of [`DataManager`](https://ej2.syncfusion.com/documentation/api/data/dataManager/).

## Sending additional parameters to server

You can use the [`addParams`](https://ej2.syncfusion.com/documentation/api/data/query/#addparams) method of [`Query`](https://ej2.syncfusion.com/documentation/api/data/query/) class, to add custom parameter to the data request.

{% tab template="data/get-started", sourceFiles="app/App.tsx,app/rowTemplate.tsx,app/orders.tsx" %}

```typescript
import { getValue } from '@syncfusion/ej2-base';
import { DataManager, ODataAdaptor, Query, ReturnOption } from '@syncfusion/ej2-data';
import * as React from 'react';
import { IOrders } from './orders';
import { Row } from './rowTemplate';

const SERVICE_URI: string = 'https://js.syncfusion.com/demos/ejServices/Wcf/Northwind.svc/Orders';

export default class App extends React.Component<{}, {}>{
    constructor(props: object) {
        super(props);
        this.state = { items: [] };
        new DataManager({ url: SERVICE_URI, adaptor: new ODataAdaptor })
            .executeQuery(new Query().addParams('$top', '8'))
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

## Adding custom headers

You can add custom headers to the request made by [`DataManager`](https://ej2.syncfusion.com/documentation/api/data/dataManager/) using the **headers** property.

```typescript

import { DataManager, ODataAdaptor, Query, ReturnOption } from '@syncfusion/ej2-data';

    const SERVICE_URI: string =  'https://js.syncfusion.com/demos/ejServices/Wcf/Northwind.svc/Orders';

    new DataManager({ url: SERVICE_URI, adaptor: new ODataAdaptor, headers:[{ 'syncfusion': 'true' }] })
        .executeQuery(new Query())
        .then((e: ReturnOption) => {
            // get result from e.result
        });

```

> Adding custom headers while making cross domain request will initiate preflight request.