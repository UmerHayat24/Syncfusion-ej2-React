---
title: " Methods in React Linear Gauge component | Syncfusion "

component: "Linear Gauge"

description: "Learn here all about the Methods of Syncfusion React Linear Gauge component and more."
---
# Methods in React Linear Gauge

The following methods are available in the Linear Gauge component.

## setPointerValue

To change the pointer value dynamically, use the [`setPointerValue`](../api/linear-gauge#setpointervalue) method in the Linear Gauge component. The following are the arguments for this method.

|   Argument name      |   Description                            |
|----------------------| -----------------------------------------|
|     axisIndex        |    Specifies the index of the axis in which the pointer value is to be updated.|
|     pointerIndex     |    Specifies the index of the pointer to be updated.           |
|     pointerValue     |    Specifies the value of the pointer to be updated.           |

{% tab template="linear-gauge/axis", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { LinearGaugeComponent, AxesDirective, AxisDirective, PointersDirective, PointerDirective } from '@syncfusion/ej2-react-lineargauge';
class App extends React.Component<{}, {}>{
public clickHandler(){
  this.linear.setPointerValue(0, 0, 30);
}
private linear: LinearGaugeComponent;
render(){
    return (<div>
    <ButtonComponent value='btn' onClick= { this.clickHandler.bind(this)}>Click</ButtonComponent>
    <LinearGaugeComponent id='gauge' ref={g => this.linear = g}>
        <AxesDirective>
            <AxisDirective>
                <PointersDirective>
                    <PointerDirective value={80}>
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

## setAnnotationValue

To change the annotation content dynamically, use the [`setAnnotationValue`](../api/linear-gauge#setannotationvalue) method in the Linear Gauge component. The following are the arguments for this method.

|   Argument name      |   Description                            |
|----------------------| -----------------------------------------|
|     annotationIndex  |    Specifies the index number of the annotation to be updated. |
|     content          |    Specifies the text for the annotation to be updated.        |
|     axisValue        |    Specifies the value of the axis where the annotation is to be placed.|

{% tab template="linear-gauge/axis", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { Annotations, AnnotationsDirective, AnnotationDirective, LinearGaugeComponent, AxesDirective, AxisDirective, PointersDirective, Inject, PointerDirective } from '@syncfusion/ej2-react-lineargauge';
class App extends React.Component<{}, {}>{
public clickHandler(){
  this.linear.setAnnotationValue(0, '50', 50);
}
private linear: LinearGaugeComponent;
render(){
    return (<div>
    <ButtonComponent value='btn' onClick= { this.clickHandler.bind(this)}>Click</ButtonComponent>
    <LinearGaugeComponent id='gauge' ref={g => this.linear = g}>
        <Inject services={[Annotations]}/>
        <AnnotationsDirective>
            <AnnotationDirective content='10' axisValue={0} zIndex='1'>
            </AnnotationDirective>
        </AnnotationsDirective>
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

## refresh

The [`refresh`](../api/linear-gauge#refresh) method can be used to change the state of the component and render it again. In the following example, the gauge is rendered again using the [`refresh`](../api/linear-gauge#refresh) method.

{% tab template="linear-gauge/axis", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { LinearGaugeComponent, AxesDirective, AxisDirective, PointersDirective, PointerDirective } from '@syncfusion/ej2-react-lineargauge';
class App extends React.Component<{}, {}>{
public clickHandler(){
  this.linear.refresh();
}
private linear: LinearGaugeComponent;
render(){
    return (<div>
    <ButtonComponent value='btn' onClick= { this.clickHandler.bind(this)}>Click</ButtonComponent>
    <LinearGaugeComponent id='gauge' ref={g => this.linear = g}>
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
