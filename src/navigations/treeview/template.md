---
title: "Template"
component: "TreeView"
description: "Customize treeview nodes using template"
---

# Template

The TreeView component allows you to customize the look of TreeView nodes by using the [nodeTemplate](../api/treeview#nodetemplate)
property. This property accepts either `template string` or HTML element ID.

In the following sample, employee information such as employee photo, name, and designation have been included using the `nodeTemplate` property.

The template expression should be provided inside the `${...}` interpolation syntax.

{% tab template="tree-view/template", sourceFiles="app/**/*.tsx,style.css", compileJsx=true %}

```typescript

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {enableRipple} from '@syncfusion/ej2-base';
enableRipple(true);
import {TreeViewComponent} from '@syncfusion/ej2-react-navigations';

export default class App extends React.Component<{}, {}> {

public employees: { [key: string]: Object }[] = [
   { id: 1, name: 'Steven Buchanan', eimg: '10', job: 'CEO', hasChild: true, expanded: true },
        { id: 2, pid: 1, name: 'Laura Callahan', eimg: '2', job: 'Product Manager', hasChild: true },
        { id: 3, pid: 2, name: 'Andrew Fuller', eimg: '7', job: 'Team Lead', hasChild: true },
        { id: 4, pid: 3, name: 'Anne Dodsworth', eimg: '1', job: 'Developer' },
        { id: 5, pid: 1, name: 'Nancy Davolio', eimg: '4', job: 'Product Manager', hasChild: true },
        { id: 6, pid: 5, name: 'Michael Suyama', eimg: '9', job: 'Team Lead', hasChild: true },
        { id: 7, pid: 6, name: 'Robert King', eimg: '8', job: 'Developer ' },
        { id: 8, pid: 7, name: 'Margaret Peacock', eimg: '6', job: 'Developer' },
        { id: 9, pid: 1, name: 'Janet Leverling', eimg: '3', job: 'HR' },
];
private fields: Object = { dataSource: this.employees,  id: 'id', parentID: 'pid', text: 'name', hasChildren: 'hasChild' };
private cssClass:string = "custom";
private nodeTemplate(data:any): JSX.Element {
    return (
      <div>
        <img className='eimage' src={`./../template-cs1/${data.eimg}.png`} alt='${data.eimg}'/>
        <div className='ename'>{data.name}</div>
        <div className='ejob'>{data.job}</div>
      </div>
        )
    }
  render() {
    return (
        // specifies the tag for render the TreeView component
        <TreeViewComponent fields={this.fields} cssClass={this.cssClass} nodeTemplate={this.nodeTemplate}/>
    );
  }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

## See Also

* [How to customize the expand and collapse icons](./how-to/customize-the-expand-and-collapse-icons)
* [How to customize the tree nodes based on levels](./how-to/customize-the-tree-nodes-based-on-levels)