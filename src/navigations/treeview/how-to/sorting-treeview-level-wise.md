# Sort the tree nodes based on levels

You can sort the TreeView nodes based on their level. When using the `sortOrder` property, the whole TreeView is sorted. When you sort a particular level, you can use the following code sample. The following code sample demonstrates how to sort the parent node alone in TreeView.

{% tab template="tree-view/sort-tree", sourceFiles="app/**/*.tsx,style.css"  %}

```typescript

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import {TreeViewComponent, NodeExpandEventArgs } from '@syncfusion/ej2-react-navigations';
import {enableRipple} from '@syncfusion/ej2-base';
import { DataManager, Query } from '@syncfusion/ej2-data';
enableRipple(true);

export default class App extends React.Component<{}, {}> {

   // Data source for TreeView component
   private Countries: { [key: string]: Object }[]= [
    { id: 1, name: 'India', hasChild: true },
    { id: 2, pid: 1, name: 'Assam' },
    { id: 3, pid: 1, name: 'Bihar' },
    { id: 4, pid: 1, name: 'Tamil Nadu' },
    { id: 6, pid: 1, name: 'Punjab' },
    { id: 7, name: 'Brazil', hasChild: true },
    { id: 8, pid: 7, name: 'Paraná' },
    { id: 9, pid: 7, name: 'Ceará' },
    { id: 10, pid: 7, name: 'Acre' },
    { id: 11, name: 'France', hasChild: true },
    { id: 12, pid: 11, name: 'Pays de la Loire' },
    { id: 13, pid: 11, name: 'Aquitaine' },
    { id: 14, pid: 11, name: 'Brittany' },
    { id: 15, pid: 11, name: 'Lorraine' },
    { id: 16, name: 'Australia', hasChild: true },
    { id: 17, pid: 16, name: 'New South Wales' },
    { id: 18, pid: 16, name: 'Victoria' },
    { id: 19, pid: 16, name: 'South Australia' },
    { id: 20, pid: 16, name: 'Western Australia' },
    { id: 21, name: 'China', hasChild: true },
    { id: 22, pid: 21, name: 'Guangzhou' },
    { id: 23, pid: 21, name: 'Shanghai' },
    { id: 24, pid: 21, name: 'Beijing' },
    { id: 25, pid: 21, name: 'Shantou' }
   ]

    private field:Object ={  dataSource: this.Countries, id: 'id', text: 'name', parentID: 'pid', hasChildren: 'hasChild' };
    public newData: any;
    public treeObj: TreeViewComponent;

    onNodeExpand(args: NodeExpandEventArgs): void {
        if (args.isInteracted && args.node.querySelector('li') === null){
            let id: any = parseInt(args.node.getAttribute("data-uid"));
            let childData: any =  new DataManager(this.newData).executeLocal(new Query().where(this.treeObj.fields.parentID, 'equal', id, false));
            this.treeObj.addNodes(childData, args.node,null)
        }
    }

    onCreate(){
        this.newData = this.treeObj.fields.dataSource;
        // Selects the first level nodes alone
        let resultData = new DataManager(this.treeObj.getTreeData()).executeLocal(new Query().where(this.treeObj.fields.parentID, 'equal', undefined, false));
        let name = [];
        for (let i = 0; i < resultData.length; i++){
            name.push(resultData[i][this.treeObj.fields.text]);
        }
        name.sort();
        let arr = [];
        for (let j = 0; j < name.length; j++) {
            let sortedData = new DataManager(this.treeObj.getTreeData()).executeLocal(new Query().where(this.treeObj.fields.text, 'equal', name[j], false));
            let childData =  new DataManager(this.newData).executeLocal(new Query().where(this.treeObj.fields.parentID, 'equal', parseInt(sortedData[0][this.treeObj.fields.id]), false));
            arr.push(sortedData[0]);
        }
        // Renders treeview with sorted Nodes
        this.changeDataSource(arr);
        this.treeObj.dataBind();
    }

     changeDataSource(data: any){
        this.treeObj.fields = {
            dataSource: data, id: 'id', text: 'name', parentID: 'pid', hasChildren: 'hasChild'
        }
    }
    render() {
    return (
      <div className = 'control-pane'>
        <div className='control-section'>
        <div className='control_wrapper'>
            {/* Render TreeView */}
            <TreeViewComponent fields={this.field} ref={(treeview) => { this.treeObj = treeview as TreeViewComponent; }} created={this.onCreate.bind(this)} nodeExpanding={this.onNodeExpand.bind(this)} />
        </div>
        </div>
      </div>
    )
  }
}

ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}