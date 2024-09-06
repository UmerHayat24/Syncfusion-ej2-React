---
title: "Integrate other component inside the card"
component: "Card"
description: "This example demonstrates how to integrate other Essential JS 2 controls inside the Essential JS 2 Card control."
---

# Integrate other component inside the card

You can integrate any component inside the card element. Here ListView component is placed inside the card for showcasing the To-Do list.

{% tab template="card/card_with_list", sourceFiles="app/**/*.tsx"   %}

```typescript
import { ListViewComponent } from '@syncfusion/ej2-react-lists';
import * as React from "react";
import * as ReactDOM from "react-dom";

export default class ReactApp extends React.Component<{}, {}> {
  public fields = { text: 'todoList' };
  // define the array of JSON
  public todoList: any = [
    { todoList: 'Pay Bills' },
    { todoList: 'Call Chris' },
    { todoList: 'Meet Andrew' },
    { todoList: 'Visit Manager' },
    { todoList: 'Customer Meeting' },
  ];
  public render() {
    return (
      <div>
        <div className="e-card" id="basic">
          <div className="e-card-title">To-Do List</div>
          <div className="e-card-separator" />
          <div className="e-card-content">
            <ListViewComponent dataSource={this.todoList} fields={this.fields} showCheckBox={true} />
          </div>
        </div>
      </div>
    );
  }
}
ReactDOM.render(<ReactApp />, document.getElementById("element"));
```

{% endtab %}