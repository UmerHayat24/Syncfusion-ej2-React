# Select one child at a time out of one specific parent

TreeView allows both single and multiple selections. If your application needs to select one child at a time under one specific parent, refer to the following example. Here, you can achieve this in the `nodeSelecting` event of TreeView. However, you can reset the selected child and make another selection by pressing Ctrl + selected nodes.

{% tab template="tree-view/select-one-child", sourceFiles="app/**/*.tsx,style.css"  %}

```typescript

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import {TreeViewComponent, NodeSelectEventArgs } from '@syncfusion/ej2-react-navigations';

export default class App extends React.Component<{}, {}> {
  
  // Self-referential list data source for TreeView component
  private localData: { [key: string]: Object }[]= [
    { id: 1, name: 'Parent 1', hasChild: true, expanded: true },
    { id: 2, pid: 1, name: 'Child 1' },
    { id: 3, pid: 1, name: 'Child 2' },
    { id: 4, pid: 1, name: 'Child 3' },
    { id: 7, name: 'Parent 2', hasChild: true, expanded: true },
    { id: 8, pid: 7, name: 'Child 1' },
    { id: 9, pid: 7, name: 'Child 2' },
    { id: 10, pid: 7, name: 'Child 3' },
  ];
  private field: Object = { dataSource: this.localData, id: 'id', parentID: 'pid', text: 'name', hasChildren: 'hasChild' };
  private allowMultiSelection: boolean = true;
  private loadOnDemand: boolean = false;
  private parent: any; private child: any;
  private count: boolean = false;
  private childCount: boolean = false;
  public treeObj: TreeViewComponent;
  // Triggers when you select any node
  onNodeSelecting(args: NodeSelectEventArgs): void {
    let id: any = args.nodeData.parentID;
    if (!this.count) {
       this.parent = id;
       this.count = true;
    }
    if (!this.childCount){
       this.child = args.nodeData.id;
       this.childCount = true
    }
    if (id != null && id === this.parent) {
      let element: HTMLElement = this.treeObj.element.querySelector('[data-uid="' + id + '"]');
      let liElements: any = element.querySelectorAll('ul li');
      for (let i: number = 0; i < liElements.length; i++) {
        let nodeData: any = this.treeObj.getNode(liElements[i]);
        if (nodeData.selected && args.action === "select" && this.child !== args.nodeData.id) {
          args.cancel = true;
        }
        // For unselect the selectedNodes
        else  if (args.action === "un-select" && this.child === args.nodeData.id) {
          this.childCount = false;
          this.child = null;
          this.parent = null;
          this.count = false;
        }
      }
    } else if (id !== this.parent && id !== null) {
        if(args.action == "select"){
          args.cancel = true
        }
    } else if (id === null){
       this.childCount = false;
          this.child = null;
          this.parent = null;
          this.count = false
    }
  }
  render() {
    return (
      <div className = 'control-pane'>
          <div className='control-section'>
            <div className='control_wrapper'>
              {/* Render TreeView */}
              <TreeViewComponent fields={this.field} loadOnDemand={this.loadOnDemand} nodeSelecting={this.onNodeSelecting.bind(this)} allowMultiSelection={this.allowMultiSelection}  ref={(treeview) => { this.treeObj = treeview as TreeViewComponent; }}/>
            </div>
          </div>
        </div>
      )
  }
}

ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}