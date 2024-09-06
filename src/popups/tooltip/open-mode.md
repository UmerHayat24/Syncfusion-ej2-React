---
title: "Tooltip Open Mode"
component: "Tooltip"
description: "React tooltip supports the mode on which the Tooltip is to be opened on a page, i.e., on hovering, focusing, or clicking on the target elements."
---

# Open Mode

You can decide the mode on which the Tooltip is to be opened on a page, i.e., on hovering, focusing, or clicking on the target elements.

> On mobile devices, Tooltips appear when you tap and hold the element, even if the `opensOn` option is assigned with `Hover`.
> Tooltips are also displayed as long as you continue to tap and hold the element. On lift, it  disappears in the next 1.5 seconds.
> If there is another action before that time ends, then the Tooltip disappears.

The `opensOn` property can take either a single or a combination of multiple values, separated by space from the following options.
 The table  below explains how the Tooltip opens on both desktop and mobile based on the value(s) assigned to the `opensOn` property.
  By default, it takes `Auto` value.

| Values | Desktop | Mobile |
| ------------- | ------------- | ------------- |
| `Auto` | Tooltip appears when you hover over the target or when the target element receives the focus. | Tooltip opens on tap and hold of the target element. |
| `Hover` | Tooltip appears when you hover over the target. | Tooltip opens on tap and hold of the target element. |
| `Click` | Tooltip appears when you click a target element. | Tooltip appears when you single tap the target element. |
| `Focus` | Tooltip appears when you focus (say through tab key) on a target element. | Tooltip appears with a single tap on the target element. |
| `Custom` | Tooltip is not triggered by any default action. So, you have to bind your own events and use either `open` or `close` public methods. | Same as Desktop. |

To open the Tooltip for multiple actions, say while hovering over or clicking on a target element, the `opensOn` property can be assigned
 with multiple values, separated by space as `hover click`.

> `Auto` value cannot be used with any combination for multiple values.

The following code example shows how to set the open mode for Tooltips.

{% tab template="tooltip/open-mode", isDefaultActive=true, sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```javascript
import * as React from 'react';
import * as ReactDom from 'react-dom';
import { TooltipComponent } from '@syncfusion/ej2-react-popups';

class App extends React.Component<{}, {}> {
    private buttonElement: HTMLElement;
    private tooltipInstance: TooltipComponent;
    private handleClick(): void {
      if (this.buttonElement.getAttribute('data-tooltip-id')) {
        this.tooltipInstance.close();
      } else {
        this.tooltipInstance.open(this.buttonElement);
      }
    };
  render() {
    let style: object = {
        margin: '150px auto 0 auto',transform: 'translateY(-50%)'
    };
    let margin: object = {
        margin: '40px'
    };
    return (

      <div id='container'>
          <table style={style}>
              <tbody>
                  <tr>
                      <td>
                          <TooltipComponent  content='Tooltip from hover' opensOn='Hover' target='#hoverButton'>
                              <button style={margin} id='hoverButton' className="e-btn blocks">Hover Me !(Default)</button>
                          </TooltipComponent>
                      </td>
                      <td>
                          <TooltipComponent content='Tooltip from click' opensOn='Click' target='#clickButton'>
                              <button style={margin} id='clickButton' className="e-btn blocks">Click Me !</button>
                          </TooltipComponent>
                      </td>
                  </tr>
                  <tr>
                      <td>
                        <TooltipComponent content='Tooltip from focus' opensOn='Focus' target='#tooltipfocus'>
                                <span style={margin} id="textbox" className="e-float-input blocks">
                                    <input id="tooltipfocus" type="text" placeholder="Focus and blur" />
                                </span>
                        </TooltipComponent>
                      </td>
                      <td>
                          <TooltipComponent className="wrap" ref={t => this.tooltipInstance = t} opensOn='custom' content='Tooltip from custom mode'>
                                <input id="box" type="button" className="e-btn" ref={d => this.buttonElement = d} onClick={this.handleClick.bind(this)} value="Click to open tooltip manually" />
                          </TooltipComponent>
                      </td>
                  </tr>
              </tbody>
          </table>
      </div>

    );
  }
}
ReactDom.render(<App />,document.getElementById('sample'));
```

{% endtab %}

## Custom open mode

Other than the above specified options, the `custom` mode makes the Tooltip appear on screen for user-defined custom actions such as
 `right-click`, `double-click`, and so on. Here, the tooltip is not triggered by any default action, and you have to bind your own events
  and use either `open` or `close` public methods to show or hide the Tooltips.

The following code example shows how to define custom open mode for the Tooltip.

{% tab template="tooltip/custom-open", isDefaultActive=true, sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```javascript
import * as React from 'react';
import * as ReactDom from 'react-dom';
import { TooltipComponent } from '@syncfusion/ej2-react-popups';

class App extends React.Component<{}, {}> {
    private buttonElement: HTMLElement;
    private tooltipInstance: TooltipComponent;
    private handleDoubleClick(): void {
        if (this.buttonElement.getAttribute('data-tooltip-id')) {
            this.tooltipInstance.close();
        } else {
            this.tooltipInstance.open(this.buttonElement);
        }
    };
    render() {
        return (
            <TooltipComponent className="wrap" ref={t => this.tooltipInstance = t} opensOn='custom' content='Tooltip from custom mode'>
            <input id="box" type="button" ref={d => this.buttonElement = d} onDoubleClick={this.handleDoubleClick.bind(this)} value="Double click to open tooltip" />
            </TooltipComponent>
        );
    }
}
ReactDom.render(<App />,document.getElementById('sample'));
```

{% endtab %}

## Sticky mode

With this mode set to `true`, Tooltips can be made to show up on the screen as long as the close icon is pressed. In this mode, close
 icon is attached to the Tooltip located at the top right corner. This mode can be enabled or disabled using the `isSticky` property.

{% tab template="tooltip/sticky", isDefaultActive=true, sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```javascript
import * as React from 'react';
import * as ReactDom from 'react-dom';
import { TooltipComponent } from '@syncfusion/ej2-react-popups';

class App extends React.Component<{}, {}> {
  render() {
    return (
        <TooltipComponent className="tooltip-box" isSticky={true} content='Click close icon to close me'>
            <div id='target'>Show Tooltip</div>
        </TooltipComponent>
    );
  }
}
ReactDom.render(<App />,document.getElementById('sample'));

```

{% endtab %}

## Open/Close Tooltip with delay

The Tooltips can be opened or closed after some delay by using the `openDelay` and `closeDelay` properties.

{% tab template="tooltip/open-delay", isDefaultActive=true, sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```javascript
import * as React from 'react';
import * as ReactDom from 'react-dom';
import { TooltipComponent } from '@syncfusion/ej2-react-popups';

class App extends React.Component<{}, {}> {
  render() {
    return (
        <TooltipComponent className="tooltip-box" content='Tooltip with delay' openDelay={1000} closeDelay={1000}>
            <div id='target'>Show Tooltip</div>
        </TooltipComponent>
    );
  }
}
ReactDom.render(<App />,document.getElementById('sample'));

```

{% endtab %}
