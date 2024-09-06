---
title: "Drop-down list Template"
component: "DropDownList"
description: "This section shows how to customize the appearance of each item in the pop-up list of Syncfusion react drop-down list component using template option."
---

# Templates

The DropDownList has been provided with several options to customize each list item, group title,
selected value, header, and footer elements.

## Item template

The content of each list item within the DropDownList can be customized with the
help of [itemTemplate](../api/drop-down-list/#itemtemplate)
property.

In the following sample, each list item is split into two columns to display relevant data's.

{% tab template="dropdownlist/item-template", sourceFiles="app/**/*.tsx,index.html,styles.css" %}

```typescript

// import DataManager related classes
import { DataManager, ODataV4Adaptor, Query } from '@syncfusion/ej2-data';
import { DropDownListComponent } from '@syncfusion/ej2-react-dropdowns';
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
  private sortOrder: string = 'Ascending';


  public render() {
    return (
      // specifies the tag for render the DropDownList component
      <DropDownListComponent id="ddlelement" query={this.query} itemTemplate={this.itemTemplate = this.itemTemplate.bind(this)} dataSource={this.employeeData} sortOrder={this.sortOrder} fields={this.fields} placeholder="Select an employee" />
    );
  }

  // set the value to itemTemplate property
  private itemTemplate(data: any): JSX.Element {
    return (
      <span><span className='name'>{data.FirstName}</span><span className='city'>{data.City}</span></span>
    );
  }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

## Value template

The currently selected value that is displayed by default on the DropDownList input element can
be customized using the [valueTemplate](../api/drop-down-list/#valuetemplate) property.

In the following sample, the selected value is displayed as a combined text of both `FirstName` and `City`
in the DropDownList input, which is separated by a hyphen.

{% tab template="dropdownlist/item-template", sourceFiles="app/**/*.tsx,index.html,styles.css" %}

```typescript
// import DataManager related classes
import { DataManager, ODataV4Adaptor, Query } from '@syncfusion/ej2-data';
import { DropDownListComponent } from '@syncfusion/ej2-react-dropdowns';
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
    private sortOrder: string = 'Ascending';
    // set the value to itemTemplate property

    public render() {
        return (
             // specifies the tag for render the DropDownList component
            <DropDownListComponent id="ddlelement" valueTemplate={this.valueTemplate = this.valueTemplate.bind(this)} query={this.query} itemTemplate={this.itemTemplate = this.itemTemplate.bind(this)} sortOrder={this.sortOrder} dataSource={this.employeeData} fields={this.fields} placeholder="Select an employee" />
        );
    }

    private itemTemplate(data: any): JSX.Element {
      return (
       <span><span className='name'>{data.FirstName}</span><span className ='city'>{data.City}</span></span>
        );
      }
       // set the value to valueTemplate property
     private valueTemplate(data: any): JSX.Element {
      return (
       <span>{data.FirstName} - {data.City}</span>
        );
      }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

## Group template

The group header title under which appropriate sub-items are categorized can also be
customize with the help of
[groupTemplate](../api/drop-down-list/#grouptemplate) property.
This template is common for both inline and floating group header template.

In the following sample, employees are grouped according to their city.

{% tab template="dropdownlist/basic", sourceFiles="app/**/*.tsx,index.html" %}

```typescript

// import DataManager related classes
import { DataManager, ODataV4Adaptor, Predicate, Query } from '@syncfusion/ej2-data';
import { DropDownListComponent } from '@syncfusion/ej2-react-dropdowns';
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
  private sortOrder: string = 'Ascending';

  public render() {
    return (
      // specifies the tag for render the DropDownList component
      <DropDownListComponent id="ddlelement" query={this.query} groupTemplate={this.groupTemplate = this.groupTemplate.bind(this)} dataSource={this.employeeData} sortOrder={this.sortOrder} fields={this.fields} placeholder="Select an employee" />
    );
  }
  // set the value to groupTemplate
  private groupTemplate(data: any): JSX.Element {
    return (
      <strong>{data.City}</strong>
    );
  }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

## Header template

The header element is shown statically at the top of the popup list items within the
DropDownList, and any custom element can be placed as a header element using the
[headerTemplate](../api/drop-down-list/#headertemplate) property.

In the following sample, the list items and its headers are designed and displayed as two columns
similar to multiple columns of the grid.

{% tab template="dropdownlist/header-template", sourceFiles="app/**/*.tsx,index.html,styles.css" %}

```typescript
// import DataManager related classes
import { DataManager, ODataV4Adaptor, Query } from '@syncfusion/ej2-data';
import { DropDownListComponent } from '@syncfusion/ej2-react-dropdowns';
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
    private sortOrder: string = 'Ascending';

    public render() {
        return (
             // specifies the tag for render the DropDownList component
            <DropDownListComponent id="ddlelement" query={this.query} headerTemplate={this.headerTemplate = this.headerTemplate.bind(this)} dataSource={this.employeeData} sortOrder={this.sortOrder} itemTemplate={this.itemTemplate = this.itemTemplate.bind(this)}  fields={this.fields} placeholder="Select an employee" />
        );
    }

    // set the value to header template
    private headerTemplate(data: any): JSX.Element {
      return (
       <span className='head'><span className='name'>Name</span><span className='city'>City</span></span>
        );
    }
    // set the value to item template
    private itemTemplate(data: any): JSX.Element {
      return (
       <span className='item' ><span className='name'>{data.FirstName}</span><span className='city'>{data.City}</span></span>
        );
    }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

## Footer template

The DropDownList has options to show a footer element at the bottom of the list items in the popup list.
Here, you can place any custom element as a footer element using
the [footerTemplate](../api/drop-down-list/#footertemplate) property.

In the following sample, footer element displays the total number of list items present in the DropDownList.

{% tab template="dropdownlist/footer-template", sourceFiles="app/**/*.tsx,index.html,styles.css" %}

```typescript

import { DropDownListComponent } from '@syncfusion/ej2-react-dropdowns';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class App extends React.Component<{}, {}> {
    // define the array of data
    private sportsData: string[] = ["BasketBall", "Cricket", "Football", "Golf"];


    public render() {
        return (
              // specifies the tag for render the DropDownList component
            <DropDownListComponent id="ddlelement" footerTemplate={this.footerTemplate = this.footerTemplate.bind(this)} dataSource={this.sportsData} placeholder="Select a game" />
        );
    }

    // set the value to footer template
    private footerTemplate(data: any): JSX.Element {
      return (
       <span className='foot'/>
        );
    }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

## No records template

The DropDownList is provided with support to custom design the popup list content when no data is found
and no matches found on search with the help of
[noRecordsTemplate](../api/drop-down-list/#norecordstemplate) property.

In the following sample, popup list content displays the notification of no data available.

{% tab template="dropdownlist/norecords-template", sourceFiles="app/**/*.tsx,index.html,styles.css" %}

```typescript

import { DropDownListComponent } from '@syncfusion/ej2-react-dropdowns';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class App extends React.Component<{}, {}> {
    // define the array of data
    private data: { [key: string]: Object }[] = [];


    public render() {
        return (
              // specifies the tag for render the DropDownList component
            <DropDownListComponent id="ddlelement" noRecordsTemplate={this.noRecordsTemplate = this.noRecordsTemplate.bind(this)} dataSource={this.data} placeholder="Select an item" />
        );
    }

    // set the value to noRecords template
    private noRecordsTemplate(data: any): JSX.Element {
      return (
       <span className='norecord'> NO DATA AVAILABLE</span>
        );
    }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

## Action failure template

There is also an option to custom design the popup list content when the data fetch request
fails at the remote server. This can be achieved using the
[actionFailureTemplate](../api/drop-down-list/#actionfailuretemplate) property.

In the following sample, when the data fetch request fails, the DropDownList displays the notification.

{% tab template="dropdownlist/norecords-template", sourceFiles="app/**/*.tsx,index.html,styles.css" %}

```typescript
// import DataManager related classes
import { DataManager, ODataV4Adaptor, Query } from '@syncfusion/ej2-data';
import { DropDownListComponent } from '@syncfusion/ej2-react-dropdowns';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class App extends React.Component<{}, {}> {
  // bind the DataManager instance to dataSource property
  private customerData: DataManager = new DataManager({
    adaptor: new ODataV4Adaptor,
    crossDomain: true,
    url: 'https://services.odata.org/V4/Northwind/Northwind.svcs/'
  });
  // bind the Query instance to query property
  private query: Query = new Query().from('Customers').select(['ContactName', 'CustomerID']).take(6);
  // maps the appropriate column to fields property
  private fields: object = { text: 'ContactName', value: 'CustomerID' };

  public render() {
    return (
      // specifies the tag for render the DropDownList component
      <DropDownListComponent id="ddlelement" query={this.query} actionFailureTemplate={this.failureTemplate = this.failureTemplate.bind(this)} dataSource={this.customerData} fields={this.fields} placeholder="Select a customer" />
    );
  }
  // set the value to action failure template
  private failureTemplate(data: any): JSX.Element {
    return (
      <span className='action-failure'> Data fetch get fails</span>
    );
  }
}
ReactDOM.render(<App />, document.getElementById('sample'));
```

{% endtab %}

## See Also

* [How to achieve filtering](./filtering/)
* [How to group the data using header](./grouping/)
* [How to show the list items with icon](./how-to/icons-support/)
* [How to render tooltip for the options](./how-to/tooltip/)