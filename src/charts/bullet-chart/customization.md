---
title: " Bullet Chart Customization | React "

component: "Bullet Chart"

description: "Bullet Chart have different customizable features like different orientation, flow directions and animation features"
---

# Customization

## Orientation

The Bullet Chart can be rendered in different orientations such as **Horizontal** or **Vertical** via the [`orientation`](https://ej2.syncfusion.com/react/documentation/api/bullet-chart/#orientation) property. By default, the Bullet Chart is rendered in the **Horizontal** orientation.

{% tab template="bullet-chart/customization", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import { BulletChartComponent, Inject} from '@syncfusion/ej2-react-charts';
import { BulletRangeCollectionDirective, BulletRangeDirective} from '@syncfusion/ej2-react-charts';
import * as React from "react";
import * as ReactDOM from "react-dom";

class App extends React.Component<{}, {}>{
  render() {
    return (<BulletChartComponent id='ranges'
                animation={{ enable: false }}
                        valueField='value'
                        targetField='target'
                        title='Sales Rate in dollars'
                        width='20%'
                        orientation='vertical'
                        minimum={0}
                        maximum={100}
                        interval={20}
                        dataSource={[{value: 55, target: 45}]}>
                        <BulletRangeCollectionDirective>
                            <BulletRangeDirective end={35}></BulletRangeDirective>
                            <BulletRangeDirective end={50}></BulletRangeDirective>
                            <BulletRangeDirective end={100}></BulletRangeDirective>
                        </BulletRangeCollectionDirective>
            </BulletChartComponent>);
  }
};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Right-to-left (RTL)

The Bullet Chart supports the right-to-left rendering that can be enabled by setting the [`enableRtl`](https://ej2.syncfusion.com/react/documentation/api/bullet-chart/#enablertl) property to **true**.

{% tab template="bullet-chart/customization", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import { BulletChartComponent, Inject} from '@syncfusion/ej2-react-charts';
import { BulletRangeCollectionDirective, BulletRangeDirective} from '@syncfusion/ej2-react-charts';
import * as React from "react";
import * as ReactDOM from "react-dom";

class App extends React.Component<{}, {}>{
  render() {
    return (<BulletChartComponent id='ranges'
                animation={{ enable: false }}
                        valueField='value'
                        targetField='target'
                        enableRtl={true}
                        minimum={0}
                        maximum={2000}
                        interval={200}
                        dataSource={[{value: 1500, target: 1000}]}>
                        <BulletRangeCollectionDirective>
                            <BulletRangeDirective end={500} color='red' ></BulletRangeDirective>
                            <BulletRangeDirective end={1500} color='blue'></BulletRangeDirective>
                            <BulletRangeDirective end={2000} color='green'></BulletRangeDirective>
                        </BulletRangeCollectionDirective>
            </BulletChartComponent>);
  }
};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Animation

The actual and the target bar supports the linear animation via the [`animation`](https://ej2.syncfusion.com/react/documentation/api/bullet-chart/#animation) setting. The speed and the delay are controlled using the `duration` and `delay` properties respectively.

{% tab template="bullet-chart/customization", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import { BulletChartComponent, Inject} from '@syncfusion/ej2-react-charts';
import { BulletRangeCollectionDirective, BulletRangeDirective} from '@syncfusion/ej2-react-charts';
import * as React from "react";
import * as ReactDOM from "react-dom";

class App extends React.Component<{}, {}>{
  render() {
    return (<BulletChartComponent id='ranges'
                animation={{ enable: true }}
                        valueField='value'
                        targetField='target'
                        minimum={0}
                        maximum={2000}
                        interval={200}
                        dataSource={[{value: 1500, target: 1000}]}>
                        <BulletRangeCollectionDirective>
                            <BulletRangeDirective end={500} color='red' ></BulletRangeDirective>
                            <BulletRangeDirective end={1500} color='blue'></BulletRangeDirective>
                            <BulletRangeDirective end={2000} color='green'></BulletRangeDirective>
                        </BulletRangeCollectionDirective>
            </BulletChartComponent>);
  }
};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Theme

The Bullet Chart supports different type of themes via the [`theme`](https://ej2.syncfusion.com/react/documentation/api/bullet-chart/#theme) property.

{% tab template="bullet-chart/customization", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import { BulletChartComponent, Inject} from '@syncfusion/ej2-react-charts';
import { BulletRangeCollectionDirective, BulletRangeDirective} from '@syncfusion/ej2-react-charts';
import * as React from "react";
import * as ReactDOM from "react-dom";

class App extends React.Component<{}, {}>{
  render() {
    return (<BulletChartComponent id='ranges'
                animation={{ enable: false }}
                        valueField='value'
                        targetField='target'
                        title='Profit in %'
                        theme='HighContrast'
                        minimum={0}
                        maximum={100}
                        interval={10}
                        dataSource={[{value: 50, target: 45}]}>
                        <BulletRangeCollectionDirective>
                            <BulletRangeDirective end={15} color='red' ></BulletRangeDirective>
                            <BulletRangeDirective end={50} color='blue'></BulletRangeDirective>
                            <BulletRangeDirective end={100} color='green'></BulletRangeDirective>
                        </BulletRangeCollectionDirective>
            </BulletChartComponent>);
  }
};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}