# Customize the TreeView into accordion

Accordion is an interface where a list of items can be collapsed or expanded, but only one list can be collapsed or expanded at a time. You can customize the TreeView to make it behave as an accordion. Refer to the following code sample to create an accordion tree.

{% tab template="tree-view/accordion-tree", sourceFiles="app/**/*.tsx,style.css" %}

```typescript

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import {TreeViewComponent, NodeSelectEventArgs } from '@syncfusion/ej2-react-navigations';

export default class App extends React.Component<{}, {}> {

   // Data source for TreeView component
    private continents: { [key: string]: Object }[] = [
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
            { code: "IND", name: "India", selected: true },
            { code: "JPN", name: "Japan" }
        ]
    },
    {
        code: "EU", name: "Europe", countries: [
            { code: "DNK", name: "Denmark" },
            { code: "FIN", name: "Finland" },
            { code: "AUT", name: "Austria",
             }
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
        code: "OC", name: "Oceania", countries: [
            { code: "AUS", name: "Australia" },
            { code: "NZL", name: "New Zealand" },
            { code: "WSM", name: "Samoa" }
        ]
    }
    ];
    private field:Object ={ dataSource: this.continents,  id: "code", text: "name", child: "countries" };
    private style: string = 'accordiontree';
    public treeObj: TreeViewComponent;

    nodeSelect(args: NodeSelectEventArgs): void {
      if (args.node.classList.contains('e-level-1')) {
        this.treeObj.collapseAll();
        this.treeObj.expandAll([args.node]);
        this.treeObj.expandOn = 'None'
      }
    }

    render() {
        return (
            <div className = 'control-pane'>
                <div className='control-section'>
                    <div className='control_wrapper'>
                        {/* Render TreeView */}
                        <TreeViewComponent fields={this.field} cssClass={this.style} ref={(treeview) => { this.treeObj = treeview as TreeViewComponent; }} nodeSelected={this.nodeSelect.bind(this)}/>
                    </div>
                </div>
            </div>
        )
    }
}

ReactDOM.render(<App />, document.getElementById('sample'));


```

{% endtab %}