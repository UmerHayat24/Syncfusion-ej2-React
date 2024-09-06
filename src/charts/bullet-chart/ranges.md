---
title: " Bullet Chart Ranges | React "

component: "Bullet Chart"

description: "Bullet Chart scale can be rendered by using different types of end values. They are used to represnt the status of each data. "
---

# Ranges

Ranges represent the quality of a specific range such as **Good**, **Bad** and **Satisfactory** in the Bullet Chart scale. The ending point of a qualitative range is specified in the [`end`](https://ej2.syncfusion.com/angular/documentation/api/bullet-chart/rangeModel/#end) property in [`ranges`](https://ej2.syncfusion.com/angular/documentation/api/bullet-chart/#ranges). The [`minimum`](https://ej2.syncfusion.com/angular/documentation/api/bullet-chart/#minimum) value of a quantitative scale is considered the starting point of the first range or the previous range end point.

## Color Customization

Enhance the readability of ranges with color and opacity. It can be applied using the [`color`](https://ej2.syncfusion.com/react/documentation/api/bullet-chart/rangeModel/#color) and [`opacity`](https://ej2.syncfusion.com/react/documentation/api/bullet-chart/rangeModel/#opacity) properties in [`ranges`](https://ej2.syncfusion.com/angular/documentation/api/bullet-chart/#ranges).

{% tab template="bullet-chart/working-with-data/local-data", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import { BulletChartComponent, Inject} from '@syncfusion/ej2-react-charts';
import { BulletRangeCollectionDirective, BulletRangeDirective} from '@syncfusion/ej2-react-charts';
import * as React from "react";
import * as ReactDOM from "react-dom";

class App extends React.Component<{}, {}>{
  render() {
    return (<BulletChartComponent id='ranges'
                animation={{ enable: false }}
                height="400"
                valueField='value'
                targetField='target'
                categoryField='category'
                categoryLabelStyle={{color:'red', size:'13', fontWeight:'bold'}}
                title='ales Rate'
                minimum={0}
                maximum={100}
                interval={10}
                dataSource={[{value: 55, target: 7.5, category: 'Year 1'},
                {value: 7, target: 5, category: 'Year 2'},
                {value: 10, target: 6, category: 'Year 3'}]}>
                <BulletRangeCollectionDirective>
                    <BulletRangeDirective end={35} color='darkred' opacity={0.5}></BulletRangeDirective>
                    <BulletRangeDirective end={50} color='red' opacity={1}></BulletRangeDirective>
                    <BulletRangeDirective end={75} color='blue' opacity={0.7}></BulletRangeDirective>
                    <BulletRangeDirective end={90} color='lightgreen' opacity={1}></BulletRangeDirective>
                    <BulletRangeDirective end={100} color='green' opacity={1}></BulletRangeDirective>
                </BulletRangeCollectionDirective>

            </BulletChartComponent>);
  }
};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}