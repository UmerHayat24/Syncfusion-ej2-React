---
title: " User Interactions in React Linear Gauge component | Syncfusion "

component: "Linear Gauge"

description: "Learn here all about the User Interaction feature of Syncfusion React Linear Gauge component and more."
---

# User Interaction in React Linear Gauge

<!-- markdownlint-disable MD013 -->

## Tooltip

<!-- markdownlint-disable MD036 -->

Linear Gauge displays the details about a pointer value through [`tooltip`](../api/linear-gauge/tooltipSettings/), when the mouse hovers over the pointer. To enable the tooltip, set [`enable`](../api/linear-gauge/tooltipSettings/#enable) property as "**true**" and inject **GaugeTooltip** into **services**.

{% tab template="linear-gauge/user-interaction", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { LinearGaugeComponent, AxesDirective, AxisDirective, PointersDirective, PointerDirective,GaugeTooltip, Inject } from '@syncfusion/ej2-react-lineargauge';

ReactDOM.render(
    <LinearGaugeComponent id='gauge' tooltip={ { enable: true } }>
        <Inject services={[GaugeTooltip]}/>
        <AxesDirective>
            <AxisDirective>
                <PointersDirective>
                    <PointerDirective value={80}>
                    </PointerDirective>
                </PointersDirective>
            </AxisDirective>
        </AxesDirective>
    </LinearGaugeComponent>,document.getElementById('gauge'));

```

{% endtab %}

<!-- markdownlint-disable MD013 -->

### Tooltip format

<!-- markdownlint-disable MD013 -->
Tooltip in the Linear Gauge control can be formatted using the [`format`](../api/linear-gauge/tooltipSettings/#format) property in [`tooltip`](../api/linear-gauge/tooltipSettings/). It is used to render the tooltip in certain format or to add a user-defined unit in the tooltip. By default, the tooltip shows the pointer value only. In addition to that, more information can be added in the tooltip. For example, the format "**{value}km**" shows pointer value with kilometer unit in the tooltip.

{% tab template="linear-gauge/user-interaction", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { LinearGaugeComponent, AxesDirective, AxisDirective, PointersDirective, PointerDirective, GaugeTooltip, Inject } from '@syncfusion/ej2-react-lineargauge';

ReactDOM.render(
    <LinearGaugeComponent id='gauge' tooltip={ { enable: true, format: '{value}km' } }>
    <Inject services={[GaugeTooltip]}/>
        <AxesDirective>
            <AxisDirective>
                <PointersDirective>
                    <PointerDirective value={80}>
                    </PointerDirective>
                </PointersDirective>
            </AxisDirective>
        </AxesDirective>
    </LinearGaugeComponent>,document.getElementById('gauge'));

```

{% endtab %}

### Tooltip Template

The HTML elements rendered in the tooltip of the Linear Gauge using the [`template`](../api/linear-gauge/tooltipSettings/#template) property of the [`tooltip`](../api/linear-gauge/tooltipSettings/). The "**${value}**" can be used as placeholders in the HTML element to display the pointer values of the corresponding axis.

{% tab template="linear-gauge/user-interaction", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { LinearGaugeComponent, AxesDirective, AxisDirective, PointersDirective, PointerDirective, GaugeTooltip, Inject } from '@syncfusion/ej2-react-lineargauge';

ReactDOM.render(
    <LinearGaugeComponent id='gauge' tooltip={ { enable: true, template: '<div>Pointer: 80 </div>' } }>
    <Inject services={[GaugeTooltip]}/>
        <AxesDirective>
            <AxisDirective>
                <PointersDirective>
                    <PointerDirective value={80}>
                    </PointerDirective>
                </PointersDirective>
            </AxisDirective>
        </AxesDirective>
    </LinearGaugeComponent>,document.getElementById('gauge'));

```

{% endtab %}

### Customize the appearance of the tooltip

The tooltip can be customized using the following properties in [`tooltip`](../api/linear-gauge/tooltipSettings/).

* [`fill`](../api/linear-gauge/tooltipSettings/#fill) - To fill the color for tooltip.
* [`enableAnimation`](../api/linear-gauge/tooltipSettings/#enableanimation) - To enable or disable the tooltip animation.
* [`border`](../api/linear-gauge/tooltipSettings/#border) - To set the color and width for the border of the tooltip.
* [`textStyle`](../api/linear-gauge/tooltipSettings/#textstyle) - To customize the style of the text in tooltip.
* [`showAtMousePosition`](../api/linear-gauge/tooltipSettings/#showatmouseposition) - To show the tooltip at the mouse position.

{% tab template="linear-gauge/user-interaction", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { LinearGaugeComponent, AxesDirective, AxisDirective, PointersDirective, PointerDirective, GaugeTooltip, Inject } from '@syncfusion/ej2-react-lineargauge';

ReactDOM.render(
    <LinearGaugeComponent id='gauge' tooltip={ { enable: true, fill: '#e5bcbc', border: { color: '#000000' } } }>
    <Inject services={[GaugeTooltip]}/>
        <AxesDirective>
            <AxisDirective>
                <PointersDirective>
                    <PointerDirective value={80}>
                    </PointerDirective>
                </PointersDirective>
            </AxisDirective>
        </AxesDirective>
    </LinearGaugeComponent>,document.getElementById('gauge'));

```

{% endtab %}

### Positioning the tooltip

The tooltip is positioned at the "**End**" of the pointer. To change the position of the tooltip at the start, or center of the pointer, set the [`position`](../api/linear-gauge/tooltipSettings/#position) property to "**Start**" or "**Center**".

{% tab template="linear-gauge/user-interaction", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { LinearGaugeComponent, AxesDirective, AxisDirective, PointersDirective, PointerDirective, GaugeTooltip, Inject } from '@syncfusion/ej2-react-lineargauge';

ReactDOM.render(
    <LinearGaugeComponent id='gauge' tooltip={ { enable: true, position: "Center" } }>
    <Inject services={[GaugeTooltip]}/>
        <AxesDirective>
            <AxisDirective>
                <PointersDirective>
                    <PointerDirective value={80} type="Bar">
                    </PointerDirective>
                </PointersDirective>
            </AxisDirective>
        </AxesDirective>
    </LinearGaugeComponent>,document.getElementById('gauge'));

```

{% endtab %}

## Pointer Drag

To drag either marker or bar pointer to the desired axis value, set the [`enableDrag`](../api/linear-gauge/pointer/#enabledrag) property as "**true**" in the [`PointerDirective`](../api/linear-gauge/pointerModel/).

{% tab template="linear-gauge/user-interaction", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { LinearGaugeComponent, AxesDirective, AxisDirective, PointersDirective, PointerDirective } from '@syncfusion/ej2-react-lineargauge';

ReactDOM.render(
    <LinearGaugeComponent id='gauge'>
        <AxesDirective>
            <AxisDirective>
                <PointersDirective>
                    <PointerDirective value={80} enableDrag={true}>
                    </PointerDirective>
                </PointersDirective>
            </AxisDirective>
        </AxesDirective>
    </LinearGaugeComponent>,document.getElementById('gauge'));

```

{% endtab %}