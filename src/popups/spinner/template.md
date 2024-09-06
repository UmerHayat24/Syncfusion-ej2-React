---
title: "Template"
component: "Spinner"
description: "This example demonstrates how to customize the Essential JS 2 Spinner control based on different needs."
---

# Set the template to the Spinner

You can use custom templates on the Spinner instead of the default Spinner by specifying the template in the `setSpinner` method.

The following steps explains you on how to define template for Spinner.

* Import the `setSpinner` method from `ej2-react-popups` library into your `index.tsx` as shown in below.

```typescript
import { setSpinner } from '@syncfusion/ej2-react-popups';
```

* Pass your custom template to the `setSpinner` method like as below.

```typescript
// Specify the template content to be displayed in the Spinner

setSpinner({ template: '<div style="width:100%;height:100%" class="custom-rolling"><div></div></div>'});
```

> You should set the template to the Spinner before creating the respective Essential JS 2 component.
> Also,until we replace `setSpinner` template, the further Essential JS 2 component rendering is created with given template only.

* Now, render the Essential JS 2 component. It's render the Spinner with the template specified in the `setSpinner` method.

> In the below sample, we have rendered the Grid component with custom Spinner using `setSpinner` method.
> You have to define the styles for the template in `index.html`.

{% tab template="spinner/set-spinner", sourceFiles="app/App.tsx",  compileJsx=true, isDefaultActive=true %}

```typescript

import * as React from 'react';
import * as ReactDOM from "react-dom";
import { GridComponent, ColumnsDirective, ColumnDirective } from '@syncfusion/ej2-react-grids';
import { setSpinner } from '@syncfusion/ej2-react-popups';
import { data } from './datasource';

export default class App extends React.Component<{}, {}> {
    private gridData: Object[] = data.slice(0, 7);

    public onFirstGridCreated(): void {
        this.hideSpinner = () => true;

        // Specify the template content to be displayed in the Spinner
        setSpinner({ template: '<div style="width:100%;height:100%" class="custom-rolling"><div></div></div>' });
    }
    public onSecondGridCreated(): void {
        this.hideSpinner = () => true;
    }
    render() {
        return (
            <div>
                <GridComponent id='grid1' dataSource={this.gridData} created={this.onFirstGridCreated}>
                    <ColumnsDirective>
                        <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign='right' type='number'></ColumnDirective>
                        <ColumnDirective field='CustomerID' headerText='Customer ID' width='140' type='string'></ColumnDirective>
                        <ColumnDirective field='Freight' headerText='Freight' width='120' format='C' textAlign='right' />
                        <ColumnDirective field='OrderDate' headerText='Order Date' width='140' format='yMd' textAlign='right' />
                    </ColumnsDirective>
                </GridComponent>
                <br/><br/><br/>
                <GridComponent id='grid2' dataSource={this.gridData} created={this.onSecondGridCreated}>
                    <ColumnsDirective id='grid2' dataSource={this.gridData}>
                        <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign='right' type='number'></ColumnDirective>
                        <ColumnDirective field='CustomerID' headerText='Customer ID' width='140' type='string'></ColumnDirective>
                        <ColumnDirective field='Freight' headerText='Freight' width='120' format='C' textAlign='right' />
                        <ColumnDirective field='OrderDate' headerText='Order Date' width='140' format='yMd' textAlign='right' />
                    </ColumnsDirective>
                </GridComponent>
            </div>
        );
    }
}

```

{% endtab %}