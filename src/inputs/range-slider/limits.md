---
title: "Slider Limits"
component: "Slider"
description: "React slider component supports limits feature that restricts thumb movement in min & max values and also supports interval dragging between range values."
---

# Movement Limits

The slider limits restrict the slider thumb between a particular range. This is used if higher or lower value affects the process
or product where the slider is being used.

The following are the six options in the slider's limits object. Each API in the limits object is optional.

* ``enabled``: Enables the limits in the Slider.
* ``minStart``: Sets the minimum limit for the first handle.
* ``minEnd``: Sets the maximum limit for the first handle.
* ``maxStart``: Sets the minimum limit for the second handle.
* ``maxEnd``: Sets the maximum limit for the second handle.
* ``startHandleFixed``: Locks the first handle.
* ``endHandleFixed``: Locks the second handle.

## Default and MinRange Slider limits

There is only one handle in the Default and MinRange Slider, so ``minStart``, ``minEnd``, and ``startHandleFixed`` options can be used.
When the limits are enabled in the Slider, the limited area becomes darken. So you can differentiate the allowed and restricted area.
Refer to the following snippet to enable the limits in the Slider.

```typescript

    ......

    limits: { enabled: true, minStart: 10, minEnd: 40 }

    ......

```

{% tab template="slider/limits", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html,index.css" %}

```typescript

import * as React from 'react';
import * as ReactDOM from "react-dom";
import { SliderComponent } from '@syncfusion/ej2-react-inputs';

export default class App extends React.Component<{}, {}> {
    public limits: object = { enabled: true, minStart: 10, minEnd: 40 };
    public tooltip: object = { isVisible: true };
    public value: number = 30;
    render() {
        return (
            <div id='container'>
                <div className='wrap'>
                    <div className="sliderwrap">
                        <SliderComponent value={this.value} type='MinRange' min={0} max={100} limits={this.limits}
                        tooltip={this.tooltip} />
                    </div>
                </div>
            </div>
        );
    }
}

ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}

## Range Slider limits

In the range slider, both handles can be restricted and locked from the limit's object. In this sample, the first handle is limited between
10 and 40, and the second handle is limited between 60 and 90.

```typescript

    ......

    limits: { enabled: true, minStart: 10, minEnd: 40, maxStart: 60, maxEnd: 90 }

    ......

```

{% tab template="slider/limits", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html,index.css" %}

```typescript

import * as React from 'react';
import * as ReactDOM from "react-dom";
import { SliderComponent } from '@syncfusion/ej2-react-inputs';

export default class App extends React.Component<{}, {}> {
    public limits: object = { enabled: true, minStart: 10, minEnd: 40, maxStart: 60, maxEnd: 90 };
    public tooltip: object = { isVisible: true };
    public value: number[] = [30, 70];
    render() {
        return (
            <div id='container'>
                <div className='wrap'>
                    <div className="sliderwrap">
                        <SliderComponent value={this.value} type='Range' min={0} max={100} limits={this.limits}
                        tooltip={this.tooltip} />
                    </div>
                </div>
            </div>
        );
    }
}

ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}

## Handle lock

The movement of slider handles can be locked by enabling the ``startHandleFixed`` and ``endHandleFixed`` properties in the limit's object.
In this sample, the movement of both slider handles has been locked.

```typescript

    ......

    limits: { enabled: true, startHandleFixed: true, endHandleFixed: true }

    ......

```

{% tab template="slider/limits", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html,index.css" %}

```typescript

import { Slider } from '@syncfusion/ej2-inputs';

import * as React from 'react';
import * as ReactDOM from "react-dom";
import { SliderComponent } from '@syncfusion/ej2-react-inputs';

export default class App extends React.Component<{}, {}> {
    public limits: object = { enabled: true, startHandleFixed: true, endHandleFixed: true };
    public tooltip: object = { isVisible: true };
    public value: number[] = [30, 70];
    render() {
        return (
            <div id='container'>
                <div className='wrap'>
                    <div className="sliderwrap">
                        <SliderComponent value={this.value} type='Range' min={0} max={100} limits={this.limits}
                        tooltip={this.tooltip} />
                    </div>
                </div>
            </div>
        );
    }
}

ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}