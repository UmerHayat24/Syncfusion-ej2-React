---
title: " Events in React Linear Gauge component | Syncfusion "

component: "Linear Gauge"

description: "Learn here all about Events of Syncfusion React Linear Gauge component and more."
---

# Events in React Linear Gauge

This section describes the Linear Gauge component's event that gets triggered when corresponding operations are performed.

## animationComplete

When the pointer animation is completed, the [`animationComplete`](../api/linear-gauge#animationcomplete) event will be triggered. To know more about the arguments of this event, refer [here](../api/linear-gauge/iAnimationCompleteEventArgs/).

{% tab template="linear-gauge/axis", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { LinearGaugeComponent, AxesDirective, AxisDirective, PointersDirective, PointerDirective, IAnimationCompleteEventArgs } from '@syncfusion/ej2-react-lineargauge';
class App extends React.Component<{}, {}>{
public animationComplete(args: IAnimationCompleteEventArgs){
}
private linear: LinearGaugeComponent;
render(){
    return (<div>
    <LinearGaugeComponent id='gauge' ref={g => this.linear = g} animationComplete={this.animationComplete.bind(this)}>
        <AxesDirective>
            <AxisDirective>
                <PointersDirective>
                    <PointerDirective value={10}>
                    </PointerDirective>
                </PointersDirective>
            </AxisDirective>
        </AxesDirective>
    </LinearGaugeComponent></div>)
    }
};
ReactDOM.render(<App />, document.getElementById('gauge'));

```

{% endtab %}

## annotationRender

Before the annotation is rendered in the Linear Gauge, the [`annotationRender`](../api/linear-gauge#annotationrender) event will be triggered. To know more about the arguments of this event, refer [here](../api/linear-gauge/iAnnotationRenderEventArgs/).

{% tab template="linear-gauge/axis", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { Annotations, AnnotationsDirective, AnnotationDirective, LinearGaugeComponent,Inject, IAnnotationRenderEventArgs } from '@syncfusion/ej2-react-lineargauge';
class App extends React.Component<{}, {}>{
public annotationRender(args: IAnnotationRenderEventArgs){
}
private linear: LinearGaugeComponent;
render(){
    return (<div>
    <LinearGaugeComponent id='gauge' ref={g => this.linear = g} annotationRender={this.annotationRender.bind(this)}>
        <Inject services={[Annotations]}/>
        <AnnotationsDirective>
            <AnnotationDirective content='<div id="first"><h1>Gauge</h1></div>' axisValue={0} zIndex='1'>
            </AnnotationDirective>
        </AnnotationsDirective>
    </LinearGaugeComponent></div>)
    }
};
ReactDOM.render(<App />, document.getElementById('gauge'));

```

{% endtab %}

## axisLabelRender

Before each axis label is rendered in the Linear Gauge, the [`axisLabelRender`](../api/linear-gauge#axislabelrender) event is fired. To know more about the arguments of this event, refer [here](../api/linear-gauge/iAxisLabelRenderEventArgs/).

{% tab template="linear-gauge/axis", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { LinearGaugeComponent, AxesDirective, AxisDirective, PointersDirective, PointerDirective, IAxisLabelRenderEventArgs } from '@syncfusion/ej2-react-lineargauge';
class App extends React.Component<{}, {}>{
public axisLabelRender(args: IAxisLabelRenderEventArgs){
}
private linear: LinearGaugeComponent;
render(){
    return (<div>
    <LinearGaugeComponent id='gauge' ref={g => this.linear = g} axisLabelRender={this.axisLabelRender.bind(this)}>
        <AxesDirective>
            <AxisDirective>
                <PointersDirective>
                    <PointerDirective>
                    </PointerDirective>
                </PointersDirective>
            </AxisDirective>
        </AxesDirective>
    </LinearGaugeComponent></div>)
    }
};
ReactDOM.render(<App />, document.getElementById('gauge'));

```

{% endtab %}

## beforePrint

The [`beforePrint`](../api/linear-gauge/#beforeprint) event is fired before the print begins. To know more about the arguments of this event, refer [here](../api/linear-gauge/iPrintEventArgs/).

{% tab template="linear-gauge/axis", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { LinearGaugeComponent, Print, Inject, IPrintEventArgs } from '@syncfusion/ej2-react-lineargauge';
class App extends React.Component<{}, {}>{
public clickHandler(){
  this.linear.print();
}
public beforePrint(args: IPrintEventArgs){
}
private linear: LinearGaugeComponent;
render(){
        return (<div>
        <ButtonComponent value='print' onClick= { this.clickHandler.bind(this)}>print</ButtonComponent>
        <LinearGaugeComponent id='gauge' allowPrint={true}  ref={g => this.linear = g} beforePrint={this.beforePrint.bind(this)}>
            <Inject services={[Print]} />
        </LinearGaugeComponent></div>)
        }
};
ReactDOM.render(<App />, document.getElementById('gauge'));

```

{% endtab %}

## dragEnd

The [`dragEnd`](../api/linear-gauge#dragend) event will be fired before the pointer drag is completed. To know more about the argument of this event, refer [here](../api/linear-gauge/iPointerDragEventArgs/).

{% tab template="linear-gauge/axis", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { LinearGaugeComponent, AxesDirective, AxisDirective, PointersDirective, PointerDirective, IPointerDragEventArgs } from '@syncfusion/ej2-react-lineargauge';
class App extends React.Component<{}, {}>{
public dragEnd(args: IPointerDragEventArgs){
}
private linear: LinearGaugeComponent;
render(){
    return (<div>
    <LinearGaugeComponent id='gauge' ref={g => this.linear = g} dragEnd={this.dragEnd.bind(this)}>
        <AxesDirective>
            <AxisDirective>
                <PointersDirective>
                    <PointerDirective enableDrag={true}>
                    </PointerDirective>
                </PointersDirective>
            </AxisDirective>
        </AxesDirective>
    </LinearGaugeComponent></div>)
    }
};
ReactDOM.render(<App />, document.getElementById('gauge'));

```

{% endtab %}

## dragMove

The [`dragMove`](../api/linear-gauge#dragmove) event will be fired when the pointer is dragged. To know more about the arguments of this event, refer [here](../api/linear-gauge/iPointerDragEventArgs/).

{% tab template="linear-gauge/axis", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { LinearGaugeComponent, AxesDirective, AxisDirective, PointersDirective, PointerDirective, IPointerDragEventArgs } from '@syncfusion/ej2-react-lineargauge';
class App extends React.Component<{}, {}>{
public dragMove(args: IPointerDragEventArgs){
}
private linear: LinearGaugeComponent;
render(){
    return (<div>
    <LinearGaugeComponent id='gauge' ref={g => this.linear = g} dragMove={this.dragMove.bind(this)}>
        <AxesDirective>
            <AxisDirective>
                <PointersDirective>
                    <PointerDirective enableDrag={true}>
                    </PointerDirective>
                </PointersDirective>
            </AxisDirective>
        </AxesDirective>
    </LinearGaugeComponent></div>)
    }
};
ReactDOM.render(<App />, document.getElementById('gauge'));

```

{% endtab %}

## dragStart

When the pointer drag begins, the [`dragStart`](../api/linear-gauge#dragstart) event is triggered. To know more about the arguments of this event, refer [here](../api/linear-gauge/iPointerDragEventArgs/).

{% tab template="linear-gauge/axis", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { LinearGaugeComponent, AxesDirective, AxisDirective, PointersDirective, PointerDirective, IPointerDragEventArgs } from '@syncfusion/ej2-react-lineargauge';
class App extends React.Component<{}, {}>{
public dragStart(args: IPointerDragEventArgs){
}
private linear: LinearGaugeComponent;
render(){
    return (<div>
    <LinearGaugeComponent id='gauge' ref={g => this.linear = g} dragStart={this.dragStart.bind(this)}>
        <AxesDirective>
            <AxisDirective>
                <PointersDirective>
                    <PointerDirective enableDrag={true}>
                    </PointerDirective>
                </PointersDirective>
            </AxisDirective>
        </AxesDirective>
    </LinearGaugeComponent></div>)
    }
};
ReactDOM.render(<App />, document.getElementById('gauge'));

```

{% endtab %}

## gaugeMouseDown

When mouse is pressed down on the gauge, the [`gaugeMouseDown`](../api/linear-gauge#gaugemousedown) event is triggered. To know more about the arguments of this event, refer [here](../api/linear-gauge/iMouseEventArgs/).

{% tab template="linear-gauge/axis", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { LinearGaugeComponent, IMouseEventArgs } from '@syncfusion/ej2-react-lineargauge';
class App extends React.Component<{}, {}>{
public gaugeMouseDown(args: IMouseEventArgs){
}
private linear: LinearGaugeComponent;
render(){
    return (<div>
    <LinearGaugeComponent id='gauge' ref={g => this.linear = g} gaugeMouseDown={this.gaugeMouseDown.bind(this)}>
    </LinearGaugeComponent></div>)
    }
};
ReactDOM.render(<App />, document.getElementById('gauge'));

```

{% endtab %}

## gaugeMouseLeave

When mouse pointer moves over the gauge, the [`gaugemouseleave`](../api/linear-gauge#gaugemouseleave) event is triggered. To know more about the arguments of this event, refer [here](../api/linear-gauge/iMouseEventArgs/).

{% tab template="linear-gauge/axis", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { LinearGaugeComponent, IMouseEventArgs } from '@syncfusion/ej2-react-lineargauge';
class App extends React.Component<{}, {}>{
public gaugeMouseLeave(args: IMouseEventArgs){
}
private linear: LinearGaugeComponent;
render(){
    return (<div>
    <LinearGaugeComponent id='gauge' ref={g => this.linear = g} gaugeMouseLeave={this.gaugeMouseLeave.bind(this)}>
    </LinearGaugeComponent></div>)
    }
};
ReactDOM.render(<App />, document.getElementById('gauge'));

```

{% endtab %}

## gaugeMouseMove

When mouse pointer leaves the gauge, the [`gaugeMouseMove`](../api/linear-gauge#gaugemousemove) event is triggered. To know more about the arguments of this event, refer [here](../api/linear-gauge/iMouseEventArgs/).

{% tab template="linear-gauge/axis", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { LinearGaugeComponent, IMouseEventArgs } from '@syncfusion/ej2-react-lineargauge';
class App extends React.Component<{}, {}>{
public gaugeMouseMove(args: IMouseEventArgs){
}
private linear: LinearGaugeComponent;
render(){
    return (<div>
    <LinearGaugeComponent id='gauge' ref={g => this.linear = g} gaugeMouseMove={this.gaugeMouseMove.bind(this)}>
    </LinearGaugeComponent></div>)
    }
};
ReactDOM.render(<App />, document.getElementById('gauge'));

```

{% endtab %}

## gaugeMouseUp

When the mouse pointer is released over the Linear Gauge, the [`gaugeMouseUp`](../api/linear-gauge#gaugemouseup) event is triggered. To know more about the arguments of this event, refer [here](../api/linear-gauge/iMouseEventArgs/).

{% tab template="linear-gauge/axis", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { LinearGaugeComponent, IMouseEventArgs } from '@syncfusion/ej2-react-lineargauge';
class App extends React.Component<{}, {}>{
public gaugeMouseUp(args: IMouseEventArgs){
}
private linear: LinearGaugeComponent;
render(){
    return (<div>
    <LinearGaugeComponent id='gauge' ref={g => this.linear = g} gaugeMouseUp={this.gaugeMouseUp.bind(this)}>
    </LinearGaugeComponent></div>)
    }
};
ReactDOM.render(<App />, document.getElementById('gauge'));

```

{% endtab %}

## load

Before the Linear Gauge is loaded, the [`load`](../api/linear-gauge#load) event is fired. To know more about the arguments of this event, refer [here](../api/linear-gauge/iLoadEventArgs/).

{% tab template="linear-gauge/axis", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { LinearGaugeComponent, ILoadEventArgs } from '@syncfusion/ej2-react-lineargauge';
class App extends React.Component<{}, {}>{
public load(args: ILoadEventArgs){
}
private linear: LinearGaugeComponent;
render(){
    return (<div>
    <LinearGaugeComponent id='gauge' ref={g => this.linear = g} load={this.load.bind(this)}>
    </LinearGaugeComponent></div>)
    }
};
ReactDOM.render(<App />, document.getElementById('gauge'));

```

{% endtab %}

## loaded

After the Linear Gauge has been loaded, the [`loaded`](../api/linear-gauge#loaded) event will be triggered. To know more about the arguments of this event, refer [here](../api/linear-gauge/iLoadedEventArgs/).

{% tab template="linear-gauge/axis", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { LinearGaugeComponent, ILoadedEventArgs } from '@syncfusion/ej2-react-lineargauge';
class App extends React.Component<{}, {}>{
public loaded(args: ILoadedEventArgs){
}
private linear: LinearGaugeComponent;
render(){
    return (<div>
    <LinearGaugeComponent id='gauge' ref={g => this.linear = g} loaded={this.loaded.bind(this)}>
    </LinearGaugeComponent></div>)
    }
};
ReactDOM.render(<App />, document.getElementById('gauge'));

```

{% endtab %}

## resized

After the window resizing, the [`resized`](../api/linear-gauge#resized) event is triggered. To know more about the arguments of this event, refer [here](../api/linear-gauge/iResizeEventArgs/).

{% tab template="linear-gauge/axis", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { LinearGaugeComponent, IResizeEventArgs } from '@syncfusion/ej2-react-lineargauge';
class App extends React.Component<{}, {}>{
public resized(args: IResizeEventArgs){
}
private linear: LinearGaugeComponent;
render(){
    return (<div>
    <LinearGaugeComponent id='gauge' ref={g => this.linear = g} loaded={this.resized.bind(this)}>
    </LinearGaugeComponent></div>)
    }
};
ReactDOM.render(<App />, document.getElementById('gauge'));

```

{% endtab %}

## tooltipRender

The [`tooltipRender`](../api/linear-gauge#tooltiprender) event is fired before the tooltip is rendered. To know more about the arguments of this event, refer [here](../api/linear-gauge/iTooltipRenderEventArgs/).

{% tab template="linear-gauge/axis", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { LinearGaugeComponent, AxesDirective, AxisDirective, PointersDirective, PointerDirective, ITooltipRenderEventArgs } from '@syncfusion/ej2-react-lineargauge';
class App extends React.Component<{}, {}>{
public tooltipRender(args: ITooltipRenderEventArgs){
}
private linear: LinearGaugeComponent;
render(){
    return (<div>
    <LinearGaugeComponent id='gauge' ref={g => this.linear = g} tooltipRender={this.tooltipRender.bind(this)} tooltip={{ enable: true }}>
        <AxesDirective>
            <AxisDirective>
                <PointersDirective>
                    <PointerDirective>
                    </PointerDirective>
                </PointersDirective>
            </AxisDirective>
        </AxesDirective>
    </LinearGaugeComponent></div>)
    }
};
ReactDOM.render(<App />, document.getElementById('gauge'));

```

{% endtab %}

## valueChange

The [`valueChange`](../api/linear-gauge#valuechange) event is triggered when the pointer is dragged from one value to another. To know more about the arguments of this event, refer [here](../api/linear-gauge/iValueChangeEventArgs/).

{% tab template="linear-gauge/axis", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { LinearGaugeComponent, AxesDirective, AxisDirective, PointersDirective, PointerDirective, IValueChangeEventArgs } from '@syncfusion/ej2-react-lineargauge';
class App extends React.Component<{}, {}>{
public valueChange(args: IValueChangeEventArgs){
}
private linear: LinearGaugeComponent;
render(){
    return (<div>
    <LinearGaugeComponent id='gauge' ref={g => this.linear = g} valueChange={this.valueChange.bind(this)}>
        <AxesDirective>
            <AxisDirective>
                <PointersDirective>
                    <PointerDirective enableDrag={true}>
                    </PointerDirective>
                </PointersDirective>
            </AxisDirective>
        </AxesDirective>
    </LinearGaugeComponent></div>)
    }
};
ReactDOM.render(<App />, document.getElementById('gauge'));

```

{% endtab %}