---
title: "Autocomplete Data binding"
component: "AutoComplete"
description: "This section for Syncfusion react autocomplete component shows how to bind with local data source and how to fetch data from remote data service."
---

# Data Binding

The AutoComplete loads the data either from local data sources or remote data services using the
[`dataSource`](../api/auto-complete/#datasource) property .
It supports the data type of array or `DataManager`.

The AutoComplete also supports different kinds of data services such as OData, OData V4, and Web API,
and data formats such as XML, JSON, and JSONP with the help of DataManager Adaptors.

| Fields | Type | Description |
|------|------|-------------|
| value |  `number or string` | Specifies the hidden data value mapped to each list item that should contain a unique value. |
| groupBy |  `string` | Specifies the category under which the list item has to be grouped. |
| iconCss |  `string` | Specifies the icon class of each list item.|

> When binding complex data to the AutoComplete, fields should be mapped correctly. Otherwise, the selected item remains undefined.

## Binding local data

Local data can be represented in two ways as described below.

### Array of string

The AutoComplete has support to load array of primitive data such as strings and numbers.

{% tab template="autocomplete/basic", sourceFiles="app/**/*.tsx,index.html" %}

```typescript
import { AutoCompleteComponent } from '@syncfusion/ej2-react-dropdowns';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class App extends React.Component<{}, {}> {

    // define the array of string
    private sportsData: string[] = ['Badminton', 'Basketball', 'Cricket', 'Football', 'Golf', 'Hockey', 'Snooker', 'Tennis'];

    public render() {
        return (
              // specifies the tag for render the AutoComplete component
            <AutoCompleteComponent id="atcelement" dataSource={this.sportsData} placeholder="Find a game" />
        );
    }
}
ReactDOM.render(<App />, document.getElementById('sample'));
```

{% endtab %}

### Array of object

The AutoComplete can generate its list items through an array of complex data. For this, the appropriate columns should be
mapped to the [`fields`](../api/auto-complete/#fields) property.

In the following example, `sports` column from complex data have been mapped to the `value` field.

{% tab template="autocomplete/basic", sourceFiles="app/**/*.tsx,index.html" %}

```typescript

import { AutoCompleteComponent } from '@syncfusion/ej2-react-dropdowns';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class App extends React.Component<{}, {}> {

    // define the JSON of data
    private sportsData: { [key: string]: Object }[] = [
       { id: 'Game1', game: 'Badminton' },
       { id: 'Game2', game: 'Basketball' },
       { id: 'Game3', game: 'Cricket' },
       { id: 'Game4', game: 'Football' },
       { id: 'Game5', game: 'Golf' },
       { id: 'Game6', game: 'Hockey' },
       { id: 'Game7', game: 'Rugby' },
       { id: 'Game8', game: 'Snooker' }
    ];

    // maps the appropriate column to fields property
    private fields: object = { value: 'game' };

    public render() {
        return (
             // specifies the tag for render the AutoComplete component
            <AutoCompleteComponent id="atcelement" dataSource={this.sportsData} fields={this.fields} placeholder="Find a game" />
        );
    }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

### Array of Complex object

The AutoComplete can generate its list items through an array of complex data. For this, the appropriate columns should be
mapped to the [`fields`](../api/auto-complete/#fields) property.

In the following example, `Country.Name` column from complex data have been mapped to the `value` field.

{% tab template="autocomplete/basic", sourceFiles="app/**/*.tsx,index.html" %}

```typescript

import { AutoCompleteComponent } from '@syncfusion/ej2-react-dropdowns';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class App extends React.Component<{}, {}> {

    // define the JSON of data
    private countriesData: { [key: string]: Object }[] = [
        { Country: { Name: 'Australia' }, Code: { Id: 'AU' }},
        { Country: { Name: 'Bermuda' },Code: { Id: 'BM' }},
        { Country:{ Name: 'Canada'}, Code:{ Id: 'CA'} },
        { Country:{Name: 'Cameroon'}, Code:{ Id: 'CM'} },
        { Country:{Name: 'Denmark'}, Code:{ Id: 'DK' }},
        { Country:{Name: 'France'}, Code: { Id:'FR'} },
        { Country:{Name: 'Finland'}, Code:  { Id:'FI'} },
        { Country:{Name: 'Germany'}, Code: { Id:'DE'} },
        { Country:{Name: 'Greenland'}, Code:{ Id: 'GL' }},
        { Country:{Name: 'Hong Kong'}, Code: { Id:'HK'} },
        { Country:{Name: 'India'}, Code:{ Id: 'IN'} },
        { Country:{ Name: 'Italy'}, Code: { Id:'IT'} },
        { Country:{ Name: 'Japan'}, Code: { Id: 'JP'} },
        { Country:{Name: 'Mexico'}, Code: { Id: 'MX' }},
        { Country:{Name: 'Norway'}, Code: { Id: 'NO'} },
        { Country:{Name: 'Poland'}, Code: { Id: 'PL' }},
        { Country:{Name: 'Switzerland'}, Code: { Id: 'CH'} },
        { Country:{Name: 'United Kingdom'},Code: { Id: 'GB'} },
        { Country:{Name: 'United States'}, Code: { Id: 'US'} }
    ];

    // maps the appropriate column to fields property
    private fields: object = { value: 'Country.Name' };

    public render() {
        return (
             // specifies the tag for render the AutoComplete component
            <AutoCompleteComponent id="atcelement" dataSource={this.countriesData} fields={this.fields} placeholder="Find a country" />
        );
    }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

## Binding remote data

The AutoComplete supports retrieval of data from remote data services with the help of
`DataManager` component. The [`Query`](../api/auto-complete/#query)
property is used to fetch data from the database and bind it to the AutoComplete.

The below sample displays the first 6 contacts from the `Customers` table of the `Northwind` data service.

{% tab template="autocomplete/basic", sourceFiles="app/**/*.tsx,index.html" %}

```typescript
// import DataManager related classes
import { DataManager, ODataV4Adaptor, Query } from '@syncfusion/ej2-data';
import { SortOrder } from '@syncfusion/ej2-lists';
import { AutoCompleteComponent } from '@syncfusion/ej2-react-dropdowns';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class App extends React.Component<{}, {}> {
    // bind the DataManager instance to dataSource property
    private customerData: DataManager = new DataManager({
        adaptor: new ODataV4Adaptor,
        crossDomain: true,
        url: 'https://services.odata.org/V4/Northwind/Northwind.svc/'
    });
    // bind the Query instance to query property
    private query: Query = new Query().from('Customers').select(['ContactName', 'CustomerID']).take(6);
    // maps the appropriate column to fields property
    private fields: object = { value: 'ContactName' };
    // sort the resulted items
    private sortOrder: SortOrder = 'Ascending';

    public render() {
        return (
              // specifies the tag for render the AutoComplete component
            <AutoCompleteComponent id="atcelement" query={this.query} dataSource={this.customerData}
            fields={this.fields} sortOrder={this.sortOrder} placeholder="Find a customer"/>
        );
    }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

## See Also

* [How to load data using template](./templates#item-template)
* [How to group the data using header](./grouping/)
* [How to filter the bound data](./filtering/)