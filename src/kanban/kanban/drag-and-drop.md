---
title: "Kanban drag and drop"
component: "Kanban"
description: "This article explains how to drag and drop the card information from an external source and vice versa."
---

# Drag and drop

All cards can be dragged and dropped across the columns or within the columns or swimlane row or kanban to an external source and vice versa.

The following drag and drop types are available in the Kanban board.

* Internal drag and drop
    * Column drag and drop
    * Swimlane drag and drop
* External drag and drop
    * Kanban to Kanban
    * Kanban to External source and vice versa.

> Dropped card position varies based on the `sortSettings` property.

## Internal drag and drop

Allows the user to drag and drop the cards within the kanban board. Based on this, we can categorize into two ways.

* Column drag and drop
* Swimlane drag and drop

### Column drag and drop

By default, all cards can be dragged and dropped across the columns and within the columns. You cannot drag and drop the cards when disabling the `allowDragAndDrop` property.

> You can prevent the drag or drop behavior of the particular column by disabling the `allowDrag` or `allowDrop` property.
> You can also control the flow of transition cards between the columns by using the `transitionColumns` property.

In the following example, disable the drag and drop behavior on the Kanban board.

{% tab template="kanban/drag-and-drop", iframeHeight="588px", compileJsx=true %}

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
    return <KanbanComponent id="kanban" keyField="Status" dataSource={this.data} cardSettings={{ contentField: "Summary", headerField: "Id" }} allowDragAndDrop={false}>
                <ColumnsDirective>
                  <ColumnDirective headerText="To Do" keyField="Open" />
                  <ColumnDirective headerText="In Progress" keyField="InProgress" />
                  <ColumnDirective headerText="Testing" keyField="Testing" />
                  <ColumnDirective headerText="Done" keyField="Close" />
                </ColumnsDirective>
            </KanbanComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('kanban'));

```

{% endtab %}

### Swimlane drag and drop

By default, Swimlane allows drag and drop across the columns within the swimlane row. Kanban does not allow dragging the cards across the swimlane rows.

Enabling the `dragAndDrop` property allows you to drag the cards across the swimlane rows, which is specified inside the `swimlaneSettings` property.

{% tab template="kanban/swimlane-drag-and-drop", iframeHeight="588px", compileJsx=true %}

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
    return <KanbanComponent id="kanban" keyField="Status" dataSource={this.data} cardSettings={{ contentField: "Summary", headerField: "Id" }} swimlaneSettings={{ keyField: "Assignee",allowDragAndDrop: true }}>
                <ColumnsDirective>
                  <ColumnDirective headerText="To Do" keyField="Open" />
                  <ColumnDirective headerText="In Progress" keyField="InProgress" />
                  <ColumnDirective headerText="Testing" keyField="Testing" />
                  <ColumnDirective headerText="Done" keyField="Close" />
                </ColumnsDirective>
            </KanbanComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('kanban'));

```

{% endtab %}

## External drag and drop

Allows the user to drag and drop the cards from one kanban to another kanban or Kanban to an external source and vice versa.

### Kanban to kanban

Drag and drop the card from one kanban to another kanban and vice versa. This can be achieved by specifying the `externalDropId` property which is used to specify the id of the dropped kanban element and the `dragStop` event which is used to delete the card on dragged Kanban and add the card on dropped Kanban using the `deleteCard` and `addCard` public methods.

> Before adding a card to dropped kanban, you can manually change the card data `headerField` when the same card data `headerField` is dropped to another Kanban.

In the following example, Drag the card from one Kanban and drop it into another kanban using the `dragStop` event. In this event, remove the card from the dragged Kanban by using the `deleteCard` public method and add the card to the dropped Kanban by using the `addCard` public method.

{% tab template="kanban/kanban-to-kanban", iframeHeight="588px", compileJsx=true %}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { extend, closest } from '@syncfusion/ej2-base';
import { KanbanComponent, ColumnsDirective, ColumnDirective, DragEventArgs, Kanban } from "@syncfusion/ej2-react-kanban";
import { kanbanAData, kanbanBData } from './datasource';

class App extends React.Component<{}, {}>{
  public kanbanA: Kanban | null;
  public kanbanB: Kanban | null;
   constructor() {
        super(...arguments);
        this.dataA = extend([], kanbanAData, null, true);
        this.dataB = extend([], kanbanBData, null, true);
        this.externalKanbanADropId = ["#KanbanB"];
        this.externalKanbanBDropId = ["#KanbanA"];
    }
    private onKanbanADragStop(args: DragEventArgs): void {
        let kanbanBElement: Element = closest(args.event.target as Element, '#KanbanB');
        if (kanbanBElement) {
          this.kanbanA.deleteCard(args.data);
          args.data.forEach((card: Record<string, any>, i: number) => {
              const index: number = this.kanbanB.kanbanData.findIndex((colData: Record<string, any>) =>
                  colData[this.kanbanB.cardSettings.headerField] === card[this.kanbanB.cardSettings.headerField]);
              if (index !== -1) {
                  card[this.kanbanB.cardSettings.headerField] = Math.max(...this.kanbanB.kanbanData.map(
                      (obj: Record<string, string>) => parseInt(obj[this.kanbanB.cardSettings.headerField], 10))) + ++i;
              }
          });
          this.kanbanB.addCard(args.data, args.dropIndex);
          args.cancel = true;
        }
    }
    private onKanbanBDragStop(args: DragEventArgs): void {
        let kanbanAElement: Element = closest(args.event.target as Element, '#KanbanA');
        if (kanbanAElement) {
          this.kanbanB.deleteCard(args.data);
          args.data.forEach((card: Record<string, any>, i: number) => {
              const index: number = this.kanbanA.kanbanData.findIndex((colData: Record<string, any>) =>
                  colData[this.kanbanA.cardSettings.headerField] === card[this.kanbanA.cardSettings.headerField]);
              if (index !== -1) {
                  card[this.kanbanA.cardSettings.headerField] = Math.max(...this.kanbanA.kanbanData.map(
                      (obj: Record<string, string>) => parseInt(obj[this.kanbanA.cardSettings.headerField], 10))) + ++i;
              }
          });
          this.kanbanA.addCard(args.data, args.dropIndex);
          args.cancel = true;
       }
  }
  render() {
    return <div>
              <div className="container-fluid">
                  <div className="row">
                      <div className="col-sm-6">
                        <h4>Kanban A</h4>
                            <KanbanComponent id="KanbanA" ref={kanbanA => this.kanbanA = kanbanA} keyField="Status" dataSource={this.dataA} cardSettings={{ contentField: "Summary", headerField: "Id" }} dragStop={this.onKanbanADragStop.bind(this)} externalDropId={this.externalKanbanADropId}>
                                <ColumnsDirective>
                                    <ColumnDirective headerText="To Do" keyField="Open" />
                                    <ColumnDirective headerText="Done" keyField="Close" />
                                </ColumnsDirective>
                            </KanbanComponent>
                      </div>
                      <div className="col-sm-6">
                          <h4>Kanban B</h4>
                            <KanbanComponent id="KanbanB" ref={kanbanB => this.kanbanB = kanbanB} keyField="Status" dataSource={this.dataB} cardSettings={{ contentField: "Summary", headerField: "Id" }} dragStop={this.onKanbanBDragStop.bind(this)} externalDropId={this.externalKanbanBDropId}>
                                <ColumnsDirective>
                                    <ColumnDirective headerText="To Do" keyField="Open" />
                                    <ColumnDirective headerText="Done" keyField="Close" />
                                </ColumnsDirective>
                            </KanbanComponent>
                      </div>
                  </div>
              </div>
        </div>
  }
};
ReactDOM.render(<App />, document.getElementById('kanban'));

```

{% endtab %}

### Treeview to Kanban

Drag the card from the Kanban board and drop it to the Treeview component and vice versa.

In the following sample, remove the data from the Kanban board using the `deleteCard` public method and add to the Treeview component using the `addNodes` public method at Kanban `dragStop` event when dragging the card and dropping it to the Treeview component. Remove the data from Treeview using the `removeNodes` public method and add to Kanban board using the `openDialog` public method when dragging the list from the Treeview component and dropping it to the kanban board.

{% tab template="kanban/kanban-to-treeview", iframeHeight="588px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { extend, closest } from '@syncfusion/ej2-base';
import { KanbanComponent, ColumnsDirective, ColumnDirective, DragEventArgs, Kanban } from "@syncfusion/ej2-react-kanban";
import { DragAndDropEventArgs } from '@syncfusion/ej2-navigations';
import { TreeViewComponent } from '@syncfusion/ej2-react-navigations';
import { kanbanData, treeViewData } from './datasource';

class App extends React.Component<{}, {}>{
  public kanbanObj: Kanban | null;
  public treeViewObj: TreeViewComponent | null;
   constructor() {
        super(...arguments);
        this.data = extend([], kanbanData, null, true);
        this.treeData = extend([], treeViewData, null, true);
        this.fields = { dataSource: this.treeData, id: 'Id', text: 'Status' };
        this.allowDragAndDrops = true;
        this.externalKanbanDropId = ["#treeView"];
    }
    private treeTemplate(props: KanbanDataModel): JSX.Element {
        return (<div><div id="treelist"><div id="treeviewlist">{props.Id} - {props.Status}</div>
                </div></div>);
    }
    private onKanbanADragStop(args: DragEventArgs): void {
       let treeViewElement: Element = closest(args.event.target as Element, '#treeView');
          if (treeViewElement) {
              this.kanbanObj.deleteCard(args.data);
              this.treeViewObj.addNodes(args.data);
              args.cancel = true;
          }
    }
    private onTreeDragStop(args: DragAndDropEventArgs): void {
      let kanbanElement: Element = closest(args.event.target as Element, '#Kanban');
          if (kanbanElement) {
              let treeData = this.treeViewObj.fields.dataSource as { [key: string]: Object }[];
              const filteredData =
                  treeData.filter((item: any) => item.Id === parseInt(args.draggedNodeData.id as string, 10));
              this.treeViewObj.removeNodes([args.draggedNodeData.id] as string[]);
              this.kanbanObj.openDialog('Add', filteredData[0]);
              args.cancel = true;
          }
    }
  render() {
    return <div>
          <div className="container-fluid">
                  <div className="row">
                      <div className="col-sm-6">
                        <h4>Kanban</h4>
                            <KanbanComponent id="Kanban" ref={kanban => this.kanbanObj = kanban} keyField="Status" dataSource={this.data} cardSettings={{ contentField: "Summary", headerField: "Id" }} dragStop={this.onKanbanADragStop.bind(this)} externalDropId={this.externalKanbanDropId} >
                                <ColumnsDirective>
                                    <ColumnDirective headerText="To Do" keyField="Open" />
                                    <ColumnDirective headerText="Done" keyField="Close" />
                                </ColumnsDirective>
                            </KanbanComponent>
                      </div>
                    <div className="col-sm-6">
                    <h4>TreeView</h4>
                             <TreeViewComponent id="treeView" ref={treeView => this.treeViewObj = treeView} nodeTemplate={this.treeTemplate.bind(this)} fields={this.fields} nodeDragStop={this.onTreeDragStop.bind(this)} allowDragAndDrop={this.allowDragAndDrops} />
                    </div>
                </div>
            </div>
        </div>
  }
};
ReactDOM.render(<App />, document.getElementById('kanban'));

```

{% endtab %}

### Schedule to Kanban

Drag the card from the Kanban board and drop it to the Schedule component and vice versa.

In the following sample, remove the data from the Kanban board using the `deleteCard` public method and add to the schedule component using the `addNodes` public method at Kanban `dragStop` event when dragging the card and dropping it to the Treeview component. Remove the data from Treeview using the `removeNodes` public method and add to Kanban board using the `addCard` public method when dragging the list from the Treeview component and dropping it to the kanban board.

{% tab template="kanban/kanban-to-schedule", iframeHeight="588px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { extend, closest, removeClass } from '@syncfusion/ej2-base';
import { KanbanComponent, ColumnsDirective, ColumnDirective, DragEventArgs, Kanban } from "@syncfusion/ej2-react-kanban";
import {
  ScheduleComponent, ResourcesDirective, ResourceDirective,
  ViewsDirective, ViewDirective, Inject, TimelineViews,
  Resize, DragAndDrop, TimelineMonth
} from '@syncfusion/ej2-react-schedule';
import { kanbanData, scheduleData } from './datasource';

class App extends React.Component<{}, {}>{
  public kanbanObj: Kanban | null;
  public scheduleObj: ScheduleComponent | null;
   constructor() {
        super(...arguments);
        this.data = extend([], kanbanData, null, true);
        this.scheduleDataSource = extend([], scheduleData, null, true);
        this.externalKanbanDropId = ["#Schedule"];
    }
    private departmentData: Object[] = [
      { Text: 'GENERAL', Id: 1, Color: '#bbdc00' },
      { Text: 'DENTAL', Id: 2, Color: '#9e5fff' }
    ];
    private consultantData: Object[] = [
      { Text: 'Alice', Id: 1, GroupId: 1, Color: '#bbdc00', Designation: 'Cardiologist' },
      { Text: 'Nancy', Id: 2, GroupId: 2, Color: '#9e5fff', Designation: 'Orthodontist' },
      { Text: 'Robert', Id: 3, GroupId: 1, Color: '#bbdc00', Designation: 'Optometrist' },
      { Text: 'Robson', Id: 4, GroupId: 2, Color: '#9e5fff', Designation: 'Periodontist' },
      { Text: 'Laura', Id: 5, GroupId: 1, Color: '#bbdc00', Designation: 'Orthopedic' },
      { Text: 'Margaret', Id: 6, GroupId: 2, Color: '#9e5fff', Designation: 'Endodontist' }
    ];
    private getConsultantName(value: ResourceDetails | TreeViewArgs): string {
      return (value as ResourceDetails).resourceData[(value as ResourceDetails).resource.textField] as string;
    }

    private getConsultantDesignation(value: ResourceDetails): string {
      return (value as ResourceDetails).resourceData.Designation as string;
    }

    private resourceHeaderTemplate(props: any): JSX.Element {
      return (<div className="template-wrap"><div className="specialist-category"><div className="specialist-name">
        {this.getConsultantName(props)}</div><div className="specialist-designation">{this.getConsultantDesignation(props)}</div></div></div>);
    }
    private onKanbanDragStop(args: DragEventArgs): void {
       let scheduleElement: Element = closest(args.event.target as Element, '#Schedule');
        if (scheduleElement) {
            this.kanbanObj.deleteCard(args.data);
            this.scheduleObj.openEditor(args.data[0], 'Add', true);
            args.cancel = true;
        }
    }
    private scheduleDragStop(args: ScheduleDragEventArgs): void {
        let kanbanElement: Element = closest(args.event.target as Element, '#Kanban');
        if (kanbanElement) {
             this.scheduleObj.deleteEvent(args.data.Id);
             removeClass([this.scheduleObj.element.querySelector('.e-selected-cell')], 'e-selected-cell');
             this.kanbanObj.openDialog('Add', args.data);
             args.cancel = true;
        }
    }
  render() {
    return <div>
          <div className="container-fluid">
                  <div className="row">
                      <div className="col-sm-6">
                        <h4>Kanban</h4>
                            <KanbanComponent id="Kanban" ref={kanban => this.kanbanObj = kanban} keyField="DepartmentName" dataSource={this.data} cardSettings={{ contentField: "Name", headerField: "Id" }} dragStop={this.onKanbanDragStop.bind(this)} externalDropId={this.externalKanbanDropId}>
                                <ColumnsDirective>
                                    <ColumnDirective headerText="GENERAL" keyField="GENERAL" />
                                </ColumnsDirective>
                            </KanbanComponent>
                      </div>
                    <div className="col-sm-6">
                    <h4>Schedule</h4>
                          <ScheduleComponent id="Schedule" ref={schedule => this.scheduleObj = schedule} cssClass='schedule-drag-drop' width='100%' height='650px' selectedDate={new Date(2018, 7, 1)}
                              currentView='TimelineDay' resourceHeaderTemplate={this.resourceHeaderTemplate.bind(this)}
                                  eventSettings={{
                                    dataSource: this.scheduleDataSource,
                                    fields: {
                                      subject: { title: 'Patient Name', name: 'Name' },
                                      startTime: { title: "From", name: "StartTime" },
                                      endTime: { title: "To", name: "EndTime" },
                                      description: { title: 'Reason', name: 'Description' }
                                    }
                                  }}
                                  group={{ enableCompactView: false, resources: ['Departments', 'Consultants'] }}
                                  dragStop={this.scheduleDragStop.bind(this)} >
                                  <ResourcesDirective>
                                    <ResourceDirective field='DepartmentID' title='Department' name='Departments' allowMultiple={false}
                                      dataSource={this.departmentData} textField='Text' idField='Id' colorField='Color'>
                                    </ResourceDirective>
                                    <ResourceDirective field='ConsultantID' title='Consultant' name='Consultants' allowMultiple={false}
                                      dataSource={this.consultantData} textField='Text' idField='Id' groupIDField="GroupId" colorField='Color'>
                                    </ResourceDirective>
                                  </ResourcesDirective>
                                  <ViewsDirective>
                                    <ViewDirective option='TimelineDay' />
                                    <ViewDirective option='TimelineMonth' />
                                  </ViewsDirective>
                                  <Inject services={[TimelineViews, TimelineMonth, Resize, DragAndDrop]} />
                          </ScheduleComponent>
                    </div>
                </div>
            </div>
        </div>
  }
};
ReactDOM.render(<App />, document.getElementById('kanban'));

```

{% endtab %}
