# Filter nodes in TreeView

You can filter the tree nodes based on their text using the  `DataManager` plugin and the `fields` property of the TreeView.

The following code example demonstrates how to filter the tree nodes in a TreeView.

{% tab template="tree-view/filtering", sourceFiles="app/**/*.tsx"  %}

```typescript

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { DataManager, Query, ReturnOption, Predicate } from '@syncfusion/ej2-data';
import { MaskedTextBoxComponent, ChangeEventArgs} from "@syncfusion/ej2-react-inputs";
import {TreeViewComponent} from '@syncfusion/ej2-react-navigations';

export default class App extends React.Component<{}, {}> {

    // list data source for TreeView component
    private localData: { [key: string]: Object }[] = [
        { id: 1, name: "Australia", hasChild: true },
        { id: 2, pid: 1, name: "New South Wales" },
        { id: 3, pid: 1, name: "Victoria" },
        { id: 4, pid: 1, name: "South Australia" },
        { id: 6, pid: 1, name: "Western Australia" },
        { id: 7, name: "Brazil", hasChild: true },
        { id: 8, pid: 7, name: "Paraná" },
        { id: 9, pid: 7, name: "Ceará" },
        { id: 10, pid: 7, name: "Acre" },
        { id: 11, name: "China", hasChild: true },
        { id: 12, pid: 11, name: "Guangzhou" },
        { id: 13, pid: 11, name: "Shanghai" },
        { id: 14, pid: 11, name: "Beijing" },
        { id: 15, pid: 11, name: "Shantou" },
        { id: 16, name: "France", hasChild: true },
        { id: 17, pid: 16, name: "Pays de la Loire" },
        { id: 18, pid: 16, name: "Aquitaine" },
        { id: 19, pid: 16, name: "Brittany" },
        { id: 20, pid: 16, name: "Lorraine" },
        { id: 21, name: "India", hasChild: true },
        { id: 22, pid: 21, name: "Assam" },
        { id: 23, pid: 21, name: "Bihar" },
        { id: 24, pid: 21, name: "Tamil Nadu" },
        { id: 25, pid: 21, name: "Punjab" }
    ];

    // Mapping TreeView fields property with data source properties
    private field:Object = { dataSource: this.localData, id: 'id', parentID: 'pid', text: 'name', hasChildren: 'hasChild', expanded: "expanded" }
    public treeObj: TreeViewComponent;
    public maskObj: MaskedTextBoxComponent;

   //Change the dataSource for TreeView
     changeDataSource(data: any) {
        this.treeObj.fields = {
            dataSource: data, id: 'id', text: 'name',parentID: 'pid', hasChildren: 'hasChild'
        }
    }

    //Filtering the TreeNodes
     searchNodes(args: ChangeEventArgs) {
        let _text = this.maskObj.element.value;
        let predicats = [], _array = [], _filter = [];
        if (_text == "") {
            this.changeDataSource(this.localData);
        }
        else {
            let predicate = new Predicate('name', 'startswith', _text, true);
            let filteredList : any = new DataManager(this.localData).executeLocal(new Query().where(predicate));
            console.log(filteredList)
            for (let j = 0; j < filteredList.length; j++) {
                _filter.push(filteredList[j]["id"]);
                let filters = this.getFilterItems(filteredList[j], this.localData);
                for (let i = 0; i < filters.length; i++) {
                    if (_array.indexOf(filters[i]) == -1 && filters[i] != null) {
                        _array.push(filters[i]);
                        predicats.push(new Predicate('id', 'equal', filters[i], false));
                    }
                }
            }
            if (predicats.length == 0) {
                this.changeDataSource([]);
            } else {
                let query = new Query().where(Predicate.or(predicats));
                let newList : any =new DataManager(this.localData).executeLocal(query);
                this.changeDataSource(newList);
                let proxy: any = this.treeObj as TreeViewComponent;
                setTimeout(function (this: any) {
                    proxy.expandAll();
                }, 100);
            }
        }
    }

    //Find the Parent Nodes for corresponding childs
    public getFilterItems(fList: any, list: any): any {
        let nodes = [];
        nodes.push(fList["id"]);
        let query2 = new Query().where('id', 'equal', fList["pid"], false);
        let fList1 = new  DataManager(list).executeLocal(query2);
        if (fList1.length != 0) {
            let pNode:any= this.getFilterItems(fList1[0], list);
            for (let i = 0; i < pNode.length; i++) {
                if (nodes.indexOf(pNode[i]) == -1 && pNode[i] != null)
                    nodes.push(pNode[i]);
                }
                return nodes;
        }
            return nodes;
    }

    render() {
        return (
            <div className = 'control-pane'>
                <div className='control-section'>
                    <div className='control_wrapper'>
                        <MaskedTextBoxComponent ref={(mask) => { this.maskObj = mask as MaskedTextBoxComponent; }} change={this.searchNodes.bind(this)} />
                        {/* Render TreeView */}
                        <TreeViewComponent fields={this.field}  ref={(treeview) => { this.treeObj = treeview as TreeViewComponent; }}/>
                    </div>
                </div>
            </div>
        )
    }
}

ReactDOM.render(<App />, document.getElementById('sample'));


```

{% endtab %}