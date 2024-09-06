---
title: "How To"
component: "Gantt"
description: "Learn how to maintain zoomtofit."
---

# Maintain zoomToFit

In the Gantt control, While performing edit actions or dynamically change dataSource, the timeline gets refreshed. When zoomToFit toolbar item is clicked and perform editing actions or dynamically change dataSource, the timeline gets refreshed. So that, the timeline will not fit to the project any more.

## Maintain zoomToFit after edit actions

We can maintain `zoomToFit` after editing actions(cell edit,dialog edit,taskbar edit) by using [`fitToProject`](../api/gantt/#fittoproject) method in `actionComplete` and `taskbarEdited` event.

{% tab template="gantt/how-to-maintainzoomtofit", compileJsx=true %}

```typescript
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { GanttComponent, Inject, Toolbar, Edit, Selection, ToolbarItem }from '@syncfusion/ej2-react-gantt';
import { data } from './datasource';
class App extends React.Component<{}, {}>{
    private ganttInstance: any;
    public taskFields: any = {
    id: 'TaskID',
    name: 'TaskName',
    startDate: 'StartDate',
    duration: 'Duration',
    progress: 'Progress',
    dependency: 'Predecessor',
    child: 'subtasks'
  };
  public editSettings: any = {
    allowEditing: true,
    allowTaskbarEditing: true
  };
  public toolbarOptions: ToolbarItem[] = ['Edit','ZoomToFit'];
  actionComplete(args) {
    if ((args.action === "CellEditing" || args.action === "DialogEditing") && args.requestType === "save") {
        this.ganttInstance.dataSource = data;
        this.ganttInstance.fitToProject();
      }
  };
  taskbarEdited(args) {
      if (args) {
        this.ganttInstance.dataSource = data;
        this.ganttInstance.fitToProject();
      }
  };
    render() {
        return <GanttComponent dataSource={data} taskFields={this.taskFields}
        toolbar={this.toolbarOptions} editSettings={this.editSettings} actionComplete={this.actionComplete.bind(this)} taskbarEdited={this.taskbarEdited.bind(this)} height = '450px' ref={gantt => this.ganttInstance = gantt}>
           <Inject services={[Toolbar, Edit, Selection]} />
        </GanttComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('root'));
```

{% endtab %}

## Maintain zoomToFit after change dataSource dynamically

We can maintain `zoomToFit` after change dataSource dynamically, by calling [`fitToProject`](../api/gantt/#fittoproject) method in dataBound event.

{% tab template="gantt/how-to-maintainzoomtofitdatasource", compileJsx=true %}

```typescript
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { GanttComponent, Inject, Toolbar, ToolbarItem }from '@syncfusion/ej2-react-gantt';
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { data, changeData } from './datasource';
class App extends React.Component<{}, {}>{
    private ganttInstance: any;
    public taskFields: any = {
    id: 'TaskID',
    name: 'TaskName',
    startDate: 'StartDate',
    duration: 'Duration',
    progress: 'Progress',
    dependency: 'Predecessor',
    child: 'subtasks'
  };
  public toolbarOptions: ToolbarItem[] = ['ZoomToFit'];
  public clickHandler() {
    this.ganttInstance.dataSource = changeData;
  };
  dataBound(args) {
    this.ganttInstance.fitToProject();
  };
    render() {
        return (<div>
        <ButtonComponent onClick= { this.clickHandler.bind(this)}>Change Data</ButtonComponent>
        <GanttComponent dataSource={data} taskFields={this.taskFields} dataBound={this.dataBound.bind(this)}
        toolbar={this.toolbarOptions} height = '450px' ref={gantt => this.ganttInstance = gantt}>
           <Inject services={[Toolbar]} />
        </GanttComponent></div>)
    }
};
ReactDOM.render(<App />, document.getElementById('root'));
```

{% endtab %}