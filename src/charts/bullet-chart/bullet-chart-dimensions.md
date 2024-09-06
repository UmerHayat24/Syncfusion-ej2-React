---
title: " Bullet Chart Appearance | React "

component: "Bullet Chart"

description: "We can set bullet-chart size manually by using width and height properties. We can set percentage or pixel size values to the bullet-chart."
---

# Bullet Chart Dimensions

## Size for Container

The size of the Bullet Chart is determined by the container size, and it can be changed inline or via CSS as following.

```html
 <div id="charts" style="width:650px; height:350px"></div>
```

{% tab template="bullet-chart/bullet-chart-dimensions/container", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import { BulletChartComponent, Inject} from '@syncfusion/ej2-react-charts';
import { BulletRangeCollectionDirective, BulletRangeDirective} from '@syncfusion/ej2-react-charts';
import * as React from "react";
import * as ReactDOM from "react-dom";

class App extends React.Component<{}, {}>{
  render() {
    return (<BulletChartComponent id='ranges'
                        animation={{ enable: false }}
                        width="80%"
                        height="90%"
                        valueField='value'
                        targetField='target'
                        title='Revenue'
                        minimum={0}
                        maximum={30}
                        interval={5}
                        dataSource={[{value: 23, target: 22}]}>
                        <BulletRangeCollectionDirective>
                            <BulletRangeDirective end={20} color='red' ></BulletRangeDirective>
                            <BulletRangeDirective end={25} color='blue'></BulletRangeDirective>
                            <BulletRangeDirective end={30} color='green'></BulletRangeDirective>
                        </BulletRangeCollectionDirective>

            </BulletChartComponent>);
  }
};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Size for Bullet Chart

The [`width`](https://ej2.syncfusion.com/react/documentation/api/bullet-chart/#width) and [`height`](https://ej2.syncfusion.com/react/documentation/api/bullet-chart/#height) properties are used to adjust the size of the Bullet Chart.

{% tab template="bullet-chart/bullet-chart-dimensions/container", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import { BulletChartComponent, Inject} from '@syncfusion/ej2-react-charts';
import { BulletRangeCollectionDirective, BulletRangeDirective} from '@syncfusion/ej2-react-charts';
import * as React from "react";
import * as ReactDOM from "react-dom";

class App extends React.Component<{}, {}>{
  render() {
    return (<BulletChartComponent id='ranges'
                        animation={{ enable: false }}
                        width="80%"
                        height="90%"
                        valueField='value'
                        targetField='target'
                        title='Revenue'
                        minimum={0}
                        maximum={30}
                        interval={5}
                        dataSource={[{value: 23, target: 22}]}>
                        <BulletRangeCollectionDirective>
                            <BulletRangeDirective end={20} color='red' ></BulletRangeDirective>
                            <BulletRangeDirective end={25} color='blue'></BulletRangeDirective>
                            <BulletRangeDirective end={30} color='green'></BulletRangeDirective>
                        </BulletRangeCollectionDirective>
            </BulletChartComponent>);
  }
};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

### Pixel

Can set the size of the Bullet Chart in pixels as shown below.

{% tab template="bullet-chart/bullet-chart-dimensions/container", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import { BulletChartComponent, Inject} from '@syncfusion/ej2-react-charts';
import { BulletRangeCollectionDirective, BulletRangeDirective} from '@syncfusion/ej2-react-charts';
import * as React from "react";
import * as ReactDOM from "react-dom";

class App extends React.Component<{}, {}>{
  render() {
    return (<BulletChartComponent id='ranges'
                        animation={{ enable: false }}
                        width="600px"
                        height="100px"
                        valueField='value'
                        targetField='target'
                        title='Revenue'
                        minimum={0}
                        maximum={30}
                        interval={5}
                        dataSource={[{value: 23, target: 22}]}>
                        <BulletRangeCollectionDirective>
                            <BulletRangeDirective end={20} color='red' ></BulletRangeDirective>
                            <BulletRangeDirective end={25} color='blue'></BulletRangeDirective>
                            <BulletRangeDirective end={30} color='green'></BulletRangeDirective>
                        </BulletRangeCollectionDirective>

            </BulletChartComponent>);
  }
};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

### Percentage

By setting a value in percentage, the Bullet Chart gets its dimension with respect to its container. For example, when the height is **50%**, the Bullet Chart renders to half of the container’s height.

{% tab template="bullet-chart/bullet-chart-dimensions/container", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import { BulletChartComponent, Inject} from '@syncfusion/ej2-react-charts';
import { BulletRangeCollectionDirective, BulletRangeDirective} from '@syncfusion/ej2-react-charts';
import * as React from "react";
import * as ReactDOM from "react-dom";

class App extends React.Component<{}, {}>{
  render() {
    return (<BulletChartComponent id='ranges'
                        animation={{ enable: false }}
                        width="80%"
                        height="90%"
                        valueField='value'
                        targetField='target'
                        title='Revenue'
                        minimum={0}
                        maximum={30}
                        interval={5}
                        dataSource={[{value: 23, target: 22}]}>
                        <BulletRangeCollectionDirective>
                            <BulletRangeDirective end={20} color='red' ></BulletRangeDirective>
                            <BulletRangeDirective end={25} color='blue'></BulletRangeDirective>
                            <BulletRangeDirective end={30} color='green'></BulletRangeDirective>
                        </BulletRangeCollectionDirective>

            </BulletChartComponent>);
  }
};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

>If the size is not specified, the Bullet Chart will be rendered with a height of **126px** and a width of the window.