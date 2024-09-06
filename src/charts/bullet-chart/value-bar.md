---
title: " Bullet Chart Value Bar | React "

component: "Bullet Chart"

description: "The main data value is encoded by a length of the main bar in the middle of the chart, known as the Feature Measure. "
---

# Actual Bar

To display the primary data or the current value of the data being measured known as the **Feature Measure** that should be encoded as a bar. This is called as the **Actual Bar** or the **Feature Bar** in the Bullet Chart, and to display the actual bar the [`valueField`](https://ej2.syncfusion.com/react/documentation/api/bullet-chart/#valuefield) should be mapped to the appropriate field from the data source.

{% tab template="bullet-chart/value-bar", sourceFiles="app/**/*.tsx", compileJsx=true %}

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
                        title='Sales Rate'
                        minimum={0}
                        maximum={100}
                        interval={20}
                        dataSource={[{value: 55, target: 75}]}>
                        <BulletRangeCollectionDirective>
                            <BulletRangeDirective end={35} ></BulletRangeDirective>
                            <BulletRangeDirective end={50} ></BulletRangeDirective>
                            <BulletRangeDirective end={100} ></BulletRangeDirective>
                        </BulletRangeCollectionDirective>
            </BulletChartComponent>);
  }
};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Types of Actual Bar

The shape of the actual bar can be customized using the [`type`](https://ej2.syncfusion.com/react/documentation/api/bullet-chart/#type) property of the Bullet Chart. The actual bar contains `Rect` and `Dot` shapes. By default, the actual bar shape is Rect.

{% tab template="bullet-chart/value-bar", sourceFiles="app/**/*.tsx", compileJsx=true %}

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
                        title='Sales Rate'
                        type='Dot'
                        minimum={0}
                        maximum={100}
                        interval={20}
                        dataSource={[{value: 55, target: 75}]}>
                        <BulletRangeCollectionDirective>
                            <BulletRangeDirective end={35} ></BulletRangeDirective>
                            <BulletRangeDirective end={50} ></BulletRangeDirective>
                            <BulletRangeDirective end={100} ></BulletRangeDirective>
                        </BulletRangeCollectionDirective>
            </BulletChartComponent>);
  }
};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Actual Bar Customization

### Border Customization

Using the [`valueBorder`](https://ej2.syncfusion.com/react/documentation/api/bullet-chart/#valueborder) property of the bullet chart, you can customize the border `color` and `width` of the actual bar.

{% tab template="bullet-chart/value-bar", sourceFiles="app/**/*.tsx", compileJsx=true %}

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
                        title='Sales Rate'
                        valueBorder={{color: 'red', width: 3}}
                        minimum={0}
                        maximum={100}
                        interval={20}
                        dataSource={[{value: 55, target: 75}]}>
                        <BulletRangeCollectionDirective>
                            <BulletRangeDirective end={35} ></BulletRangeDirective>
                            <BulletRangeDirective end={50} ></BulletRangeDirective>
                            <BulletRangeDirective end={100} ></BulletRangeDirective>
                        </BulletRangeCollectionDirective>
            </BulletChartComponent>);
  }
};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

### Fill color and height Customization

Customize the fill color and height of the actual bar using the [`valueFill`](https://ej2.syncfusion.com/react/documentation/api/bullet-chart/#valuefill) and [`valueHeight`](https://ej2.syncfusion.com/react/documentation/api/bullet-chart/#valueheight) properties of the bullet chart.

{% tab template="bullet-chart/value-bar", sourceFiles="app/**/*.tsx", compileJsx=true %}

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
                        title='Sales Rate'
                        valueFill='blue'
                        valueHeight={15}
                        minimum={0}
                        maximum={100}
                        interval={20}
                        dataSource={[{value: 55, target: 75}]}>
                        <BulletRangeCollectionDirective>
                            <BulletRangeDirective end={35} ></BulletRangeDirective>
                            <BulletRangeDirective end={50} ></BulletRangeDirective>
                            <BulletRangeDirective end={100} ></BulletRangeDirective>
                        </BulletRangeCollectionDirective>
            </BulletChartComponent>);
  }
};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}