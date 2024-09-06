---
title: "ListBox data binding and initialization through HTML tags"
component: "ListBox"
description: "ListBox supports databinding with local and remote data source."
---

# Data Binding

The ListBox loads the data either from local data sources or remote data services using the [`dataSource`](../api/list-box/#datasource) property. It supports
the data type of `array` or `DataManager`.

| Fields | Type | Description |
|------|------|-------------|
| [`text`](../api/list-box/fieldSettingsModel/#text) |  `string` | Specifies the display text of each list item. |
| [`value`](../api/list-box/fieldSettingsModel/#value) |  `string` | Specifies the hidden data value mapped to each list item that should contain a unique value. |
| [`groupBy`](../api/list-box/fieldSettingsModel/#groupby) |  `string` | Specifies the category under which the list item has to be grouped. |
| [`iconCss`](../api/list-box/fieldSettingsModel/#iconcss) |  `string` | Specifies the iconCss class that needs to be mapped. |
| [`htmlAttributes`](../api/list-box/fieldSettingsModel/#htmlattributes) |  `string` | Allows additional attributes to configure the elements in various ways to meet the criteria. |

> When binding complex data to the ListBox, fields should be mapped correctly. Otherwise, the selected item remains undefined.

## Local Data

Local data can be represented by the following ways as described below.

### Array of string

The ListBox has support to load array of primitive data such as strings or numbers. Here, both value and text field acts as same.

{% tab template="listbox/basic", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { ListBoxComponent } from '@syncfusion/ej2-react-dropdowns';

export default class App extends React.Component<{}, {}> {
   private data: string[] = ['Badminton', 'Cricket', 'Football', 'Golf', 'Tennis', 'Basket Ball', 'Base Ball', 'Hockey', 'Volley Ball'];
  render() {
    return (
      <ListBoxComponent dataSource={this.data} />
    );
  }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

### Array of object

The ListBox can generate its list items through an array of object data. For this,
the appropriate columns should be mapped to the [`fields`](../api/list-box/#fields) property.

In the following example, `id` and `sports` column from complex data have been mapped to the `value` field and `text` field, respectively.

{% tab template="listbox/basic", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { ListBoxComponent } from '@syncfusion/ej2-react-dropdowns';

export default class App extends React.Component<{}, {}> {
  // define the array of object
   private data: { [key: string]: Object }[] = [
    { text: 'Hennessey Venom', id: 'list-01' },
    { text: 'Bugatti Chiron', id: 'list-02' },
    { text: 'Bugatti Veyron Super Sport', id: 'list-03' },
    { text: 'SSC Ultimate Aero', id: 'list-04' },
    { text: 'Koenigsegg CCR', id: 'list-05' },
    { text: 'McLaren F1', id: 'list-06' },
    { text: 'Aston Martin One- 77', id: 'list-07' },
    { text: 'Jaguar XJ220', id: 'list-08' },
    { text: 'McLaren P1', id: 'list-09' },
    { text: 'Ferrari LaFerrari', id: 'list-10' },
];
  render() {
    return (
      <ListBoxComponent dataSource={this.data} />
    );
  }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

### Array of complex object

The ListBox can generate its list items through an array of complex data. For this,
the appropriate columns should be mapped to the [`fields`](../api/list-box/#fields) property.

In the following example, `sports.Name` column from complex data have been mapped to the `text` field.

{% tab template="listbox/basic", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { ListBoxComponent } from '@syncfusion/ej2-react-dropdowns';

export default class App extends React.Component<{}, {}> {
  // define the array of object
private data: { [key: string]: Object }[] = [
    { id: 'game1', sports: { Name: 'Badminton'} },
    { id: 'game2', sports: { Name: 'Cricket'} },
    { id: 'game3', sports: { Name: 'Football'} },
    { id: 'game4', sports: { Name: 'Golf'} },
    { id: 'game5', sports: { Name: 'Tennis'} },
    { id: 'game6', sports: { Name: 'Basket Ball'} },
    { id: 'game7', sports: { Name: 'Base Ball'} },
    { id: 'game8', sports: { Name: 'Hockey'} },
    { id: 'game9', sports: { Name: 'Volley Ball'} }
];

private fields: object = { text:"sports.Name", value:"id"};

  render() {
    return (
      <ListBoxComponent dataSource={this.data} fields={this.fields} />
    );
  }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

## Remote Data

The ListBox supports retrieval of data from remote data services with the help of [`DataManager`](https://ej2.syncfusion.com/documentation/data/getting-started/) component.

The following sample displays the employee names from `Employee` table.

{% tab template="listbox/basic", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { ListBoxComponent } from '@syncfusion/ej2-react-dropdowns';
import { DataManager, ODataV4Adaptor } from '@syncfusion/ej2-data';

export default class App extends React.Component<{}, {}> {

private fields: object = { text:'FirstName', value:'EmployeeID'};
private data:DataManager = new DataManager({
    adaptor: new ODataV4Adaptor,
    crossDomain: true,
    url: 'https://ej2services.syncfusion.com/production/web-services/api/Employees'
});
  render() {
    return (
        // specifies the tag for render the ListBox component
      <ListBoxComponent dataSource={this.data} fields={this.fields} />
    );
  }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}