---
title: "Enable/Disable Grid and its actions"
component: "Grid"
description: "Learn how to Enable/Disable Grid and its actions."
---

# Enable/Disable Grid and its actions

You can enable/disable the Grid and its actions by applying/removing corresponding CSS styles.

To enable/disable the grid and its actions, follow the given steps:

**Step 1**:

Create CSS class with custom style to override the default style of Grid.

```css
    .disablegrid {
        pointer-events: none;
        opacity: 0.4;
    }
    .wrapper {
        cursor: not-allowed;
    }

```

**Step 2**:

Add/Remove the CSS class to the Grid in the click event handler of Button.

```typescript

  public btnClick(): void {
    if (this.grid && this.grid.element.classList.contains('disablegrid')) {
      this.grid.element.classList.remove('disablegrid');
      (document.getElementById("GridParent") as HTMLElement).classList.remove('wrapper');
    }
    else if (this.grid) {
      this.grid.element.classList.add('disablegrid');
      (document.getElementById("GridParent") as HTMLElement).classList.add('wrapper');
    }
  }

```

In the below demo, the button click will enable/disable the Grid and its actions.

{% tab template="grid/enable-disable-actions", sourceFiles="app/App.tsx,app/css/custom.css,app/datasource.tsx" %}

```typescript
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { ColumnDirective, ColumnsDirective, EditSettingsModel, GridComponent } from '@syncfusion/ej2-react-grids';
import { Edit, Grid, Inject, Toolbar, ToolbarItems } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import './custom.css';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {
  public editOptions: EditSettingsModel = { allowAdding:true, allowEditing: true, allowDeleting:true };
  public toolbarOptions: ToolbarItems[] = ['Add', 'Edit', 'Delete', 'Update', 'Cancel'];
  private grid: Grid | null;

  public btnClick(): void {
    if (this.grid && this.grid.element.classList.contains('disablegrid')) {
      this.grid.element.classList.remove('disablegrid');
      (document.getElementById("GridParent") as HTMLElement).classList.remove('wrapper');
    }
    else if (this.grid) {
      this.grid.element.classList.add('disablegrid');
      (document.getElementById("GridParent") as HTMLElement).classList.add('wrapper');
    }
  }

  public render() {
    this.btnClick = this.btnClick.bind(this);
    return (
      <div>
        <ButtonComponent cssClass='e-flat e-primary' iconCss='e-icons e-play-icon'
        isToggle ={true} onClick={ this.btnClick }>Enable/Disable Grid</ButtonComponent>
        <div id="GridParent">
          <GridComponent dataSource={data} editSettings={this.editOptions} toolbar={this.toolbarOptions}
            height={265} ref={(scope) => { this.grid = scope; }}>
            <ColumnsDirective>
              <ColumnDirective field='OrderID' headerText='Order ID' width='100' textAlign="Right" isPrimaryKey={true}/>
              <ColumnDirective field='CustomerID' headerText='Customer ID' width='120'/>
              <ColumnDirective field='ShipCountry' headerText='Ship Country' width='150'/>
            </ColumnsDirective>
            <Inject services={[Edit, Toolbar]} />
          </GridComponent>
        </div>
      </div>)
  }
};
```

{% endtab %}