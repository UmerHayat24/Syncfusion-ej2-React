---
title: "Bullet Chart Axis Customization | React "

component: "Bullet Chart"

description: "Bullet Chart axis includes different customizations such as majortick and minortick, axis label, axis range."
---

# Axis Customization

## MajorTickLines and MinorTickLines Customization

The following properties can be used to customize [`majorTicklines`](https://ej2.syncfusion.com/react/documentation/api/bullet-chart/#majorticklines) and [`minorTicklines`](https://ej2.syncfusion.com/react/documentation/api/bullet-chart/#minorticklines).

* **width** - Specifies the width of ticklines.
* **height** - Specifies the height of ticklines.
* **color** - Specifies the color of ticklines.
* **useRangeColor** - Specifies the color of ticklines and represents the color from corresponding range colors.

{% tab template="bullet-chart/axis-customization/axis", sourceFiles="app/**/*.tsx", compileJsx=true %}

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
                        title='Revenue'
                        majorTickLines={{ color: 'blue', width: 5}}
                        minorTickLines={{ width: 4, color: 'red'}}
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

## Tick Placement

The major and the minor ticks can be placed **inside** or **outside** the ranges using the [`tickPosition`](https://ej2.syncfusion.com/react/documentation/api/bullet-chart/#tickposition) property.

{% tab template="bullet-chart/axis-customization/axis", sourceFiles="app/**/*.tsx", compileJsx=true %}

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
                        title='Revenue'
                        tickPosition='inside'
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

## Label Format

Axis numeric labels can be formatted by using the [`labelFormat`](https://ej2.syncfusion.com/react/documentation/api/bullet-chart/#labelformat) property. Axis labels support all globalize formats.

{% tab template="bullet-chart/axis-customization/axis", sourceFiles="app/**/*.tsx", compileJsx=true %}

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
                        title='Revenue'
                        labelFormat='c'
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

The following table describes the result of applying some commonly used formats to numeric axis labels.

<!-- markdownlint-disable MD033 -->
<table>
<tr>
<td><b>Label Value</b></td>
<td><b>Label Format property value</b></td>
<td><b>Result </b></td>
<td><b>Description </b></td>
</tr>
<tr>
<td>1000</td>
<td>n1</td>
<td>1000.0</td>
<td>The Number is rounded to 1 decimal place</td>
</tr>
<tr>
<td>1000</td>
<td>n2</td>
<td>1000.00</td>
<td>The Number is rounded to 2 decimal place</td>
</tr>
<tr>
<td>1000</td>
<td>n3</td>
<td>1000.000</td>
<td>The Number is rounded to 3 decimal place</td>
</tr>
<tr>
<td>0.01</td>
<td>p1</td>
<td>1.0%</td>
<td>The Number is converted to percentage with 1 decimal place</td>
</tr>
<tr>
<td>0.01</td>
<td>p2</td>
<td>1.00%</td>
<td>The Number is converted to percentage with 2 decimal place</td>
</tr>
<tr>
<td>0.01</td>
<td>p3</td>
<td>1.000%</td>
<td>The Number is converted to percentage with 3 decimal place</td>
</tr>
<tr>
<td>1000</td>
<td>c1</td>
<td>$1000.0</td>
<td>The Currency symbol is appended to number and number is rounded to 1 decimal place</td>
</tr>
<tr>
<td>1000</td>
<td>c2</td>
<td>$1000.00</td>
<td>The Currency symbol is appended to number and number is rounded to 2 decimal place</td>
</tr>
</table>

## GroupingSeparator

To separate the groups of thousands, set the [`enableGroupSeparator`](https://ej2.syncfusion.com/react/documentation/api/bullet-chart/#enablegroupseparator) property to **true**

{% tab template="bullet-chart/axis-customization/axis", sourceFiles="app/**/*.tsx", compileJsx=true %}

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
                        enableGroupSeparator={true}
                        minimum={0}
                        maximum={2500}
                        interval={250}
                        dataSource={[{value: 1500, target: 1300}]}>
                        <BulletRangeCollectionDirective>
                            <BulletRangeDirective end={500} color='red' ></BulletRangeDirective>
                            <BulletRangeDirective end={1500} color='blue'></BulletRangeDirective>
                            <BulletRangeDirective end={2500} color='green'></BulletRangeDirective>
                        </BulletRangeCollectionDirective>

            </BulletChartComponent>);
  }
};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Custom Label Format

Using the [`labelFormat`](https://ej2.syncfusion.com/react/documentation/api/bullet-chart/#labelformat) property, axis labels can be specified with a custom defined format in addition to the axis value. The label format uses a placeholder such as **${value}K**, which represents the axis label.

{% tab template="bullet-chart/axis-customization/axis", sourceFiles="app/**/*.tsx", compileJsx=true %}

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
                        labelFormat='${value}K'
                        minimum={0}
                        maximum={2500}
                        interval={250}
                        dataSource={[{value: 1500, target: 1300}]}>
                        <BulletRangeCollectionDirective>
                            <BulletRangeDirective end={500} color='red' ></BulletRangeDirective>
                            <BulletRangeDirective end={1500} color='blue'></BulletRangeDirective>
                            <BulletRangeDirective end={2500} color='green'></BulletRangeDirective>
                        </BulletRangeCollectionDirective>

            </BulletChartComponent>);
  }
};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Label Placement

Label can be placed **Inside** or **Outside** of the ranges using the [`labelPosition`](https://ej2.syncfusion.com/react/documentation/api/bullet-chart/#labelposition) property.

{% tab template="bullet-chart/axis-customization/axis", sourceFiles="app/**/*.tsx", compileJsx=true %}

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
                        title='Revenue'
                        labelPosition='inside'
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

## Opposed Position

To place an axis opposite to its original position, set the [`opposedPosition`](https://ej2.syncfusion.com/react/documentation/api/bullet-chart/#opposedposition) property to **true**.

{% tab template="bullet-chart/axis-customization/axis", sourceFiles="app/**/*.tsx", compileJsx=true %}

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
                        title='Revenue'
                        majorTickLines={{ color: 'blue', width: 5}}
                        minorTickLines={{ width: 4, color: 'red'}}
                        opposedPosition={true}
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

## Category Label

The Bullet Chart supports X-axis label by specifying the property from the data source to the [`categoryField`](https://ej2.syncfusion.com/react/documentation/api/bullet-chart/#categoryfield). It helps to understand the input data in a more efficient way.

{% tab template="bullet-chart/axis-customization/axis", sourceFiles="app/**/*.tsx", compileJsx=true %}

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
                        categoryField='category'
                        minimum={0}
                        maximum={2500}
                        interval={250}
                        dataSource={[{value: 1500, target: 1300, category: 'Product A'}]}>
                        <BulletRangeCollectionDirective>
                            <BulletRangeDirective end={500} color='red' ></BulletRangeDirective>
                            <BulletRangeDirective end={1500} color='blue'></BulletRangeDirective>
                            <BulletRangeDirective end={2500} color='green'></BulletRangeDirective>
                        </BulletRangeCollectionDirective>

            </BulletChartComponent>);
  }
};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Category Label Customization

The label color, opacity, font size, font family, font weight, and font style can be customized by using the [`categoryLabelStyle`](https://ej2.syncfusion.com/react/documentation/api/bullet-chart/#categorylabelstyle) setting for category and the [`labelStyle`](https://ej2.syncfusion.com/react/documentation/api/bullet-chart/#labelstyle) setting for axis label. The [`useRangeColor`](https://ej2.syncfusion.com/react/documentation/api/bullet-chart/bulletLabelStyleModel/#userangecolor) property specifies the color of the axis label and represents the color from the corresponding range colors.

{% tab template="bullet-chart/axis-customization/axis", sourceFiles="app/**/*.tsx", compileJsx=true %}

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
                        categoryField='category'
                        categoryLabelStyle={{ color:'Orange' }}
                        minimum={0}
                        maximum={2500}
                        interval={250}
                        dataSource={[{value: 1500, target: 1300, category: 'Product A'}]}>
                        <BulletRangeCollectionDirective>
                            <BulletRangeDirective end={500} color='red' ></BulletRangeDirective>
                            <BulletRangeDirective end={1500} color='blue'></BulletRangeDirective>
                            <BulletRangeDirective end={2500} color='green'></BulletRangeDirective>
                        </BulletRangeCollectionDirective>

            </BulletChartComponent>);
  }
};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}