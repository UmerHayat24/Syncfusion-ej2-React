---
title: "Multiselect Template"
component: "MultiSelect"
description: "This section shows the customization of the appearance of each item in the pop-up list of Syncfusion react multiselect component using template option."
---

# Templates

The MultiSelect has been provided with several options to customize each list item, group title,
selected value, header, and footer elements.

## Item template

The content of each list item within the MultiSelect can be customized with the
help of [itemTemplate](../api/multi-select/#itemtemplate)
property.

In the following sample, each list item is split into two columns to display relevant data's.

{% tab template="multiselect/item-template", sourceFiles="app/**/*.tsx,index.html,styles.css" %}

```typescript

// import DataManager related classes
import { DataManager, ODataV4Adaptor, Query } from '@syncfusion/ej2-data';
import { SortOrder } from '@syncfusion/ej2-lists';
import { MultiSelectComponent } from '@syncfusion/ej2-react-dropdowns';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class App extends React.Component<{}, {}> {
    // bind the DataManager instance to dataSource property
    private employeeData: DataManager = new DataManager({
        adaptor: new ODataV4Adaptor,
        crossDomain: true,
        url: 'https://services.odata.org/V4/Northwind/Northwind.svc/'
    });
    // bind the Query instance to query property
    private query: Query = new Query().from('Employees').select(['FirstName', 'City', 'EmployeeID']).take(6);
    // maps the appropriate column to fields property
    private fields: object = { text: 'FirstName', value: 'EmployeeID' };
    // sort the resulted items
    private sortOrder: SortOrder = 'Ascending';

    // set the value to itemTemplate property
    public itemTemplate(data: any): JSX.Element {
      return (
       <span><span className='name'>{data.FirstName}</span><span className ='city'>{data.City}</span></span>
        );
    }
    public render() {
        return (
             // specifies the tag for render the MultiSelect component
            <MultiSelectComponent id="mtselement" query={this.query} itemTemplate={this.itemTemplate = this.itemTemplate.bind(this)} dataSource={this.employeeData} sortOrder={this.sortOrder} fields={this.fields} placeholder="Select an employee" />
        );
    }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

## Value template

The currently selected value that is displayed by default on the MultiSelect input element can be customized using the
[valueTemplate](../api/multi-select/#valuetemplate) property.

In the following sample, the selected value is displayed as a combined text of both `FirstName` and `City`
in the MultiSelect input, which is separated by a hyphen.

{% tab template="multiselect/item-template", sourceFiles="app/**/*.tsx,index.html,styles.css" %}

```typescript
// import DataManager related classes
import { DataManager, ODataV4Adaptor, Query } from '@syncfusion/ej2-data';
import { SortOrder } from '@syncfusion/ej2-lists';
import { MultiSelectComponent } from '@syncfusion/ej2-react-dropdowns';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class App extends React.Component<{}, {}> {
    // bind the DataManager instance to dataSource property
    private employeeData: DataManager = new DataManager({
        adaptor: new ODataV4Adaptor,
        crossDomain: true,
        url: 'https://services.odata.org/V4/Northwind/Northwind.svc/'
    });
    // bind the Query instance to query property
    private query: Query = new Query().from('Employees').select(['FirstName', 'City', 'EmployeeID']).take(6);
    // maps the appropriate column to fields property
    private fields: object = { text: 'FirstName', value: 'EmployeeID' };
    // sort the resulted items
    private sortOrder: SortOrder = 'Ascending';
    // set the value to itemTemplate property
     public itemTemplate(data: any): JSX.Element {
      return (
       <span><span className='name'>{data.FirstName}</span><span className ='city'>{data.City}</span></span>
        );
    }
      // set the value to valueTemplate property
    public valueTemplate(data: any): JSX.Element {
      return (
       <span>${data.FirstName} - ${data.City}</span>
        );
    }

    public render() {
        return (
             // specifies the tag for render the MultiSelect component
            <MultiSelectComponent id="mtselement" valueTemplate={this.valueTemplate} query={this.query} itemTemplate={this.itemTemplate} sortOrder={this.sortOrder} dataSource={this.employeeData} fields={this.fields} placeholder="Select an employee" />
        );
    }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

## Group template

The group header title under which appropriate sub-items are categorized can also be
customize with the help of
[groupTemplate](../api/multi-select/#grouptemplate) property.
This template is common for both inline and floating group header template.

In the following sample, employees are grouped according to their city.

{% tab template="multiselect/basic", sourceFiles="app/**/*.tsx,index.html" %}

```typescript

// import DataManager related classes
import { DataManager, ODataV4Adaptor, Predicate, Query } from '@syncfusion/ej2-data';
import { SortOrder } from '@syncfusion/ej2-lists';
import { MultiSelectComponent } from '@syncfusion/ej2-react-dropdowns';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class App extends React.Component<{}, {}> {
    // bind the DataManager instance to dataSource property
    private employeeData: DataManager = new DataManager({
        adaptor: new ODataV4Adaptor,
        crossDomain: true,
        url: 'https://services.odata.org/V4/Northwind/Northwind.svc/'
    });
    // form  predicate to fetch the grouped data
    private groupPredicate = new Predicate('City', 'equal', 'london').or('City', 'equal', 'seattle');
    // bind the Query instance to query property
    private query: Query = new Query().from('Employees').select(['FirstName', 'City', 'EmployeeID']).take(6).where(this.groupPredicate);
    // maps the appropriate column to fields property
    private fields: object = { text: 'FirstName', value: 'EmployeeID', groupBy: 'City' };
    // sort the resulted items
    private sortOrder: SortOrder = 'Ascending';
    // set the value to groupTemplate
    public groupTemplate(data: any): JSX.Element {
      return (
       <strong>{data.City}</strong>
        );
    }
    public render() {
        return (
             // specifies the tag for render the MultiSelect component
            <MultiSelectComponent id="mtselement" query={this.query} groupTemplate={this.groupTemplate = this.groupTemplate.bind(this)} dataSource={this.employeeData} sortOrder={this.sortOrder} fields={this.fields} placeholder="Select an employee" />
        );
    }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

## Header template

The header element is shown statically at the top of the popup list items within the
MultiSelect, and any custom element can be placed as a header element using the
[headerTemplate](../api/multi-select/#headertemplate) property.

In the following sample, the list items and its headers are designed and displayed as two columns
similar to multiple columns of the grid.

{% tab template="multiselect/header-template", sourceFiles="app/**/*.tsx,index.html,styles.css" %}

```typescript
// import DataManager related classes
import { DataManager, ODataV4Adaptor, Query } from '@syncfusion/ej2-data';
import { SortOrder } from '@syncfusion/ej2-lists';
import { MultiSelectComponent } from '@syncfusion/ej2-react-dropdowns';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class App extends React.Component<{}, {}> {
    // bind the DataManager instance to dataSource property
    private employeeData: DataManager = new DataManager({
        adaptor: new ODataV4Adaptor,
        crossDomain: true,
        url: 'https://services.odata.org/V4/Northwind/Northwind.svc/'
    });
    // bind the Query instance to query property
    private query: Query = new Query().from('Employees').select(['FirstName', 'City', 'EmployeeID']).take(6);
    // maps the appropriate column to fields property
    private fields: object = { text: 'FirstName', value: 'EmployeeID' };
    // sort the resulted items
    private sortOrder: SortOrder = 'Ascending';
    // set the value to header template
    public headerTemplate(data: any): JSX.Element {
      return (
       <span className='head'><span className='name'>Name</span><span className='city'>City</span></span>
        );
    }
    // set the value to item template
    public itemTemplate(data: any): JSX.Element {
      return (
       <span className='item' ><span className='name'>{data.FirstName}</span><span className='city'>{data.City}</span></span>
        );
    }
    public render() {
        return (
             // specifies the tag for render the MultiSelect component
            <MultiSelectComponent id="mtselement" query={this.query} headerTemplate={this.headerTemplate} dataSource={this.employeeData} sortOrder={this.sortOrder} itemTemplate={this.itemTemplate}  fields={this.fields} placeholder="Select an employee" />
        );
    }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

## Footer template

The MultiSelect has options to show a footer element at the bottom of the list items in the popup list. Here, you can place
 any custom element as a footer element using the [footerTemplate](../api/multi-select/#footertemplate) property.

In the following sample, footer element displays the total number of list items present in the MultiSelect.

{% tab template="multiselect/footer-template", sourceFiles="app/**/*.tsx,index.html,styles.css" %}

```typescript

import { MultiSelectComponent } from '@syncfusion/ej2-react-dropdowns';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class App extends React.Component<{}, {}> {
    // define the array of data
    private sportsData: string[] = ["BasketBall", "Cricket", "Football", "Golf"];

    // set the value to footer template
    public footerTemplate(): JSX.Element {
      return (
       <span className='foot'/>
        );
    }
    public render() {
        return (
              // specifies the tag for render the MultiSelect component
            <MultiSelectComponent id="mtselement" footerTemplate={this.footerTemplate} dataSource={this.sportsData} placeholder="Select a game" />
        );
    }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

## No records template

The MultiSelect is provided with support to custom design the popup list content when no data is found
and no matches found on search with the help of
[noRecordsTemplate](../api/multi-select/#norecordstemplate) property.

In the following sample, popup list content displays the notification of no data available.

{% tab template="multiselect/norecords-template", sourceFiles="app/**/*.tsx,index.html,styles.css" %}

```typescript

import { MultiSelectComponent } from '@syncfusion/ej2-react-dropdowns';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class App extends React.Component<{}, {}> {
    // define the array of data
    private data: string[] = [];

    // set the value to noRecords template
     public noRecordsTemplate(data: any): JSX.Element {
      return (
      <span className='norecord'> NO DATA AVAILABLE</span>
        );
    }
    public render() {
        return (
              // specifies the tag for render the MultiSelect component
            <MultiSelectComponent id="mtselement" noRecordsTemplate={this.noRecordsTemplate = this.noRecordsTemplate.bind(this)} dataSource={this.data} placeholder="Select an item" />
        );
    }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

## Action failure template

There is also an option to custom design the popup list content when the data fetch request
fails at the remote server. This can be achieved using the
[actionFailureTemplate](../api/multi-select/#actionfailuretemplate) property.

In the following sample, when the data fetch request fails, the MultiSelect displays the notification.

{% tab template="multiselect/norecords-template", sourceFiles="app/**/*.tsx,index.html,styles.css" %}

```typescript
// import DataManager related classes
import { DataManager, ODataV4Adaptor, Query } from '@syncfusion/ej2-data';
import { MultiSelectComponent } from '@syncfusion/ej2-react-dropdowns';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class App extends React.Component<{}, {}> {
    // bind the DataManager instance to dataSource property
    private customerData: DataManager = new DataManager({
        adaptor: new ODataV4Adaptor,
        crossDomain: true,
        url: 'http://services.odata.org/V4/Northwind/Northwind.svcs/'
    });
    // bind the Query instance to query property
    private query: Query = new Query().from('Customers').select(['ContactName', 'CustomerID']).take(6);
    // maps the appropriate column to fields property
    private fields: object = { text: 'ContactName', value: 'CustomerID' };
    // set the value to action failure template
     public failureTemplate(data: any): JSX.Element {
      return (
      <span className='action-failure'> Data fetch get fails</span>
        );
    }
    public render() {
        return (
              // specifies the tag for render the MultiSelect component
            <MultiSelectComponent id="mtselement" query={this.query} actionFailureTemplate={this.failureTemplate = this.failureTemplate.bind(this)} dataSource={this.customerData} fields={this.fields} placeholder="Select a customer" />
        );
    }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

## See Also

* [How to bind the data](./data-binding/)
* [How to group the data using header](./grouping/)
* [How to customize the options in MultiSelect](./chip-customization/)