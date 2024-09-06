---
title: "Complex Data Binding with list of Array Of Objects"
component: "Grid"
description: "Learn how to set Complex data for datasource having Array Of Objects."
---

# Complex Data Binding with list of Array Of Objects

The following example shows how to set Complex field for datasource having Array Of Objects.

{% tab template="grid/complex-binding", sourceFiles="app/App.tsx,app/datasource.tsx" %}

```typescript
import { ColumnDirective, ColumnsDirective, GridComponent } from '@syncfusion/ej2-react-grids';
import * as React from 'react';
import { complexData } from './datasource';

export default class App extends React.Component<{}, {}> {
  public render() {
    return (<div>
    <GridComponent dataSource={complexData} height={315 }>
        <ColumnsDirective>
          <ColumnDirective field='EmployeeID' headerText='Employee ID' width='120' textAlign="Right"/>
          <ColumnDirective field='Names.0.LastName' headerText='Last Name' width='120'/>
          <ColumnDirective field='Region' headerText='Region' width='120'/>
          <ColumnDirective field='City' headerText='City' width='150'/>
        </ColumnsDirective>
    </GridComponent>
    </div>)
  }
};
```

{% endtab %}