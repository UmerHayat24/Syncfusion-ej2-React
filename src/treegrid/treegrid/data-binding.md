---
title: "Data binding"
component: "TreeGrid"
description: "Learn how to bind local and remote data in the Essential JS 2 TreeGrid control."
---

# Data Binding

The TreeGrid uses **DataManager**, which supports both RESTful JSON data services binding and local JavaScript object array binding. The [`dataSource`](../api/treegrid#dataSource) property can be assigned either with the instance of [`DataManager`](https://ej2.syncfusion.com/documentation/data/data-binding/) or JavaScript object array collection.
It supports two kinds of data binding method:
* Local data
* Remote data

To get start quickly with Data Binding, you can check on this video:

`youtube:6XtJbCG8wAU`

## Local Data

In Local Data binding, data source for rendering the TreeGrid control is retrieved from the same application locally.

Two types of Data binding are possible with the TreeGrid control.

* Hierarchical Datasource binding
* Self-Referential Data binding (Flat Data)

To bind local data to the treegrid, you can assign a JavaScript object array to the [`dataSource`](../api/treegrid#datasource) property. The local data source can also be provided as an instance of the **DataManager**.

> By default, **DataManager** uses [`JsonAdaptor`](https://ej2.syncfusion.com/documentation/data/adaptors/#json-adaptor) for local data-binding.

### Hierarchy data source binding

The [`childMapping`](../api/treegrid#childMapping) property is used to map the child records in hierarchy data source.

The following code example shows you how to bind the hierarchical local data into the TreeGrid control.

{% tab template="treegrid/data-binding", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, Inject, Page, PageSettingsModel, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { sampleData } from './datasource';

export default class App extends React.Component<{}, {}>{
    public pageOptions: PageSettingsModel = { pageSize: 7 };
    public render() {
        return <TreeGridComponent dataSource={sampleData} treeColumnIndex={1} childMapping='subtasks'
            allowPaging='true' pageSettings={this.pageOptions}>
            <ColumnsDirective>
              <ColumnDirective field='taskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='taskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='startDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Page]}/>
        </TreeGridComponent>
    }
};
```

> * Remote data binding is not supported for Hierarchy Data.

{% endtab %}

### Self-Referential Data binding (Flat Data)

TreeGrid is rendered from Self-Referential data structures by providing two fields, ID field and parent ID field.

* **ID Field**: This field contains unique values used to identify nodes. Its name is assigned to the [`idMapping`](../api/treegrid#idMapping) property.
* **Parent ID Field**: This field contains values that indicate parent nodes. Its name is assigned to the [`parentIdMapping`](../api/treegrid#parentIdMapping) property.

{% tab template="treegrid/data-binding", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { ColumnDirective, ColumnsDirective, Inject, Page, PageSettingsModel, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { projectData } from './datasource';

export default class App extends React.Component<{}, {}>{

    public pageOptions: PageSettingsModel = { pageSize: 7 };

    public render() {
        return <TreeGridComponent dataSource={projectData} treeColumnIndex={1} idMapping='TaskID'
            parentIdMapping='parentID' allowPaging='true' pageSettings={this.pageOptions}>
            <ColumnsDirective>
              <ColumnDirective field='TaskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='TaskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='StartDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
              <ColumnDirective field='Duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Page]}/>
        </TreeGridComponent>
    }
};
```

{% endtab %}

> Herewith we have provided list of reserved properties and the purpose used in TreeGrid. We recommend to avoid these reserved properties for Internal purpose(To get rid of conflicts).

Reserved keywords | Purpose
-----|-----
childRecords | Specifies the childRecords of a parentData
hasChildRecords | Specifies whether the record contains child records
hasFilteredChildRecords | Specifies whether the record contains filtered child records
expanded | Specifies whether the child records are expanded
parentItem | Specifies the parentItem of childRecords
index | Specifies the index of current record
level | Specifies the hierarchy level of record
filterLevel | Specifies the hierarchy level of filtered record
parentIdMapping | Specifies the parentID
uniqueID | Specifies the unique ID of a record
parentUniqueID | Specifies the parent Unique ID of a record
checkboxState | Specifies the checkbox state of a record
isSummaryRow | Specifies the summary of a record
taskData | Specifies the main data
primaryParent | Specifies the Primary data

## Remote data

To bind remote data to TreeGrid component, assign service data as an instance of **DataManager** to the [`dataSource`](../api/treegrid#datasource) property. To interact with remote data source,  provide the endpoint **url** and define the [`hasChildMapping`](../api/treegrid#hasChildMapping) property of treegrid.

The [`hasChildMapping`](../api/treegrid/#haschildmapping) property maps the field name in data source, that denotes whether current record holds any child records. This is useful internally to show expand icon while binding child data on demand.

The TreeGrid provides **Load on Demand** support for rendering remote data. The Load on demand is considered in TreeGrid for the following actions.

* Expanding root nodes.
* Navigating pages, with paging enabled in TreeGrid.

When load on demand is enabled, all the root nodes are rendered in collapsed state at initial load.

When load on demand support is enabled in TreeGrid with paging, the current or active page’s root node alone will be rendered in collapsed state. On expanding the root node, the child nodes will be loaded from the remote server.

When a root node is expanded, its child nodes are rendered and are cached locally, such that on consecutive expand/collapse actions on root node, the child nodes are loaded from the cache instead from the remote server.

Similarly, if the user navigates to a new page, the root nodes of that specific page, will be rendered with request to the remote server.

>Remote Data Binding supports only Self-Referential Data and by default the `pageSizeMode` for Remote Data is `Root` mode. i.e only root node’s count will be shown in pager while using Remote Data

{% tab template="treegrid/data-binding", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript

import { DataManager, WebApiAdaptor } from '@syncfusion/ej2-data';
import { ColumnDirective, ColumnsDirective, Inject, Page, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
export default class App extends React.Component<{}, {}>{
    public data = new DataManager({
        adaptor: new WebApiAdaptor,
        crossDomain: true,
        url: 'https://ej2services.syncfusion.com/production/web-services/api/SelfReferenceData'
    });
    public render() {
        return <TreeGridComponent dataSource={this.data} hasChildMapping='isParent' treeColumnIndex={1} idMapping='TaskID' parentIdMapping='ParentItem' height='260' allowPaging='true'>
            <ColumnsDirective>
                <ColumnDirective field='TaskID' headerText='Task ID' width='90' textAlign='Right'/>
                <ColumnDirective field='TaskName' headerText='Task Name' width='180'/>
                <ColumnDirective field='StartDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
                <ColumnDirective field='Duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Page]}/>
        </TreeGridComponent>
    }
};
```

{% endtab %}

> By default, **DataManager** uses [`ODataAdaptor`](https://ej2.syncfusion.com/documentation/data/adaptors/#odata-adaptor) for remote data-binding.
> Based on the RESTful web services, set the corresponding adaptor to DataManager. Refer [`here`](https://ej2.syncfusion.com/documentation/data/adaptors/?no-cache=1) for more details.
> Filtering and searching server-side data operations are not supported in load on demand

### LoadChildOnDemand

While binding remote data to Tree Grid component, by default Tree Grid renders parent rows in collapsed state. Tree Grid provides option to load the child records also during the initial rendering itself for remote data binding by setting [`loadChildOnDemand`](https://ej2.syncfusion.com/react/documentation/api/treegrid/#loadchildondemand) as true.

When [`loadChildOnDemand`](https://ej2.syncfusion.com/react/documentation/api/treegrid/#loadchildondemand) is enabled parent records are rendered in expanded state.

The following code example describes the behavior of the loadChildOnDemand feature of Tree Grid.

```typescript

import { DataManager, UrlAdaptor } from '@syncfusion/ej2-data';
import { ColumnDirective, ColumnsDirective, Inject, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';

export default class App extends React.Component<{}, {}>{

    public dataManager: DataManager = new DataManager({
        adaptor: new UrlAdaptor,
        insertUrl: "Home/Insert",
        removeUrl: "Home/Delete",
        updateUrl: "Home/Update",
        batchUrl: "Home/Remove",
        url: "Home/DataSource",
    });

    public render() {
        return <TreeGridComponent dataSource={this.dataManager} treeColumnIndex={1} idMapping= 'TaskID'
        parentIdMapping='parentID' loadChildOnDemand='true' height='270' allowPaging='true'>
            <ColumnsDirective>
              <ColumnDirective field='TaskID' headerText='Task ID' width='90' textAlign='Right'/>
              <ColumnDirective field='TaskName' headerText='Task Name' width='180'/>
              <ColumnDirective field='StartDate' headerText='Start Date' width='90' textAlign='Right' format='yMd' type='date' />
              <ColumnDirective field='EndDate' headerText='End Date' width='90' format='yMd' textAlign='Right' />
              <ColumnDirective field='Priority' headerText='Priority' width='110'/>
            </ColumnsDirective>
        </TreeGridComponent>
    }
}

```

>Also while using **loadChildOnDemand** we need to handle the child records on server end and it is applicable to CRUD operations also.

The following code example describes handling of child records at server end.

```typescript

public ActionResult UrlDatasource(DataManagerRequest dm)
{
    if (TreeData.tree.Count == 0)
          TreeData.GetTree();
    IEnumerable DataSource = TreeData.tree;

    DataOperations operation = new DataOperations();
    if (dm.Where != null && dm.Where.Count > 0)
    {
        DataSource = operation.PerformFiltering(DataSource, dm.Where, "and");    //perform filtering
    }
    if (dm.Sorted != null && dm.Sorted.Count > 0)
    {
        DataSource = operation.PerformSorting(DataSource, dm.Sorted);  //perform sorting
    }
    var count = DataSource.ToList<TreeData>().Count();
    if (dm.Skip != 0)
    {
        DataSource = operation.PerformSkip(DataSource, dm.Skip);   //Paging
    }
    if (dm.Take != 0)
    {
        DataSource = operation.PerformTake(DataSource, dm.Take);
    }
    if (dm.Where != null)
    {
        DataSource = CollectChildRecords(DataSource, dm);  // method to collect child records
    }

    return dm.RequiresCounts ? Json(new { result = DataSource, count = count }) : Json(DataSource);
}

 public IEnumerable CollectChildRecords(IEnumerable datasource, DataManagerRequest dm)
 {
     DataOperations operation = new DataOperations();
     IEnumerable DataSource = TreeData.tree;   // use the total DataSource here
     string IdMapping = "TaskID";     // define your IdMapping field name here
     int[] TaskIds = new int[0];
     foreach (var rec in datasource)
     {
        int taskid = (int)rec.GetType().GetProperty(IdMapping).GetValue(rec);
        TaskIds = TaskIds.Concat(new int[] { taskid }).ToArray();  //get the Parentrecord Ids based on IdMapping Field
     }
    IEnumerable ChildRecords = null;
     foreach (int id in TaskIds)
     {
        dm.Where[0].value = id;
        IEnumerable records = operation.PerformFiltering(DataSource, dm.Where, dm.Where[0].Operator);   //perform filtering to collect the childrecords based on Ids
        ChildRecords = ChildRecords == null || (ChildRecords.AsQueryable().Count() == 0) ? records : ((IEnumerable<object>)ChildRecords).Concat((IEnumerable<object>)records);  //concate the childrecords with dataSource
     }
     if (ChildRecords != null)
     {
        ChildRecords = CollectChildRecords(ChildRecords, dm);  // repeat the operation for inner level child
        if (dm.Sorted != null && dm.Sorted.Count > 0) // perform Sorting
        {
            ChildRecords = operation.PerformSorting(ChildRecords, dm.Sorted);
        }
        datasource = ((IEnumerable<object>)datasource).Concat((IEnumerable<object>)ChildRecords);  //concate the childrecords with dataSource
     }
    return datasource;
 }

```

### Offline Mode

On remote data binding, all treegrid actions such as paging, loading child on-demand, will be processed on server-side. To avoid postback, set the treegrid to load all data on initialization and make the actions process in client-side. To enable this behavior, use the **offline** property of **DataManager**.

{% tab template="treegrid/data-binding", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript

import { DataManager, WebApiAdaptor } from '@syncfusion/ej2-data';
import { ColumnDirective, ColumnsDirective, Inject, Page, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
export default class App extends React.Component<{}, {}>{
    public data = new DataManager({
        adaptor: new WebApiAdaptor,
        crossDomain: true,
        offline: true,
        url: 'https://ej2services.syncfusion.com/production/web-services/api/SelfReferenceData'
    });
    public render() {
        return <TreeGridComponent dataSource={this.data} hasChildMapping='isParent' treeColumnIndex={1}
        idMapping='TaskID' parentIdMapping='ParentItem' height='260' allowPaging='true'>
            <ColumnsDirective>
                <ColumnDirective field='TaskID' headerText='Task ID' width='90' textAlign='Right'/>
                <ColumnDirective field='TaskName' headerText='Task Name' width='180'/>
                <ColumnDirective field='StartDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
                <ColumnDirective field='Duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Page]}/>
        </TreeGridComponent>
    }
};
```

{% endtab %}

### Custom Adaptor

You can create your own adaptor by extending the built-in adaptors. The following demonstrates custom adaptor approach and how to add a serial number for the records by overriding the built-in response processing using the `processResponse` method of the `ODataAdaptor`.

{% tab template="treegrid/data-binding", sourceFiles="app/App.tsx,app/serialNoAdaptor.tsx", compileJsx=true %}

```typescript
import { DataManager } from '@syncfusion/ej2-data';
import { ColumnDirective, ColumnsDirective, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';
import { SerialNoAdaptor } from './serialNoAdaptor';

export default class App extends React.Component<{}, {}>{
    public data = new DataManager({
        adaptor: new SerialNoAdaptor,
        crossDomain: true,
        url: 'https://ej2services.syncfusion.com/production/web-services/api/SelfReferenceData'
    });
    public render() {
        return <TreeGridComponent dataSource={this.data} hasChildMapping='isParent' treeColumnIndex={2} idMapping='TaskID' parentIdMapping='ParentItem' height='260'>
            <ColumnsDirective>
              <ColumnDirective field='Sno' headerText='Sno' width='90' textAlign='Right'/>
                <ColumnDirective field='TaskID' headerText='Task ID' width='90' textAlign='Right'/>
                <ColumnDirective field='TaskName' headerText='Task Name' width='180'/>
                <ColumnDirective field='StartDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
                <ColumnDirective field='Duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
        </TreeGridComponent>
    }
};
```

{% endtab %}

### Sending additional parameters to the server

To add a custom parameter to the data request, use the [`addParams`](https://ej2.syncfusion.com/documentation/api/data/query/#addparams) method of [`Query`](https://ej2.syncfusion.com/documentation/api/data/query/#query) class. Assign the [`Query`](https://ej2.syncfusion.com/documentation/api/data/query/#query) object with additional parameters to the treegrid [`query`](../api/treegrid#query) property.

{% tab template="treegrid/data-binding", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript

import { DataManager, Query, WebApiAdaptor } from '@syncfusion/ej2-data';
import { ColumnDirective, ColumnsDirective, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';

export default class App extends React.Component<{}, {}>{
    public data = new DataManager({
        adaptor: new WebApiAdaptor,
        crossDomain: true,
        url: 'https://ej2services.syncfusion.com/production/web-services/api/SelfReferenceData'
    });

    public query = new Query().addParams('ej2treegrid', 'true');
    public render() {
        return <TreeGridComponent dataSource={this.data} hasChildMapping='isParent' treeColumnIndex={1} idMapping='TaskID' parentIdMapping='ParentItem' height='260' query={this.query}>
            <ColumnsDirective>
                <ColumnDirective field='TaskID' headerText='Task ID' width='90' textAlign='Right'/>
                <ColumnDirective field='TaskName' headerText='Task Name' width='180'/>
                <ColumnDirective field='StartDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
                <ColumnDirective field='Duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
        </TreeGridComponent>
    }
};
```

{% endtab %}

### Handling HTTP error

During server interaction from the treegrid, some server-side exceptions may occur, and you can acquire those error messages or exception details
in client-side using the [`actionFailure`](../api/treegrid#actionfailure) event.

The argument passed to the [`actionFailure`](../api/treegrid#actionfailure) event contains the error details returned from the server.

{% tab template="treegrid/data-binding", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript

import { DataManager } from '@syncfusion/ej2-data';
import { FailureEventArgs } from '@syncfusion/ej2-grids';
import { ColumnDirective, ColumnsDirective, TreeGrid, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';

export default class App extends React.Component<{}, {}>{
    public treegrid: TreeGrid | null;
    public data = new DataManager({
        url: 'http://some.com/invalidUrl'
    });
    public onActionFailure(e: FailureEventArgs) {
        const span: HTMLElement = document.createElement('span');
        if (this.treegrid) {
            (this.treegrid.element.parentNode as HTMLElement)
                .insertBefore(span, this.treegrid.element);
            span.style.color = "#FF0000";
            span.innerHTML = "Server exception: 404 Not found";
        }
    }
    public render() {
        this.onActionFailure = this.onActionFailure.bind(this);
        return <TreeGridComponent dataSource={this.data} ref={g => this.treegrid = g} hasChildMapping='isParent' treeColumnIndex={1} idMapping='TaskID' parentIdMapping='ParentItem' height='260' actionFailure={this.onActionFailure}>
            <ColumnsDirective>
                <ColumnDirective field='TaskID' headerText='Task ID' width='90' textAlign='Right'/>
                <ColumnDirective field='TaskName' headerText='Task Name' width='180'/>
                <ColumnDirective field='StartDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
                <ColumnDirective field='Duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
        </TreeGridComponent>
    }
};
```

{% endtab %}

> The [`actionFailure`](../api/treegrid#actionfailure) event will be triggered not only for the server errors, but also when there is an exception while processing the treegrid actions.

## Binding with Ajax

You can use TreeGrid [`dataSource`](../api/treegrid#datasource) property to bind the data source to TreeGrid from external Ajax request. In the below code we have fetched the data source from the server with the help of Ajax request and provided that to [`dataSource`](../api/treegrid#datasource) property by using `onSuccess` event of the Ajax.

{% tab template="treegrid/data-binding", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { Ajax } from '@syncfusion/ej2-base';
import { ColumnDirective, ColumnsDirective, TreeGrid, TreeGridComponent } from '@syncfusion/ej2-react-treegrid';
import { Inject, Page, PageSettingsModel } from '@syncfusion/ej2-react-treegrid';
import * as React from 'react';
import './App.css';

export default class App extends React.Component<{}, {}>{
    public pageOptions: PageSettingsModel = { pageSize: 7 };
    public treegridInstance: TreeGrid | null;
    public handleClick() {
        if (this.treegridInstance) {
            const ajax = new Ajax("https://ej2services.syncfusion.com/production/web-services/api/SelfReferenceData","GET");
            this.treegridInstance.showSpinner();
            const treegrid = this.treegridInstance;
            ajax.send();
            ajax.onSuccess = (data: string) => {
                treegrid.hideSpinner();
                treegrid.dataSource = JSON.parse(data);
            };
        }
    }
    public render() {
        this.handleClick = this.handleClick.bind(this);
        return (<div className='control-pane'>
        <div className='control-section'>
        <button onClick={this.handleClick}>Bind Data</button>
        <TreeGridComponent treeColumnIndex={1} idMapping='TaskID' parentIdMapping='ParentItem' height='210' allowPaging='true'
         pageSettings={this.pageOptions} ref={treegrid => this.treegridInstance=treegrid}>
            <ColumnsDirective>
                <ColumnDirective field='TaskID' headerText='Task ID' width='90' textAlign='Right'/>
                <ColumnDirective field='TaskName' headerText='Task Name' width='180'/>
                <ColumnDirective field='StartDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' type='date' />
                <ColumnDirective field='Duration' headerText='Duration' width='80' textAlign='Right' />
            </ColumnsDirective>
            <Inject services={[Page]}/>
        </TreeGridComponent>
        </div>
    </div>);
    }
};
```

{% endtab %}

> If you bind the dataSource from this way, then it acts like a local dataSource. So you cannot perform any server side crud actions.

## Custom Binding

It is possible to handle data processing externally and bind the result to the TreeGrid. This helps you to provide your own custom data logic. TreeGrid expects an object as the result of the custom logic and the emitted value should be an object with properties result and count.

>In this context, we are going to use Ajax from our @syncfusion/ej2-base library for handling remote interaction, you can choose any HTTP client as per your choice.

```typescript

import React, { Component } from 'react';
import './App.css';
import { Ajax, getValue } from '@syncfusion/ej2-base';
import { TreeGridComponent, ColumnsDirective, ColumnDirective, Inject, Page, Edit, Sort, PageSettingsModel, EditSettingsModel, DataStateChangeEventArgs } from '@syncfusion/ej2-react-treegrid';
import { DataResult } from '@syncfusion/ej2-data';

class App extends Component {

  public treegridObj: TreeGridComponent;
  public dataService: DataService = new DataService();
  public pageSettings: PageSettingsModel = { pageSize: 2, pageSizeMode: 'Root' };
  public editSettings: EditSettingsModel = { allowAdding: true, allowDeleting:true, allowEditing: true, mode: 'Row' };

  public getData(): void {
    if(this.treegridObj && (this.treegridObj.dataSource instanceof Array
      && !(this.treegridObj.dataSource as object[]).length)) {
      const state = { skip: 0, take: 2 };  /// take value should always be equal to the pageSize of  TreeGrid
      this.dataStateChange(state);
  }
  }

  public dataStateChange(state : DataStateChangeEventArgs): void {
    this.dataService.execute(state).then(( treedata ) => {
      if(this.treegridObj) {
        this.treegridObj.dataSource = treedata
      }
    });
  }

  render() {
    return (
      <div className="App">
        <TreeGridComponent dataSource={[]} dataBound={this.getData.bind(this)}
         ref={treegrid =>  this.treegridObj = treegrid} hasChildMapping='isParent'
                           dataStateChange={this.dataStateChange.bind(this)} id="TreeGrid" idMapping='TaskId' parentIdMapping='ParentId' allowPaging={true} treeColumnIndex={1} pageSettings={this.pageSettings} editSettings={this.editSettings} >
          <ColumnsDirective>
            <ColumnDirective field='TaskId' headerText='ID' width='70' textAlign='Right' isPrimaryKey={true}></ColumnDirective>
            <ColumnDirective field='Task Name' headerText='Name' width='160'></ColumnDirective>
            <ColumnDirective field='Duration' headerText='Duration' width='90' textAlign='Right' />
            <ColumnDirective field='Progress' headerText='Progress' width='90' textAlign='Right' />
          </ColumnsDirective>
          <Inject services={[Page, Edit, Sort]} />
        </TreeGridComponent>
      </div>
    );
  }
}

export default App;


export class DataService {
  public ajax: Ajax = new Ajax({
      mode: true,
      onFailure: (e: Error) => false,
      type: 'GET'
  });


  /// this url is just a test url, provide the required url for fetching the data from server.
  private BASE_URL: string = 'http://localhost:51473/api/Tasks';

  public execute(state: DataStateChangeEventArgs): Promise<DataResult> {
      return this.getData(state);
  }

  private getData(state: DataStateChangeEventArgs): Promise<DataResult> {
      const pageQuery = `$skip=${state.skip}&$top=${state.take}`;

      /// filter query for fetching only the root level records
      const treegridQuery = "$filter='ParentId eq null'";

      this.ajax.url = `${this.BASE_URL}?${pageQuery}&${treegridQuery}&$inlinecount=allpages&$format=json`;

      return this.ajax.send().then((response: any) => {
          const data: any = JSON.parse(response);
          return {
              count:  parseInt(getValue('d.__count', data), 10),
              result: getValue('d.results', data)
          };
      });
  }
};

```

> We have a limitation for Custom Binding feature of TreeGrid. This feature works only for Self Referential data binding with `pageSizeMode` as `Root`.

### Handling Child Data

Using the custom binding feature you can bind the child data for a parent record as per your custom logic. When a parent record is expanded, [`dataStateChange`](../api/treegrid/#datastatechange) event is triggered in which you can assign your custom data to the `childData` property of the `dataStateChange`](../api/treegrid/#datastatechange) event arguments.
After assigning the child data, `childDataBind` method should be called from the
[`dataStateChange`](../api/treegrid/#datastatechange) event arguments to indicate that the data is bound.

> In this context, initially we have assigned only the parent records to the treegrid dataSource and fetched the required child records in the [`dataStateChange`](../api/treegrid/#datastatechange) event.

````typescript

import React, { Component } from 'react';
import './App.css';
import { Ajax, getValue } from '@syncfusion/ej2-base';
import { TreeGridComponent, ColumnsDirective, ColumnDirective, Inject, Page, Edit, Sort, PageSettingsModel, EditSettingsModel, DataStateChangeEventArgs } from '@syncfusion/ej2-react-treegrid';
import { DataResult } from '@syncfusion/ej2-data';

class App extends Component {

  public treegridObj: TreeGridComponent;
  public dataService: DataService = new DataService();
  public pageSettings: PageSettingsModel = { pageSize: 4, pageSizeMode: 'Root' };
  public editSettings: EditSettingsModel = { allowAdding: true, allowDeleting:true, allowEditing: true, mode: 'Row' };

  public getData(): void {
    if(this.treegridObj && (this.treegridObj.dataSource instanceof Array
      && !(this.treegridObj.dataSource as object[]).length)) {
      const state = { skip: 0, take: 4 }; /// take value should always be equal to the pageSize of   TreeGrid
      this.dataStateChange(state);
  }
  }

  public dataStateChange(state : DataStateChangeEventArgs): void {
    if(state.requestType === 'expand'){
      this.dataService.execute(state).then((childData: any) => {
          state.childData  = childData;
          state.childDataBind();
      });
    } else {
      this.dataService.execute(state).then(( treedata ) => {
        if(this.treegridObj) {
          this.treegridObj.dataSource = treedata
        }
      });
    }
  }

  render() {
    return (
      <div className="App">
        <TreeGridComponent dataSource={[]} dataBound={this.getData.bind(this)}
        ref={treegrid => this.treegridObj = treegrid} hasChildMapping='isParent'
                           dataStateChange={this.dataStateChange.bind(this)} id="TreeGrid" idMapping='TaskId' parentIdMapping='ParentId' allowPaging={true} treeColumnIndex={1} pageSettings={this.pageSettings} editSettings={this.editSettings} >
          <ColumnsDirective>
            <ColumnDirective field='TaskId' headerText='ID' width='70' textAlign='Right' isPrimaryKey={true}></ColumnDirective>
            <ColumnDirective field='Task Name' headerText='Name' width='160'></ColumnDirective>
            <ColumnDirective field='Duration' headerText='Duration' width='90' textAlign='Right' />
            <ColumnDirective field='Progress' headerText='Progress' width='90' textAlign='Right' />
          </ColumnsDirective>
          <Inject services={[Page, Edit, Sort]} />
        </TreeGridComponent>
      </div>
    );
  }
}

export default App;


export class DataService {
  public ajax: Ajax = new Ajax({
      mode: true,
      onFailure: (e: Error) => false,
      type: 'GET'
  });
  private BASE_URL: string = 'http://localhost:51473/api/Tasks';

  public execute(state: DataStateChangeEventArgs): Promise<DataResult> {
    if (state.requestType === 'expand') {
      return this.getChildData(state);
    }
    else {
      return this.getData(state);
    }
  }

  private getData(state: DataStateChangeEventArgs): Promise<DataResult> {
      const pageQuery = `$skip=${state.skip}&$top=${state.take}`;

      /// filter query for fetching only the root level records
      const treegridQuery = "$filter='ParentId eq null'";

      this.ajax.url = `${this.BASE_URL}?${pageQuery}&${treegridQuery}&$inlinecount=allpages&$format=json`;

      return this.ajax.send().then((response: any) => {
          const data: any = JSON.parse(response);
          return {
              count:  parseInt(getValue('d.__count', data), 10),
              result: getValue('d.results', data)
          };
      });
  }

  private getChildData(state: DataStateChangeEventArgs): Promise<DataResult> {
    let expandQuery: any;
    if(state.requestType === 'expand') {

      /// filter query for fetching the respective child records
      expandQuery = `$filter=${'ParentId eq ' + getValue('TaskId', state.data)}`;
    }

    this.ajax.url = `${this.BASE_URL}?&${expandQuery}&$inlinecount=allpages&$format=json`;

    return this.ajax.send().then((response: any) => {
        const data: any = JSON.parse(response);
        return data;
    });
}
};

````

### Handling TreeGrid Actions

For TreeGrid actions such as paging, sorting, etc dataStateChange event will be invoked. You have to query and resolve data using Ajax in this event based on the state arguments.

```typescript

import React, { Component } from 'react';
import './App.css';
import { Ajax, getValue } from '@syncfusion/ej2-base';
import { TreeGridComponent, ColumnsDirective, ColumnDirective, Inject, Page, Edit, Sort, PageSettingsModel, EditSettingsModel, DataStateChangeEventArgs } from '@syncfusion/ej2-react-treegrid';
import { DataResult } from '@syncfusion/ej2-data';

class App extends Component {

  public treegridObj: TreeGridComponent;
  public dataService: DataService = new DataService();
  public pageSettings: PageSettingsModel = { pageSize: 2, pageSizeMode: 'Root' };
  public editSettings: EditSettingsModel = { allowAdding: true, allowDeleting:true, allowEditing: true, mode: 'Row' };

  public getData(): void {
    if(this.treegridObj && (this.treegridObj.dataSource instanceof Array
      && !(this.treegridObj.dataSource as object[]).length)) {
      const state = { skip: 0, take: 2 }; /// take value should always be equal to the pageSize of   TreeGrid
      this.dataStateChange(state);
  }
  }

  public dataStateChange(state : DataStateChangeEventArgs): void {
    this.dataService.execute(state).then(( treedata ) => {
      if(this.treegridObj) {
        this.treegridObj.dataSource = treedata
      }
    });
  }

  render() {
    return (
      <div className="App">
        <TreeGridComponent dataSource={[]} dataBound={this.getData.bind(this)}
        ref={treegrid => this.treegridObj = treegrid} hasChildMapping='isParent'
                           dataStateChange={this.dataStateChange.bind(this)} id="TreeGrid" idMapping='TaskId' parentIdMapping='ParentId' allowPaging={true} treeColumnIndex={1} pageSettings={this.pageSettings} editSettings={this.editSettings} >
          <ColumnsDirective>
            <ColumnDirective field='TaskId' headerText='ID' width='70' textAlign='Right' isPrimaryKey={true}></ColumnDirective>
            <ColumnDirective field='Task Name' headerText='Name' width='160'></ColumnDirective>
            <ColumnDirective field='Duration' headerText='Duration' width='90' textAlign='Right' />
            <ColumnDirective field='Progress' headerText='Progress' width='90' textAlign='Right' />
          </ColumnsDirective>
          <Inject services={[Page, Edit, Sort]} />
        </TreeGridComponent>
      </div>
    );
  }
}

export default App;


export class DataService {
  public ajax: Ajax = new Ajax({
      mode: true,
      onFailure: (e: Error) => false,
      type: 'GET'
  });
  private BASE_URL: string = 'http://localhost:51473/api/Tasks';

  public execute(state: DataStateChangeEventArgs): Promise<DataResult> {
      return this.getData(state);
  }

  private getData(state: DataStateChangeEventArgs): Promise<DataResult> {
      const pageQuery = `$skip=${state.skip}&$top=${state.take}`;

      /// filter query for fetching only the root level records
      const treegridQuery = "$filter='ParentId eq null'";

      let sortQuery: string = '';
  
      if (state && (state.sorted || []).length) {
        sortQuery = `&$orderby=` + ((state).sorted as Sorts[]).map((obj: Sorts) => {
            return obj.direction === 'descending' ? `${obj.name} desc` : obj.name;
        }).reverse().join(',');
      }

      this.ajax.url = `${this.BASE_URL}?${pageQuery}&${treegridQuery}&${sortQuery}&$inlinecount=allpages&$format=json`;

      return this.ajax.send().then((response: any) => {
          const data: any = JSON.parse(response);
          return {
              count:  parseInt(getValue('d.__count', data), 10),
              result: getValue('d.results', data)
          };
      });
  }
};

```

### Performing CRUD Actions

The [`dataSourceChanged`](../api/treegrid/#datasourcechanged) event will be triggered for updating the grid data. You can perform the save operation based on the event arguments and call the endEdit method to indicate the completion of save operation.

````typescript

import * as React from 'react';
import './App.css';
import { Ajax, getValue } from '@syncfusion/ej2-base';
import { TreeGridComponent, ColumnsDirective, ColumnDirective, Inject, Page, Edit, Sort, PageSettingsModel, EditSettingsModel, DataStateChangeEventArgs } from '@syncfusion/ej2-react-treegrid';
import { DataResult } from '@syncfusion/ej2-data';
import * as ReactDOM from 'react-dom';
import { DataSourceChangedEventArgs } from '@syncfusion/ej2-grids';

export default class App extends React.Component<{},{}> {


    constructor(prop: any){
        super(prop);
        this.getData = this.getData.bind(this);
        this.dataStateChange = this.dataStateChange.bind(this);
    }

  public treegridObj: TreeGridComponent;
  public dataService: DataService = new DataService();
  public pageSettings: PageSettingsModel = { pageSize: 4, pageSizeMode: 'Root' };
  public editSettings: EditSettingsModel = { allowAdding: true, allowDeleting:true, allowEditing: true, mode: 'Row' };

  public getData(): void {
    if(this.treegridObj && (this.treegridObj.dataSource instanceof Array
      && !(this.treegridObj.dataSource as object[]).length)) {
      const state = { skip: 0, take: 4 }; /// take value should always be equal to the pageSize of   TreeGrid
      this.dataStateChange(state);
  }
  }

  public dataStateChange(state : DataStateChangeEventArgs): void {
    if (state.requestType === 'expand') {
      this.dataService.execute(state).then((childData: any) => {
          state.childData  = childData;
          state.childDataBind();
      });
    } else {
      this.dataService.execute(state).then(( treedata ) => {
        if(this.treegridObj) {
          this.treegridObj.dataSource = treedata;
        }
      });
    }
  }

  public dataSourceChanged(state: any){
    if (state.action === 'add') {
        this.dataService.addRecord(state).then(() => state.endEdit());
      } else if (state.action === 'edit') {
        this.dataService.updateRecord(state).then(() => state.endEdit());
      } else if (state.requestType === 'delete') {
        this.dataService.deleteRecord(state).then(() => state.endEdit());
      }
  }

  render() {
    return (
      <div className="App">
        <TreeGridComponent dataSource={[]} dataBound={this.getData} ref={treegrid => this.treegridObj = treegrid} dataSourceChanged={this.dataSourceChanged} dataStateChange={this.dataStateChange} id="TreeGrid" idMapping='TaskId' parentIdMapping='ParentId' allowPaging={true} treeColumnIndex={1} pageSettings={this.pageSettings} editSettings={this.editSettings} hasChildMapping='isParent'>
          <ColumnsDirective>
            <ColumnDirective field='TaskId' headerText='ID' width='70' textAlign='Right' isPrimaryKey={true}/>
            <ColumnDirective field='Task Name' headerText='Name' width='160'/>
            <ColumnDirective field='Duration' headerText='Duration' width='90' textAlign='Right' />
            <ColumnDirective field='Progress' headerText='Progress' width='90' textAlign='Right' />
          </ColumnsDirective>
          <Inject services={[Page, Edit, Sort]} />
        </TreeGridComponent>
      </div>
    );
  }
}

export class DataService {
  public ajax: Ajax = new Ajax({
      mode: true,
      onFailure: (e: Error) => false,
      type: 'GET'
  });
  private BASE_URL: string = 'http://localhost:51473/api/Tasks';

  public execute(state: DataStateChangeEventArgs): Promise<DataResult> {
    if (state.requestType === 'expand') {
      return this.getChildData(state);
    } else {
      return this.getData(state);
    }
  }

  private getData(state: DataStateChangeEventArgs): Promise<DataResult> {
      const pageQuery = `$skip=${state.skip}&$top=${state.take}`;

      /// filter query for fetching only the root level records
      const treegridQuery = "$filter='ParentId eq null'";

      this.ajax.url = `${this.BASE_URL}?${pageQuery}&${treegridQuery}&$inlinecount=allpages&$format=json`;

      return this.ajax.send().then((response: any) => {
          const data: any = JSON.parse(response);
          return {
              count:  parseInt(getValue('d.__count', data), 10),
              result: getValue('d.results', data)
          };
      });
  }

  private getChildData(state: DataStateChangeEventArgs): Promise<DataResult> {
        let expandQuery: any;
        if(state.requestType === 'expand') {
        expandQuery = `$filter=${'ParentId eq ' + getValue('TaskId', state.data)}`;
        }
        this.ajax.url = `${this.BASE_URL}?&${expandQuery}&$inlinecount=allpages&$format=json`;

        return this.ajax.send().then((response: any) => {
            const data: any = JSON.parse(response);
            return data;
        });
    }

    public addRecord(state: DataSourceChangedEventArgs) : Promise<DataResult> {
        const add: Ajax = new Ajax({
            mode: true,
            onFailure: (e: Error) => false,
            type: 'POST'
        });
        return add.send(JSON.stringify(state.data)).then((response: any) => {
            const data: any = JSON.parse(response);
            return data;
        });
    }
    public updateRecord(state: DataSourceChangedEventArgs) : Promise<DataResult> {
        const update: Ajax = new Ajax({
            mode: true,
            onFailure: (e: Error) => false,
            type: 'PUT'
        });
        return update.send(JSON.stringify(state.data)).then((response: any) => {
            const data: any = JSON.parse(response);
            return data;
        });
    }
    public deleteRecord(state: DataSourceChangedEventArgs) : Promise<DataResult> {
        const remove: Ajax = new Ajax({
            mode: true,
            onFailure: (e: Error) => false,
            type: 'DELETE'
        });
        return remove.send(JSON.stringify((state.data && state.data[0]))).then((response: any) => {
            const data: any = JSON.parse(response);
            return data;
        });
    }
};

ReactDOM.render(<App />, document.getElementById('grid'));

````

### Calculate aggregates

The footer aggregate values  should be calculated and sent along with the **dataSource** property as follows. The aggregate property of the data source should contain the aggregate value assigned to the property named in the **field – type** format. For example, the **Sum** aggregate value for the **Duration** field should be assigned to the property named as **Duration - sum**.

```json
{
    result: [{..}, {..}, {..}, ...],
    count: 830,
    aggregates: { 'Freight - sum' : 450,'EmployeeID - min': 1 }
}
```

### Provide Excel Filter data source

The [`dataStateChange`](../api/treegrid/#datastatechange) event will be triggered with appropriate arguments when the excel filter requests the filter choice data source. You need to resolve the excel filter data source using the **dataSource** resolver function from the state argument as follows.

```typescript

import React, { Component } from 'react';
import './App.css';
import { Ajax, getValue } from '@syncfusion/ej2-base';
import { TreeGridComponent, ColumnsDirective, ColumnDirective, Inject, Page, Edit, Sort, PageSettingsModel, EditSettingsModel, FilterSettingsModel, DataStateChangeEventArgs } from '@syncfusion/ej2-react-treegrid';
import { DataResult } from '@syncfusion/ej2-data';

class App extends Component {

  public treegridObj: TreeGridComponent;
  public dataService: DataService = new DataService();
  public pageSettings: PageSettingsModel = { pageSize: 2, pageSizeMode: 'Root' };
  public filterSettings: FilterSettingsModel = { type: 'Excel' },
  public editSettings: EditSettingsModel = { allowAdding: true, allowDeleting:true, allowEditing: true, mode: 'Row' };

  public getData(): void {
    if(this.treegridObj && (this.treegridObj.dataSource instanceof Array
      && !(this.treegridObj.dataSource as object[]).length)) {
      const state = { skip: 0, take: 2 };  /// take value should always be equal to the pageSize of  TreeGrid
      this.dataStateChange(state);
  }
  }

  public dataStateChange(state : DataStateChangeEventArgs): void {
    if (state.action && (state.action.requestType === 'filterchoicerequest'
            || state.action.requestType ==='filtersearchbegin')) {
          this.dataService.execute(state).then((e) => state.dataSource && state.dataSource(e.result));
        }
   else {
      this.dataService.execute(state).then(( treedata ) => {
      if(this.treegridObj) {
        this.treegridObj.dataSource = treedata;
      }
    });
  }

  }

  render() {
    return (
      <div className="App">
        <TreeGridComponent dataSource={[]} dataBound={this.getData.bind(this)}
        ref={treegrid => this.treegridObj = treegrid} hasChildMapping='isParent'
                           dataStateChange={this.dataStateChange.bind(this)} id="TreeGrid" idMapping='TaskId' parentIdMapping='ParentId' allowPaging={true} treeColumnIndex={1} pageSettings={this.pageSettings} editSettings={this.editSettings} >
          <ColumnsDirective>
            <ColumnDirective field='TaskId' headerText='ID' width='70' textAlign='Right' isPrimaryKey={true}></ColumnDirective>
            <ColumnDirective field='Task Name' headerText='Name' width='160'></ColumnDirective>
            <ColumnDirective field='Duration' headerText='Duration' width='90' textAlign='Right' />
            <ColumnDirective field='Progress' headerText='Progress' width='90' textAlign='Right' />
          </ColumnsDirective>
          <Inject services={[Page, Edit, Sort]} />
        </TreeGridComponent>
      </div>
    );
  }
}

export default App;


export class DataService {
  public ajax: Ajax = new Ajax({
      mode: true,
      onFailure: (e: Error) => false,
      type: 'GET'
  });


  /// this url is just a test url, provide the required url for fetching the data from server.
  private BASE_URL: string = 'http://localhost:51473/api/Tasks';

  public execute(state: DataStateChangeEventArgs): Promise<DataResult> {
      return this.getData(state);
  }

  private getData(state: DataStateChangeEventArgs): Promise<DataResult> {
      const pageQuery = `$skip=${state.skip}&$top=${state.take}`;

      /// filter query for fetching only the root level records
      const treegridQuery = "$filter='ParentId eq null'";

      this.ajax.url = `${this.BASE_URL}?${pageQuery}&${treegridQuery}&$inlinecount=allpages&$format=json`;

      return this.ajax.send().then((response: any) => {
          const data: any = JSON.parse(response);
          return {
              count:  parseInt(getValue('d.__count', data), 10),
              result: getValue('d.results', data)
          };
      });
  }
};

```