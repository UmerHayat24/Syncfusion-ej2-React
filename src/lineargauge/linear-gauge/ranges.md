---
title: " Ranges in React Linear Gauge component | Syncfusion "

component: "Linear Gauge"

description: "Learn here all about the Ranges feature of Syncfusion React Linear Gauge component and more."
---

# Ranges in React Linear Gauge

<!-- markdownlint-disable MD013 -->
Range is the set of values in the axis. The range can be defined using the [`start`](../api/linear-gauge/rangeModel/#start) and [`end`](../api/linear-gauge/rangeModel/#end) properties in the [`RangeDirective`](../api/linear-gauge/rangeModel/). Any number of ranges can be added to the Linear Gauge using the [`RangesDirective`](../api/linear-gauge/axisModel/#ranges).

{% tab template="linear-gauge/ranges", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { LinearGaugeComponent, AxesDirective, AxisDirective, RangesDirective, RangeDirective } from '@syncfusion/ej2-react-lineargauge';

ReactDOM.render(
    <LinearGaugeComponent id='gauge'>
        <AxesDirective>
            <AxisDirective>
                <RangesDirective>
                    <RangeDirective start={50} end={80}>
                    </RangeDirective>
                </RangesDirective>
            </AxisDirective>
        </AxesDirective>
    </LinearGaugeComponent>,document.getElementById('gauge'));

```

{% endtab %}

## Customizing the range

Ranges can be customized using the following properties in [`RangeDirective`](../api/linear-gauge/rangeModel/).

* [`startWidth`](../api/linear-gauge/rangeModel/#startwidth) - To set the thickness of the range at the start axis value.
* [`endWidth`](../api/linear-gauge/rangeModel/#endwidth) - To set the thickness of the range at the end axis value.
* [`color`](../api/linear-gauge/rangeModel/#color) - To set the color of the range.
* [`position`](../api/linear-gauge/rangeModel/#position) - To place the range. By default, the range is placed outside of the axis. To change the position, this property can be set as "**Inside**", "**Outside**", "**Cross**", or "**Auto**".
* [`offset`](../api/linear-gauge/rangeModel/#offset) - To place the range with the specified distance from the axis.
* [`border`](../api/linear-gauge/rangeModel/#border) - To set the color and width for the border of the range.

{% tab template="linear-gauge/ranges", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { LinearGaugeComponent, AxesDirective, AxisDirective, RangesDirective, RangeDirective } from '@syncfusion/ej2-react-lineargauge';

ReactDOM.render(
    <LinearGaugeComponent id='gauge'>
        <AxesDirective>
            <AxisDirective>
                <RangesDirective>
                    <RangeDirective start={50} end={80} statWidth={10} endWidth={20} color='red'>
                    </RangeDirective>
                </RangesDirective>
            </AxisDirective>
        </AxesDirective>
    </LinearGaugeComponent>,document.getElementById('gauge'));

```

{% endtab %}

## Setting the range color for the labels

To set the color of the labels like the range color, set the [`useRangeColor`](../api/linear-gauge/labelModel/#userangecolor) property as "**true**" in the [`labelStyle`](../api/linear-gauge/axis/#labelstyle).

{% tab template="linear-gauge/ranges", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { LinearGaugeComponent, AxesDirective, AxisDirective, RangesDirective, RangeDirective } from '@syncfusion/ej2-react-lineargauge';

ReactDOM.render(
    <LinearGaugeComponent id='gauge'>
        <AxesDirective>
            <AxisDirective labelStyle={{ useRangeColor: true}}>
                <RangesDirective>
                    <RangeDirective start={50} end={80} statWidth={10} endWidth={10} color='red'>
                    </RangeDirective>
                </RangesDirective>
            </AxisDirective>
        </AxesDirective>
    </LinearGaugeComponent>,document.getElementById('gauge'));

```

{% endtab %}

## Multiple ranges

Multiple ranges can be added to the Linear Gauge by adding multiple [`RangeDirective`](../api/linear-gauge/rangeModel/) in the [`RangesDirective`](../api/linear-gauge/axisModel/#ranges) class and customization for the ranges can be done with [`RangeDirective`](../api/linear-gauge/rangeModel/).

{% tab template="linear-gauge/ranges", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { LinearGaugeComponent, AxesDirective, AxisDirective, RangesDirective, RangeDirective } from '@syncfusion/ej2-react-lineargauge';

ReactDOM.render(
    <LinearGaugeComponent id='gauge'>
        <AxesDirective>
            <AxisDirective>
                <RangesDirective>
                    <RangeDirective start={0} end={30} statWidth={10} endWidth={10} color='#41f47f'>
                    </RangeDirective>
                    <RangeDirective start={30} end={50} statWidth={10} endWidth={10} color='#f49441'>
                    </RangeDirective>
                    <RangeDirective start={50} end={100} statWidth={10} endWidth={10} color='#cd41f4'>
                    </RangeDirective>
                </RangesDirective>
            </AxisDirective>
        </AxesDirective>
    </LinearGaugeComponent>,document.getElementById('gauge'));

```

{% endtab %}

## Gradient Color

Gradient support allows the addition of multiple colors in the range of the Linear Gauge. The following gradient types are supported in the Linear Gauge.

* Linear Gradient
* Radial Gradient

### Linear Gradient

Using linear-gradient, colors will be applied in a linear progression. The start value of the linear gradient can be set using the [`startValue`](../api/linear-gauge/linearGradient/#startvalue) property. The end value of the linear gradient will be set using the [`endValue`](../api/linear-gauge/linearGradient/#endvalue) property. The color stop values such as [`color`](../api/linear-gauge/colorStopModel/#color), [`opacity`](../api/linear-gauge/colorStopModel/#opacity), and [`offset`](../api/linear-gauge/colorStopModel/#offset) are set using [`colorStop`](../api/linear-gauge/linearGradient/#colorstop) property. The linear gradient can be rendered for the range in the Linear Gauge by using the below example.

{% tab template="linear-gauge/ranges", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { LinearGaugeComponent, AxesDirective, AxisDirective, PointersDirective, PointerDirective, RangesDirective, Gradient, Inject, RangeDirective } from '@syncfusion/ej2-react-lineargauge';

ReactDOM.render(
    <LinearGaugeComponent id='gauge' container={{width: 30, offset: 30}} orientation="Horizontal">
    <Inject services={[Gradient]}/>
        <AxesDirective>
            <AxisDirective minimum={0} maximum={100} line={{width: 0}} majorTicks={{width: 0, interval:25}}
                minorTicks={{width:  0}} labelStyle={{font: {color: '#424242'}, offset: 70}}>
                <PointersDirective>
                    <PointerDirective value={80} height={25} width={35} placement="Near" offset={-44} markerType="Triangle" color= '#f54ea2'>
                    </PointerDirective>
                </PointersDirective>
                <RangesDirective>
                    <RangeDirective start={0} end={80} startWidth={30} endWidth={30} color="#f54ea2" offset={30}
                        linearGradient = {{
                            startValue: '0%',
                            endValue: '100%',
                            colorStop: [
                            { color: '#fef3f9', offset: '0%', opacity: 1 },
                            { color: '#f54ea2', offset: '100%', opacity: 1 }]
                        }}>
                    </RangeDirective>
                </RangesDirective>
            </AxisDirective>
        </AxesDirective>
    </LinearGaugeComponent>,document.getElementById('gauge'));

```

{% endtab %}

### Radial Gradient

Using radial gradient, colors will be applied in circular progression. The inner circle position of the radial gradient will be set using the [`innerPosition`](../api/linear-gauge/radialGradient/#innerposition) property. The outer circle position of the radial gradient can be set using the [`outerPosition`](../api/linear-gauge/radialGradient/#outerposition) property. The color stop values such as [`color`](../api/linear-gauge/colorStopModel/#color), [`opacity`](../api/linear-gauge/colorStopModel/#opacity) and [`offset`](../api/linear-gauge/colorStopModel/#offset) are set using [`colorStop`](../api/linear-gauge/radialGradient/#colorstop) property. The radial gradient can be rendered for the range in the Linear Gauge by using the below example.

{% tab template="linear-gauge/ranges", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { LinearGaugeComponent, AxesDirective, AxisDirective, PointersDirective, PointerDirective, RangesDirective, Gradient, Inject, RangeDirective } from '@syncfusion/ej2-react-lineargauge';

ReactDOM.render(
    <LinearGaugeComponent id='gauge' container={{width: 30, offset: 30}} orientation="Horizontal">
    <Inject services={[Gradient]}/>
        <AxesDirective>
            <AxisDirective minimum={0} maximum={100} line={{width: 0}} majorTicks={{width: 0, interval: 25}}
                minorTicks={{width:  0}} labelStyle={{font: {color: '#424242'}, offset: 70}}>
                <PointersDirective>
                    <PointerDirective value={80} height={25} width={35} placement="Near" offset={-44} markerType="Triangle" color= '#f54ea2'>
                    </PointerDirective>
                </PointersDirective>
                <RangesDirective>
                    <RangeDirective start={0} end={80} startWidth={30} endWidth={30} color="#f54ea2" offset={30}
                        radialGradient = {{
                            radius: '65%',
                            outerPosition: { x: '50%', y: '70%' },
                            innerPosition: { x: '60%', y: '60%' },
                            colorStop: [
                            { color: '#fff5f5', offset: '5%', opacity: 0.9 },
                            { color: '#f54ea2', offset: '100%', opacity: 0.9 }]
                        }}>
                    </RangeDirective>
                </RangesDirective>
            </AxisDirective>
        </AxesDirective>
    </LinearGaugeComponent>,document.getElementById('gauge'));

```

{% endtab %}

> Note: If we set both gradients for the range, only the linear gradient gets rendered. If we set the [`startValue`](../api/linear-gauge/linearGradient/#startvalue) and [`endValue`](../api/linear-gauge/linearGradient/#endvalue) of the [`linearGradient`](../api/linear-gauge/linearGradient/) as empty strings, then the radial gradient gets rendered in the range of the Linear Gauge.