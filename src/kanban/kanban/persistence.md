---
title: "Kanban State Persistence"
component: "Kanban"
description: "This section explains how to persist the column and swimlane expand/collapse state in the browser’s local storage."
---

# State Persistence

State persistence refers to the Kanban state maintained in the browser's [`localStorage`](https://www.w3schools.com/html/html5_webstorage.asp#) even if the browser is refreshed or if you move to the next page within the browser.

State persistence stores Kanban datasource, column and swimlane expand/collapse state in the local storage when the [`enablePersistence`](../api/kanban/#enablepersistence) is defined as true.

{% tab template="kanban/persistence", iframeHeight="588px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { extend } from '@syncfusion/ej2-base';
import { KanbanComponent, ColumnsDirective, ColumnDirective } from "@syncfusion/ej2-react-kanban";
import { kanbanData } from './datasource';

class App extends React.Component<{}, {}>{
   constructor() {
        super(...arguments);
        this.data = extend([], kanbanData, null, true);
    }
  render() {
    return <KanbanComponent id="kanban" keyField="Status" dataSource={this.data} cardSettings={{ contentField: "Summary", headerField: "Id" }} enablePersistence={true} swimlaneSettings={{ keyField: "Assignee" }}>
                <ColumnsDirective>
                  <ColumnDirective headerText="To Do" keyField="Open" allowToggle={true} />
                  <ColumnDirective headerText="In Progress" keyField="InProgress" allowToggle={true} />
                  <ColumnDirective headerText="Testing" keyField="Testing" allowToggle={true} />
                  <ColumnDirective headerText="Done" keyField="Close" allowToggle={true} />
                </ColumnsDirective>
            </KanbanComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('kanban'));

```

{% endtab %}
