---
title: " Annotations in React Linear Gauge component | Syncfusion "

component: "Linear Gauge"

description: "Learn here all about Annotations feature of Syncfusion React Linear Gauge component and more."
---

# Annotations in React Linear Gauge

<!-- markdownlint-disable MD013 -->

Annotations are used to mark the specific area of interest in the Linear Gauge with text, HTML elements, or images. Any number of annotations can be added to the Linear Gauge component.

## Adding annotation

To render the custom HTML elements in the Linear Gauge component, use the [`content`](../api/linear-gauge/annotation/#content) property in the [`AnnotationDirective`](../api/linear-gauge/annotation). The annotation can be rendered either by specifying the id of the element or specifying the code to create a new element that needs to be displayed in the gauge area.

<!-- markdownlint-disable MD036 -->

 ```html

<script id='fruits' type="text/x-template">
    <div id='apple'>
        <img src='src/lineargauge/images/apple.png'>
    </div>
</script>

```

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { LinearGaugeComponent, AnnotationsDirective, AnnotationDirective, Annotations, Inject } from '@syncfusion/ej2-react-lineargauge';

ReactDOM.render(
    <LinearGaugeComponent>
        <Inject services={[Annotations]}/>
        <AnnotationsDirective>
            <AnnotationDirective content='#fruits' x={100} zIndex='1' y={100}>
            </AnnotationDirective>
        </AnnotationsDirective>
    </LinearGaugeComponent>,document.getElementById('gauge'));

```

## Customization

The following properties are used to customize the annotation.

* [`zIndex`](../api/linear-gauge/annotation/#zindex) - This property is used to bring the annotation to the front or back, when annotation overlaps with another element.
* [`axisValue`](../api/linear-gauge/annotation/#axisvalue) - This property is used to place the annotation in the specified axis value with respect to the provided axis index.
* [`axisIndex`](../api/linear-gauge/annotation/#axisindex) - This property is used to place the annotation in the specified axis with respect to the provided axis value.
* [`horizontalAlignment`](../api/linear-gauge/annotation#horizontalalignment) - This property is used to place the annotation horizontally.
* [`verticalAlignment`](../api/linear-gauge/annotation#verticalalignment) - This property is used to place the annotation vertically.
* [`x`](../api/linear-gauge/annotation/#x-number), [`y`](../api/linear-gauge/annotation/#y-number) - This property is used to place the annotation in the specified location.

### Changing the z-index

To change the stack order of an annotation element, the [`zIndex`](../api/linear-gauge/annotation/#zindex) property of the [`AnnotationDirective`](../api/linear-gauge/annotation/) can be used.

{% tab template="linear-gauge/annotations", compileJsx=true sourceFiles="app/**/*.tsx" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { LinearGaugeComponent, AnnotationsDirective, AnnotationDirective, Annotations,Inject } from '@syncfusion/ej2-react-lineargauge';

ReactDOM.render(
    <LinearGaugeComponent  id='gauge'>
        <Inject services={[Annotations]}/>
        <AnnotationsDirective>
            <AnnotationDirective content='<div id="first"><h1>Gauge</h1></div>' zIndex='1' >
            </AnnotationDirective>
        </AnnotationsDirective>
    </LinearGaugeComponent>,document.getElementById('gauge'));

```

{% endtab %}

### Positioning an annotation

The annotation can be placed anywhere in the Linear Gauge by setting the pixel value to the [`x`](../api/linear-gauge/annotation/#x) and [`y`](../api/linear-gauge/annotation/#y) properties in the [`AnnotationDirective`](../api/linear-gauge/annotation/).

{% tab template="linear-gauge/annotations", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { LinearGaugeComponent, AnnotationsDirective, AnnotationDirective, Annotations, Inject } from '@syncfusion/ej2-react-lineargauge';

ReactDOM.render(
    <LinearGaugeComponent  id='gauge'>
        <Inject services={[Annotations]}/>
        <AnnotationsDirective>
            <AnnotationDirective content='<div id="first"><h1>Gauge</h1></div>' x={100} y={100} zIndex='1' >
            </AnnotationDirective>
        </AnnotationsDirective>
    </LinearGaugeComponent>,document.getElementById('gauge'));

```

{% endtab %}

<!-- markdownlint-disable MD036 -->

### Alignment of annotation

The annotation can be aligned horizontally and vertically by using the [`horizontalAlignment`](../api/linear-gauge/annotation/#horizontalalignment) and [`verticalAlignment`](../api/linear-gauge/annotation/#verticalalignment) properties respectively. The possible values can be "**Center**", "**Far**", "**Near**", and "**None**". The [`horizontalAlignment`](../api/linear-gauge/annotation/#horizontalalignment) and [`verticalAlignment`](../api/linear-gauge/annotation/#verticalalignment) properties are not applicable when the [`x`](../api/linear-gauge/annotation/#x) and [`y`](../api/linear-gauge/annotation/#y) properties are set in the [`AnnotationDirective`](../api/linear-gauge/annotation/).

{% tab template="linear-gauge/annotations", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { LinearGaugeComponent, AnnotationsDirective, AnnotationDirective, Annotations, Inject } from '@syncfusion/ej2-react-lineargauge';

ReactDOM.render(
    <LinearGaugeComponent  id='gauge'>
        <Inject services={[Annotations]}/>
        <AnnotationsDirective>
            <AnnotationDirective content='<div id="first"><h1>Gauge</h1></div>' verticalAlignment="Center" horizontalAlignment="Center" zIndex='1' >
            </AnnotationDirective>
        </AnnotationsDirective>
    </LinearGaugeComponent>,document.getElementById('gauge'));

```

{% endtab %}

## Multiple annotations

Multiple annotations can be added to the Linear Gauge component by adding the multiple [`AnnotationDirective`](../api/linear-gauge/annotation/) in the [`AnnotationsDirective`](../api/linear-gauge/#annotations) and customization for the annotation can be done with the [`AnnotationDirective`](../api/linear-gauge/annotation/).

{% tab template="linear-gauge/annotations", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { LinearGaugeComponent, AnnotationsDirective, AnnotationDirective, Annotations, Inject } from '@syncfusion/ej2-react-lineargauge';

ReactDOM.render(
    <LinearGaugeComponent  id='gauge'>
        <Inject services={[Annotations]}/>
        <AnnotationsDirective>
            <AnnotationDirective content='<div><h1 style="color:red;">Speed</h1></div>' verticalAlignment='Near' horizontalAlignment='Center' zIndex='1'>
            </AnnotationDirective>
            <AnnotationDirective content='<div><h1 style="color:blue;">Meter</h1></div>' zIndex='1' x={150} y={400}>
            </AnnotationDirective>
        </AnnotationsDirective>
    </LinearGaugeComponent>,document.getElementById('gauge'));

```

{% endtab %}
