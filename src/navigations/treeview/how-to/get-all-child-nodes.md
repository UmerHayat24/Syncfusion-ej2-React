# Get all child nodes through parentID

This section demonstrates how to get the child nodes from corresponding parent ID. Using the `getNode` method, you can get the node details of TreeView. Please refer to the following sample.

{% tab template="tree-view/get-child-nodes", sourceFiles="app/**/*.tsx" %  %}

```typescript

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import {TreeViewComponent, NodeSelectEventArgs } from '@syncfusion/ej2-react-navigations';
import {enableRipple} from '@syncfusion/ej2-base';
enableRipple(true);

export default class App extends React.Component<{}, {}> {

   // Data source for TreeView component
  private data: { [key: string]: Object }[]= [
        {
            code: "AF", name: "Africa", countries: [
                { code: "NGA", name: "Nigeria" },
                { code: "EGY", name: "Egypt" },
                { code: "ZAF", name: "South Africa" }
            ]
        },
        {
            code: "AS", name: "Asia", countries: [
                { code: "CHN", name: "China" },
                { code: "IND", name: "India" , countries: [
                    { code: "TN", name: "TamilNadu" }
                ]},
                { code: "JPN", name: "Japan" }
            ]
        },
        {
            code: "EU", name: "Europe", countries: [
                { code: "DNK", name: "Denmark" },
                { code: "FIN", name: "Finland" },
                { code: "AUT", name: "Austria" }
            ]
        },
        {
            code: "NA", name: "North America", countries: [
                { code: "USA", name: "United States of America" },
                { code: "CUB", name: "Cuba" },
                { code: "MEX", name: "Mexico" }
            ]
        },
        {
            code: "SA", name: "South America", countries: [
                { code: "BR", name: "Brazil" },
                { code: "COL", name: "Colombia" },
                { code: "ARG", name: "Argentina" }
            ]
        },
    ];

    private field:Object ={  dataSource: this.data, id: 'code', text: 'name', child: 'countries' };
    private loadOnDemand: Boolean= false;
    public treeObj: TreeViewComponent;

     onCreate(): void {
        let proxy = this.treeObj;
        document.getElementById("btn").addEventListener("click",(event)=>{
            let id: any =document.getElementById('Nodes') as HTMLInputElement
            let element= proxy.element.querySelector('[data-uid="' + id.value + '"]');
            // Gets the child Element
            let liElements : any= element.querySelectorAll('ul li');
            let arr : any= [];
            for (let i = 0; i < liElements.length; i++) {
                let nodeData= proxy.getNode(liElements[i]);
                arr.push(nodeData);
            }
            alert(JSON.stringify(arr));
        });
    }
    render() {
        return (
            <div className = 'control-pane'>
                <div className='control-section'>
                    <div className='control_wrapper'>
                        {/* Render TreeView */}
                        <TreeViewComponent fields={this.field}  ref={(treeview) => { this.treeObj = treeview as TreeViewComponent; }} loadOnDemand={this.loadOnDemand} created={this.onCreate.bind(this)}/>
                    </div>
                </div>
            </div>
        )
    }
}

ReactDOM.render(<App />, document.getElementById('sample'));


```

{% endtab %}