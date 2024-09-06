---
title: "Set item-wise custom template"
component: "Toolbar"
description: "This example demonstrates how to create custom template into the Essential JS 2 Toolbar component items."
---

# Set item wise custom template

The Toolbar supports adding template commands using the  `template` property. Template property can be given as the `HTML element`
that is either a `string`  or a `query selector`.

## As string

The HTML element tag can be given as a string for the template property. Here, the checkbox is rendered as a HTML template.

```typescript
template: "<div><input type='checkbox' id='check1' checked=''>Accept</input></div>"

```

## As selector

The template property also allows getting template content through query `selector`. Here, checkbox 'ID' attribute is specified in the template.

```typescript
template: "#Template"

```

{% tab template="toolbar/toolbar-templateID", compileJsx=true %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import { Tooltip } from '@syncfusion/ej2-popups';
import { ToolbarComponent, ItemsDirective, ItemDirective } from '@syncfusion/ej2-react-navigations';

class ReactApp extends React.Component<{}, {}> {
  render() {
       return (
           <ToolbarComponent >
            <ItemsDirective>
              <ItemDirective text="Cut" />
              <ItemDirective type="Separator"/>
              <ItemDirective text="Paste"/>
              <ItemDirective type="Separator"/>
              <ItemDirective template="<div><input type='checkbox' id='check1' checked=''>Accept</input></div>"/>
              <ItemDirective text="Undo"/>
              <ItemDirective text="Redo"/>
              <ItemDirective template="#Template"/>
            </ItemsDirective>
           </ToolbarComponent>
       );
  }
}
ReactDOM.render(<ReactApp/>, document.getElementById("toolbar"));

```

{% endtab %}