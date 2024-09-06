---
title: "Template Configuration"
component: "Toolbar"
description: "This example demonstrates how to customize the Essential JS 2 Toolbar control based on different needs."
---

# Template Configuration

The Toolbar can be rendered by item based collection and by HTML elements.  To render it based on the given HTML element, use `id`
as the `target` property. To render the Toolbar, follow the below structure of the HTML elements:

```html
  <div id='template_toolbar'>   --> Root Toolbar Element
    <div>      --> Toolbar Items Container
       <div>   --> Toolbar Item Element
       </div>
    </div>
  </div>
```

Here, the template ID, `#template_toolbar` is directly appended to the Toolbar.

{% tab template="toolbar/toolbar", compileJsx=true %}

```typescript
import { ToolbarComponent } from '@syncfusion/ej2-react-navigations';
import * as React from "react";
import * as ReactDOM from "react-dom";

export default class ReactApp extends React.Component<{}, {}> {
  public render() {
    return (
      <ToolbarComponent>
        <div id='template_toolbar'>
          <div> <button className="e-btn e-tbar-btn">Cut</button> </div>
          <div> <button className="e-btn e-tbar-btn">Copy</button> </div>
          <div> <button className="e-btn e-tbar-btn">Paste</button> </div>
          <div className="e-separator" />
          <div> <button className="e-btn e-tbar-btn">Bold</button> </div>
          <div> <button className="e-btn e-tbar-btn">Italic</button> </div>
        </div>
      </ToolbarComponent>
    );
  }
}
ReactDOM.render(<ReactApp />, document.getElementById("toolbar"));

```

{% endtab %}

## Popup customization

`Popup` is one of the supported responsive modes of the Toolbar. The Toolbar commands, popup mode priority and button text mode
customizations are
achieved in the item based rendering through property declaration. For more information on popup mode, refer [here](./responsive-mode/)

The above behavior can also be achieved with template rendering by defining `equivalent class` names instead of property declaration.

Equivalent class names listed below are needed to add the Toolbar items' `div` element.

### Priority

Class              | Description
------------       | -------------
  e-overflow-show  | Commands are always displayed on the `Toolbar with primary` priority.
  e-overflow-hide  | Commands are always displayed in the `popup with secondary` priority.

### Button text mode

  Class         | Description
------------       | -------------
  e-popup-text     | Button Text is only visible in the `Popup`.
  e-toolbar-text   | Button Text is only visible on the `Toolbar`.

{% tab template="toolbar/toolbar", compileJsx=true %}

```typescript
import { ToolbarComponent } from '@syncfusion/ej2-react-navigations';
import * as React from "react";
import * as ReactDOM from "react-dom";

export default class ReactApp extends React.Component<{}, {}> {
  public render() {
    return (
      <ToolbarComponent width="300" overflowMode="Popup">
        <div>
          <div className="e-overflow-show e-popup-text"><button className="e-btn e-tbar-btn"><span className="e-cut-icon tb-icons e-icons e-btn-icon" /><div className="e-tbar-btn-text">Cut</div></button> </div>
          <div className="e-overflow-show e-popup-text"><button className="e-btn e-tbar-btn"><span className="e-copy-icon tb-icons e-icons e-btn-icon" /><div className="e-tbar-btn-text">Copy</div></button> </div>
          <div className="e-overflow-show e-popup-text"><button className="e-btn e-tbar-btn"><span className="e-paste-icon tb-icons e-icons e-btn-icon" /><div className="e-tbar-btn-text">Paste</div></button> </div>
          <div className="e-separator" />
          <div className="e-overflow-show e-popup-text"><button className="e-btn e-tbar-btn"><span className="e-bold-icon tb-icons e-icons e-btn-icon" /><div className="e-tbar-btn-text">Bold</div></button> </div>
          <div className="e-overflow-hide e-popup-text"><button className="e-btn e-tbar-btn"><span className="e-underline-icon tb-icons e-icons e-btn-icon" /><div className="e-tbar-btn-text">Underline</div></button> </div>
          <div className="e-overflow-show e-popup-text"><button className="e-btn e-tbar-btn"><span className="e-italic-icon tb-icons e-icons e-btn-icon" /><div className="e-tbar-btn-text">Italic</div></button> </div>
          <div className="e-overflow-show e-popup-text"><button className="e-btn e-tbar-btn"><span className="e-ascending-icon tb-icons e-icons e-btn-icon" /><div className="e-tbar-btn-text">A-Z Sort</div></button> </div>
          <div className="e-overflow-show e-popup-text"><button className="e-btn e-tbar-btn"><span className="e-descending-icon tb-icons e-icons e-btn-icon" /><div className="e-tbar-btn-text">Z-A Sort</div></button> </div>
        </div>
      </ToolbarComponent>
    );
  }
}
ReactDOM.render(<ReactApp />, document.getElementById("toolbar"));

```

{% endtab %}