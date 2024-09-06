---
title: "Multiselect Filtering"
component: "MultiSelect"
description: "This section explains the built-in filtering support with a rich set of filtering configurations in Syncfusion react multiselect component."
---

# Filtering

The MultiSelect has built-in support to filter data items when `allowFiltering` is enabled. The filter
operation starts as soon as you start typing characters in the MultiSelect input.

To display filtered items in the popup, filter the required data and return it to the MultiSelect
via [updateData](/drop-down-list/api-filteringEventArgs.html#updatedata) method by using the [filtering](../api/multi-select/#filtering) event.

The following sample illustrates how to query the data source and pass the data to the MultiSelect
through the `updateData` method in `filtering` event.

{% tab template="multiselect/basic", sourceFiles="app/**/*.tsx,index.html" %}

```typescript

// import DataManager related classes
import { Query } from '@syncfusion/ej2-data';
import { FilteringEventArgs, MultiSelectComponent } from '@syncfusion/ej2-react-dropdowns';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class App extends React.Component<{}, {}> {
    // define the filtering data
    private searchData: { [key: string]: Object }[] = [
        { index: "s1", country: "Alaska" }, { index: "s2", country: "California" },
        { index: "s3", country: "Florida" }, { index: "s4", country: "Georgia" }
    ];
    // maps the appropriate column to fields property
    private fields: object = { text: "country", value: "index" };
    constructor(props: any) {
        super(props);
        this.onFiltering = this.onFiltering.bind(this);
    }
    // filtering event handler to filter a country
    public onFiltering(args: FilteringEventArgs) {
        let query = new Query();
        // frame the query based on search string with filter type.
        query = (args.text !== "") ? query.where("country", "startswith", args.text, true) : query;
        // pass the filter data source, filter query to updateData method.
        args.updateData(this.searchData, query);
    }

    public render() {
        return (
             // specifies the tag for render the MultiSelect component
            <MultiSelectComponent id="mtselement" popupHeight="250px" fields={this.fields} filtering={this.onFiltering} allowFiltering={true} dataSource={this.searchData} placeholder="Select a country" />
        );
    }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

## Limit the minimum filter character

When filtering the list items, you can set the limit for character count to raise remote request and fetch
filtered data on the MultiSelect. This can be done by manual validation within the filter event handler.

In the following example, the remote request does not fetch the search data until the search key contains three characters.

{% tab template="multiselect/basic", sourceFiles="app/**/*.tsx,index.html" %}

```typescript

import { DataManager, ODataV4Adaptor, Query } from '@syncfusion/ej2-data';
import { SortOrder } from '@syncfusion/ej2-lists';
import { FilteringEventArgs, MultiSelectComponent } from '@syncfusion/ej2-react-dropdowns';
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
    private fields: object = { text: 'ContactName', value: 'CustomerID' };
    // bind the Query instance to query property
    private query: Query = new Query().select(['ContactName', 'CustomerID']).take(7);
    // sort the resulted items
    private sortOrder: SortOrder = 'Ascending';
    constructor(props: any) {
        super(props);
        this.onFiltering = this.onFiltering.bind(this);
    }
     // filtering event handler to filter a customer
    public onFiltering(e: FilteringEventArgs) {
        // load overall data when search key empty.
        if (e.text === '') {
            e.updateData(this.searchData);
        } else {
            // restrict the remote request until search key contains 3 characters.
            if (e.text.length < 3) { return; }
            let query: Query = new Query().select(['ContactName', 'CustomerID']);
            query = (e.text !== '') ? query.where('ContactName', 'startswith', e.text, true) : query;
            e.updateData(this.searchData, query);
        }
    }

    public render() {
        return (
             // specifies the tag for render the MultiSelect component
            <MultiSelectComponent id="mtselement" allowFiltering={true} popupHeight="250px" filtering={this.onFiltering} sortOrder={this.sortOrder} query={this.query} dataSource={this.searchData} fields={this.fields} placeholder="Select a customer" />
        );
    }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

## Change the filter type

While filtering, you can change the filter type to `contains`,
`startsWith`, or `endsWith` for string type within the filter event handler.

In the following examples, data filtering is done with `endsWith` type.

{% tab template="multiselect/basic", sourceFiles="app/**/*.tsx,index.html" %}

```typescript

// import DataManager related classes
import { DataManager, ODataV4Adaptor, Query } from '@syncfusion/ej2-data';
import { SortOrder } from '@syncfusion/ej2-lists';
import { FilteringEventArgs, MultiSelectComponent } from '@syncfusion/ej2-react-dropdowns';
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
    private fields: object = { text: 'ContactName', value: 'CustomerID' };
    // bind the Query instance to query property
    private query: Query = new Query().select(['ContactName', 'CustomerID']).take(7);
    // sort the resulted items
    private sortOrder: SortOrder = 'Ascending';
    constructor(props: any) {
        super(props);
        this.onFiltering = this.onFiltering.bind(this);
    }
    // filtering event handler to filter a customer
    public onFiltering(e: FilteringEventArgs) {
        // load overall data when search key empty.
        if (e.text === '') {
            e.updateData(this.searchData);
        } else {
            let query: Query = new Query().select(["ContactName", "CustomerID"]);
            // change the type of filtering
            query = (e.text !== '') ? query.where('ContactName', 'endsWith', e.text, true) : query;
            e.updateData(this.searchData, query);
        }
    }

    public render() {
        return (
             // specifies the tag for render the MultiSelect component
            <MultiSelectComponent id="mtselement" allowFiltering={true} popupHeight="250px" filtering={this.onFiltering} query={this.query} sortOrder={this.sortOrder} dataSource={this.searchData} fields={this.fields} placeholder="Select a customer" />
        );
    }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

## Case sensitive filtering

Data items can be filtered either with or without case sensitivity using the DataManager. This can be done by passing the fourth optional parameter of the `where` clause.

The following example shows how to perform case-sensitive filter.

{% tab template="multiselect/basic", sourceFiles="app/**/*.tsx,index.html" %}

```typescript

import { Query } from '@syncfusion/ej2-data';
import { SortOrder } from '@syncfusion/ej2-lists';
import { FilteringEventArgs, MultiSelectComponent } from '@syncfusion/ej2-react-dropdowns';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class App extends React.Component<{}, {}> {

    // define the JSON of data
    private sportsData: { [key: string]: Object }[] = [
        { id: 'game1', sports: 'Badminton' },
        { id: 'game2', sports: 'Tennis' },
        { id: 'game3', sports: 'Football' }
    ];

    // maps the appropriate column to fields property
    private fields: object = { text: 'sports', value: 'id' };

    // sort the resulted items
    private sortOrder: SortOrder = 'Ascending';
    // filtering event handler to filter a customer

    public onFiltering = (e: FilteringEventArgs) => {
        // load overall data when search key empty.
        if (e.text === '') {
            e.updateData(this.sportsData);
        } else {
            let query: Query = new Query().select(["sports", "id"]);
            // enable the case sensitive filtering by passing false to 4th parameter.
            query = (e.text !== '') ? query.where('sports', 'startsWith', e.text, false) : query;
            e.updateData(this.sportsData, query);
        }
    }

    public render() {
        return (
            // specifies the tag for render the MultiSelect component
            <MultiSelectComponent id="mtselement" dataSource={this.sportsData} fields={this.fields} placeholder="Select a game" allowFiltering={true} filtering={this.onFiltering = this.onFiltering.bind(this)} sortOrder={this.sortOrder} />
        );
    }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

## Diacritics Filtering

MultiSelect supports diacritics filtering which will ignore the [diacritics](https://en.wikipedia.org/wiki/Diacritic) and
makes it easier to filter the results in international characters lists
when the [ignoreAccent](../api/multi-select/#ignoreaccent) is enabled.

In the following sample,data with diacritics are bound as dataSource for MultiSelect.

{% tab template="multiselect/basic", sourceFiles="app/**/*.tsx,index.html" %}

```typescript

import { MultiSelectComponent } from '@syncfusion/ej2-react-dropdowns';
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
            <MultiSelectComponent id="diacritics" ignoreAccent={true} allowFiltering={true} dataSource={this.diacriticsData} placeholder="e.g: aero" />
    );
  }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

## See Also

* [How to bind the data](./data-binding/)
* [How to group the data using header](./grouping/)
* [How to add custom value to the MultiSelect](./custom-value/)