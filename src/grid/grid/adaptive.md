---
title: "Adaptive"
component: "Grid"
description: "Learn how to render the row elements, filter, sort, and edit dialogs adaptively in the Essential JS 2 DataGrid control."
---

# Adaptive View

The Grid user interface (UI) was redesigned to provide an optimal viewing experience and improve usability on small screens. This interface will render the filter, sort, and edit dialogs adaptively and have an option to render the grid row elements in the vertical direction.

## Render adaptive dialogs

When we enable the [`enableAdaptiveUI`](../api/grid/#enableadaptiveui) property, the grid will render the filter, sort, and edit dialogs in full screen for a better user experience. This behavior is demonstrated in the below demo.

{% tab template="grid/adaptive", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent, Inject } from '@syncfusion/ej2-react-grids';
import { Filter, Sort, Edit, Toolbar, Page } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public editSettings: any = { allowEditing: true, allowAdding: true, allowDeleting: true, mode: 'Dialog' };
  public toolbarOptions: any = ['Add', 'Edit', 'Delete', 'Update', 'Cancel', 'Search'];
  public validationRule: Object = { required: true };
  public orderidRules: Object = { required: true, number: true };
  public filterOptions: any = { type: 'Excel' };
  public grid: GridComponent;
  public load(): void {
    (this as any).adaptiveDlgTarget = document.getElementsByClassName('e-mobile-content')[0] as HTMLElement;
  }
  public menuFilter = { type: 'Menu' };
  public checkboxFilter = { type: 'CheckBox' };
  public render(){
      return (<div className="e-adaptive-demo e-bigger">
              <div className="e-mobile-layout">
                <div className="e-mobile-content">
                    <GridComponent id="adaptivebrowser" dataSource={data} height='100%' ref={grid => this.grid = grid} enableAdaptiveUI={true} allowFiltering={true} allowSorting={true} allowPaging={true} filterSettings={this.filterOptions} toolbar={this.toolbarOptions} editSettings={this.editSettings} load={this.load}>
                      <ColumnsDirective>
                        <ColumnDirective field='SNO' headerText='S NO' width='150' isPrimaryKey={true} validationRules={this.orderidRules}></ColumnDirective>
                        <ColumnDirective field='Model' headerText='Model Name' width='200' editType='dropdownedit' validationRules={this.validationRule} />
                        <ColumnDirective field='Developer' headerText='Developer' width='200' filter={this.menuFilter} validationRules={this.validationRule}></ColumnDirective>
                        <ColumnDirective field='ReleaseDate' headerText='Released Date' editType='datepickeredit' type='date' format='yMMM' width='200'></ColumnDirective>
                        <ColumnDirective field='AndroidVersion' headerText='Android Version' width='200' filter={this.checkboxFilter} validationRules={this.validationRule}></ColumnDirective>
                      </ColumnsDirective>
                      <Inject services={[Filter, Sort, Edit, Toolbar, Page]} />
                    </GridComponent>
                </div>
              </div>
              <br></br>
                <div className="datalink">Source:
                  <a href="https://en.wikipedia.org/wiki/List_of_Android_smartphones"
                    target="_blank">Wikipedia: List of Android smartphones</a>
                </div>
              </div>
            )
      }
}
```

{% endtab %}

## Vertical row rendering

The grid will render the row elements in vertical order while setting the [`rowRenderingMode`](../api/grid/rowRenderingMode/) property value as **Vertical**.

{% tab template="grid/adaptive", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent, Inject } from '@syncfusion/ej2-react-grids';
import { AggregateColumnsDirective, AggregateColumnDirective, AggregateDirective, AggregatesDirective } from '@syncfusion/ej2-react-grids';
import { Filter, Sort, Edit, Toolbar, Aggregate, Page } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { data } from './datasource';

export default class App extends React.Component<{}, {}>{
  public editSettings: any = { allowEditing: true, allowAdding: true, allowDeleting: true, mode: 'Dialog' };
  public toolbarOptions: any = ['Add', 'Edit', 'Delete', 'Update', 'Cancel', 'Search'];
  public validationRule: Object = { required: true };
  public orderidRules: Object = { required: true, number: true };
  public filterOptions: any = { type: 'Excel' };
  public renderingMode: any = 'Vertical';
  public grid: GridComponent;
  public load(): void {
    (this as any).adaptiveDlgTarget = document.getElementsByClassName('e-mobile-content')[0] as HTMLElement;
  }
  public footerSum(props): any {
    return (<span>Total Models: {props.Count}</span>)
  }
  public menuFilter = { type: 'Menu' };
  public checkboxFilter = { type: 'CheckBox' };
  public render(){
      return (<div className="e-adaptive-demo e-bigger">
              <div className="e-mobile-layout">
                <div className="e-mobile-content">
                    <GridComponent id="adaptivebrowser" dataSource={data} height='100%' ref={grid => this.grid = grid} enableAdaptiveUI={true} rowRenderingMode={this.renderingMode} allowFiltering={true} allowSorting={true} allowPaging={true} filterSettings={this.filterOptions} toolbar={this.toolbarOptions} editSettings={this.editSettings} load={this.load}>
                      <ColumnsDirective>
                        <ColumnDirective field='SNO' headerText='S NO' width='150' isPrimaryKey={true} validationRules={this.orderidRules}></ColumnDirective>
                        <ColumnDirective field='Model' headerText='Model Name' width='200' editType='dropdownedit' validationRules={this.validationRule} />
                        <ColumnDirective field='Developer' headerText='Developer' width='200' filter={this.menuFilter} validationRules={this.validationRule}></ColumnDirective>
                        <ColumnDirective field='ReleaseDate' headerText='Released Date' editType='datepickeredit' type='date' format='yMMM' width='200'></ColumnDirective>
                        <ColumnDirective field='AndroidVersion' headerText='Android Version' width='200' filter={this.checkboxFilter} validationRules={this.validationRule}></ColumnDirective>
                      </ColumnsDirective>
                      <Inject services={[Filter, Sort, Edit, Toolbar, Aggregate, Page]} />
                       <AggregatesDirective>
                        <AggregateDirective>
                          <AggregateColumnsDirective>
                            <AggregateColumnDirective field='Model' type='Count' footerTemplate={this.footerSum}> </AggregateColumnDirective>
                          </AggregateColumnsDirective>
                        </AggregateDirective>
                      </AggregatesDirective>
                    </GridComponent>
                </div>
              </div>
              <br></br>
                <div className="datalink">Source:
                  <a href="https://en.wikipedia.org/wiki/List_of_Android_smartphones"
                    target="_blank">Wikipedia: List of Android smartphones</a>
                </div>
              </div>
            )
      }
}
```

{% endtab %}

> * [`enableAdaptiveUI`](../api/grid/#enableadaptiveui) property must be enabled for vertical row rendering.

### Supported features by vertical row rendering

The following features are only supported in vertical row rendering:

* Paging
* Sorting
* Filtering
* Selection
* Dialog Editing
* Aggregate
* Infinite scroll
* Toolbar
