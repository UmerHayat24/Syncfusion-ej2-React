# Get selected items from ListView

Single or many items can be selected by users in the ListView component. An API is used to get selected items from the
list items. This is called as the
[`getSelectedItems`](../../api/list-view/#getselecteditems)
method.

## `getSelectedItems` method

This is used to get the details of the currently selected item from the list items. It returns the
[`SelectedItem`](../../api/list-view/selectedItem/) |
[`SelectedCollection`](../../api/list-view/selectedCollection/)

The `getSelectedItems` method returns the following items from the selected list items.

| Return type | Purpose |
|------------|-------------------|
| text | Returns the text of selected item lists |
| data | Returns the whole data of selected list items, i.e., returns the fields data of selected li.|
| item | Returns the collections of list items |

{% tab template="listview/selected-item", isDefaultActive=true, sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```typescript

import * as React from 'react';
import * as ReactDOM from "react-dom";
import { ListViewComponent } from '@syncfusion/ej2-react-lists';
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';

interface MyState {
  selectedItemsValue: any[];
}

export default class App extends React.Component<{}, MyState> {
  listobj: ListViewComponent | null = null;

  constructor(props: any) {
    super(props);
    this.state = {
      selectedItemsValue: []
    };
  }

  // define the array of Json
  private data: { [key: string]: Object }[] = [
    { text: "Hennessey Venom", id: "list-01" },
    { text: "Bugatti Chiron", id: "list-02", isChecked: true },
    { text: "Bugatti Veyron Super Sport", id: "list-03" },
    { text: "SSC Ultimate Aero", id: "list-04", isChecked: true },
    { text: "Koenigsegg CCR", id: "list-05" },
    { text: "McLaren F1", id: "list-06" },
    { text: "Aston Martin One- 77", id: "list-07", isChecked: true },
    { text: "Jaguar XJ220", id: "list-08" }
  ];

  getSelectedItems(): void {
    if (this.listobj) {
      this.setState({
        selectedItemsValue: (this.listobj.getSelectedItems() as any).data
      });
    }
  }

  render() {
    return (
      <div>
        <ListViewComponent
          id="list"
          dataSource={this.data}
          showCheckBox={true}
          ref={scope => {
            this.listobj = scope;
          }}
        />
        <ButtonComponent id="btn" onClick={this.getSelectedItems.bind(this)}>
          Get Selected Items
        </ButtonComponent>
        <div>
          <table>
            <tbody>
              <tr>
                <th>Text</th>
                <th>Id</th>
              </tr>

              {this.state.selectedItemsValue.map((item: any, index: number) => {
                return (
                  <tr key={index}>
                    <td>{item.text}</td>
                    <td>{item.id}</td>
                  </tr>
                );
              })}
            </tbody>
          </table>
        </div>
      </div>
    );
  }
}

ReactDOM.render(<App />, document.getElementById('element'));
```

{% endtab %}
