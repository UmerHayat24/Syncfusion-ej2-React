---
title: " Bullet Chart Target Bar | React "

component: "Bullet Chart"

description: "The line marker that runs perpendicular to the orientation of the graph is known as the `Comparative Measure`. "
---

# Target Bar

The line marker that runs perpendicular to the orientation of the graph is known as the **Comparative Measure** and it is used as a target marker to compare against the feature measure value. This is also called as the **Target Bar** in the Bullet Chart. To display the target bar, the [`targetField`](https://ej2.syncfusion.com/react/documentation/api/bullet-chart/#targetfield) should be mapped to the appropriate field from the datasource.

{% tab template="bullet-chart/target-bar", sourceFiles="app/**/*.tsx", compileJsx=true %}

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

## Types of Target Bar

The shape of the target bar can be customized using the [`targetTypes`](https://ej2.syncfusion.com/react/documentation/api/bullet-chart/#targettypes) property and it supports **Circle**, **Cross**, and **Rect** shapes. The default type of the target bar is **Rect**.

{% tab template="bullet-chart/target-bar", sourceFiles="app/**/*.tsx", compileJsx=true %}

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
                        targetTypes={['Circle']}
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

## Target Bar Customization

The following properties can be used to customize the Target Bar.

* [`targetColor`](https://ej2.syncfusion.com/react/documentation/api/bullet-chart/#targetcolor) - Specifies the fill color of Target Bar.
* [`targetWidth`](https://ej2.syncfusion.com/react/documentation/api/bullet-chart/#targetwidth) - Specifies the width of Target Bar.

{% tab template="bullet-chart/target-bar", sourceFiles="app/**/*.tsx", compileJsx=true %}

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
                        targetColor='red'
                        targetWidth={15}
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