# Display spinner until list items are loaded

The features of the ListView component such as remote data-binding take more time to fetch data from corresponding dataSource/remote URL. In this case, you can use EJ2 [Spinner](https://ej2.syncfusion.com/react/documentation/spinner/getting-started/) to enhance the appearance of the UI. This section explains how to load a spinner component to groom the appearance.

Refer to the following code sample to render the spinner component.

```typescript
    createSpinner({
        target: this.spinnerInstance
    });
    showSpinner(this.spinnerInstance);
```

Here, the data is fetched from `Northwind` Service URL; it takes a few seconds to load the data. To enhance the UI, the spinner component has been rendered initially. After the data is loaded from remote URL, the spinner component will be hidden in ListView [actionComplete](../../api/list-view/#actioncomplete) event.

{% tab template="listview/data-binding", isDefaultActive=true, sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```typescript

import * as React from 'react';
import * as ReactDOM from "react-dom";
import { ListViewComponent } from '@syncfusion/ej2-react-lists';
//import DataManager related classes
import { DataManager, Query, ODataV4Adaptor } from '@syncfusion/ej2-data';
import { createSpinner, hideSpinner, showSpinner} from '@syncfusion/ej2-react-popups';

export default class App extends React.Component<{}, {}> {
  //bind the DataManager instance to dataSource property
  private data = new DataManager({
    url: "//js.syncfusion.com/ejServices/Wcf/Northwind.svc/",
    crossDomain: true
  });

  //map the appropriate columns to fields property
  private fields = { id: "ProductID", text: "ProductName" };
  spinnerInstance: HTMLElement | null = null;

  //bind the Query instance to query property
  private query = new Query()
    .from("Products")
    .select("ProductID,ProductName")
    .take(10);

  componentDidMount() {
    if (this.spinnerInstance) {
      createSpinner({
        target: this.spinnerInstance
      });
      showSpinner(this.spinnerInstance);
    }
  }

  public onActionComplete() {
    if (this.spinnerInstance) this.spinnerInstance.style.display = "none";
  }

  render() {
    return (
      <div>
        <ListViewComponent
          id="list"
          dataSource={this.data}
          fields={this.fields}
          query={this.query}
          showHeader={true}
          headerTitle="Product Name"
          actionComplete={this.onActionComplete.bind(this)}
        />
        <div
          ref={spinner => {
            this.spinnerInstance = spinner;
          }}
          id="spinner"
        />
      </div>
    );
  }
}

ReactDOM.render(<App />, document.getElementById('element'));
```

{% endtab %}
