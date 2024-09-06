---
title: "Drop-down list Filtering"
component: "DropDownList"
description: "This section explains the built-in filtering support with a rich set of filtering configurations in Syncfusion react drop-down list component."
---

# Filtering

The DropDownList has built-in support to filter data items when `allowFiltering` is enabled. The filter
operation starts as soon as you start typing characters in the search box.

To display filtered items in the popup, filter the required data and return it to the DropDownList
via `updateData` method by using the [filtering](../api/drop-down-list/#filtering) event.

The following sample illustrates how to query the data source and pass the data to the DropDownList
through the `updateData` method in `filtering` event.

{% tab template="dropdownlist/basic", sourceFiles="app/**/*.tsx,index.html" %}

```typescript

// import DataManager related classes
import { Query } from '@syncfusion/ej2-data';
import { DropDownListComponent, FilteringEventArgs } from '@syncfusion/ej2-react-dropdowns';
import * as React from 'react';
import * as ReactDOM from 'react-dom';


export default class App extends React.Component<{}, {}> {

    // maps the appropriate column to fields property
    private fields: object = { text: "Country", value: "Index" };
    // define the filtering data
    private searchData: { [key: string]: Object }[] = [
      { Index: "s1", Country: "Alaska" }, { Index: "s2", Country: "California" },
      { Index: "s3", Country: "Florida" }, { Index: "s4", Country: "Georgia" }
  ];

    // filtering event handler to filter a Country
    public onFiltering(args: FilteringEventArgs) {
        let query = new Query();
        // frame the query based on search string with filter type.
        query = (args.text !== "") ? query.where("Country", "startswith", args.text, true) : query;
        // pass the filter data source, filter query to updateData method.
        args.updateData(this.searchData, query);
    }

    public render() {
        return (
             // specifies the tag for render the DropDownList component
            <DropDownListComponent id="ddlelement" popupHeight="250px" fields={this.fields} filtering={this.onFiltering = this.onFiltering.bind(this)} allowFiltering={true} dataSource={this.searchData} placeholder="Select a country" />
        );
    }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

## Limit the minimum filter character

When filtering the list items, you can set the limit for character count to raise remote request and fetch
filtered data on the DropDownList. This can be done by manual validation within the filter event handler.

In the following example, the remote request does not fetch the search data until the search key contains three characters.

{% tab template="dropdownlist/basic", sourceFiles="app/**/*.tsx,index.html" %}

```typescript

import { DataManager, ODataV4Adaptor, Query } from '@syncfusion/ej2-data';
import { SortOrder } from '@syncfusion/ej2-lists';
import { DropDownListComponent, FilteringEventArgs } from '@syncfusion/ej2-react-dropdowns';
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
      // specifies the tag for render the DropDownList component
      <DropDownListComponent id="ddlelement" allowFiltering={true} popupHeight="250px" filtering={this.onFiltering = this.onFiltering.bind(this)} sortOrder={this.sortOrder} query={this.query} dataSource={this.searchData} fields={this.fields} placeholder="Select a customer" />
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

{% tab template="dropdownlist/basic", sourceFiles="app/**/*.tsx,index.html" %}

```typescript
// import DataManager related classes
import { Query } from '@syncfusion/ej2-data';
import { SortOrder } from '@syncfusion/ej2-lists';
import { DropDownListComponent, FilteringEventArgs } from '@syncfusion/ej2-react-dropdowns';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class App extends React.Component<{}, {}> {
  // bind the DataManager instance to dataSource property
  private searchData: { [key: string]: Object }[] = [
    { Index: "s1", Country: "Alaska" }, { Index: "s2", Country: "Californiag" },
    { Index: "s3", Country: "Florida" }, { Index: "s4", Country: "Georgia" }
]
// maps the appropriate column to fields property
private fields: object = { value: "Country" };
  // sort the resulted items
  private sortOrder: SortOrder = 'Ascending';
  // filtering event handler to filter a customer
  public onFiltering(e: FilteringEventArgs) {
    // load overall data when search key empty.
    if (e.text === '') {
      e.updateData(this.searchData);
    } else {
      let query: Query = new Query();
      // change the type of filtering
      query = (e.text !== '') ? query.where('Country', 'endsWith', e.text, true) : query;
      e.updateData(this.searchData, query);
    }
  }

  public render() {
    return (
      // specifies the tag for render the DropDownList component
      <DropDownListComponent id="ddlelement" allowFiltering={true} popupHeight="250px" filtering={this.onFiltering = this.onFiltering.bind(this)}  sortOrder={this.sortOrder} dataSource={this.searchData} fields={this.fields} placeholder="Select a customer" />
    );
  }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

## Case sensitive filtering

Data items can be filtered either with or without case sensitivity using the DataManager. This can be done
by passing the fourth optional parameter of the `where` clause.

The following example shows how to perform case-sensitive filter.

{% tab template="dropdownlist/basic", sourceFiles="app/**/*.tsx,index.html" %}

```typescript

import { Query } from '@syncfusion/ej2-data';
import { SortOrder } from '@syncfusion/ej2-lists';
import { DropDownListComponent, FilteringEventArgs } from '@syncfusion/ej2-react-dropdowns';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class App extends React.Component<{}, {}> {
    // bind the DataManager instance to dataSource property
    private searchData: { [key: string]: Object }[] = [
      { Index: "s1", Country: "Alaska" }, { Index: "s2", Country: "Californiag" },
      { Index: "s3", Country: "Florida" }, { Index: "s4", Country: "Georgia" }
  ]
  // maps the appropriate column to fields property
  private fields: object = { value: "Country" };
    // sort the resulted items
    private sortOrder: SortOrder = 'Ascending';
    // filtering event handler to filter a customer
    public onFiltering(e: FilteringEventArgs) {
      // load overall data when search key empty.
      if (e.text === '') {
        e.updateData(this.searchData);
      } else {
        let query: Query = new Query();
        // change the type of filtering
        query = (e.text !== '') ? query.where('Country', 'contains', e.text, false) : query;
        e.updateData(this.searchData, query);
      }
    }

    public render() {
        return (
             // specifies the tag for render the DropDownList component
            <DropDownListComponent id="ddlelement" popupHeight="245px" allowFiltering={true} filtering={this.onFiltering = this.onFiltering.bind(this)} sortOrder={this.sortOrder} dataSource={this.searchData} fields={this.fields} placeholder="Select a customer" />
        );
    }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

## Diacritics Filtering

DropDownList supports diacritics filtering which will ignore the [diacritics](https://en.wikipedia.org/wiki/Diacritic) and
makes it easier to filter the results in international characters lists
when the [ignoreAccent](../api/drop-down-list/#ignoreaccent) is enabled.

In the following sample,data with diacritics are bound as dataSource for DropDownList.

{% tab template="dropdownlist/basic", sourceFiles="app/**/*.tsx,index.html" %}

```typescript

import { DropDownListComponent } from '@syncfusion/ej2-react-dropdowns';
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
           <DropDownListComponent id="diacritics" ignoreAccent={true} dataSource={this.diacriticsData} allowFiltering={true} placeholder="Select a value" filterBarPlaceholder="e.g: aero" />
    );
  }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

> You can also explore our [React DropDownList Filtering example]( https://ej2.syncfusion.com/react/demos/#/material/drop-down-list/filtering) that shows how to render the DropDownList Filter in React.

## See Also

* [How to limit the search result while filtering](./how-to/search-on-filtering/)
* [How to highlight the matched characters in filtering](./how-to/highlight-filtering/)
* [How to modify the result data using remote data source](./how-to/modify-data/)