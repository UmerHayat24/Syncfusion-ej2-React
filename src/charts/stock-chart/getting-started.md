---
title: "Stock Chart Getting Started | React "

component: "Stock Chart"

description: "Getting started file explains how to configure and install chart packages and also how to create basic Stock Chart, module injections."
---
<!-- markdownlint-disable MD036 -->

# Getting Started

This section explains you the steps required to create a simple Stock Chart and demonstrate the basic usage of the Stock Chart control.

## Dependencies

Below is the list of minimum dependencies required to use the chart component.

```javascript

|-- @syncfusion/ej2-react-charts
    |-- @syncfusion/ej2-base
    |-- @syncfusion/ej2-data
    |-- @syncfusion/ej2-charts
    |-- @syncfusion/ej2-react-base
    |-- @syncfusion/ej2-pdf-export
    |-- @syncfusion/ej2-file-utils
    |-- @syncfusion/ej2-compression
    |-- @syncfusion/ej2-svg-base
    |-- @syncfusion/ej2-navigations
    |-- @syncfusion/ej2-calendars
    |-- @syncfusion/ej2-popups
    |-- @syncfusion/ej2-lists
    |-- @syncfusion/ej2-inputs
    |-- @syncfusion/ej2-buttons
    |-- @syncfusion/ej2-splitbuttons

```

## Installation and configuration

You can use [`create-react-app`](https://github.com/facebookincubator/create-react-app) to setup the applications.
To install `create-react-app` run the following command.

```sh
npm install -g create-react-app
```

* To setup basic `React` sample use following commands.

<div class='tsx'>

```sh
create-react-app quickstart --scripts-version=react-scripts-ts

cd quickstart

npm install

```

</div>

<div class='jsx'>

```sh

create-react-app quickstart

cd quickstart

```

</div>

* Install Syncfusion packages using below command.

```sh
npm install @syncfusion/ej2-react-charts --save
```

## Add Stock Chart to the Project

Now, you can start adding Chart component in the application.
For getting started, add the Chart component in `src/App.tsx` file using following code.

{% tab compileJsx=true%}

```tsx

import {StockChartComponent} from '@syncfusion/ej2-react-charts';
import * as React from 'react';

class  App  extends  React.Component  {

  render() {
    return  (<StockChartComponent />);
  }

}
export  default  App;

```

{% endtab %}

Now run the `npm start` command in the console, it will run your application and open the browser window.

```sh
npm start
```

he below example shows a basic Chart.

{% tab template="stock-chart/getting-started/initialize", sourceFiles="app/**/*.tsx", compileJsx=true,  isDefaultActive=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import {
    StockChartComponent, StockChartSeriesCollectionDirective, StockChartSeriesDirective, Inject, ITooltipRenderEventArgs, IStockChartEventArgs, ChartTheme,
    DateTime, Tooltip, RangeTooltip, Crosshair, LineSeries, SplineSeries, CandleSeries, HiloOpenCloseSeries, HiloSeries, RangeAreaSeries, Trendlines
} from '@syncfusion/ej2-react-charts';
import {
    EmaIndicator, RsiIndicator, BollingerBands, TmaIndicator, MomentumIndicator, SmaIndicator, AtrIndicator,
    AccumulationDistributionIndicator, MacdIndicator, StochasticIndicator, Export
} from '@syncfusion/ej2-react-charts';
import { chartData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

    render() {
        return (
            <StockChartComponent id='stockchart'
                primaryXAxis={{
                    valueType: 'DateTime',
                    majorGridLines: { width: 0 }, majorTickLines: { color: 'transparent' },
                    crosshairTooltip: { enable: true }
                }}
                primaryYAxis={{
                    labelFormat: 'n0',
                    lineStyle: { width: 0 }, rangePadding: 'None',
                    majorTickLines: { width: 0 }
                }}
                height='350'
            >
                <Inject services={[DateTime, Tooltip, RangeTooltip, Crosshair, LineSeries, SplineSeries, CandleSeries, HiloOpenCloseSeries, HiloSeries, RangeAreaSeries, Trendlines,
                    EmaIndicator, RsiIndicator, BollingerBands, TmaIndicator, MomentumIndicator, SmaIndicator, AtrIndicator, Export,
                    AccumulationDistributionIndicator, MacdIndicator, StochasticIndicator]} />
                <StockChartSeriesCollectionDirective>
                    <StockChartSeriesDirective dataSource={chartData} type='Candle'>
                    </StockChartSeriesDirective>
                </StockChartSeriesCollectionDirective>
            </StockChartComponent>
        )
    }
};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Module Injection

Stock Chart component are segregated into individual feature-wise modules. In order to use a particular feature,
you need to inject its feature service in the AppModule. In the current application, we are
going to modify the above basic chart to visualize stock value of a company.
For this application we are going to use candle series, tooltip, data label, DateTime axis
feature of the chart. Please find the relevant feature
service name and description as follows.

* `CandleSeries` - Inject this module in to `services` to use candle series.
* `Tooltip` - Inject this module in to `services` to use tooltip feature.
* `DataLabel` - Inject this module in to `services` to use datalabel feature.
* `DateTime`  - Inject this module in to `services` to use DateTime feature.

These modules should be injected to the `services` section as follows,

 {% tab compileJsx=true%}

```tsx
import { DateTime, StockChartComponent, DataLabel, CandleSeries, Tooltip } from '@syncfusion/ej2-react-charts';
import * as React from "react";
import * as ReactDOM from "react-dom";

class App extends React.Component<{}, {}> {

  render() {
    return <StockChartComponent id='stockcharts'>
      <Inject services={[CandleSeries, Tooltip, DataLabel, Category]} />
    </StockChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Populate Chart with Data

This section explains how to plot below JSON data to the  Stock Chart.Please find the below imported datasource.

{% tab compileJsx=true%}

```tsx
export let data: any[] = [{
            "x": new Date('2012-04-02T00:00:00.000Z'),
            "open": 320.705719,
            "high": 324.074066,
            "low": 317.737732,
            "close": 323.783783,
            "volume": 45638000
        }, {
            "x": new Date('2012-04-03T00:00:00.000Z'),
            "open": 323.028015,
            "high": 324.299286,
            "low": 319.639648,
            "close": 321.631622,
            "volume": 40857000
        }, {
            "x": new Date('2012-04-04T00:00:00.000Z'),
            "open": 319.544556,
            "high": 319.819824,
            "low": 315.865875,
            "close": 317.892883,
            "volume": 32519000
        }, {
            "x": new Date('2012-04-05T00:00:00.000Z'),
            "open": 316.436432,
            "high": 318.533539,
            "low": 314.599609,
            "close": 316.476471,
            "volume": 46327000
        }]
```

{% endtab %}

 Add a series object to the chart by using [`series`](../api/stock-chart/stockSeries/) property and then set the JSON data to [`dataSource`](../api/stock-chart/stockSeries/#datasource) property.

Since the JSON contains DateTime data, set the [`valueType`](../api/stock-chart/stockChartAxis/#valuetype)for horizontal axis to `DateTime`. By default, the axis valueType is `Numeric`.

{% tab template="stock-chart/getting-started/datasource", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import {
    StockChartComponent, StockChartSeriesCollectionDirective, StockChartSeriesDirective, Inject, ITooltipRenderEventArgs, IStockChartEventArgs, ChartTheme,
    DateTime, Tooltip, RangeTooltip, Crosshair, LineSeries, SplineSeries, CandleSeries, HiloOpenCloseSeries, HiloSeries, RangeAreaSeries, Trendlines
} from '@syncfusion/ej2-react-charts';
import {
    EmaIndicator, RsiIndicator, BollingerBands, TmaIndicator, MomentumIndicator, SmaIndicator, AtrIndicator,
    AccumulationDistributionIndicator, MacdIndicator, StochasticIndicator, Export
} from '@syncfusion/ej2-react-charts';
import { chartData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

    render() {
        return (
            <StockChartComponent id='stockchart'
                primaryXAxis={{
                    valueType: 'DateTime',
                    majorGridLines: { width: 0 }, majorTickLines: { color: 'transparent' },
                    crosshairTooltip: { enable: true }
                }}
                primaryYAxis={{
                    labelFormat: 'n0',
                    lineStyle: { width: 0 }, rangePadding: 'None',
                    majorTickLines: { width: 0 }
                }}
                height='350'
            >
                <Inject services={[DateTime, Tooltip, RangeTooltip, Crosshair, LineSeries, SplineSeries, CandleSeries, HiloOpenCloseSeries, HiloSeries, RangeAreaSeries, Trendlines,
                    EmaIndicator, RsiIndicator, BollingerBands, TmaIndicator, MomentumIndicator, SmaIndicator, AtrIndicator, Export,
                    AccumulationDistributionIndicator, MacdIndicator, StochasticIndicator]} />
                <StockChartSeriesCollectionDirective>
                    <StockChartSeriesDirective dataSource={chartData} type='Candle'>
                    </StockChartSeriesDirective>
                </StockChartSeriesCollectionDirective>
            </StockChartComponent>
        )
    }
};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Add Stock Chart Title

You can add a title using [`title`](../api/stock-chart/stockChartModel/#title) property to the Stock Chart to provide
quick information to the user about the data plotted in the chart.

{% tab template="stock-chart/getting-started/datasource", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import {
    StockChartComponent, StockChartSeriesCollectionDirective, StockChartSeriesDirective, Inject, ITooltipRenderEventArgs, IStockChartEventArgs, ChartTheme,
    DateTime, Tooltip, RangeTooltip, Crosshair, LineSeries, SplineSeries, CandleSeries, HiloOpenCloseSeries, HiloSeries, RangeAreaSeries, Trendlines
} from '@syncfusion/ej2-react-charts';
import {
    EmaIndicator, RsiIndicator, BollingerBands, TmaIndicator, MomentumIndicator, SmaIndicator, AtrIndicator,
    AccumulationDistributionIndicator, MacdIndicator, StochasticIndicator, Export
} from '@syncfusion/ej2-react-charts';
import { chartData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

    render() {
        return (
            <StockChartComponent id='stockchart'
                primaryXAxis={{
                    valueType: 'DateTime',
                    majorGridLines: { width: 0 }, majorTickLines: { color: 'transparent' },
                    crosshairTooltip: { enable: true }
                }}
                primaryYAxis={{
                    labelFormat: 'n0',
                    lineStyle: { width: 0 }, rangePadding: 'None',
                    majorTickLines: { width: 0 }
                }}
                title= 'Sales Analysis'
                height='350'
            >
                <Inject services={[DateTime, Tooltip, RangeTooltip, Crosshair, LineSeries, SplineSeries, CandleSeries, HiloOpenCloseSeries, HiloSeries, RangeAreaSeries, Trendlines,
                    EmaIndicator, RsiIndicator, BollingerBands, TmaIndicator, MomentumIndicator, SmaIndicator, AtrIndicator, Export,
                    AccumulationDistributionIndicator, MacdIndicator, StochasticIndicator]} />
                <StockChartSeriesCollectionDirective>
                    <StockChartSeriesDirective dataSource={chartData} type='Candle'>
                    </StockChartSeriesDirective>
                </StockChartSeriesCollectionDirective>
            </StockChartComponent>
        )
    }
};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Add Crosshair

Crosshair has a vertical and horizontal line to view the value of the axis at mouse or touch position.

Crosshair lines can be enabled by using [`enable`](../api/chart/crosshairSettings/#enable) property in the `crosshair`. Likewise tooltip label for an axis can be enabled by using [`enable`](../api/chart/crosshairTooltipModel/#enable) property of `crosshairTooltip` in the corresponding axis.

{% tab template="stock-chart/getting-started/crosshair", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import {
    StockChartComponent, StockChartSeriesCollectionDirective, StockChartSeriesDirective, Inject, ITooltipRenderEventArgs, IStockChartEventArgs, ChartTheme,
    DateTime, Tooltip, RangeTooltip, Crosshair, LineSeries, SplineSeries, CandleSeries, HiloOpenCloseSeries, HiloSeries, RangeAreaSeries, Trendlines
} from '@syncfusion/ej2-react-charts';
import {
    EmaIndicator, RsiIndicator, BollingerBands, TmaIndicator, MomentumIndicator, SmaIndicator, AtrIndicator,
    AccumulationDistributionIndicator, MacdIndicator, StochasticIndicator, Export
} from '@syncfusion/ej2-react-charts';
import { chartData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

    render() {
        return (
            <StockChartComponent id='stockchart'
                primaryXAxis={{
                    valueType: 'DateTime',
                    majorGridLines: { width: 0 }, majorTickLines: { color: 'transparent' },
                    crosshairTooltip: { enable: true }
                }}
                primaryYAxis={{
                    labelFormat: 'n0',
                    lineStyle: { width: 0 }, rangePadding: 'None',
                    majorTickLines: { width: 0 }
                }}
                title= 'Sales Analysis'
                crosshair={{ enable: true }}
                height='350'
            >
                <Inject services={[DateTime, Tooltip, RangeTooltip, Crosshair, LineSeries, SplineSeries, CandleSeries, HiloOpenCloseSeries, HiloSeries, RangeAreaSeries, Trendlines,
                    EmaIndicator, RsiIndicator, BollingerBands, TmaIndicator, MomentumIndicator, SmaIndicator, AtrIndicator, Export,
                    AccumulationDistributionIndicator, MacdIndicator, StochasticIndicator]} />
                <StockChartSeriesCollectionDirective>
                    <StockChartSeriesDirective dataSource={chartData} type='Candle'>
                    </StockChartSeriesDirective>
                </StockChartSeriesCollectionDirective>
            </StockChartComponent>
        )
    }
};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

## Add Trackball

Trackball is used to track a data point closest to the mouse or touch position. Trackball marker
indicates the closest point and trackball tooltip displays the information about the point.
To use trackball feature, we need to inject `Crosshair` and `Tooltip` module into the `services`.

Trackball can be enabled by setting the [`enable`](../api/chart/crosshairSettings/#enable) property
of the crosshair to true and [`shared`](../api/chart/tooltipSettingsModel/#shared) property
in `tooltip` to true in chart.

{% tab template="stock-chart/getting-started/trackball", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import {
    StockChartComponent, StockChartSeriesCollectionDirective, StockChartSeriesDirective, Inject, ITooltipRenderEventArgs, IStockChartEventArgs, ChartTheme,
    DateTime, Tooltip, RangeTooltip, Crosshair, LineSeries, SplineSeries, CandleSeries, HiloOpenCloseSeries, HiloSeries, RangeAreaSeries, Trendlines
} from '@syncfusion/ej2-react-charts';
import {
    EmaIndicator, RsiIndicator, BollingerBands, TmaIndicator, MomentumIndicator, SmaIndicator, AtrIndicator,
    AccumulationDistributionIndicator, MacdIndicator, StochasticIndicator, Export
} from '@syncfusion/ej2-react-charts';
import { trackData } from 'datasource.ts';

class App extends React.Component<{}, {}> {

    render() {
        return (
            <StockChartComponent id='stockchart'
                primaryXAxis={{
                    valueType: 'DateTime',
                }}
                height='350'
                title= 'Sales Analysis'
                tooltip={{ enable: true, shared: true, format: '${series.name} : ${point.x} : ${point.y}'}}
                crosshair={{ enable: true, lineType: 'Vertical' }}
            >
                <Inject services={[DateTime, Tooltip, RangeTooltip, Crosshair, LineSeries, SplineSeries, CandleSeries, HiloOpenCloseSeries, HiloSeries, RangeAreaSeries, Trendlines,
                    EmaIndicator, RsiIndicator, BollingerBands, TmaIndicator, MomentumIndicator, SmaIndicator, AtrIndicator, Export,
                    AccumulationDistributionIndicator, MacdIndicator, StochasticIndicator]} />
                <StockChartSeriesCollectionDirective>
                    <StockChartSeriesDirective dataSource={trackData} xName='x' yName='y' name='John' type='Line' width={2} marker={{ visible: true }}>
                    </StockChartSeriesDirective>
                    <StockChartSeriesDirective dataSource={trackData} xName='x' yName='y1' name='Andrew' type='Line' width={2} marker={{ visible: true }}></StockChartSeriesDirective>
                    <StockChartSeriesDirective dataSource={trackData} xName='x' yName='y2' name='Thomas' type='Line' width={2} marker={{ visible: true }}></StockChartSeriesDirective>
                    <StockChartSeriesDirective dataSource={trackData} xName='x' yName='y3' name='Mark' type='Line' width={2} marker={{ visible: true }}></StockChartSeriesDirective>
                    <StockChartSeriesDirective dataSource={trackData} xName='x' yName='y4' name='William' type='Line' width={2} marker={{ visible: true }}></StockChartSeriesDirective>
                </StockChartSeriesCollectionDirective>
            </StockChartComponent>
        )
    }
};
ReactDOM.render(<App />, document.getElementById("charts"));
```

{% endtab %}

> You can refer to our [React Stock Chart](https://www.syncfusion.com/react-ui-components/react-stock-chart) feature tour page for its groundbreaking feature representations. You can also explore our [React Stock Chart example](https://ej2.syncfusion.com/react/demos/#/material/stock-chart) that shows you how to present and manipulate data.