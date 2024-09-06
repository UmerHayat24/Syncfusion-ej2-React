---
title: "Set command customization"
component: "Toolbar"
description: "This example demonstrates how to set the HTML attribute commands to Essential JS 2 Toolbar control items."
---

# Set command customization

The [`htmlAttributes`](../../api/toolbar/item#htmlattributes) property of the Toolbar item is used to set the HTML attributes ('ID', 'class', 'style' ,'role') for the commands.

When style attributes are added, if the same attributes were already present, they will be replaced. This is not so in the case of
`class` attribute. Classes will be added to the element instead of replacing the existing ones.

Single or multiple CSS classes can be added to the Toolbar commands using the Toolbar item [`cssClass`](../../api/toolbar/item#cssclass) property.

{% tab template="toolbar/toolbar", compileJsx=true %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import { ToolbarComponent, ItemsDirective, ItemDirective } from '@syncfusion/ej2-react-navigations';

class ReactApp extends React.Component<{}, {}> {
  render() {
        let boldAttribute: any = {
          'class': 'custom_bold', 'id': 'itemId'
        };
        let italicAttribute: any = { 'class': 'custom_italic' };
        let underAttribute: any = { 'class': 'custom_underline' };
        return (
           <ToolbarComponent width="300" >
            <ItemsDirective>
              <ItemDirective text="Bold" htmlAttributes={boldAttribute}  />
              <ItemDirective text="Italic" htmlAttributes={italicAttribute}/>
              <ItemDirective text="Underline" htmlAttributes={underAttribute}/>
              <ItemDirective type="Separator"/>
              <ItemDirective text="Uppercase" cssClass="e-txt-casing"  />
            </ItemsDirective>
           </ToolbarComponent>
       );
  }
}
ReactDOM.render(<ReactApp/>, document.getElementById("toolbar"));

```

{% endtab %}