---
title: "Dynamically change Kanban columns"
component: "Kanban"
description: "This article demonstrates how to dynamically change the particular column or complete column in the Kanban board."
---

# Change Kanban columns dynamically

You can dynamically change the Kanban columns by using the [`columns`](../../api/kanban#columns) property.

In the below sample, you can dynamically change the [`allowToggle`](../../api/kanban/columnsModel/#allowtoggle) property at the particular column when you click on the button. You can also change the initially created columns to the new Kanban columns by using the [`columns`](../../api/kanban#columns) property when you click on the button.

{% tab template="kanban/auto", iframeHeight="588px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { extend } from '@syncfusion/ej2-base';
import { KanbanComponent, ColumnsDirective, ColumnDirective } from "@syncfusion/ej2-react-kanban";
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { kanbanData } from './datasource';

class App extends React.Component<{}, {}>{
   constructor() {
        super(...arguments);
        this.data = extend([], kanbanData, null, true);
    }
    particularColumn() {
        this.kanbanObj.columns[1].allowToggle= true;
    }
    column() {
      this.kanbanObj.columns = [
        { headerText: 'To Do', keyField: 'Open' },
        { headerText: 'Done', keyField: 'Close' }
      ]
    }
  render() {
    return <div className='control-wrapper'>
                <ButtonComponent id='particularColumn' className="e-btn" onClick={this.particularColumn.bind(this)} >Enable Allow Toggle</ButtonComponent>
                <ButtonComponent id='column' className="e-btn" onClick={this.column.bind(this)}>Change Columns</ButtonComponent>
                <KanbanComponent id="kanban" keyField="Status" dataSource={this.data} cardSettings={{ contentField: "Summary", headerField: "Id" }} ref={(kanban) => { this.kanbanObj = kanban }}>
                    <ColumnsDirective>
                        <ColumnDirective headerText="To Do" keyField="Open"/>
                        <ColumnDirective headerText="In Progress" keyField="InProgress"/>
                        <ColumnDirective headerText="Testing" keyField="Testing"/>
                        <ColumnDirective headerText="Done" keyField="Close"/>
                    </ColumnsDirective>
                </KanbanComponent>
            </div>
  }
};
ReactDOM.render(<App />, document.getElementById('kanban'));

```

{% endtab %}