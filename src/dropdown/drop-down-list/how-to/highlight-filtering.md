---
title: "Drop-down list hightlight the character in filtering"
component: "DropDownList"
description: "This section explains on how to highlight the matched character in filtering Syncfusion React drop-down list component."
---

# Highlight the matched character in filtering

By using the `highlightSearch` method, you can highlight the matched character in DropDownList filtering.

The following example demonstrates about how to highlight the matched character in filtering.

{% tab template="dropdownlist/basic", sourceFiles="app/**/*.tsx,index.html" %}

```typescript

import { DataManager, ODataV4Adaptor, Query } from '@syncfusion/ej2-data';
import { DropDownListComponent, FilteringEventArgs, highlightSearch } from '@syncfusion/ej2-react-dropdowns';
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
  private fields: object = {
    itemCreated: this.onItemCreated.bind(this),
    text: 'ContactName', value: 'CustomerID'
  };
  // bind the Query instance to query property
  private query: Query = new Query().select(['ContactName', 'CustomerID']).take(7);
  private queryString: string;
  constructor(props: any) {
    super(props);
  }
  // highlight the item
  public onItemCreated(e: any) {
    highlightSearch(e.item, this.queryString, true, 'StartsWith');
  }
  // filtering event handler to filter a customer
  public onFiltering(e: FilteringEventArgs) {
    // take text for highlight the character in list items.
    this.queryString = e.text;
    let query: Query = new Query().select(['ContactName', 'CustomerID']);
    // frame the query based on search string with filter type.
    query = (e.text !== '') ? query.where('ContactName', 'startswith', e.text, true) : query;
    // pass the filter data source, filter query to updateData method.
    e.updateData(this.searchData, query);
  }

  public render() {
    return (
      // specifies the tag for render the DropDownList component
      <DropDownListComponent id="ddlelement" allowFiltering={true} popupHeight="250px" filtering={this.onFiltering = this.onFiltering.bind(this)} query={this.query} dataSource={this.searchData} fields={this.fields} placeholder="Select a customer" />
    );
  }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}