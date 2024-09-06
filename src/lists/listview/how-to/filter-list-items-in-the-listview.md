# Filter list items in the ListView

The filtered data can be displayed in the ListView component depending upon on user inputs using the
[`DataManager`](https://ej2.syncfusion.com/react/documentation/data/getting-started/). Refer to the
following steps to render the ListView with filtered data.

* Render a textbox to get input for filtering data.

* Render ListView with
  [`dataSource`](../../api/list-view/#datasource), and set
  the [`sortOrder`](../../api/list-view/#sortorder) property.

* Bind the `keyup` event for textbox to perform filtering operation. To filter list data, pass the list data source to the
  `DataManager`, manipulate the data using the
  [`executeLocal`](https://ej2.syncfusion.com/documentation/api/data/dataManager/#executelocal) method,
  and then update filtered data as ListView dataSource.

{% tab template="listview/filter", isDefaultActive=true, sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import { DataManager, Query, ODataV4Adaptor } from "@syncfusion/ej2-data";
import { ListViewComponent } from "@syncfusion/ej2-react-lists";

interface MyState {
  listData: any[];
}

export default class App extends React.Component<{}, MyState> {
  constructor(props: any) {
    super(props);
    this.state = { listData: this.list };
  }
  public list: any[] = [
    { text: "Hennessey Venom", id: "list-01" },
    { text: "Bugatti Chiron", id: "list-02" },
    { text: "Bugatti Veyron Super Sport", id: "list-03" },
    { text: "SSC Ultimate Aero", id: "list-04" },
    { text: "Koenigsegg CCR", id: "list-05" },
    { text: "McLaren F1", id: "list-06" }
  ];

  public fields: Object = { text: "text", id: "id" };

  public onKeyUp(e: any) {
    let value = e.target.value;
    let data = new DataManager(this.state.listData).executeLocal(
      new Query().where("text", "startswith", value, true)
    );
    if (!value) {
      this.setState({
        listData: this.list
      });
    } else {
      this.setState({
        listData: data
      });
    }
  }

  render() {
    return (
      <div id="sample">
        <input
          className="e-input"
          type="text"
          id="textbox"
          placeholder="Filter"
          onKeyUp={this.onKeyUp.bind(this)}
          title="Type in a name"
        />
        <ListViewComponent
          id="list"
          dataSource={this.state.listData}
          fields={this.fields}
          sortOrder="Ascending"
        />
      </div>
    );
  }
}
ReactDOM.render(<App />, document.getElementById("element"));
```

{% endtab %}

> In this demo, data has been filtered with starting character of the list items. You can also filter list items with ending
> character by passing the `endswith` in
> [where](https://ej2.syncfusion.com/documentation/api/data/query/#where)
> clause instead of `startswith`.
