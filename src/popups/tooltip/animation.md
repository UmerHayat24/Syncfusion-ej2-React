---
title: "Animation For Tooltip"
component: "Tooltip"
description: "React tooltip component supports various animation effects while showing or hiding the tooltip."
---

# Animation

To animate the Tooltip, a set of specific animation effects are available, and it can be controlled using the `animation` property.
 The animation property also allows you to set delay, duration, and various other effects of your choice.

[`AnimationModel`](https://ej2.syncfusion.com/react/documentation/api/tooltip/animationModel/) is derived from base to apply the chosen animation effect, duration, etc. on Tooltips.

By default, Tooltip entrance occurs over 150 ms using the `ease-out` timing function. It exits also at 150 ms,
but uses `ease-in` timing function.

{% tab template="tooltip/animation", isDefaultActive=true, sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```javascript
import * as React from 'react';
import * as ReactDom from 'react-dom';
import { TooltipComponent } from '@syncfusion/ej2-react-popups';

class App extends React.Component<{}, {}> {
    public TooltipAnimation: Object = {
        open: { effect: 'ZoomIn', duration: 1000, delay: 0 },
        close: { effect: 'ZoomOut', duration: 500, delay: 0 }
    };
    render() {
        return (
            <TooltipComponent className="tooltip-box" content='Tooltip animation effect' animation={this.TooltipAnimation}>
                <div id='target'>Show Tooltip</div>
            </TooltipComponent>
        );
    }
}
ReactDom.render(<App />,document.getElementById('sample'));

```

{% endtab %}

The default animation effect for the Tooltip is set to `FadeIn` for its open action, and `FadeOut` for its close action.
The default `duration` is set to 150 ms and `delay` is set to 0.

## Animation effects

The animation effects that are applicable to Tooltips are:

* FadeIn
* FadeOut
* FadeZoomIn
* FadeZoomOut
* FlipXDownIn
* FlipXDownOut
* FlipXUpIn
* FlipXUpOut
* FlipYLeftIn
* FlipYLeftOut
* FlipYRightIn
* FlipYRightOut
* ZoomIn
* ZoomOut
* None

When the `effect` is specified as `none`, no effect will be applied to the Tooltip, and animation is considered to be set to `off`.

> Some of the above animation effects suits the Tooltip better when its tip pointer is hidden.
> This can be achieved by setting the `showTipPointer` to false.

## Animating via open/close methods

Animations can also be applied on Tooltips dynamically through `open` and `close` methods. These methods accept the animation model as an
 optional parameter. If you pass `TooltipAnimationSettings`, animation takes this model; otherwise, it takes the values from the
  `animation` property. It is also possible to pass different animations for Tooltips on each target.

Refer to the code snippet below to apply animations using public methods.

{% tab template="tooltip/effects", isDefaultActive=true, sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```javascript
import * as React from 'react';
import * as ReactDom from 'react-dom';
import { TooltipComponent, TooltipAnimationSettings } from '@syncfusion/ej2-react-popups';

class App extends React.Component<{}, {}> {
    private tooltipInstance: TooltipComponent;
    private handleClick(): void {
        if (this.tooltipInstance.element.getAttribute('data-tooltip-id')) {
            let closeAnimation: TooltipAnimationSettings = { effect: 'FadeOut', duration: 1000 };
            this.tooltipInstance.close(closeAnimation);
        } else {
            let openAnimation: TooltipAnimationSettings = { effect: 'FadeIn', duration: 1000 };
            this.tooltipInstance.open(this.tooltipInstance.element,openAnimation);
        }
    };
    render() {
        return (
            <TooltipComponent className="tooltip-box" content='Tooltip content' opensOn='custom' ref={t => this.tooltipInstance = t}>
                <div id='target' onClick={this.handleClick.bind(this)}>Click Here</div>
            </TooltipComponent>
        );
    }
}
ReactDom.render(<App />,document.getElementById('sample'));

```

{% endtab %}

## Apply transition

The transition effect can be applied on Tooltips by using the `beforeRender` event as given in the
 following work-around code example.

{% tab template="tooltip/transition", isDefaultActive=true, sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```javascript
import * as React from 'react';
import * as ReactDom from 'react-dom';
import { TooltipComponent, TooltipEventArgs } from '@syncfusion/ej2-react-popups';

class App extends React.Component<{}, {}> {
    private tooltipInstance: TooltipComponent;
    private TooltipAnimation: Object = {
        open: { effect: 'ZoomIn', duration: 500 },
        close: { effect: 'ZoomOut', duration: 500 }
    };
    private onBeforeRender(args: TooltipEventArgs): void {
        if (args.element) {
            this.tooltipInstance.animation = { open: { effect: 'None' } };
            args.element.style.display = 'block';
            args.element.style.transitionProperty = 'left,top';
            args.element.style.transitionDuration = '1000ms';
        }
    };
    private onAfterClose(args: TooltipEventArgs): void {
        this.tooltipInstance.animation = this.TooltipAnimation;
    };
    render() {
          let c1: Object = {
            top: '18%',
            left: '5%'
          };
          let c2: Object = {
            top: '30%',
            left: '30%'
          };
          let c3: Object = {
            top: '80%',
            left: '80%'
          };
          let c4: Object = {
            top: '65%',
            left: '50%'
          };
          let c5: Object = {
            top: '75%',
            left: '15%'
          };
          let c6: Object = {
            top: '30%',
            left: '70%'
          };
        return (
            <div className='wrap'>
            <h3> Transition effect </h3>
            <TooltipComponent className='circle-container' target='.circle-tool' animation={this.TooltipAnimation} closeDelay={1000} ref={t => this.tooltipInstance = t} beforeRender={this.onBeforeRender.bind(this)} afterClose={this.onAfterClose.bind(this)}>
                <div className="circle-tool" style={c1} title="This is Turtle !!!"></div>
                <div className="circle-tool" style={c2} title="This is Snake !!!"></div>
                <div className="circle-tool" style={c3} title="This is Croc !!!"></div>
                <div className="circle-tool" style={c4} title="This is String Ray !!!"></div>
                <div className="circle-tool" style={c5} title="This is Blob Fish !!!"></div>
                <div className="circle-tool" style={c6} title="This is Mammoth !!!"></div>
            </TooltipComponent>
            </div>
        );
    }
}
ReactDom.render(<App />,document.getElementById('sample'));

```

{% endtab %}
