---
title: "Tooltip of Kanban"
component: "Kanban"
description: "This article demonstrates how to show the tooltip when hovering card elements and also explained how to use template."
---

# Tooltip

The tooltip is used to show the card information when the cursor hover over the card elements using the `enableTooltip` property. Tooltip content is dynamically set based on hovering over the card elements.

> If you wish to show tooltip on Kanban board custom elements, you need to add `e-tooltip-text` class name of a particular element.

## Tooltip template

You can customize the tooltip content with any HTML or CSS element and styling using the `tooltipTemplate` property. In the following demo, the tooltip is customized with HTML elements.

{% tab template="kanban/tooltip-template", iframeHeight="588px", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { extend } from '@syncfusion/ej2-base';
import { KanbanComponent, ColumnsDirective, ColumnDirective } from "@syncfusion/ej2-react-kanban";
import { kanbanData } from './datasource';

class App extends React.Component<{}, {}>{
   constructor() {
        super(...arguments);
        this.data = extend([], kanbanData, null, true);
    }
      private template(props): JSX.Element {
        return (<div className="e-kanbantooltiptemp">
            <table>
                <tr>
                    <td className="e-kanban-card-details">
                        <table>
                            <colgroup>
                                <col style={{ width: "30%" }} />
                                <col style={{ width: "70%" }} />
                            </colgroup>
                            <tbody><tr><td className="CardHeader">Assignee:</td><td>{props.Assignee}</td></tr>
                                <tr><td className="CardHeader">Type:</td><td>{props.Type}</td></tr><tr>
                                    <td className="CardHeader">Estimate:</td><td>{props.Estimate}</td></tr>
                                <tr><td className="CardHeader">Summary:</td><td>{props.Summary}</td></tr></tbody>
                        </table>
                    </td></tr>
            </table>
        </div>);
    }
  render() {
    return <KanbanComponent id="kanban" keyField="Status" dataSource={this.data} cardSettings={{ contentField: "Summary", headerField: "Id" }} enableTooltip={true} tooltipTemplate={this.template.bind(this)}>
                <ColumnsDirective>
                  <ColumnDirective headerText="To Do" keyField="Open" />
                  <ColumnDirective headerText="In Progress" keyField="InProgress" />
                  <ColumnDirective headerText="Testing" keyField="Testing" />
                  <ColumnDirective headerText="Done" keyField="Close" />
                </ColumnsDirective>
            </KanbanComponent>
  }
};
ReactDOM.render(<App />, document.getElementById('kanban'));

```

{% endtab %}
