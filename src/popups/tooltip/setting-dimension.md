---
title: "Setting Dimension for Tooltip"
component: "Tooltip"
description: "React tooltip component’s dimension can either be assigned auto height and width values or specific pixel values."
---

# Setting Dimension

## Height and width

The Tooltip can either be assigned auto height and width values or specific pixel values. The `width` and `height` properties are used to
 set the outer dimension of the Tooltip element. The default value for both the properties is `auto`.
  It also accepts string and number values in pixels.

The following sample explains how to set dimensions for the Tooltip.

{% tab template="tooltip/height-width", isDefaultActive=true, sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```javascript
import * as React from 'react';
import * as ReactDom from 'react-dom';
import { TooltipComponent } from '@syncfusion/ej2-react-popups';

class App extends React.Component<{}, {}> {
  render() {
    return (
      <TooltipComponent width="180px" height="40px" content="This tooltip has 180px width and 40px height">
        <div id='target'>Show Tooltip</div>
      </TooltipComponent>
    );
  }
}
ReactDom.render(<App />,document.getElementById('sample'));

```

{% endtab %}

### Scroll mode

When `height` is specified with a certain pixel value and the Tooltip content overflows, the scrolling mode gets enabled.

{% tab template="tooltip/scroll-mode", isDefaultActive=true, sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```javascript
import * as React from 'react';
import * as ReactDom from 'react-dom';
import { TooltipComponent } from '@syncfusion/ej2-react-popups';

class App extends React.Component<{}, {}> {
  private content() {
    return(
      <div id='tooltipContent'>
      <p><strong>Environmentally friendly</strong> or <strong>environment-friendly</strong>, <i>(also referred to as eco-friendly, nature-friendly, and green)</i> are marketing and sustainability terms referring to goods and services, laws, guidelines and policies that inflict reduced, minimal, or no harm upon ecosystems or the environment.</p></div>
    )
  }
  render() {
    let style: object = {
      display: 'inline-block',
      padding : '5px'
    };
    return (
        <p>A green home is a type of house designed to be
            <TooltipComponent width="300px" height="60px" isSticky={true} content={this.content} style={style}>
            <a><u>environmentally friendly</u></a>
            </TooltipComponent> and sustainable. And also focuses on the efficient use of "energy, water, and building materials." As green homes
            have become more prevalent we have also seen the emergence of green affordable housing.
        </p>
    );
  }
}
ReactDom.render(<App />,document.getElementById('sample'));
```

{% endtab %}

> The scrolling mode can best be seen when the sticky mode of the Tooltip is enabled. To enable sticky mode, set the `isSticky` property to true.
