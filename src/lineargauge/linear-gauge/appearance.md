---
title: " Appearance in React Linear Gauge component | Syncfusion "

component: "Linear Gauge"

description: "Learn here all about the Appearance of Syncfusion React Linear Gauge component and more."
---

# Appearance in React Linear Gauge

<!-- markdownlint-disable MD013 -->

## Customizing the Linear Gauge area

The following properties are available in the [`LinearGaugeComponent`](../api/linear-gauge/) to customize the Linear Gauge area.

* [`background`](../api/linear-gauge/#background) - Applies the background color for the Linear Gauge.
* [`border`](../api/linear-gauge/#border) - To customize the color and width of the border in Linear Gauge.
* [`margin`](../api/linear-gauge/#margin) - To customize the margins of the Linear Gauge.

{% tab template="linear-gauge/appearance", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { LinearGaugeComponent } from '@syncfusion/ej2-react-lineargauge';

ReactDOM.render(
    <LinearGaugeComponent id='gauge' background='skyblue' border= { { color: "#FF0000", width: 2 } }
        margin= { { left: 40, right: 40, top: 40, bottom: 40 } }>
    </LinearGaugeComponent>,document.getElementById('gauge'));

```

{% endtab %}

## Setting up the Linear Gauge title

The title for the Linear Gauge can be set using [`title`](../api/linear-gauge/#title) property in [`LinearGaugeComponent`](../api/linear-gauge/). Its appearance can be customized using the [`titleStyle`](../api/linear-gauge/#titlestyle) with the below properties.

* [`color`](../api/linear-gauge/fontModel/#color) - Specifies the text color of the title.
* [`fontStyle`](../api/linear-gauge/fontModel/#fontStyle) - Specifies the font style of the title.
* [`fontWeight`](../api/linear-gauge/fontModel/#fontweight) - Specifies the font weight of the title.
* [`size`](../api/linear-gauge/fontModel/#size) - Specifies the font size of the title.
* [`opacity`](../api/linear-gauge/fontModel/#opacity) - Specifies the opacity of the title.
* [`fontFamily`](../api/linear-gauge/fontModel/#fontfamily) - Specifies the font family of the title.

{% tab template="linear-gauge/appearance", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { LinearGaugeComponent } from '@syncfusion/ej2-react-lineargauge';

ReactDOM.render(
    <LinearGaugeComponent id='gauge' title='linear gauge'
        titleStyle={ { fontFamily:'Arial', fontStyle:'italic', fontWeight:'regular', color:'#E27F2D', size:'23px' } }>
    </LinearGaugeComponent>,document.getElementById('gauge'));

```

{% endtab %}

## Customizing the Linear Gauge container

The area used to render the ranges and pointers at the center position of the gauge is called container. It is of three types namely,

* Normal
* Rounded Rectangle
* Thermometer

The type of the container can be modified by using the [`type`](../api/linear-gauge/containerModel/#type) property in [`container`](../api/linear-gauge/containerModel/). The container can be customized by using the following properties in [`container`](../api/linear-gauge/containerModel/).

* [`offset`](../api/linear-gauge/containerModel/#offset) - To place the container with the specified distance from the axis of the Linear Gauge.
* [`width`](../api/linear-gauge/containerModel/#width) - To set the thickness of the container.
* [`height`](../api/linear-gauge/containerModel/#height) - To set the length of the container.
* [`backgroundColor`](../api/linear-gauge/containerModel/#backgroundcolor) - To set the background color of the container.
* [`border`](../api/linear-gauge/container/#border) - To set the color and width for the border of the container.

### Normal

The "**Normal**" type will render the container as a rectangle and this is the default container type.

{% tab template="linear-gauge/appearance", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { LinearGaugeComponent, AxesDirective, AxisDirective , PointersDirective, PointerDirective } from '@syncfusion/ej2-react-lineargauge';

ReactDOM.render(
    <LinearGaugeComponent id='gauge' container={ { width:30 } }>
        <AxesDirective>
            <AxisDirective>
                <PointersDirective>
                    <PointerDirective value={50} width={15} type='Bar'>
                    </PointerDirective>
                </PointersDirective>
            </AxisDirective>
        </AxesDirective>
    </LinearGaugeComponent>,document.getElementById('gauge'));

```

{% endtab %}

### Rounded Rectangle

The "**RoundedRectangle**" type will render the container as a rectangle with rounded corner radius. The rounded corner radius of the container can be customized using the [`roundedCornerRadius`](../api/linear-gauge/container/#roundedcornerradius) property in [`container`](../api/linear-gauge/containerModel/).

{% tab template="linear-gauge/appearance", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { LinearGaugeComponent, AxesDirective, AxisDirective , PointersDirective, PointerDirective } from '@syncfusion/ej2-react-lineargauge';

ReactDOM.render(
    <LinearGaugeComponent id='gauge' container={ { width:30, type:'RoundedRectangle' } }>
        <AxesDirective>
            <AxisDirective>
                <PointersDirective>
                    <PointerDirective value={50} width={15} type='Bar'>
                    </PointerDirective>
                </PointersDirective>
            </AxisDirective>
        </AxesDirective>
    </LinearGaugeComponent>,document.getElementById('gauge'));

```

{% endtab %}

### Thermometer

The "**Thermometer**" type will render the container similar to the appearance of thermometer.

{% tab template="linear-gauge/appearance", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { LinearGaugeComponent, AxesDirective, AxisDirective , PointersDirective, PointerDirective } from '@syncfusion/ej2-react-lineargauge';

ReactDOM.render(
    <LinearGaugeComponent id='gauge' container={ { width:30, type:'Thermometer' } }>
        <AxesDirective>
            <AxisDirective>
                <PointersDirective>
                    <PointerDirective value={50} width={15} type='Bar'>
                    </PointerDirective>
                </PointersDirective>
            </AxisDirective>
        </AxesDirective>
    </LinearGaugeComponent>,document.getElementById('gauge'));

```

{% endtab %}

## Fitting the Linear Gauge to the control

The Linear Gauge component is rendered with margin by default. To remove the margin around the Linear Gauge, the [`allowMargin`](../api/linear-gauge/#allowmargin) property in [`LinearGaugeComponent`](../api/linear-gauge/) is set as "**false**".

{% tab template="linear-gauge/appearance", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { LinearGaugeComponent } from '@syncfusion/ej2-react-lineargauge';

ReactDOM.render(
    <LinearGaugeComponent allowMargin={false} id='gauge' height="100%" width="100%" orientation='Horizontal' margin= {{ left: 0, right: 0, top: 0, bottom: 0 }} border= {{ width: 2, color: "red" }}>
    </LinearGaugeComponent>,document.getElementById('gauge'));

```

{% endtab %}

> Note: To use this feature, set the [`allowMargin`](../api/linear-gauge/#allowmargin) property to "**false**", the [`width`](../api/linear-gauge/#width) property to "**100%**" and the properties of [`margin`](../api/linear-gauge/#margin) to "**0**".