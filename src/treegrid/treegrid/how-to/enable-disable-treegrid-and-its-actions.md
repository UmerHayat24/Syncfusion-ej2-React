---
title: "Enable/Disable TreeGrid and its actions"
component: "TreeGrid"
description: "Learn how to Enable/Disable TreeGrid and its actions."
---

# Enable/Disable TreeGrid and its actions

You can enable/disable the TreeGrid and its actions by applying/removing corresponding CSS styles.

To enable/disable the treegrid and its actions, follow the given steps:

**Step 1**:

Create CSS class with custom style to override the default style of TreeGrid.

```css
    .disabletreegrid {
        pointer-events: none;
        opacity: 0.4;
    }
    .wrapper {
        cursor: not-allowed;
    }
```

**Step 2**:

Add/Remove the CSS class to the TreeGrid in the click event handler of Button.

```typescript

public btnClick(): void {
    if (this.treegridObj && this.treegridObj.element.classList.contains('disabletreegrid')) {
      this.treegridObj.element.classList.remove('disabletreegrid');
      (document.getElementById("TreeGridParent") as HTMLElement).classList.remove('wrapper');
    }
    else if (this.treegridObj) {
      this.treegridObj.element.classList.add('disabletreegrid');
      (document.getElementById("TreeGridParent") as HTMLElement).classList.add('wrapper');
    }
  }

```

In the below demo, the button click will enable/disable the TreeGrid and its actions.

{% tab template="treegrid/enable-disable-actions", sourceFiles="app/App.tsx,app/datasource.tsx,app/custom.css", compileJsx=true %}

```typescript

import * as React from 'react';
import { projectData } from './datasource';
import { ColumnsDirective, ColumnDirective, TreeGridComponent, EditSettingsModel } from '@syncfusion/ej2-react-treegrid';
import { Inject, Page, Edit, Toolbar, ToolbarItems } from '@syncfusion/ej2-react-treegrid';
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';

/* tslint:disable */

export default class App extends React.Component {
  public editOptions: EditSettingsModel = { allowAdding:true, allowEditing: true, allowDeleting:true };
  public toolbarOptions: ToolbarItems[] = ['Add', 'Delete', 'Update', 'Cancel'];
  public treegridObj: TreeGridComponent | null;
  public btnClick(): void {
      alert('dwgfgfg');
  }
  public render() {
    this.btnClick = this.btnClick.bind(this);
    return (<div>
      <ButtonComponent cssClass='e-flat e-primary' iconCss='e-icons e-play-icon'
        isToggle onClick={ this.btnClick }>Enable/Disable TreeGrid</ButtonComponent>
      <div id="TreeGridParent">
      <TreeGridComponent dataSource={projectData} treeColumnIndex={1} idMapping= 'TaskID' parentIdMapping='parentID' height={210} toolbar={this.toolbarOptions}
      ref={g=> this.treegridObj = g} editSettings={this.editOptions}>
        <ColumnsDirective>
          <ColumnDirective field='TaskID' headerText='Task ID' width='70' textAlign='Right'></ColumnDirective>
          <ColumnDirective field='TaskName' headerText='Task Name' width='100'></ColumnDirective>
          <ColumnDirective field='StartDate' headerText='Start Date' width='90' format='yMd' textAlign='Right' />
          <ColumnDirective field='Duration' headerText='Duration' width='90' textAlign='Right' />
        </ColumnsDirective>
        <Inject services={[Page, Edit, Toolbar]} />
      </TreeGridComponent>
      </div>
    </div>  
    );
  }
};

```

{% endtab %}
