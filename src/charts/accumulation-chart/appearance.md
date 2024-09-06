---
title: "Accumulation Chart Appearance | React "

component: "Accumulation Chart"

description: "We can customize chart appearance by using color palette, point level customization, chart area customization, title and margin customizations."
---

# Appearance

## Custom Color Palette

You can customize the default color of series or points by providing a custom color palette of your choice by
using the [`palettes`](../api/accumulation-chart/accumulationSeries/#palettes) property.

{% tab template="chart/series/pie", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { AccumulationChartComponent, AccumulationSeriesCollectionDirective, AccumulationSeriesDirective, PieSeries, Inject}
from'@syncfusion/ej2-react-charts';
import { accData } from 'datasource.ts';

class App extends React.Component<{}, {}> {
 constructor() {
    super(...arguments);
    this.palettes = [
      '#E94649',
      '#F6B53F',
      '#6FAAB0',
      '#FF33F3',
      '#228B22',
      '#3399FF',
    ];
  }
  render() {
    return <AccumulationChartComponent id='charts'>
      <Inject services={[PieSeries]} />
      <AccumulationSeriesCollectionDirective>
        <AccumulationSeriesDirective dataSource={accData} xName='x' yName='y' type='Pie' palettes= {this.palettes}>
        </AccumulationSeriesDirective>
      </AccumulationSeriesCollectionDirective>
    </AccumulationChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Animation

### Fluid Animation

Fluid animation used to animate series with updated dataSource continues animation rather than animation whole series. You can customize animation for a particular series using [`animate`] method.

{% tab template="chart/series/legend", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {
  AccumulationChartComponent,
  AccumulationSeriesCollectionDirective,
  AccumulationSeriesDirective,
  Inject,
  AccumulationChart,
  PieSeries,
  AccumulationLegend,
  AccumulationDataLabel,
  AccumulationTooltip,
  AccumulationSelection,
} from '@syncfusion/ej2-react-charts';
import { getInstance } from '@syncfusion/ej2-base';
import { accData } from './datasource.ts';

class App extends React.Component<{}, {}> {
  public count = 0;
  onChartLoad(args) {
    let pie = getInstance('#pie-chart2', AccumulationChart);
    document.getElementById('pie-chart2').setAttribute('title', '');
    pie.loaded = null;
    let pieinterval = setInterval(() => {
      if (document.getElementById('pie-chart2')) {
        if (this.count === 0) {
          pie.series[0].dataSource = [
            { x: 'Net-tution and Fees', y: 10 },
            { x: 'Self-supporting Operations', y: 10 },
            { x: 'Private Gifts', y: 13 },
            { x: 'All Other', y: 14 },
            { x: 'Local Revenue', y: 9 },
            { x: 'State Revenue', y: 13 },
            { x: 'Federal Revenue', y: 8 },
          ];
          pie.animate();
          this.count++;
        } else if (this.count === 1) {
          pie.series[0].dataSource = [
            { x: 'Net-tution and Fees', y: 120 },
            { x: 'Self-supporting Operations', y: 31 },
            { x: 'Private Gifts', y: 6 },
            { x: 'All Other', y: 12 },
            { x: 'Local Revenue', y: 25 },
            { x: 'State Revenue', y: 11 },
            { x: 'Federal Revenue', y: 12 },
          ];
          pie.animate();
          this.count++;
        } else if (this.count === 2) {
          pie.series[0].dataSource = [
            { x: 'Net-tution and Fees', y: 6 },
            { x: 'Self-supporting Operations', y: 22 },
            { x: 'Private Gifts', y: 11 },
            { x: 'All Other', y: 15 },
            { x: 'Local Revenue', y: 13 },
            { x: 'State Revenue', y: 10 },
            { x: 'Federal Revenue', y: 8 },
          ];
          pie.animate();
          this.count++;
        } else if (this.count === 3) {
          pie.series[0].dataSource = [
            { x: 'Net-tution and Fees', y: 15 },
            { x: 'Self-supporting Operations', y: 10 },
            { x: 'Private Gifts', y: 18 },
            { x: 'All Other', y: 20 },
            { x: 'Local Revenue', y: 30 },
            { x: 'State Revenue', y: 20 },
            { x: 'Federal Revenue', y: 25 },
          ];
          pie.animate();
          this.count++;
        } else if (this.count === 4) {
          pie.series[0].dataSource = [
            { x: 'Net-tution and Fees', y: 21 },
            { x: 'Self-supporting Operations', y: 10 },
            { x: 'Private Gifts', y: 15 },
            { x: 'All Other', y: 15 },
            { x: 'Local Revenue', y: 11 },
            { x: 'State Revenue', y: 20 },
            { x: 'Federal Revenue', y: 60 },
          ];
          pie.animate();
          this.count = 0;
        }
      } else {
        clearInterval(pieinterval);
      }
    }, 3000);
  }
  render() {
    return (
      <AccumulationChartComponent
        id="pie-chart2"
        title="Education Institutional Revenue"
        loaded={this.onChartLoad.bind(this)}
      >
        <Inject
          services={[
            AccumulationLegend,
            PieSeries,
            AccumulationDataLabel,
            AccumulationTooltip,
            AccumulationSelection,
          ]}
        />
        <AccumulationSeriesCollectionDirective>
          <AccumulationSeriesDirective
            name="Revenue"
            dataSource={accData}
            xName="x"
            yName="y"
            innerRadius="40%"
            startAngle={0}
            endAngle={360}
            dataLabel={{
              visible: true,
              position: 'Inside',
            }}
          ></AccumulationSeriesDirective>
        </AccumulationSeriesCollectionDirective>
      </AccumulationChartComponent>
    );
  }
}
ReactDOM.render(<App />, document.getElementById('charts'));

```

{% endtab %}
