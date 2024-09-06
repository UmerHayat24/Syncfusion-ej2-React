# How to integrate pager component with listview

The first and foremost step is to obtain the `Pager` component from `Grid`. Install the ej2-react-grids package using the following command.

```shell
npm install @syncfusion/ej2-react-grids --save
```

Import the Pager to the ListView sample which has been created.

```shell
import { PagerComponent } from "@syncfusion/ej2-react-grids";
```

The [`totalRecordsCount`](https://ej2.syncfusion.com/documentation/api/pager/#totalrecordscount) property of Pager must be specified whenever using this particular component. By using [`pageSize`](https://ej2.syncfusion.com/documentation/api/pager/#pagesize) property, the number of list items to be displayed is made available. The [`pageCount`](https://ej2.syncfusion.com/documentation/api/pager/#pagecount) property allows the user to specify the visibility of the page numbers accordingly. Since the paging sample in the upcoming code snippet uses these three properties, the explanation provided here were minimal and to the point. For further API concerns in Pager component, [click here](https://ej2.syncfusion.com/documentation/api/pager/).

With the help of the [`query`](../../api/list-view#query) property of ListView, the user can specify the number of records to be displayed in the current page.

The `query` property helps in splitting the entire datasource based on our convenience. In the sample provided below, when clicking the next button in pager, it fetches the datasource based on page size and current page of Pager component.

```typescript
click(args: any) {
  this.query = new Query().range((args.currentPage - 1) * this.pagesize, (args.currentPage * this.pagesize));
}
```

In the above code snippet, the event stores the [`currentPage`](https://ej2.syncfusion.com/documentation/api/pager/#currentpage) value, and the datasource which is to be displayed in the next page is obtained.

Note: When `pageize` isn't mentioned, it defaults to 12 records per page.

{% tab template="listview/paging", isDefaultActive=true, sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```typescript

import * as React from 'react';
import * as ReactDOM from "react-dom";
import { DataManager, Query, JsonAdaptor } from '@syncfusion/ej2-data';
import { ListViewComponent } from '@syncfusion/ej2-react-lists';
import { datasource } from './datasource';
import { PagerComponent } from '@syncfusion/ej2-react-grids';

export default class App extends React.Component<{}, {}> {
    public pageCount:number = 2;
    public pageSize: number = 10;
    private data = new DataManager({ json: datasource, adaptor:new JsonAdaptor });
    //bind the Query instance to query property
    public query = new Query().range(0,this.pageSize);
    headerTemplate(data: any): JSX.Element {
        return (
          <div>
               <table id="w-100"><tr><td id="w-25">Order ID</td><td id="w-45">Ship Name</td>
               <td id="w-25">Ship City</td></tr></table>
        </div>
         );
     }
    template(data: any): JSX.Element {
        return (
            <div>
              <table id="w-100"> <tr><td id="w-25">{data.OrderID}</td><td id="w-45">{data.ShipName}</td><td id="w-25">{data.ShipCity}</td></tr></table>
            </div>
      );
    }
    click(args: any) {
        this.query = new Query().range((args.currentPage - 1) * this.pageSize, (args.currentPage * this.pageSize));
      }
    render() {
        return (
            <div>
            <ListViewComponent
                id="list"
                dataSource={this.data}
                showHeader={true}
                query={this.query}
                template= {this.template}
                headerTemplate={this.headerTemplate}
            />
            <PagerComponent click={this.click.bind(this)}  pageSize = {this.pageSize} totalRecordsCount={datasource.length} pageCount={this.pageCount}></PagerComponent>
            </div>
        );
    }
}

ReactDOM.render(<App />, document.getElementById('element'));
```