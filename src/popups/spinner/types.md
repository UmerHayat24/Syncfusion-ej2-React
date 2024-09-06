---
title: "Types"
component: "Spinner"
description: "This example demonstrates how to change the type of the Essential JS 2 Spinner control based on theme."
---

# Change the type of the Spinner

By default, the Spinner is loaded in the applicable Essential JS 2 component based on the theme imported into
the page. Based on the theme, the type is set to the Spinner.

The available types are:
* Material
* Fabric
* Bootstrap

You can change the Essential JS 2 component spinner type by passing the type of the spinner as parameter to the `setSpinner` method like as below.

```typescript
// Specify the type of the Spinner to be displayed

setSpinner({ type: 'Bootstrap'});
```

> After Essential JS 2 component creation only, you can change the Essential JS 2 component spinner type.

{% tab template="spinner/default-sample", sourceFiles="app/App.tsx",  compileJsx=true, isDefaultActive=true %}

```typescript

import * as React from 'react';
import * as ReactDOM from "react-dom";
import { GridComponent, ColumnsDirective, ColumnDirective } from '@syncfusion/ej2-react-grids';
import { setSpinner } from '@syncfusion/ej2-react-popups';
import { data } from './datasource';

// By default, Spinner is rendered with specified theme inside the Grid component.
export default class App extends React.Component<{}, {}> {
    private gridData: Object[] = data.slice(0, 7);

    public onGridCreated(): void {
        this.hideSpinner = () => true;

        // Specify the type of the Spinner to be displayed in the Grid.
        setSpinner({ type: 'Bootstrap' });
    }
    render() {
        return (
            <div>
                <GridComponent id='grid' dataSource={this.gridData} created={this.onGridCreated}>
                    <ColumnsDirective>
                        <ColumnDirective field='OrderID' headerText='Order ID' width='120' textAlign='right' type='number'></ColumnDirective>
                        <ColumnDirective field='CustomerID' headerText='Customer ID' width='140' type='string'></ColumnDirective>
                        <ColumnDirective field='Freight' headerText='Freight' width='120' format='C' textAlign='right'></ColumnDirective>
                        <ColumnDirective field='OrderDate' headerText='Order Date' width='140' format='yMd' textAlign='right'></ColumnDirective>
                    </ColumnsDirective>
                </GridComponent>
            </div>
        );
    }
}

```

{% endtab %}