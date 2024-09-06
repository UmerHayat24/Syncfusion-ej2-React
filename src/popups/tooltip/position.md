---
title: "Tooltip Position"
component: "Tooltip"
description: "React tooltip can be displayed in 12 (twelve) different positions of target element that automatically collide based on view port."
---

# Tooltip Positioning

Tooltips can be attached to 12 static locations around the target.
On initializing the Tooltip, you can set the position property with any one of the following values:

* `TopLeft`
* `TopCenter`
* `TopRight`
* `BottomLeft`
* `BottomCenter`
* `BottomRight`
* `LeftTop`
* `LeftCenter`
* `LeftBottom`
* `RightTop`
* `RightCenter`
* `RightBottom`

> By default, Tooltip is placed at the `TopCenter` of the target element.

{% tab template="tooltip/position-default", isDefaultActive=true, sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```javascript
import * as React from 'react';
import * as ReactDom from 'react-dom';
import { TooltipComponent, Position } from '@syncfusion/ej2-react-popups';

class App extends React.Component<{}, {}> {
    private dropElement: HTMLSelectElement;
    private tooltipInstance: TooltipComponent;
    public  change(): void {
        this.tooltipInstance.position =  this.dropElement.value as Position;
    }

  render() {
    return (
        <div id='container'>
          <TooltipComponent  ref={t => this.tooltipInstance = t} className="tooltip-box" content='Tooltip Content' target='#tooltip'>
              <div id="tooltip">Show Tooltip</div>
          </TooltipComponent>
          <div class='ddl'>
              <select id="positions" ref={d => this.dropElement = d} onChange={this.change.bind(this)} className="form-control drop-inline">
                  <option value="TopLeft">Top Left</option>
                  <option value="TopCenter" selected>Top Center</option>
                  <option value="TopRight">Top Right</option>
                  <option value="BottomLeft">Bottom Left</option>
                  <option value="BottomCenter">Bottom Center</option>
                  <option value="BottomRight">Bottom Right</option>
                  <option value="LeftTop">Left Top</option>
                  <option value="LeftCenter">Left Center</option>
                  <option value="LeftBottom">Left Bottom</option>
                  <option value="RightTop">Right Top</option>
                  <option value="RightCenter">Right Center</option>
                  <option value="RightBottom">Right Bottom</option>
              </select>
          </div>
      </div>
    );
  }
}
ReactDom.render(<App />,document.getElementById('sample'));

```

{% endtab %}

## Tip pointer positioning

The Tooltip pointer can be attached or detached from the Tooltip by using the `showTipPointer` property.
Pointer positions can be adjusted using the `tipPointerPosition` property that can be assigned to one of the following values:

* `Auto`
* `Start`
* `Middle`
* `End`

The following code example illustrates how to set the pointer to the start position of the Tooltip.

{% tab template="tooltip/position-tip", isDefaultActive=true, sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```javascript
import * as React from 'react';
import * as ReactDom from 'react-dom';
import { TooltipComponent } from '@syncfusion/ej2-react-popups';

class App extends React.Component<{}, {}> {
  render() {
    return (
        <TooltipComponent className="tooltip-box" content='Tooltip Content' tipPointerPosition='Start' target='#target'>
            <button className="e-btn" id='target'>Show Tooltip</button>
        </TooltipComponent>
    );
  }
}
ReactDom.render(<App />,document.getElementById('sample'));

```

{% endtab %}

By default, tip pointers are auto adjusted so that the arrow does not point outside the target element.

## Dynamic positioning

The Tooltip and its tip pointer can be positioned dynamically based on the target's location. This can be achieved by using the `refresh`
 method, which auto adjusts the Tooltip over the target.

{% tab template="tooltip/dragabble", isDefaultActive=true, sourceFiles="app/**/*.tsx,index.html", compileJsx=true %}

```javascript
import * as React from 'react';
import * as ReactDom from 'react-dom';
import { TooltipComponent } from '@syncfusion/ej2-react-popups';
import { Draggable } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}> {
    private tooltipInstance: TooltipComponent;
    private tooltipAnimation: Object = {
        open: { effect: 'None' },
        close: { effect: 'None' }
    };
    public componentDidMount(): void {
        let ele: HTMLElement = document.getElementById('demoSmart');
        let drag: Draggable = new Draggable(ele, {
            clone: false,
            dragArea: '#targetContainer',
            drag: (args: any) => {
                if (args.element.getAttribute('data-tooltip-id') === null) {
                    this.tooltipInstance.open(args.element);
                } else {
                    this.tooltipInstance.refresh(args.element);
                }
            },
            dragStart: (args: any) => {
                if (args.element.getAttribute('data-tooltip-id') === null) {
                    this.tooltipInstance.open(args.element);
                }
            },
            dragStop: (args: any) => {
                this.tooltipInstance.close();
            }
        });
    }
    render() {
        return (<div id='targetContainer'>
                <TooltipComponent ref={t => this.tooltipInstance = t} target='#demoSmart' content='Drag me !!!' animation={this.tooltipAnimation}>
                <div id='demoSmart'>
                </div>
                </TooltipComponent>
            </div>
        );
    }
}
ReactDom.render(<App />,document.getElementById('sample'));

```

{% endtab %}

## Mouse trailing

Tooltips can be positioned relative to the mouse pointer. This behavior can be enabled or disabled by using the `mouseTrail` property.
 By default, it is set to `false`.

{% tab template="tooltip/mouse-trail", isDefaultActive=true, sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```javascript
import * as React from 'react';
import * as ReactDom from 'react-dom';
import { TooltipComponent } from '@syncfusion/ej2-react-popups';

class App extends React.Component<{}, {}> {
  render() {
    return (
        <TooltipComponent className="tooltip-box" content='Tooltip Content' mouseTrail={true} showTipPointer={false}>
            <div id='target'>Show Tooltip</div>
        </TooltipComponent>
    );
  }
}
ReactDom.render(<App />,document.getElementById('sample'));

```

{% endtab %}

> When mouse trailing option is enabled, the tip pointer position gets auto adjusted based on the target, and
> other position values like start, end, and middle are not applied (to prevent the pointer from moving out of target).

## Setting offset values

Offset values are set to specify the distance between the target and tooltip element.
`offsetX` and `offsetY` properties are used to specify the offset left and top values.

* `offsetX` specifies the distance between the target and Tooltip element in X axis.
* `offsetY` specifies the distance between the target and Tooltip element in Y axis.

The following code example illustrates how to set offset values.

{% tab template="tooltip/offset", isDefaultActive=true, sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```javascript
import * as React from 'react';
import * as ReactDom from 'react-dom';
import { TooltipComponent } from '@syncfusion/ej2-react-popups';

class App extends React.Component<{}, {}> {
  render() {
    return (
        <TooltipComponent className="tooltip-box" offsetX={30} offsetY={30} showTipPointer={false} mouseTrail={true} content='Tooltip Content'>
            <div id='target'>Show Tooltip</div>
        </TooltipComponent>
    );
  }
}
ReactDom.render(<App />,document.getElementById('sample'));

```

{% endtab %}

> By default, collision is handled automatically and therefore when collision is detected the Tooltip fits horizontally and flips vertically.
