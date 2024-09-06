---
title: " Getting started with React Linear Gauge component | Syncfusion "

component: "Linear Gauge"

description: "Learn here about getting started with Syncfusion React Linear Gauge component, its element, and more."
---

# Getting Started with React Linear Gauge

<!-- markdownlint-disable MD013 -->

This section explains you the steps required to create a simple Linear Gauge and demonstrate the basic usage of the Linear Gauge control.

## Dependencies

Below is the list of minimum dependencies required to use the linear gauge component.

```javascript
+-- @syncfusion/ej2-react-lineargauge
|-- @syncfusion/ej2-lineargauge
    |-- @syncfusion/ej2-base
    |-- @syncfusion/ej2-popups
        |-- @syncfusion/ej2-buttons
|-- @syncfusion/ej2-react-base
```

## Installation and configuration

Use the [`create-react-app`](https://github.com/facebookincubator/create-react-app) to setup the applications.
To get started, run the below command to create a react app.

```sh
npm install -g create-react-app
```

* Start a new project using create-react-app command as follows

<div class='tsx'>

```sh
create-react-app quickstart --scripts-version=react-scripts-ts

cd quickstart

npm install

```

</div>

* To install the Linear Gauge component, use the following command.

```sh
npm install @syncfusion/ej2-react-lineargauge --save
```

## Adding Linear Gauge component to the Project

Now, you can start adding Linear Gauge components to the application. For getting started, add the Linear Gauge component in the **src/index.tsx** file using following code.

{% tab compileJsx=true%}

```tsx

import * as React from 'react';
import { LinearGaugeComponent } from '@syncfusion/ej2-react-lineargauge';

class App extends React.Component {
render() {
   return (<LinearGaugeComponent></LinearGaugeComponent>);
  }
}
export default App;

```

{% endtab %}

## Module Injection

Linear gauge component are segregated into individual feature-wise modules. In order to use a particular feature,
inject its feature service in the **AppModule**. Please find the feature service name and description as follows.

* `Annotations` - Inject this module in to `services` to use annotation feature.
* `GaugeTooltip` - Inject this module in to `services` to use tooltip feature.

These modules should be injected into the `services` section as follows,

{% tab compileJsx=true%}

 ```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { LinearGaugeComponent, Annotations, GaugeTooltip} from '@syncfusion/ej2-react-lineargauge';

ReactDOM.render(<LinearGaugeComponent id='gauge'></LinearGaugeComponent>,
 <Inject services={[Annotations, GaugeTooltip]}/>
document.getElementById('gauge'));

```

{% endtab %}

## Adding the Linear Gauge Title

The title can be added to the Linear Gauge component using the [`title`](../api/linear-gauge/linearGaugeModel#title-string) property in the Linear Gauge.

{% tab template="linear-gauge/getting-started", compileJsx=true, sourceFiles="app/**/*.tsx",  isDefaultActive=true %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { LinearGaugeComponent } from '@syncfusion/ej2-react-lineargauge';

ReactDOM.render(
    <LinearGaugeComponent id='gauge' title='Linear Gauge'>
    </LinearGaugeComponent>,document.getElementById('gauge'));

```

{% endtab %}

## Axis Range

The range of the axis can be set using the [`minimum`](../api/linear-gauge/axis#minimum-number) and [`maximum`](../api/linear-gauge/axis#maximum-number) properties in the Linear Gauge.

{% tab template="linear-gauge/getting-started", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { LinearGaugeComponent, AxesDirective, AxisDirective } from '@syncfusion/ej2-react-lineargauge';

ReactDOM.render(
    <LinearGaugeComponent id='gauge'>
        <AxesDirective>
            <AxisDirective minimum={0} maximum={200}>
            </AxisDirective>
        </AxesDirective>
    </LinearGaugeComponent>,document.getElementById('gauge'));

```

{% endtab %}

To denote the axis values with temperature units, add the °C as suffix to each label. This can be achieved by setting the **{value}°C** to the [`format`](../api/linear-gauge/labelModel/#format-string) property in the [`labelStyle`](../api/linear-gauge/axis#labelstyle-labelmodel) object of the axis. Here, **{value}** acts as a placeholder for each axis label.

To change the pointer value from the default value of the gauge, set the [`value`](../api/linear-gauge/pointer/#value-number) property in [`pointers`](../api/linear-gauge/pointerModel/) object of the axis.

{% tab template="linear-gauge/getting-started", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { LinearGaugeComponent, AxesDirective, AxisDirective, PointersDirective, PointerDirective, RangesDirective, RangeDirective } from '@syncfusion/ej2-react-lineargauge';

ReactDOM.render(
    <LinearGaugeComponent id='gauge'>
        <AxesDirective>
            <AxisDirective minimum={0} maximum={200} labelStyle={ { format:'{value}°C' } }>
                <PointersDirective>
                    <PointerDirective value={140}>
                    </PointerDirective>
                </PointersDirective>
                <RangesDirective>
                    <RangeDirective start={0} end={80} startWidth={15} endWidth={15}>
                    </RangeDirective>
                    <RangeDirective start={80} end={120} startWidth={15} endWidth={15}>
                    </RangeDirective>
                    <RangeDirective start={120} end={140} startWidth={15} endWidth={15}>
                    </RangeDirective>
                    <RangeDirective start={140} end={200} startWidth={15} endWidth={15}>
                    </RangeDirective>
                </RangesDirective>
            </AxisDirective>
        </AxesDirective>
    </LinearGaugeComponent>,document.getElementById('gauge'));

```

{% endtab %}

## Setting the value of the pointer

The pointer value is changed in the below sample using the [`value`](../api/linear-gauge/pointer/#value-number) property in [`pointers`](../api/linear-gauge/pointer) object of the axis.

{% tab template="linear-gauge/getting-started", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { LinearGaugeComponent, AxesDirective, AxisDirective, PointersDirective, PointerDirective } from '@syncfusion/ej2-react-lineargauge';

ReactDOM.render(
    <LinearGaugeComponent id='gauge'>
        <AxesDirective>
            <AxisDirective minimum={0} maximum={200}>
                <PointersDirective>
                    <PointerDirective value={140} color='green'>
                    </PointerDirective>
                </PointersDirective>
            </AxisDirective>
        </AxesDirective>
    </LinearGaugeComponent>,document.getElementById('gauge'));

```

{% endtab %}