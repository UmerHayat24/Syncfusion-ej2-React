---
title: "How To"
component: "Gantt"
description: "Learn how to set new row position while adding new records in Gantt control."
---

# Set new row position in Gantt

In Gantt, a new row can be added in one of the following positions: Top, Bottom, Above, Below and Child. This position can be specified through the `newRowPostion` property. We can make use of the toolbarClick event to create a context menu that specifies the position in which the new row is to be added when adding a record through toolbar click.

The following code snippets demonstrate how to achieve this.

{% tab template="gantt/how-to-newrow", compileJsx=true %}

```typescript
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { GanttComponent, Inject, Edit, EditSettingsModel, Selection, Toolbar, ToolbarItem } from '@syncfusion/ej2-react-gantt';
import { ContextMenuComponent } from '@syncfusion/ej2-react-navigations';
import { data } from './datasource';
class App extends React.Component<{}, {}>{
    public taskFields: any = {
    id: 'TaskID',
    name: 'TaskName',
    startDate: 'StartDate',
    duration: 'Duration',
    progress: 'Progress',
    child: 'subtasks'
  };
  public editOptions: EditSettingsModel = {
      allowAdding: true
  };
  public toolbarOptions: ToolbarItem[] = ['Add'];
  toolbarClick(args) {
        if (args.item.id === 'GanttExport_add') {
            this.cMenu.open(40, 20);
        }
    }
  this.menuItems = [
            {
                text: 'Bottom'
            },
            {
                text: 'Above'
            },
            {
                text: 'Below'
            },
            {
                text: 'Child'
            },
            {
                text: 'Top'
            }
        ];
        select(args) {
            if (args.item.text === "Bottom") {
            this.ganttInstance.editSettings.newRowPosition = "Bottom";
            this.ganttInstance.openAddDialog();
        } else if (args.item.text === "Above") {
            if (this.ganttInstance.selectedRowIndex == -1) {
                alert("Please select any row");
            } else {
                this.ganttInstance.editSettings.newRowPosition = "Above";
                this.ganttInstance.openAddDialog();
            }
        } else if (args.item.text === "Below") {
            if (this.ganttInstance.selectedRowIndex == -1) {
                alert("Please select any row");
            } else {
                this.ganttInstance.editSettings.newRowPosition = "Child";
                this.ganttInstance.openAddDialog();
            }
        } else if (args.item.text === "Child") {
            if (this.ganttInstance.selectedRowIndex == -1) {
                alert("Please select any row");
            } else {
                this.ganttInstance.editSettings.newRowPosition = "Child";
                this.ganttInstance.openAddDialog();
            }
        } else if (args.item.text === "Top") {
            this.ganttInstance.editSettings.newRowPosition = "Top";
            this.ganttInstance.openAddDialog();
        }
        }
    render() {
        return
        <ContextMenuComponent id='contextmenu' ref={(scope) => this.cMenu = scope} items={this.menuItems} select={this.select.bind(this)}/>
        <GanttComponent dataSource={data} taskFields={this.taskFields} allowSelection={true}
        editSettings={this.editOptions} toolbar={this.toolbarOptions} toolbarClick={this.toolbarClick.bind(this)} height = '450px' ref={gantt => this.ganttInstance = gantt}>
            <Inject services={[Edit, Selection, Toolbar]} />
        </GanttComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('root'));
```

{% endtab %}