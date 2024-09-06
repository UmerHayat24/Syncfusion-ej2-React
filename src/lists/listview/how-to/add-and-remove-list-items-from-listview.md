# Add and remove list items from ListView

You can add or remove list items from the ListView component using the
[`addItem`](../../api/list-view/#additem) and
[`removeItem`](../../api/list-view/#removeitem) methods.
Refer to the following steps to add or remove a list item.

* Render the ListView with data source, and use the
[template](../../api/list-view/#template) property to append the delete icon
for each list item. Also, bind the click event for the delete icon using the
[actionComplete](../../api/list-view/#actioncomplete) handler.

* Render the Add Item button, and bind the click event. On the click event handler, pass data with random id to
the [`addItem`](../../api/list-view/#additem) method to add a
new list item on clicking the Add Item button.

* Bind the click handler to the delete icon created in step 1. Within the click event, remove the list item by passing the
delete icon list item to
[`removeItem`](../../api/list-view/#removeitem) method.

{% tab template="listview/add-item", isDefaultActive=true, sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true%}

```typescript

import * as React from 'react';
import * as ReactDOM from "react-dom";
import { ListViewComponent } from '@syncfusion/ej2-react-lists';
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';

export default class App extends React.Component<{}, {}> {
private listviewInstance: ListViewComponent = null as any;

  listTemplate(data: any): JSX.Element {
    return (
      <div className="text-content">
        {data.text}
        <span className="delete-icon" onClick={this.deleteItem.bind(this)} />
      </div>
    );
  }
  // define the array of Json
  private dataSource: any = [
    { text: "Hennessey Venom", id: "1", icon: "delete-icon" },
    { text: "Bugatti Chiron", id: "2", icon: "delete-icon" },
    { text: "Bugatti Veyron Super Sport", id: "3", icon: "delete-icon" },
    { text: "Aston Martin One- 77", id: "4", icon: "delete-icon" },
    { text: "Jaguar XJ220", id: "list-5", icon: "delete-icon" },
    { text: "McLaren P1", id: "6", icon: "delete-icon" }
  ];

  public fields: Object = { text: "text", iconCss: "icon" };

  addItem() {
    let data = {
      text: "Koenigsegg - " + (Math.random() * 1000).toFixed(0),
      id: (Math.random() * 1000).toFixed(0).toString(),
      icon: "delete-icon"
    };
    this.listviewInstance.addItem([data]);
  }

  deleteItem(args: any) {
    args.stopPropagation();
    let liItem = args.target.parentElement.parentElement;
    this.listviewInstance.removeItem(liItem);
  }

  render() {
    return (
      <div>
        <ListViewComponent
          id="sample-list"
          dataSource={this.dataSource}
          fields={this.fields}
          template={this.listTemplate.bind(this) as any}
          ref={listview => {
            this.listviewInstance = listview as any;
          }}
        />
        <ButtonComponent id="btn" onClick={this.addItem.bind(this)}>
          Add Item
        </ButtonComponent>
      </div>
    );
  }
}

ReactDOM.render(<App />, document.getElementById('element'));
```

{% endtab %}
