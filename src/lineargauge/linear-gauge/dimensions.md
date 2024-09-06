---
title: " Dimensions in React Linear Gauge component | Syncfusion "

component: "Linear Gauge"

description: "Learn here all about the Dimensions of Syncfusion React Linear Gauge component and more."
---

# Dimensions in React Linear Gauge

<!-- markdownlint-disable MD013 -->

## Size for Linear Gauge

The height and width of the Linear Gauge can be set using the [`width`](../api/linear-gauge/#width) and [`height`](../api/linear-gauge/#height) properties in [`LinearGaugeComponent`](../api/linear-gauge/).

<!-- markdownlint-disable MD036 -->

### In Pixel

The size of the Linear Gauge can be set in pixel as demonstrated below.

{% tab template="linear-gauge/dimensions", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { LinearGaugeComponent } from '@syncfusion/ej2-react-lineargauge';

ReactDOM.render(
    <LinearGaugeComponent id='gauge' width='650px' height='350px'>
    </LinearGaugeComponent>,document.getElementById('gauge'));

```

{% endtab %}

### In Percentage

By setting value in percentage, Linear Gauge receives its dimension matching to its parent. For example, when the height is set as "**50%**", Linear Gauge renders to half of the parent height. The Linear Gauge will be responsive when the width is set as "**100%**".

```html
    <div id='container'>
        <div id='element' style="width:1000px; height:600px;"></div>
    </div>
```

{% tab template="linear-gauge/dimensions", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { LinearGaugeComponent } from '@syncfusion/ej2-react-lineargauge';

ReactDOM.render(
    <LinearGaugeComponent id='gauge' width='100%' height='50%'>
    </LinearGaugeComponent>,document.getElementById('gauge'));

```

{% endtab %}

>Note: When the component's size is not specified, the height will be "**450px**" and the width will be the same as the parent element's width.