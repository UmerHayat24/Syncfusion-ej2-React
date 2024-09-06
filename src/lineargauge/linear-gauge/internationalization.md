---
title: " Internationalization in Rect Linear Gauge component | Syncfusion "

component: "Linear Gauge"

description: "Learn here all about the Internationalization feature of Syncfusion React Linear Gauge component and more."
---

# Internationalization in React Linear Gauge

Globalization is the process of designing and developing a component that works in different cultures. Internationalization is used to globalize the number content in Linear Gauge component using [`format`](../api/linear-gauge/label/#format) property in [`LinearGaugeComponent`](../api/linear-gauge/linearGaugeModel/) class. It has static text on some features such as

* Axis label
* Tooltip

The static text on above features can be changed to any culture such as Arabic, Deutsch and French. To know more about the globalization in React components, refer [here](https://ej2.syncfusion.com/react/documentation/common/internationalization/).

## Numeric Format

The text in axis labels and tooltip can be displayed in the numeric format such as currency, percentage and so on. To know more about the numeric formats in axis labels, refer [here](axis/#displaying-numeric-format-in-labels). In the below example, the axis label is displayed in the currency format.

{% tab template="linear-gauge/internationalization", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { LinearGaugeComponent, AxesDirective, AxisDirective } from '@syncfusion/ej2-react-lineargauge';

ReactDOM.render(
    <LinearGaugeComponent id='gauge' format='c'>
        <AxesDirective>
            <AxisDirective minimum={0} maximum={120} majorTicks={ { interval:10, height:10 } } minorTicks={ { interval:5, height:5 } } >
            </AxisDirective>
        </AxesDirective>
    </LinearGaugeComponent>,document.getElementById('gauge'));

```

{% endtab %}