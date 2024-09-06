---
title: "CheckBox"
component: "TreeView"
description: "Checkbox functionality in treeview"
---

# CheckBox

The TreeView component allows you to check more than one node in TreeView without affecting the UI's appearance by
enabling the [showCheckBox](../api/treeview#showcheckbox) property. When this property is enabled, checkbox
appears before each TreeView node text.

* If one of the child nodes is not in a checked state, then the parent node will be in an intermediate state.

* If all the child nodes are in checked state, then the parent node's state will also be checked.

* If a parent node is checked, then all the child nodes' state will also be checked.

By default, the checkbox state of parent and child nodes are dependent on each other. If you need independent checked state, you can achieve it using the [`autoCheck`](../api/treeview#autocheck) property.

Using the [`checkedNodes`](../api/treeview#checkednodes) property, you can set the nodes that need to be checked or get the ID of nodes that are currently checked in the TreeView component.

If you need to prevent the node check action for a particular node, the [`nodeChecking`](../api/treeview#nodechecking) event can be used which is triggered before the TreeView node is checked/unchecked. The [`nodeChecked`](../api/treeview#nodechecked) event will be triggered when the TreeView node is checked/unchecked successfully.

In the following example, the `showCheckBox` property is enabled.

{% tab template="tree-view/basic", sourceFiles="app/**/*.tsx,index.html", compileJsx=true %}

```typescript

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {enableRipple} from '@syncfusion/ej2-base';
enableRipple(true);

import {TreeViewComponent} from '@syncfusion/ej2-react-navigations';

export default class App extends React.Component<{}, {}> {

    // define the JSON of data
    private countries: { [key: string]: Object }[] = [
            { id: 1, name: 'Australia', hasChild: true, expanded: true },
            { id: 2, pid: 1, name: 'New South Wales' },
            { id: 3, pid: 1, name: 'Victoria' },
            { id: 4, pid: 1, name: 'South Australia' },
            { id: 6, pid: 1, name: 'Western Australia' },
            { id: 7, name: 'Brazil', hasChild: true },
            { id: 8, pid: 7, name: 'Paraná' },
            { id: 9, pid: 7, name: 'Ceará' },
            { id: 10, pid: 7, name: 'Acre' },
            { id: 11, name: 'China', hasChild: true },
            { id: 12, pid: 11, name: 'Guangzhou' },
            { id: 13, pid: 11, name: 'Shanghai' },
            { id: 14, pid: 11, name: 'Beijing' },
            { id: 15, pid: 11, name: 'Shantou' },
            { id: 16, name: 'France', hasChild: true },
            { id: 17, pid: 16, name: 'Pays de la Loire' },
            { id: 18, pid: 16, name: 'Aquitaine' },
            { id: 19, pid: 16, name: 'Brittany' },
            { id: 20, pid: 16, name: 'Lorraine' },
            { id: 21, name: 'India', hasChild: true },
            { id: 22, pid: 21, name: 'Assam' },
            { id: 23, pid: 21, name: 'Bihar' },
            { id: 24, pid: 21, name: 'Tamil Nadu' },
            { id: 25, pid: 21, name: 'Punjab' }
    ];
   public field: Object = { dataSource: this.countries, id: 'id', parentID: 'pid', text: 'name', hasChildren: 'hasChild' };
   public isChecked: boolean = true;
   render() {
        return (
            // specifies the tag for render the TreeView component
           <TreeViewComponent fields={this.field} showCheckBox={this.isChecked} />
        );
    }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

## Checked nodes

You can get or set the checked nodes in TreeView at initial rendering and dynamically by using the [checkedNodes](../api/treeview#checkednodes)
property. It returns the checked nodes' ID as an array.

In the following example, the **New South Wales** and **Western Australia** nodes are checked at initial rendering.
If any more nodes are checked, the checked nodes' IDs will be displayed in alert.

{% tab template="tree-view/basic", sourceFiles="app/**/*.tsx,index.html", compileJsx=true %}

```typescript

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {enableRipple} from '@syncfusion/ej2-base';
enableRipple(true);

import { TreeViewComponent, NodeCheckEventArgs} from '@syncfusion/ej2-react-navigations';

export default class App extends React.Component<{}, {}> {

    // define the JSON of data
    private countries: { [key: string]: Object }[] = [
            { id: 1, name: 'Australia', hasChild: true, expanded: true },
            { id: 2, pid: 1, name: 'New South Wales', isChecked: true },
            { id: 3, pid: 1, name: 'Victoria' },
            { id: 4, pid: 1, name: 'South Australia' },
            { id: 6, pid: 1, name: 'Western Australia', isChecked: true },
            { id: 7, name: 'Brazil', hasChild: true },
            { id: 8, pid: 7, name: 'Paraná' },
            { id: 9, pid: 7, name: 'Ceará' },
            { id: 10, pid: 7, name: 'Acre' },
            { id: 11, name: 'China', hasChild: true },
            { id: 12, pid: 11, name: 'Guangzhou' },
            { id: 13, pid: 11, name: 'Shanghai' },
            { id: 14, pid: 11, name: 'Beijing' },
            { id: 15, pid: 11, name: 'Shantou' },
            { id: 16, name: 'France', hasChild: true },
            { id: 17, pid: 16, name: 'Pays de la Loire' },
            { id: 18, pid: 16, name: 'Aquitaine' },
            { id: 19, pid: 16, name: 'Brittany' },
            { id: 20, pid: 16, name: 'Lorraine' },
            { id: 21, name: 'India', hasChild: true },
            { id: 22, pid: 21, name: 'Assam' },
            { id: 23, pid: 21, name: 'Bihar' },
            { id: 24, pid: 21, name: 'Tamil Nadu' },
            { id: 25, pid: 21, name: 'Punjab' }
    ];
   public field: Object = { dataSource: this.countries, id: 'id', parentID: 'pid', text: 'name', hasChildren: 'hasChild' };
   public isChecked: boolean = true;
   nodeChecked(args: NodeCheckEventArgs) {
        alert("The checked node's id: " + this.checkedNodes); // To alert the checked node's id.
    }
   render() {
        return (
            // specifies the tag for render the TreeView component
           <TreeViewComponent fields={this.field} showCheckBox={this.isChecked} nodeChecked={ this.nodeChecked } />
        );
    }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

## See Also

* [How to check/uncheck the checkbox on clicking the tree node text](./how-to/check-uncheck-the-checkbox-on-clicking-the-tree-node-text)

* [How to disable the checkboxes alone in the tree nodes](./how-to/disable-checkbox-of-the-tree-node/)

* [How to remove the checkbox of the parent node in treeview](./how-to/remove-parent-checkbox/)