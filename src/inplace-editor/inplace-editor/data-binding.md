---
title: "Data Binding"
component: "In-place Editor"
description: "Learn how to bind local and remote data for dependent components of the Essential JS 2 React In-place Editor component."
---

# Data Binding

The Essential JS2 React In-place Editor component can load the data either from local data sources or remote data services using the `dataSource` property and it supports the data type of an array or `DataManager`. Also supports different kind of data services such as OData, OData V4, Web API and data formats such as XML, JSON, JSONP with the help of `DataManager` adaptors.

## Local

To bind local data to the Essential JS2 React In-place Editor component, you have to assign a JavaScript array of object or string to the `dataSource` property. The local data source can also be provided as an instance of the `DataManager`.

{% tab template="in-place-editor/data", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { InPlaceEditorComponent } from '@syncfusion/ej2-react-inplace-editor';
import * as React from 'react';
import './App.css';

class App extends React.Component {
  public inplaceEditorObj: InPlaceEditorComponent;

 // define the JSON of data
 public gameList: object[] = [
    { Id: '1', Name: 'Maria Anders' },
    { Id: '2', Name: 'Ana Trujillo' },
    { Id: '3', Name: 'Antonio Moreno' },
    { Id: '4', Name: 'Thomas Hardy' },
    { Id: '5', Name: 'Chiristina Berglund' },
    { Id: '6', Name: 'Hanna Moos' }
 ];

  public model = { dataSource: this.gameList, fields: { text: 'Name' }, placeholder: 'Select a customer' };

  public render() {
    return (
    <div id='container'>
        <span className="content-title"> Select customer name: </span>
        <InPlaceEditorComponent ref={(text) => { this.inplaceEditorObj = text! }} id='dropdownelement' mode='Inline' type='DropDownList' value='Maria Anders' model={this.model} />
     </div>
    );
  }
}
export default App;
```

{% endtab %}

## Remote

To bind remote data to the Essential JS2 React In-place Editor component, assign service data as an instance of `DataManager` to the `dataSource` property. To interact with remote data source, provide the endpoint URL.

### OData V4

The OData V4 is an improved version of OData protocols, and the [DataManager](../data/getting-started/) can also retrieve and consume OData V4 services. To fetch data from the server by using `DataManager` with the adaptor property configure as [ODataV4Adaptor](../data/adaptors/#odatav4-adaptor).

In the following sample, In-place Editor renders a `DropDownList` component and its `dataSource` property configured for fetching a data from the server by using `ODataV4Adaptor` with `DataManager`.

{% tab template="in-place-editor/data", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { DataManager, ODataV4Adaptor, Query } from '@syncfusion/ej2-data';
import { InPlaceEditorComponent } from '@syncfusion/ej2-react-inplace-editor';
import * as React from 'react';
import './App.css';

class App extends React.Component {
  public query: Query = new Query().from('Customers').select(['ContactName', 'CustomerID']).take(6);
  public model = {
        dataSource: new DataManager({
          adaptor: new ODataV4Adaptor,
          crossDomain: true,  
          url: 'https://services.odata.org/V4/Northwind/Northwind.svc/'
        }),
        fields: { text: 'ContactName', value: 'CustomerID' },
        placeholder: 'Select a customer',
        query: this.query
        };

  public render() {
    return (
    <div id='container'>
        <span className="content-title"> Select customer name: </span>
        <InPlaceEditorComponent id='dropdownelement' mode='Inline' type='DropDownList' value='Maria Anders' model={this.model}/>
     </div>
    );
  }
}
export default App;
```

{% endtab %}

### Web API

Data can fetch from the server by using [DataManager](../data/getting-started/) with the adaptor property configure as [WebApiAdaptor](../data/adaptors/#web-api-adaptor).

In the following sample, In-place Editor render a `DropDownList` component and its `dataSource` property configured for fetching a data from the server by using `WebApiAdaptor` with `DataManager`.

{% tab template="in-place-editor/data", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { DataManager, Query, WebApiAdaptor } from '@syncfusion/ej2-data';
import { InPlaceEditorComponent } from '@syncfusion/ej2-react-inplace-editor';
import * as React from 'react';
import './App.css';

class App extends React.Component {
  public dm: any = new DataManager({
    adaptor: new WebApiAdaptor,
    url: 'https://js.syncfusion.com/demos/ejServices/Wcf/Northwind.svc/Customers/'
    }).executeQuery(new Query().take(8)).then((e: any) => {
        this.model.dataSource = e.result.d;
  });
  public model: any = {
    dataSource: [{}],
    fields: { text: 'ContactName', value: 'CustomerID' },
    placeholder: 'Select a customer'
  };

  public render() {
    return (
    <div id='container'>
        <span className="content-title"> Select customer name: </span>
        <InPlaceEditorComponent id='dropdownelement' mode='Inline' type='DropDownList' value='Maria Anders' model={this.model}/>
     </div>
    );
  }
}
export default App;
```

{% endtab %}