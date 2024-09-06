---
title: "ListView Data Binding"
component: "ListView"
description: "React listView supports data binding to display the list of items from local array/JSON data or server-side data source using DataManager."
---

# Data binding

ListView provides the option to load the data either from local data sources or remote data services.
This can be done through dataSource property which supports the data type of array or through DataManager.

ListView supports different kind of data services such as OData, OData V4, Web API and
data formats like XML, JSON, JSONP with the help of DataManager Adaptors.

| Fields | Type | Description |
|------|------|-------------|
| id | string | Specifies ID attribute of list item, mapped in dataSource. |
| text | string | Specifies list item display text field. |
| isChecked | string | Specifies checked status of list item. |
| isVisible | string | Specifies visibility state of list item. |
| enabled | string | Specifies enabled state of list item. |
| iconCss | string | Specifies the icon class of each list item which will be add before to inner text. |
| child | string | Specifies child dataSource fields. |
| tooltip | string | Specifies tooltip title text field. |
| groupBy | string | Specifies category of each list item. |
| sortBy | string | Specifies sorting field, which is used to sort the listview data. |
| htmlAttributes | string | Specifies list item html attributes field. |

> When complex data bind to ListView, you should map the fields properly. Otherwise, the ListView properties remain as undefined or null.

## Bind to local data

Local data represents in two ways, which are described below.

* Array of simple data
* Array of JSON data.

### Array of simple data

ListView supports to load the array of primitive data like string and numbers. Here, both value and text field act as same.

{% tab template="listview/data-binding", isDefaultActive=true, sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```typescript

import * as React from 'react';
import * as ReactDOM from "react-dom";
import { ListViewComponent } from '@syncfusion/ej2-react-lists';

export default class App extends React.Component<{}, {}> {
  private data = ["Artwork", "Abstract", "Modern Painting", "Ceramics", "Animation Art", "Oil Painting"];

  render() {
    return (
      // specifies the tag to render the ListView component
      <ListViewComponent id='list' dataSource={this.data} ></ListViewComponent>
    );
  }
}

ReactDOM.render(<App />, document.getElementById('element'));
```

{% endtab %}

### Array of JSON data

ListView can generate its list items through an array of complex data.
To get it work properly, you should map the appropriate columns to field property.

The below example illustrates the concept of binding Array of JSON data.

{% tab template="listview/data-binding", isDefaultActive=true, sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```typescript

import * as React from 'react';
import * as ReactDOM from "react-dom";
import { ListViewComponent } from '@syncfusion/ej2-react-lists';

export default class App extends React.Component<{}, {}> {
  //define the array of JSON
  private settings: { [key: string]: Object }[] = [
    {
      Name: "Display",
      id: "list-01"
    },
    {
      Name: "Notification",
      id: "list-02"
    },
    {
      Name: "Sound",
      id: "list-03"
    },
    {
      Name: "Apps",
      id: "list-04"
    },
    {
      Name: "Storage",
      id: "list-05"
    },
    {
      Name: "Battery",
      id: "list-06"
    }
  ];
  private fields = { text: "Name", tooltip: "Name", id: "id" };
  render() {
    return (
      // specifies the tag to render the ListView component
      <ListViewComponent
        id="list"
        dataSource={this.settings}
        fields={this.fields}
        showHeader={true}
        headerTitle="Device settings"
      />
    );
  }
}

ReactDOM.render(<App />, document.getElementById('element'));
```

{% endtab %}

## Bind to remote data

ListView supports to retrieve the data from remote data services with the help of DataManager component
and Query property allows to fetch data and return it to ListView from the database.

In the below sample, displayed first 6 Products from Product table of NorthWind data service.

{% tab template="listview/data-binding", isDefaultActive=true, sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```typescript

import * as React from 'react';
import * as ReactDOM from "react-dom";
import { ListViewComponent } from '@syncfusion/ej2-react-lists';
//import DataManager related classes
import { DataManager, Query, ODataV4Adaptor } from '@syncfusion/ej2-data';

export default class App extends React.Component<{}, {}> {
  //bind the DataManager instance to dataSource property
  private data = new DataManager({ url: "//js.syncfusion.com/ejServices/Wcf/Northwind.svc/", crossDomain: true });

  //bind the Query instance to query property
  private query = new Query()
    .from("Products")
    .select("ProductID,ProductName")
    .take(6);

  //map the appropriate columns to fields property
  private fields = { id: "ProductID", text: "ProductName" };

  render() {
    return (
      // specifies the tag to render the ListView component
      <ListViewComponent
        id="list"
        dataSource={this.data}
        fields={this.fields}
        query={this.query}
        showHeader={true}
        headerTitle="Product Name"
      />
    );
  }
}

ReactDOM.render(<App />, document.getElementById('element'));
```

{% endtab %}
