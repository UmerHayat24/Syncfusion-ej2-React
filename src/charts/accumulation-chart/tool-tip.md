---
title: "Accumulation Chart Tooltip | TypeScript "

component: "Accumulation Chart"

description: "Accumulation chart tooltip represents the x and y values of the current mouse pointer point."
---

# Tooltip

Tooltip for the accumulation chart can be enabled by using the `enable` property.

{% tab template="chart/series/legend", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AccumulationChartComponent, AccumulationSeriesCollectionDirective, AccumulationSeriesDirective,
 AccumulationTooltip, Inject,TooltipSettingsModel}
from'@syncfusion/ej2-react-charts';
import { accData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public tooltip: TooltipSettingsModel = { enable: true };

  render() {
    return <AccumulationChartComponent id='charts' tooltip={this.tooltip}>
      <Inject services={[AccumulationTooltip]} />
      <AccumulationSeriesCollectionDirective>
        <AccumulationSeriesDirective dataSource={accData} xName='x' yName='y'>
        </AccumulationSeriesDirective>
      </AccumulationSeriesCollectionDirective>
    </AccumulationChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

>Note:To use tooltip feature , we need to inject `AccumulationTooltip` module into the `services`.

## Header

We can specify header for the tooltip using `header` property.

{% tab template="chart/series/legend", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AccumulationChartComponent, AccumulationSeriesCollectionDirective, AccumulationSeriesDirective,
 AccumulationTooltip, Inject, TooltipSettingsModel }
from'@syncfusion/ej2-react-charts';
import { accData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public tooltip: TooltipSettingsModel = { enable: true, header: "Pie Chart" };

  render() {
    return <AccumulationChartComponent id='charts' tooltip={this.tooltip}>
      <Inject services={[AccumulationTooltip]} />
      <AccumulationSeriesCollectionDirective>
        <AccumulationSeriesDirective dataSource={accData} xName='x' yName='y'>
        </AccumulationSeriesDirective>
      </AccumulationSeriesCollectionDirective>
    </AccumulationChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Format

By default, tooltip shows information of x and y value in points. In addition to that, you can show more
information in tooltip. For example the format `${series.name} ${point.x}` shows series name and point x value.

{% tab template="chart/series/legend", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AccumulationChartComponent, AccumulationSeriesCollectionDirective,TooltipSettingsModel,
 AccumulationSeriesDirective, AccumulationTooltip, Inject, AccumulationLegend}
from'@syncfusion/ej2-react-charts';
import { accData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public tooltip: TooltipSettingsModel = { enable: true, format: '${point.x} : <b>${point.y}%</b>' };

  render() {
    return <AccumulationChartComponent id='charts' tooltip={this.tooltip}>
      <Inject services={[AccumulationLegend, AccumulationTooltip]} />
      <AccumulationSeriesCollectionDirective>
        <AccumulationSeriesDirective dataSource={accData} xName='x' yName='y'>
        </AccumulationSeriesDirective>
      </AccumulationSeriesCollectionDirective>
    </AccumulationChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Tooltip Mapping Name

By default, tooltip shows information of x and y value in points. You can show more information from datasource in tooltip by using the `tooltipMappingName` property of the tooltip. You can use the `${point.tooltip}` as place holders to display the specified tooltip content.

{% tab template="chart/series/legend", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AccumulationChartComponent, AccumulationSeriesCollectionDirective,TooltipSettingsModel,
 AccumulationSeriesDirective, AccumulationTooltip, Inject, AccumulationLegend}
from'@syncfusion/ej2-react-charts';
import { data2 } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public tooltip: TooltipSettingsModel = { enable: true, format: '${point.tooltip}' };

  render() {
    return <AccumulationChartComponent id='charts' tooltip={this.tooltip}>
      <Inject services={[AccumulationLegend, AccumulationTooltip]} />
      <AccumulationSeriesCollectionDirective>
        <AccumulationSeriesDirective dataSource={data2} xName='x' yName='y' tooltipMappingName='text'>
        </AccumulationSeriesDirective>
      </AccumulationSeriesCollectionDirective>
    </AccumulationChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Tooltip Template

Any HTML element can be displayed in the tooltip by using the `template` property.

{% tab template="chart/series/legend", sourceFiles="app/**/*.tsx", compileJsx=true %}
{% raw %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AccumulationChartComponent, AccumulationSeriesCollectionDirective, AccumulationSeriesDirective,
 AccumulationTooltip, Inject,TooltipSettingsModel}
from'@syncfusion/ej2-react-charts';
import { accData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public template:any =this.chartTemplate;
  public tooltip: TooltipSettingsModel = {
    enable: true,
    template: this.template
  };
  public chartTemplate(args:any){
    return (<div style={{ border:'1px solid black', backgroundColor:'red', padding:'2px',float:'right',            lineHeight:'20px',textAlign:'center'}}>
              <img src='sun_annotation.png' />
              <div style={{ color:'blue', padding:'2px',fontSize:'14px', fontStyle:'medium',fontFamily:'Roboto' ,float:'right',lineHeight:'20px',textAlign:'center',paddingRight:'6px'}}>
                <span>{args.y}</span>
              </div>
            </div>
          );
  }

  render() {
    return <AccumulationChartComponent id='charts' tooltip={this.tooltip}>
      <Inject services={[AccumulationTooltip]} />
      <AccumulationSeriesCollectionDirective>
        <AccumulationSeriesDirective dataSource={accData} xName='x' yName='y'>
        </AccumulationSeriesDirective>
      </AccumulationSeriesCollectionDirective>
    </AccumulationChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endraw %}

{% endtab %}

## Customization

The [`fill`](../api/chart/tooltipSettingsModel/#fill) and
[`border`](../api/chart/tooltipSettingsModel/#border) properties are used to customize the background
color and border of the tooltip respectively. The [`textStyle`](../api/chart/tooltipSettingsModel/#textstyle)
property in the tooltip is used to customize the font of the tooltip text.

{% tab template="chart/series/legend", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AccumulationChartComponent, AccumulationSeriesCollectionDirective, IAccTooltipRenderEventArgs,
 AccumulationSeriesDirective, AccumulationTooltip, Inject, TooltipSettingsModel}
from'@syncfusion/ej2-react-charts';
import { accData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public tooltip: TooltipSettingsModel = {
    enable: true, format: '${series.name} ${point.x} : ${point.y}',
    //fill for tooltip
    fill: '#7bb4eb',
    //border for tooltip
    border: {
      width: 2,
      color: 'grey'
    }
  };

  render() {
    return <AccumulationChartComponent id='charts' tooltip={this.tooltip}>
      <Inject services={[AccumulationTooltip]} />
      <AccumulationSeriesCollectionDirective>
        <AccumulationSeriesDirective dataSource={accData} xName='x' yName='y'>
        </AccumulationSeriesDirective>
      </AccumulationSeriesCollectionDirective>
    </AccumulationChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## To customize individual tooltip

Using `tooltipRender` event, you can customize a tooltip for particular point. event, you can customize a
tooltip for particular point.

{% tab template="chart/series/legend", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AccumulationChartComponent, AccumulationSeriesCollectionDirective, IAccTooltipRenderEventArgs,
 AccumulationSeriesDirective, AccumulationTooltip, Inject, AccumulationLegend,TooltipSettingsModel}
from'@syncfusion/ej2-react-charts';
import { accData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

  public tooltipRender: EmitType<IAccTooltipRenderEventArgs> = (args: IAccTooltipRenderEventArgs): void => {
    if (args.point.index === 3) {
      args.text = args.point.x + '' + ':' + args.point.y + '' + ' ' + 'customtext';
      args.textStyle.color = '#f48042';
    }
  };
  public tooltip: TooltipSettingsModel = { enable: true };

  render() {
    return <AccumulationChartComponent id='charts' tooltip={this.tooltip} tooltipRender={this.tooltipRender}>
      <Inject services={[AccumulationLegend, AccumulationTooltip]} />
      <AccumulationSeriesCollectionDirective>
        <AccumulationSeriesDirective dataSource={accData} xName='x' yName='y'>
        </AccumulationSeriesDirective>
      </AccumulationSeriesCollectionDirective>
    </AccumulationChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}