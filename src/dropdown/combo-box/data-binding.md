---
title: "Combo box Data binding"
component: "ComboBox"
description: "This section for Syncfusion react combo box component shows how to bind with local data source and how to fetch data from remote data service."
---

# Data Binding

The ComboBox loads the data either from local data sources or
remote data services using the
[dataSource](../api/combo-box/#datasource) property. It supports
the data type of `array` or `DataManager`.

The ComboBox also supports different kinds of data services such as OData, OData V4, and Web API,
and data formats such as XML, JSON, and JSONP with the help of `DataManager` adaptors.

| Fields | Type | Description |
|------|------|-------------|
| text |  `string` | Specifies the display text of each list item. |
| value |  `number or string` | Specifies the hidden data value which mapped to each list item that should be unique. |
| groupBy |  `string` | Specifies the category under which the list item needs to be grouped. |
| iconCss |  `string` | Specifies the icon class of each list item. |

> When binding complex data to the ComboBox, fields should be mapped correctly. Otherwise, the selected item remains undefined.

## Binding local data

Local data can be represented in two ways as described below.

### 1. Array of simple data

The ComboBox has support to load array of primitive data such as strings and numbers. Here, both value and text field act the same.

{% tab template="combobox/basic", sourceFiles="app/**/*.tsx, index.html" %}

```typescript
import { ComboBoxComponent } from '@syncfusion/ej2-react-dropdowns';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class App extends React.Component<{}, {}> {

    // define the array of string
    private sportsData: string[] = ['Badminton', 'Cricket', 'Football', 'Golf', 'Tennis'];

    public render() {
        return (
              // specifies the tag for render the ComboBox component
            <ComboBoxComponent id="comboelement" dataSource={this.sportsData} placeholder="Select a game" />
        );
    }
}
ReactDOM.render(<App />, document.getElementById('sample'));
```

{% endtab %}

### 2. Array of JSON data

The ComboBox can generate its list items through an array of complex data. For this,
the appropriate columns should be mapped to the
[fields](../api/combo-box/#fields) property.

In the following example, `Id` column and `Game` column from complex data have been mapped to the `value` field and `text` field, respectively.

{% tab template="combobox/basic", sourceFiles="app/**/*.tsx,index.html" %}

```typescript

import { ComboBoxComponent } from '@syncfusion/ej2-react-dropdowns';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class App extends React.Component<{}, {}> {

    // define the JSON of data
    private sportsData: { [key: string]: Object }[] = [
        { Id: 'game1', Game: 'Badminton' },
        { Id: 'game2', Game: 'Football' },
        { Id: 'game3', Game: 'Tennis' }
    ];

    // maps the appropriate column to fields property
    private fields: object = { text: 'Game', value: 'Id' };

    public render() {
        return (
             // specifies the tag for render the ComboBox component
            <ComboBoxComponent id="comboelement" dataSource={this.sportsData} fields={this.fields} placeholder="Select a game" />
        );
    }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

### 3. Array of Complex data

The ComboBox can generate its list items through an array of complex data. For this,
the appropriate columns should be mapped to the
[fields](../api/combo-box/#fields) property.

In the following example, `Code.Id` column and `Country.Name` column from complex data have been mapped
to the `value` field and `text` field, respectively.

{% tab template="combobox/basic", sourceFiles="app/**/*.tsx,index.html" %}

```typescript

import { ComboBoxComponent } from '@syncfusion/ej2-react-dropdowns';
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
        { Country:{Name: 'France'}, Code: { Id:'FR'} }
    ];

    // maps the appropriate column to fields property
    private fields: object = { text: 'Country.Name', value: 'Code.Id' };

    public render() {
        return (
             // specifies the tag for render the ComboBox component
            <ComboBoxComponent id="comboelement" dataSource={this.countriesData} fields={this.fields} placeholder="Select a country" />
        );
    }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

## Binding remote data

The ComboBox supports retrieval of data from remote data services with the help
of `DataManager` component. The [`Query`](../api/combo-box/#query) property
is used to fetch data from the database and bind it to the ComboBox.

The following sample displays the first 6 contacts from “Customers” table of the `Northwind` Data Service.

{% tab template="combobox/basic", sourceFiles="app/**/*.tsx,index.html" %}

```typescript
// import DataManager related classes
import { DataManager, ODataV4Adaptor, Query } from '@syncfusion/ej2-data';
import { SortOrder } from '@syncfusion/ej2-lists';
import { ComboBoxComponent } from '@syncfusion/ej2-react-dropdowns';
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
    private fields: object = { text: 'ContactName', value: 'CustomerID' };
    // sort the resulted items
    private sortOrder: SortOrder = 'Ascending';

    public render() {
        return (
              // specifies the tag for render the ComboBox component
            <ComboBoxComponent id="comboelement" query={this.query} dataSource={this.customerData}
            fields={this.fields} placeholder="Select a customer" sortOrder={this.sortOrder} />
        );
    }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

## See Also

* [How to achieve cascading](./how-to/cascading/)
* [How to load data using template](./templates#item-template)
* [How to group the data using header](./grouping/)
* [How to filter the bound data](./filtering/)