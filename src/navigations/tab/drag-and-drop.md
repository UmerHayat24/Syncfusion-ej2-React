---
title: "Drag and Drop"
component: "Tab"
description: "Drag and drop functionality in tab"
---

# Drag and drop items

The Tab component allows you to drag and drop any item by setting [allowDragAndDrop](../api/tab#allowdraganddrop)&nbsp;to **true**. Items can be reordered to any place by dragging and dropping them onto the desired location.

* If you need to prevent dragging action for a particular item, the [`onDragStart`](../api/tab#ondragstart) event can be used which will trigger when the item drag is started. If you need to prevent dropping action for a particular item, the [`dragged`](../api/tab#dragged) event can be used which will trigger when the drag action is stopped.

* The [`dragArea`](../api/tab#dragArea) defines the area in which the draggable element movement will be occurring. Outside that area will be restricted for the draggable element movement.

* The [`onDragStart`](../api/tab#ondragstart) event will be triggered before dragging the item from Tab.

* The [`dragging`](../api/tab#dragging) event will be triggered when the Tab item is being dragged.

* The [`dragged`](../api/tab#dragged) event will be triggered when the Tab item is dropped on the target element successfully.

In the following sample, the [allowDragAndDrop](../api/tab#allowdraganddrop) property is enabled.

{% tab template="tab/drag-and-drop/default", sourceFiles="app/**/*.tsx,index.css", compileJsx=true %}

```typescript
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { TabComponent, TabItemDirective, TabItemsDirective } from '@syncfusion/ej2-react-navigations';

export default class ReactApp extends React.Component<{}, {}> {

  public headerText: any = [{ text: "India" }, { text: "Australia" }, { text: "USA" }, { text: "France" }];
  public allowDragAndDrop: boolean = true;

  public content0() {
    return <div>
      India officially the Republic of India, is a country in South Asia. It is the seventh-largest country by area, the second-most populous country with over 1.2 billion people, and the most populous democracy in the world. Bounded by the Indian Ocean on the south, the Arabian Sea on the south-west, and the Bay of Bengal on the south-east, it shares land borders with Pakistan to the west;China, Nepal, and Bhutan to the north-east; and Burma and Bangladesh to the east. In the Indian Ocean, India is in the vicinity of Sri Lanka and the Maldives; in addition, India Andaman and Nicobar Islands share a maritime border with Thailand and Indonesia.
      </div>;
  }
  public content1() {
    return <div>
      Australia, officially the Commonwealth of Australia, is a country comprising the mainland of the Australian continent, the island of Tasmania and numerous smaller islands. It is the world sixth-largest country by total area. Neighboring countries include Indonesia, East Timor and Papua New Guinea to the north; the Solomon Islands, Vanuatu and New Caledonia to the north-east; and New Zealand to the south-east.
      </div>;
  }
  public content2() {
    return <div>
      The United States of America (USA or U.S.A.), commonly called the United States (US or U.S.) and America, is a federal republic consisting of fifty states and a federal district. The 48 contiguous states and the federal district of Washington, D.C. are in central North America between Canada and Mexico. The state of Alaska is west of Canada and east of Russia across the Bering Strait, and the state of Hawaii is in the mid-North Pacific. The country also has five populated and nine unpopulated territories in the Pacific and the Caribbean.
      </div>;
  }
  public content3() {
    return <div>
      France, officially the French Republic is a sovereign state comprising territory in western Europe and several overseas regions and territories. The European part of France, called Metropolitan France, extends from the Mediterranean Sea to the English Channel and the North Sea, and from the Rhine to the Atlantic Ocean; France covers 640,679 square kilo metres and as of August 2015 has a population of 67 million, counting all the overseas departments and territories.
      </div>;
  }

  public render() {
    return (
      <TabComponent id='draggableTab' heightAdjustMode='Auto' allowDragAndDrop={ this.allowDragAndDrop } dragArea="#container">
        <TabItemsDirective>
          <TabItemDirective header={this.headerText[0]} content={this.content0} />
          <TabItemDirective header={this.headerText[1]} content={this.content1} />
          <TabItemDirective header={this.headerText[2]} content={this.content2} />
          <TabItemDirective header={this.headerText[3]} content={this.content3} />
        </TabItemsDirective>
      </TabComponent>
    );
  }
}
ReactDOM.render(<ReactApp />, document.getElementById('element'));

```

{% endtab %}

## Drag and drop item between tabs

It is possible to drag and drop the tab items between two tabs, by manually saving those dropped items as new tab item data through the `addTab` method of Tab and removing the dragged item through the `removeTab` method of Tab.

In this example, we have used the tab control as an external source, and the item from the tab component is dragged and dropped onto another Tab. Therefore, it is necessary to use the `onDragStart` and `dragged` event of the Tab component, where we can form an event object and save it using the `addTab` method of the Tab and remove the dragged item through `removeTab` method of Tab using the dragged item index.

{% tab template="tab/drag-and-drop/tab-to-tab", sourceFiles="app/**/*.tsx,index.css", compileJsx=true %}

```typescript
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { TabComponent, TabItemDirective, TabItemsDirective, DragEventArgs } from '@syncfusion/ej2-react-navigations';
import { isNullOrUndefined } from "@syncfusion/ej2-base";

export default class ReactApp extends React.Component<{}, {}> {

  public firstTabObj: TabComponent;
  public secondTabObj: TabComponent;
  public headerText: any = [{ text: "India" }, { text: "Australia" }, { text: "USA" }, { text: "France" }, { text: "HTML" }, { text: "C Sharp(C#)" }, { text: "Java" }, { text: "VB.Net" }];
  public allowDragAndDrop: boolean = true;
  public firstTabitem: Object[] = [];
  public secondTabitem: Object[] = [];
  public dragItemIndex: number;
  public dragItemContainer: Element;

  public firstTabdragStart(args: DragEventArgs) {
    this.firstTabitem = [this.firstTabObj.items[args.index]];
    args.draggedItem.style.visibility = 'hidden';
    this.dragItemContainer = args.draggedItem.closest('.e-tab');
  }

  public firstTabDragStop(args: DragEventArgs) {
    if (!isNullOrUndefined(args.target.closest('.e-tab')) && !this.dragItemContainer.isSameNode(args.target.closest('.e-tab'))) {
      args.cancel = true;
      let TabElement: Element = args.target.closest('.e-tab');
      let dropItem: Element = args.target.closest('.e-toolbar-item');
      if (TabElement != null && dropItem != null) {
        this.dragItemIndex = Array.prototype.indexOf.call(this.firstTabObj.element.querySelectorAll('.e-toolbar-item'), args.draggedItem);
        let dropItemContainer: Element = args.target.closest('.e-toolbar-items');
        let dropItemIndex: number = (dropItemContainer != null) ? (Array.prototype.slice.call(dropItemContainer.querySelectorAll('.e-toolbar-item'))).indexOf(dropItem) : '';
        this.secondTabObj.addTab(this.firstTabitem, dropItemIndex);
        this.firstTabObj.removeTab(this.dragItemIndex);
      }
    }
  }

  public secondTabDragStart(args: DragEventArgs) {
    this.secondTabitem = [this.secondTabObj.items[args.index]];
    args.draggedItem.style.visibility = 'hidden';
    this.dragItemContainer = args.draggedItem.closest('.e-tab');
  }

  public secondTabDragStop(args: DragEventArgs) {
    if (!isNullOrUndefined(args.target.closest('.e-tab')) && !this.dragItemContainer.isSameNode(args.target.closest('.e-tab'))) {
      args.cancel = true;
      let TabElement: Element = args.target.closest('.e-tab');
      let dropItem: Element = args.target.closest('.e-toolbar-item');
      if (TabElement != null && dropItem != null) {
        this.dragItemIndex = Array.prototype.indexOf.call(this.secondTabObj.element.querySelectorAll('.e-toolbar-item'), args.draggedItem);
        let dropItemContainer: Element = args.target.closest('.e-toolbar-items');
        let dropItemIndex: number = (dropItemContainer != null) ? (Array.prototype.slice.call(dropItemContainer.querySelectorAll('.e-toolbar-item'))).indexOf(dropItem) : '';
        this.firstTabObj.addTab(this.secondTabitem, dropItemIndex);
        this.secondTabObj.removeTab(this.dragItemIndex);
      }
    }
  }

  public content0() {
    return <div>
      India officially the Republic of India, is a country in South Asia. It is the seventh-largest country by area, the second-most populous country with over 1.2 billion people, and the most populous democracy in the world. Bounded by the Indian Ocean on the south, the Arabian Sea on the south-west, and the Bay of Bengal on the south-east, it shares land borders with Pakistan to the west;China, Nepal, and Bhutan to the north-east; and Burma and Bangladesh to the east. In the Indian Ocean, India is in the vicinity of Sri Lanka and the Maldives; in addition, India Andaman and Nicobar Islands share a maritime border with Thailand and Indonesia.
      </div>;
  }
  public content1() {
    return <div>
      Australia, officially the Commonwealth of Australia, is a country comprising the mainland of the Australian continent, the island of Tasmania and numerous smaller islands. It is the world sixth-largest country by total area. Neighboring countries include Indonesia, East Timor and Papua New Guinea to the north; the Solomon Islands, Vanuatu and New Caledonia to the north-east; and New Zealand to the south-east.
      </div>;
  }
  public content2() {
    return <div>
      The United States of America (USA or U.S.A.), commonly called the United States (US or U.S.) and America, is a federal republic consisting of fifty states and a federal district. The 48 contiguous states and the federal district of Washington, D.C. are in central North America between Canada and Mexico. The state of Alaska is west of Canada and east of Russia across the Bering Strait, and the state of Hawaii is in the mid-North Pacific. The country also has five populated and nine unpopulated territories in the Pacific and the Caribbean.
      </div>;
  }
  public content3() {
    return <div>
      France, officially the French Republic is a sovereign state comprising territory in western Europe and several overseas regions and territories. The European part of France, called Metropolitan France, extends from the Mediterranean Sea to the English Channel and the North Sea, and from the Rhine to the Atlantic Ocean; France covers 640,679 square kilo metres and as of August 2015 has a population of 67 million, counting all the overseas departments and territories.
      </div>;
  }
  public content4() {
    return <div>
      HyperText Markup Language, commonly referred to as HTML, is the standard markup language used to create web pages. Along with CSS, and JavaScript, HTML is a cornerstone technology, used by most websites to create visually engaging web pages, user interfaces for web applications, and user interfaces for many mobile applications.[1] Web browsers can read HTML files and render them into visible or audible web pages. HTML describes the structure of a website semantically along with cues for presentation, making it a markup language, rather than a programming language.
      </div>;
  }
  public content5() {
    return <div>
      C# is intended to be a simple, modern, general-purpose, object-oriented programming language. Its development team is led by Anders Hejlsberg. The most recent version is C# 5.0, which was released on August 15, 2012.
      </div>;
  }
  public content6() {
    return <div>
      Java is a set of computer software and specifications developed by Sun Microsystems, later acquired by Oracle Corporation, that provides a system for developing application software and deploying it in a cross-platform computing environment. Java is used in a wide variety of computing platforms from embedded devices and mobile phones to enterprise servers and supercomputers. While less common, Java applets run in secure, sandboxed environments to provide many features of native applications and can be embedded in HTML pages.
      </div>;
  }
  public content7() {
    return <div>
      The command-line compiler, VBC.EXE, is installed as part of the freeware .NET Framework SDK. Mono also includes a command-line VB.NET compiler. The most recent version is VB 2012, which was released on August 15, 2012.
      </div>;
  }

  public render() {
    return (
        <div>
            <TabComponent ref={(tab) => { this.firstTabObj = tab }} id='firstTab' heightAdjustMode='Auto' allowDragAndDrop={this.allowDragAndDrop} dragArea="#container" onDragStart={this.firstTabdragStart.bind(this)} dragged={this.firstTabDragStop.bind(this)}>
                <TabItemsDirective>
                    <TabItemDirective header={this.headerText[0]} content={this.content0} />
                    <TabItemDirective header={this.headerText[1]} content={this.content1} />
                    <TabItemDirective header={this.headerText[2]} content={this.content2} />
                    <TabItemDirective header={this.headerText[3]} content={this.content3} />
                    </TabItemsDirective>
            </TabComponent>
            <br></br>
            <TabComponent ref={(tab) => { this.secondTabObj = tab }} id='secondTab' heightAdjustMode='Auto' allowDragAndDrop={this.allowDragAndDrop} dragArea="#container" onDragStart={this.secondTabDragStart.bind(this)} dragged={this.secondTabDragStop.bind(this)}>
                <TabItemsDirective>
                    <TabItemDirective header={this.headerText[4]} content={this.content4} />
                    <TabItemDirective header={this.headerText[5]} content={this.content5} />
                    <TabItemDirective header={this.headerText[6]} content={this.content6} />
                    <TabItemDirective header={this.headerText[7]} content={this.content7} />
                </TabItemsDirective>
            </TabComponent>
        </div>
    );
  }
}
ReactDOM.render(<ReactApp />, document.getElementById('element'));

```

{% endtab %}

## Drag and drop items to external source

It is possible to drag and drop the items to any of the external sources from the Tab, by manually saving those dropped items as new node data through the `addNodes` method of Treeview and removing the dragged item through the `removeTab` method of Tab.

In this example, we have used the tree view control as an external source, and the item from the tab component is dragged and dropped onto the child nodes of the tree view component. Therefore, it is necessary to use  the `dragged` event of the Tab component, where we can form an event object and save it using the `addNodes` method of the Treeview and remove the dragged item through the `removeTab` method of Tab using the dragged item index.

{% tab template="tab/drag-and-drop/tab-to-treeview", sourceFiles="app/**/*.tsx,index.css", compileJsx=true %}

```typescript
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { TabComponent, TabItemDirective, TabItemsDirective, DragEventArgs, TabItemModel, TreeViewComponent } from '@syncfusion/ej2-react-navigations';
import { isNullOrUndefined } from "@syncfusion/ej2-base";

export default class ReactApp extends React.Component<{}, {}> {

  public tabObj: TabComponent;
  public treeObj: TreeViewComponent;
  public headerText: any = [{ text: "India" }, { text: "Australia" }, { text: "USA" }, { text: "France" }];
  public allowDragAndDrop: boolean = true;
  public data: { [key: string]: Object }[] = [
    { text: 'Hennessey Venom', id: 'list-01' },
    { text: 'Bugatti Chiron', id: 'list-02' },
    { text: 'Bugatti Veyron Super Sport', id: 'list-03' },
    { text: 'SSC Ultimate Aero', id: 'list-04' },
    { text: 'Koenigsegg CCR', id: 'list-05' },
    { text: 'McLaren F1', id: 'list-06' },
    { text: 'Aston Martin One- 77', id: 'list-07' },
    { text: 'Jaguar XJ220', id: 'list-08' },
    { text: 'McLaren P1', id: 'list-09' },
    { text: 'Ferrari LaFerrari', id: 'list-10' },
  ];
  public field: Object = { dataSource: this.data, id: 'id', text: 'text' };
  public i: number = 0;

  public onTabCreate(): void {
    let tabElement: HTMLElement = document.getElementById('draggableTab');
    if (!isNullOrUndefined(tabElement)) {
      tabElement.querySelector('.e-tab-header').classList.add('e-droppable');
      tabElement.querySelector('.e-content').classList.add('tab-content');
    }
  }

  public tabDragStop(args: DragEventArgs) {
    let dragTabIndex: number = Array.prototype.indexOf.call(this.tabObj.element.querySelectorAll('.e-toolbar-item'), args.draggedItem);
    let dragItem: TabItemModel = this.tabObj.items[dragTabIndex];
    let dropNode: Element = args.target.closest('#draggableTreeview .e-list-item');
    if (dropNode != null && !args.target.closest('#draggableTab .e-toolbar-item')) {
      args.cancel = true;
      let dropContainer: NodeListOf<Element> = (document.querySelector('.treeview-external-drop-tab')).querySelectorAll('.e-list-item');
      let dropIndex: number = Array.prototype.indexOf.call(dropContainer, dropNode);
      let newNode: { [key: string]: Object }[] = [{ id: 'list' + this.i, text: dragItem.header.text }];
      this.tabObj.removeTab(dragTabIndex);
      this.treeObj.addNodes(newNode, 'Treeview', dropIndex);
    }
  }

  public content0() {
    return <div>
      India officially the Republic of India, is a country in South Asia. It is the seventh-largest country by area, the second-most populous country with over 1.2 billion people, and the most populous democracy in the world. Bounded by the Indian Ocean on the south, the Arabian Sea on the south-west, and the Bay of Bengal on the south-east, it shares land borders with Pakistan to the west;China, Nepal, and Bhutan to the north-east; and Burma and Bangladesh to the east. In the Indian Ocean, India is in the vicinity of Sri Lanka and the Maldives; in addition, India Andaman and Nicobar Islands share a maritime border with Thailand and Indonesia.
      </div>;
  }
  public content1() {
    return <div>
      Australia, officially the Commonwealth of Australia, is a country comprising the mainland of the Australian continent, the island of Tasmania and numerous smaller islands. It is the world sixth-largest country by total area. Neighboring countries include Indonesia, East Timor and Papua New Guinea to the north; the Solomon Islands, Vanuatu and New Caledonia to the north-east; and New Zealand to the south-east.
      </div>;
  }
  public content2() {
    return <div>
      The United States of America (USA or U.S.A.), commonly called the United States (US or U.S.) and America, is a federal republic consisting of fifty states and a federal district. The 48 contiguous states and the federal district of Washington, D.C. are in central North America between Canada and Mexico. The state of Alaska is west of Canada and east of Russia across the Bering Strait, and the state of Hawaii is in the mid-North Pacific. The country also has five populated and nine unpopulated territories in the Pacific and the Caribbean.
      </div>;
  }
  public content3() {
    return <div>
      France, officially the French Republic is a sovereign state comprising territory in western Europe and several overseas regions and territories. The European part of France, called Metropolitan France, extends from the Mediterranean Sea to the English Channel and the North Sea, and from the Rhine to the Atlantic Ocean; France covers 640,679 square kilo metres and as of August 2015 has a population of 67 million, counting all the overseas departments and territories.
      </div>;
  }

  public render() {
    return (
        <div>
            <TabComponent ref={(tab) => { this.tabObj = tab }} id='draggableTab' heightAdjustMode='Auto' allowDragAndDrop={this.allowDragAndDrop} dragArea="#container" created={this.onTabCreate.bind(this)} dragged={this.tabDragStop.bind(this)}>
                <TabItemsDirective>
                    <TabItemDirective header={this.headerText[0]} content={this.content0} />
                    <TabItemDirective header={this.headerText[1]} content={this.content1} />
                    <TabItemDirective header={this.headerText[2]} content={this.content2} />
                    <TabItemDirective header={this.headerText[3]} content={this.content3} />
                </TabItemsDirective>
            </TabComponent>
            <br></br>
            <TreeViewComponent id="draggableTreeview" ref={(treeview) => { this.treeObj = treeview }} cssClass="treeview-external-drop-tab" fields={this.field} />
        </div>
    );
  }
}
ReactDOM.render(<ReactApp />, document.getElementById('element'));

```

{% endtab %}

## Drag and drop items from external source

It is possible to drag and drop the items from any of the external sources into the Tab, by manually saving those dropped items as new item data through the `addTab` method of Tab and removing the dragged node through the `removeNodes` method of Treeview.

In this example, we have used the tree view control as an external source, and the child nodes from the tree view component are dragged and dropped onto the Tab. Therefore, it is necessary to use the `nodeDragStop` event of the Treeview component, where we can form an event object and save it using the `addTab` method of the Tab and remove the dragged node through the `removeNodes` method of Treeview.

{% tab template="tab/drag-and-drop/treeview-to-tab", sourceFiles="app/**/*.tsx,index.css", compileJsx=true %}

```typescript
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { TabComponent, TabItemDirective, TabItemsDirective, TabItemModel, TreeViewComponent, DragAndDropEventArgs } from '@syncfusion/ej2-react-navigations';
import { isNullOrUndefined } from "@syncfusion/ej2-base";

export default class ReactApp extends React.Component<{}, {}> {

  public tabObj: TabComponent;
  public treeObj: TreeViewComponent;
  public headerText: any = [{ text: "India" }, { text: "Australia" }, { text: "USA" }, { text: "France" }];
  public allowDragAndDrop: boolean = true;
  public data: { [key: string]: Object }[] = [
    { text: 'Hennessey Venom', id: 'list-01' },
    { text: 'Bugatti Chiron', id: 'list-02' },
    { text: 'Bugatti Veyron Super Sport', id: 'list-03' },
    { text: 'SSC Ultimate Aero', id: 'list-04' },
    { text: 'Koenigsegg CCR', id: 'list-05' },
    { text: 'McLaren F1', id: 'list-06' },
    { text: 'Aston Martin One- 77', id: 'list-07' },
    { text: 'Jaguar XJ220', id: 'list-08' },
    { text: 'McLaren P1', id: 'list-09' },
    { text: 'Ferrari LaFerrari', id: 'list-10' },
  ];
  public field: Object = { dataSource: this.data, id: 'id', text: 'text' };

  public onNodeDragStop(args: DragAndDropEventArgs) {
    let dropElement: Element = args.target.closest('#draggableTab .e-toolbar-item');
    if (dropElement != null) {
      let tabElement: HTMLElement = document.querySelector('#draggableTab');
      let dropItemIndex: number = [].slice.call(tabElement.querySelectorAll('.e-toolbar-item')).indexOf(dropElement);
      let newTabItem: TabItemModel[] = [{
        header: { 'text': args.draggedNodeData.text.toString() },
        content: args.draggedNodeData.text.toString() + ' Content'
      }];
      this.tabObj.addTab(newTabItem, dropItemIndex);
      this.treeObj.removeNodes([args.draggedNode]);
      args.cancel = true;
    } else {
      let dropNode: Element = args.target.closest('#draggableTreeview .e-list-item ');
      if (!isNullOrUndefined(dropNode) && args.dropIndicator === 'e-drop-in') {
        args.cancel = true;
      }
    }
  }

  public onNodeDrag(args: DragAndDropEventArgs) {
    if (!isNullOrUndefined(args.target.closest('.tab-content'))) {
      args.dropIndicator = 'e-no-drop';
    } else if (!isNullOrUndefined(args.target.closest('#draggableTab .e-tab-header'))) {
      args.dropIndicator = 'e-drop-in';
    }
  }

  public content0() {
    return <div>
      India officially the Republic of India, is a country in South Asia. It is the seventh-largest country by area, the second-most populous country with over 1.2 billion people, and the most populous democracy in the world. Bounded by the Indian Ocean on the south, the Arabian Sea on the south-west, and the Bay of Bengal on the south-east, it shares land borders with Pakistan to the west;China, Nepal, and Bhutan to the north-east; and Burma and Bangladesh to the east. In the Indian Ocean, India is in the vicinity of Sri Lanka and the Maldives; in addition, India Andaman and Nicobar Islands share a maritime border with Thailand and Indonesia.
      </div>;
  }
  public content1() {
    return <div>
      Australia, officially the Commonwealth of Australia, is a country comprising the mainland of the Australian continent, the island of Tasmania and numerous smaller islands. It is the world sixth-largest country by total area. Neighboring countries include Indonesia, East Timor and Papua New Guinea to the north; the Solomon Islands, Vanuatu and New Caledonia to the north-east; and New Zealand to the south-east.
      </div>;
  }
  public content2() {
    return <div>
      The United States of America (USA or U.S.A.), commonly called the United States (US or U.S.) and America, is a federal republic consisting of fifty states and a federal district. The 48 contiguous states and the federal district of Washington, D.C. are in central North America between Canada and Mexico. The state of Alaska is west of Canada and east of Russia across the Bering Strait, and the state of Hawaii is in the mid-North Pacific. The country also has five populated and nine unpopulated territories in the Pacific and the Caribbean.
      </div>;
  }
  public content3() {
    return <div>
      France, officially the French Republic is a sovereign state comprising territory in western Europe and several overseas regions and territories. The European part of France, called Metropolitan France, extends from the Mediterranean Sea to the English Channel and the North Sea, and from the Rhine to the Atlantic Ocean; France covers 640,679 square kilo metres and as of August 2015 has a population of 67 million, counting all the overseas departments and territories.
      </div>;
  }

  public render() {
    return (
        <div>
            <TabComponent ref={(tab) => { this.tabObj = tab }} id='draggableTab' heightAdjustMode='Auto' dragArea="#container">
                <TabItemsDirective>
                    <TabItemDirective header={this.headerText[0]} content={this.content0} />
                    <TabItemDirective header={this.headerText[1]} content={this.content1} />
                    <TabItemDirective header={this.headerText[2]} content={this.content2} />
                    <TabItemDirective header={this.headerText[3]} content={this.content3} />
                </TabItemsDirective>
            </TabComponent>
            <br></br>
            <TreeViewComponent id="draggableTreeview" ref={(treeview) => { this.treeObj = treeview }} dragArea="#container" cssClass="treeview-external-drop-tab" fields={this.field} nodeDragStop={this.onNodeDragStop.bind(this)} nodeDragging={this.onNodeDrag.bind(this)} allowDragAndDrop={this.allowDragAndDrop} />
        </div>
    );
  }
}
ReactDOM.render(<ReactApp />, document.getElementById('element'));

```

{% endtab %}