---
title: "Autocomplete Filtering"
component: "AutoComplete"
description: "This section for Syncfusion react autocomplete component shows the built-in filtering support with a rich set of filtering configurations."
---

# Filtering

The AutoComplete has built-in support for filtering the data items when [`allowFiltering`](../api/auto-complete/#allowfiltering) is enabled.
The filter operation starts as soon as you start typing
characters in the component.

## Change the filter type

Determines on which filter type, the component needs to be considered on search action.
The available [`filterType`](../api/auto-complete/#filtertype) and its supported data types are

| **Filter Type** | **Description** | **Supported Types** |
| --- | --- |
| StartsWith | Checks whether a value begins with the specified value. | String |
| EndsWith | Checks whether a value ends with specified value. | String |
| Contains | Checks whether a value contains with specified value. | String |

The following examples, data filtering is done with `StartsWith` type.

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
    private searchData: DataManager = new DataManager({
        adaptor: new ODataV4Adaptor,
        crossDomain: true,
        url: 'https://services.odata.org/V4/Northwind/Northwind.svc/'
    });
    // maps the appropriate column to fields property
    private fields: object = { value: "ContactName" };
    // bind the Query instance to query property
    private query: Query = new Query().from('Suppliers').select(["SupplierID", "ContactName"]).take(10);
    // sort the resulted items
    private sortOrder: SortOrder = 'Ascending';

    public render() {
        return (
             // specifies the tag for render the AutoComplete component
            <AutoCompleteComponent id="atcelement" query={this.query} dataSource={this.searchData} fields={this.fields} placeholder="Find a customer" filterType="StartsWith" sortOrder={this.sortOrder} />
        );
    }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

## Filter item count

You can specify the filter suggestion item count through
[`suggestionCount`](../api/auto-complete/#suggestioncount) property of AutoComplete.

The following examples, to restrict the suggestion list item counts as 2.

{% tab template="autocomplete/basic" %}

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
    private query: Query = new Query().from('Customers').select(['ContactName', 'CustomerID']);
    // maps the appropriate column to fields property
    private fields: object = { value: 'ContactName' };
    // sort the resulted items
    private sortOrder: SortOrder = 'Ascending';

    public render() {
        return (
              // specifies the tag for render the AutoComplete component
            <AutoCompleteComponent id="atcelement" query={this.query} dataSource={this.customerData}
            fields={this.fields} placeholder="Find a customer" sortOrder={this.sortOrder} suggestionCount={2} filterType= "StartsWith"/>
        );
    }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

## Limit the minimum filter character

You can set the limit for the character count to filter the data on the AutoComplete. This can be done by
set the [`minLength`](../api/auto-complete/#minlength) property to AutoComplete.

In the following example, the remote request does not fetch the search data, until the search key contains three characters.

{% tab template="autocomplete/basic", sourceFiles="app/**/*.tsx,index.html" %}

```typescript

import { DataManager, ODataV4Adaptor, Query } from '@syncfusion/ej2-data';
import { SortOrder } from '@syncfusion/ej2-lists';
import { AutoCompleteComponent } from '@syncfusion/ej2-react-dropdowns';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class App extends React.Component<{}, {}> {
    // bind the DataManager instance to dataSource property
    private searchData: DataManager = new DataManager({
        adaptor: new ODataV4Adaptor,
        crossDomain: true,
        url: 'https://services.odata.org/V4/Northwind/Northwind.svc/Customers'
    });
    // maps the appropriate column to fields property
    private fields: object = { value: 'ContactName' };
    // bind the Query instance to query property
    private query: Query = new Query().select(['ContactName', 'CustomerID']).take(10);
    // sort the resulted items
    private sortOrder: SortOrder = 'Ascending';
    public render() {
        return (
             // specifies the tag for render the AutoComplete component
            <AutoCompleteComponent id="atcelement" query={this.query} dataSource={this.searchData} sortOrder={this.sortOrder} filterType= "StartsWith" fields={this.fields} placeholder="Find a customer" minLength={3}/>
        );
    }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

## Case sensitive filtering

Data items can be filtered either with or without case sensitivity using the DataManager. This can be done by set the
[`ignoreCase`](../api/auto-complete/#ignorecase) property of AutoComplete.

The below sample depicts how to filter the data with case-sensitive.

{% tab template="autocomplete/basic", sourceFiles="app/**/*.tsx,index.html" %}

```typescript


import { SortOrder } from '@syncfusion/ej2-lists';
import { AutoCompleteComponent } from '@syncfusion/ej2-react-dropdowns';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class App extends React.Component<{}, {}> {
    // bind the DataManager instance to dataSource property
    private searchData: string[] = ['ram', 'Ravi', 'suresh', 'Suresh'];
    // maps the appropriate column to fields property
    private fields: object = { value: "ContactName" };
    // sort the resulted items
    private sortOrder: SortOrder = 'Ascending';


    public render() {
        return (
            // specifies the tag for render the AutoComplete component
            <AutoCompleteComponent id="atcelement" dataSource={this.searchData} filterType= "StartsWith" sortOrder={this.sortOrder} fields={this.fields} placeholder="eg: Ravi" ignoreCase={false} />
        );
    }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

## Diacritics Filtering

An AutoComplete supports diacritics filtering which will ignore the [diacritics](https://en.wikipedia.org/wiki/Diacritic)
and makes it easier to filter the results in international characters lists
when the [ignoreAccent](../api/auto-complete/#ignoreaccent) is enabled.

In the following sample,data with diacritics are bound as dataSource for AutoComplete.

{% tab template="autocomplete/basic", sourceFiles="app/**/*.tsx,index.html" %}

```typescript

import { AutoCompleteComponent } from '@syncfusion/ej2-react-dropdowns';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class App extends React.Component<{}, {}> {
    private diacriticsData: string[] = [
    'Aeróbics',
    'Aeróbics en Agua',
    'Aerografía',
    'Aeromodelaje',
    'Águilas',
    'Ajedrez',
    'Ala Delta',
    'Álbumes de Música',
    'Alusivos',
    'Análisis de Escritura a Mano'];

  public render() {
    return (
            <AutoCompleteComponent id="diacritics" ignoreAccent={true} dataSource={this.diacriticsData} placeholder="e.g: aero" />
    );
  }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

## See Also

* [How to achieve autofill while filtering](./how-to/autofill/)
* [How to group the data using header](./grouping/)
* [How to highlight the search data](./how-to/custom-search/)