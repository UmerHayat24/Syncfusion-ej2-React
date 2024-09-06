---
title: " Bullet Chart Title and SubTitle | React "

component: "Bullet Chart"

description: "The title and sub-title is very useful to understand the bullet chart in efficient way. It describes what kind of data which represtend by the bullet-chart. "
---

# Title and Subtitle

## Title

The title of the Bullet Chart displays the information about the data plotted by specifying it in the [`title`](https://ej2.syncfusion.com/react/documentation/api/bullet-chart/#title) property.

{% tab template="bullet-chart/title", sourceFiles="app/**/*.tsx", compileJsx=true %}

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
                            <BulletRangeDirective end={35} color='red' ></BulletRangeDirective>
                            <BulletRangeDirective end={50} color='blue'></BulletRangeDirective>
                            <BulletRangeDirective end={100} color='green'></BulletRangeDirective>
                        </BulletRangeCollectionDirective>
            </BulletChartComponent>);
  }
};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Subtitle

To show additional information about the data plotted, the Bullet Chart can also be given a subtitle using the [`subtitle`](https://ej2.syncfusion.com/react/documentation/api/bullet-chart/#subtitle) property.

{% tab template="bullet-chart/title", sourceFiles="app/**/*.tsx", compileJsx=true %}

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
                        subtitle='(in dollars $)'
                        minimum={0}
                        maximum={100}
                        interval={20}
                        dataSource={[{value: 55, target: 45}]}>
                        <BulletRangeCollectionDirective>
                            <BulletRangeDirective end={35} color='red' ></BulletRangeDirective>
                            <BulletRangeDirective end={50} color='blue'></BulletRangeDirective>
                            <BulletRangeDirective end={100} color='green'></BulletRangeDirective>
                        </BulletRangeCollectionDirective>
            </BulletChartComponent>);
  }
};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Title and SubTitle Position

The title and the subtitle positions can be customized using the [`titlePosition`](https://ej2.syncfusion.com/react/documentation/api/bullet-chart/#titleposition) property. Possible positions are **Left**, **Right**, **Top**, and **Bottom**.

### Position as Left

By setting the [`titlePosition`](https://ej2.syncfusion.com/react/documentation/api/bullet-chart/#titleposition) to **Left**, you can display the title and subtitle at the left side of the Bullet Chart.

{% tab template="bullet-chart/title", sourceFiles="app/**/*.tsx", compileJsx=true %}

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
                        subtitle='(in dollars $)'
                        titlePosition='Left'
                        labelFormat='${value}'
                        minimum={0}
                        maximum={100}
                        interval={20}
                        dataSource={[{value: 55, target: 45}]}>
                        <BulletRangeCollectionDirective>
                            <BulletRangeDirective end={35} color='red' ></BulletRangeDirective>
                            <BulletRangeDirective end={50} color='blue'></BulletRangeDirective>
                            <BulletRangeDirective end={100} color='green'></BulletRangeDirective>
                        </BulletRangeCollectionDirective>
            </BulletChartComponent>);
  }
};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

### Position as Right

By setting the [`titlePosition`](https://ej2.syncfusion.com/react/documentation/api/bullet-chart/#titleposition) to **Right**, you can display the title and subtitle at the right side of the Bullet Chart.

{% tab template="bullet-chart/title", sourceFiles="app/**/*.tsx", compileJsx=true %}

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
                        subtitle='(in dollars $)'
                        titlePosition='Right'
                        labelFormat='${value}'
                        minimum={0}
                        maximum={100}
                        interval={20}
                        dataSource={[{value: 55, target: 45}]}>
                        <BulletRangeCollectionDirective>
                            <BulletRangeDirective end={35} color='red' ></BulletRangeDirective>
                            <BulletRangeDirective end={50} color='blue'></BulletRangeDirective>
                            <BulletRangeDirective end={100} color='green'></BulletRangeDirective>
                        </BulletRangeCollectionDirective>
            </BulletChartComponent>);
  }
};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

### Position as Top

By setting the [`titlePosition`](https://ej2.syncfusion.com/react/documentation/api/bullet-chart/#titleposition) to **Top**, you can display the title and subtitle at the top of the Bullet Chart. The default title and subtitle positions of the Bullet Chart is **Top**.

{% tab template="bullet-chart/title", sourceFiles="app/**/*.tsx", compileJsx=true %}

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
                        subtitle='(in dollars $)'
                        titlePosition='Top'
                        labelFormat='${value}'
                        minimum={0}
                        maximum={100}
                        interval={20}
                        dataSource={[{value: 55, target: 45}]}>
                        <BulletRangeCollectionDirective>
                            <BulletRangeDirective end={35} color='red' ></BulletRangeDirective>
                            <BulletRangeDirective end={50} color='blue'></BulletRangeDirective>
                            <BulletRangeDirective end={100} color='green'></BulletRangeDirective>
                        </BulletRangeCollectionDirective>
            </BulletChartComponent>);
  }
};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

### Position as Bottom

By setting the [`titlePosition`](https://ej2.syncfusion.com/react/documentation/api/bullet-chart/#titleposition) to **Bottom**, you can display the title and subtitle at the bottom of the Bullet Chart.

{% tab template="bullet-chart/title", sourceFiles="app/**/*.tsx", compileJsx=true %}

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
                        subtitle='(in dollars $)'
                        titlePosition='Bottom'
                        labelFormat='${value}'
                        minimum={0}
                        maximum={100}
                        interval={20}
                        dataSource={[{value: 55, target: 45}]}>
                        <BulletRangeCollectionDirective>
                            <BulletRangeDirective end={35} color='red' ></BulletRangeDirective>
                            <BulletRangeDirective end={50} color='blue'></BulletRangeDirective>
                            <BulletRangeDirective end={100} color='green'></BulletRangeDirective>
                        </BulletRangeCollectionDirective>
            </BulletChartComponent>);
  }
};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Title Customization

The title color, opacity, font size, font family, font weight, and font style can be customized using the [`titleStyle`](https://ej2.syncfusion.com/react/documentation/api/bullet-chart/#titlestyle) property.

{% tab template="bullet-chart/title", sourceFiles="app/**/*.tsx", compileJsx=true %}

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
                        subtitle='(in dollars $)'
                        labelFormat='${value}'
                        minimum={0}
                        maximum={100}
                        interval={20}
                        titleStyle={{size: '22px', color:'red', fontFamily:'cursive', fontWeight:'Bold'}}
                        dataSource={[{value: 55, target: 45}]}>
                        <BulletRangeCollectionDirective>
                            <BulletRangeDirective end={35} color='red' ></BulletRangeDirective>
                            <BulletRangeDirective end={50} color='blue'></BulletRangeDirective>
                            <BulletRangeDirective end={100} color='green'></BulletRangeDirective>
                        </BulletRangeCollectionDirective>
            </BulletChartComponent>);
  }
};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## SubTitle Customization

The sub-title color, opacity, font size, font family, font weight, and font style can be customized using the [`subtitleStyle`](https://ej2.syncfusion.com/react/documentation/api/bullet-chart/#subtitlestyle) property.

{% tab template="bullet-chart/title", sourceFiles="app/**/*.tsx", compileJsx=true %}

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
                        subtitle='(in dollars $)'
                        labelFormat='${value}'
                        minimum={0}
                        maximum={100}
                        interval={20}
                        subtitleStyle={{size: '22px', color:'red', fontFamily:'cursive', fontWeight:'Bold'}}
                        dataSource={[{value: 55, target: 45}]}>
                        <BulletRangeCollectionDirective>
                            <BulletRangeDirective end={35} color='red' ></BulletRangeDirective>
                            <BulletRangeDirective end={50} color='blue'></BulletRangeDirective>
                            <BulletRangeDirective end={100} color='green'></BulletRangeDirective>
                        </BulletRangeCollectionDirective>
            </BulletChartComponent>);
  }
};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}