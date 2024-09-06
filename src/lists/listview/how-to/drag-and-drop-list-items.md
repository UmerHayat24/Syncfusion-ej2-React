# Drag and Drop list items

In ListView component, we don't have drag and drop support. But we can achieve this requirement using [`TreeView`](https://ej2.syncfusion.com/react/documentation/treeview/getting-started/) component with ListView appearance.

Drag and Drop in TreeView component was enabled by setting [`allowDragAndDrop`](../../api/treeview#allowdraganddrop) to `true`.

```typescript

        <TreeViewComponent id='treeview'
                dataSource={this.data}
                allowDragAndDrop = {true}
                fields= {this.field} >
        </TreeViewComponent>

```

The TreeView component is used to represent hierarchical data in a tree like structure. So, list items in TreeView can be dropped to child of target element. we can prevent this behaviour by cancelling the [`nodeDragStop`](../../api/treeview#nodedragstop) and [`nodeDragging`](../../api/treeview#nodedragging) events.

{% tab compileJsx=true%}

```typescript

onDragStop(args: DragAndDropEventArgs) {
    //Block the Child Drop operation in TreeView
   let  draggingItem: HTMLCollection = document.getElementsByClassName("e-drop-in");
    if (draggingItem.length == 1) {
        draggingItem[0].classList.add('e-no-drop');
        args.cancel = true;
    }
}

render() {
        return (
        <TreeViewComponent id='treeview'
                dataSource={this.data}
                allowDragAndDrop = {true}
                nodeDragging = {this.onDragStop.bind(this)}
                nodeDragStop = {this.onDragStop.bind(this)}
                fields= {this.field} >
        </TreeViewComponent>
        )
    }

```

{% endtab %}

In the below sample, we have rendered draggable list items.

{% tab template="listview/reorder", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```typescript

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { TreeViewComponent } from '@syncfusion/ej2-react-navigations';
import {DragAndDropEventArgs } from '@syncfusion/ej2-navigations';

export default class App extends React.Component<{}, {}> {
  //Define an array of JSON data
  public data: any[] = [
    { text: "Hennessey Venom", id: "list-01" },
    { text: "Bugatti Chiron", id: "list-02" },
    { text: "Bugatti Veyron Super Sport", id: "list-03" },
    { text: "SSC Ultimate Aero", id: "list-04" },
    { text: "Koenigsegg CCR", id: "list-05" },
    { text: "McLaren F1", id: "list-06" },
    { text: "Aston Martin One- 77", id: "list-07" },
    { text: "Jaguar XJ220", id: "list-08" },
    { text: "McLaren P1", id: "list-09" },
    { text: "Ferrari LaFerrari", id: "list-10" }
  ];

  public field: object = { dataSource: this.data, id: "id", text: "text" };

  onDragStop(args: DragAndDropEventArgs) {
    //Block the Child Drop operation in TreeView
    let draggingItem: HTMLCollection = document.getElementsByClassName("e-drop-in");
    if (draggingItem.length == 1) {
      draggingItem[0].classList.add("e-no-drop");
      args.cancel = true;
    }
  }

  render() {
    return (
      <TreeViewComponent
        id="treeview"
        allowDragAndDrop={true}
        nodeDragging={this.onDragStop.bind(this) as any}
        nodeDragStop={this.onDragStop.bind(this) as any}
        fields={this.field}
      />
    );
  }
}
ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}
