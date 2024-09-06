---
title: "BulletChart Tooltip | React "

component: "BulletChart"

description: "Tooltip is used to show the data value when mouse hover on the chart.We can able to customize format,template and appearance."
---

# Tooltip

When the mouse is hovered over a bar in the Bullet Chart, the tooltip displays important summary about the actual and the target bar values.

## Default Tooltip

The tooltip is not visible by default. To make it visible, set the [`enable`](https://ej2.syncfusion.com/react/documentation/api/bullet-chart/bulletTooltipSettingsModel/#enable) property in the [`tooltip`](https://ej2.syncfusion.com/react/documentation/api/bullet-chart/#tooltip) to **true**.

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
                        targetField='comparativeMeasureValue'
                        categoryField='category'
                        title='Profit in %'
                        minimum={0}
                        maximum={20}
                        interval={5}
                        tooltip={{enable: true}}
                        dataSource={[{value: 5, comparativeMeasureValue: 7.5, category: '2001'},
                        {value: 7, comparativeMeasureValue: 5, category: '2002'},
                        {value: 10, comparativeMeasureValue: 6, category: '2003'},
                        {value: 5, comparativeMeasureValue: 8, category: '2004'},
                        {value: 12, comparativeMeasureValue: 5, category: '2005'},
                        {value: 8, comparativeMeasureValue: 6, category: '2006'},]}>
                        <BulletRangeCollectionDirective>
                            <BulletRangeDirective end={5} ></BulletRangeDirective>
                            <BulletRangeDirective end={15}></BulletRangeDirective>
                            <BulletRangeDirective end={20}></BulletRangeDirective>
                        </BulletRangeCollectionDirective>

            </BulletChartComponent>);
  }
};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Tooltip Template

Any HTML elements can be displayed in the tooltip by using the [`template`](https://ej2.syncfusion.com/react/documentation/api/bullet-chart/bulletTooltipSettingsModel/#template) property of the [`tooltip`](https://ej2.syncfusion.com/react/documentation/api/bullet-chart/#tooltip). You can use the **${target}** and **${value}** as place holders in the HTML element to display the value and target values from the data source of corresponding data point.

## Customize the Appearance of Tooltip

The [`fill`](./https://ej2.syncfusion.com/documentation/api/bullet-chart/bulletTooltipSettingsModel/#fill) and [`border`](./https://ej2.syncfusion.com/documentation/api/bullet-chart/bulletTooltipSettingsModel/#border) properties are used to customize the background color and border of the tooltip respectively. The [`textStyle`](./https://ej2.syncfusion.com/documentation/api/bullet-chart/bulletTooltipSettingsModel/#textstyle) property in the tooltip is used to customize the font of the tooltip text.

## Tooltip Customization

The following properties can be used to customize the Bullet Chart tooltip.

* [`fill`](https://ej2.syncfusion.com/react/documentation/api/bullet-chart/bulletTooltipSettingsModel/#fill) - Specifies the color of tooltip.
* [`border`](https://ej2.syncfusion.com/react/documentation/api/bullet-chart/bulletTooltipSettingsModel/#border) - Specifies the tooltip border color and width.
* [`textStyle`](https://ej2.syncfusion.com/react/documentation/api/bullet-chart/bulletTooltipSettingsModel/#textstyle) - Specifies the tooltip font family, font style, font weight, color and size.
