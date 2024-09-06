---
title: "Tooltip Customization"
component: "Tooltip"
description: "React tooltip component’s complete look and feel can be customized by changing its background color, opacity, content font, etc."
---

# Customization

The Tooltip can be customized by using the `cssClass` property, which accepts custom CSS class names that define specific user-defined
 styles and themes to be applied on the Tooltip element.

## Tip pointer customization

Styling the tip pointer's size, background, and border colors can be done using the `cssClass` property, as given below.

{% tab template="tooltip/custom-tip", isDefaultActive=true, sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```javascript
import * as React from 'react';
import * as ReactDom from 'react-dom';
import { TooltipComponent } from '@syncfusion/ej2-react-popups';

class App extends React.Component<{}, {}> {
  render() {
    return (
        <TooltipComponent className="tooltip-box" content='Tooltip arrow customized' cssClass='customtip'>
            <div id='target'>Show Tooltip</div>
        </TooltipComponent>
    );
  }
}
ReactDom.render(<App />,document.getElementById('sample'));

```

{% endtab %}

## Tooltip customization

The complete look and feel of the Tooltip can be customized by changing it's background color, opacity, content font, etc.
 The following code example shows the way to achieve it.

{% tab template="tooltip/custom-tooltip", isDefaultActive=true, sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```javascript
import * as React from 'react';
import * as ReactDom from 'react-dom';
import { TooltipComponent } from '@syncfusion/ej2-react-popups';

class App extends React.Component<{}, {}> {
  render() {
    return (
        <TooltipComponent className="tooltip-box" content='Tooltip customized' cssClass='customtooltip'>
            <div id="target">Show Tooltip</div>
        </TooltipComponent>
    );
  }
}
ReactDom.render(<App />,document.getElementById('sample'));

```

{% endtab %}
