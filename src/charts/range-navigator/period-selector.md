---
title: " RangeNavigator Period Selector | React "

component: "RangeNavigator"

description: "The period selector allows to select a range with specified periods."
---

# Period selector

The period selector allows to select a range with specified periods.

## Periods

An array of objects that allows the users to specify pre-defined time intervals. The [`interval`](https://ej2.syncfusion.com/react/documentation/api/range-navigator/#interval) property specifies the count value of the button, and the `text` property specifies the text to be displayed on the button. The [`intervaltype`](https://ej2.syncfusion.com/react/documentation/api/range-navigator/#intervaltype) property allows the users to customize the interval type, and it supports the following types:

* Auto
* Years
* Quarter
* Months
* Weeks
* Days
* Hours
* Minutes
* Seconds

{% tab template="rangenavigator/getting-started", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import {
     AreaSeries, DateTime, Inject, RangeNavigatorComponent, RangenavigatorSeriesCollectionDirective,
     RangenavigatorSeriesDirective,RangeTooltip, PeriodSelector, RangeTooltipSettingsModel, PeriodSelectorSettingsModel
} from '@syncfusion/ej2-react-charts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { bitCoinData } from 'default_data.ts';

class App extends React.Component<{}, {}> {

  public data: object[] = bitCoinData;
  public tooltip: RangeTooltipSettingsModel = { enable: true };
  public periodselector: PeriodSelectorSettingsModel = {
    position: 'Top',
    periods: [
      { text: '1M', interval: 1, intervalType: 'Months' },
      { text: '3M', interval: 3, intervalType: 'Months' },
      { text: '6M', interval: 6, intervalType: 'Months' }, { text: 'YTD' },
      { text: '1Y', interval: 1, intervalType: 'Years' },
      { text: '2Y', interval: 2, intervalType: 'Years', selected: true }, { text: 'All' }
    ]
  };

  render() {
    return <RangeNavigatorComponent id='charts'
      valueType='DateTime' labelFormat='MMM-yy' value={[new Date('2017-09-01'), new Date('2018-02-01')]}
      tooltip={this.tooltip}
      periodSelectorSettings={this.periodselector}>
      <Inject services={[AreaSeries, DateTime, RangeTooltip, PeriodSelector]} />
      <RangenavigatorSeriesCollectionDirective>
        <RangenavigatorSeriesDirective dataSource={this.data} xName='x' yName='y' type='Area' width={2} />
      </RangenavigatorSeriesCollectionDirective>
    </RangeNavigatorComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

>To use the period selector feature, inject the `PeriodSelector` module using the `RangeNavigator.Inject(PeriodSelector)` method.

## Positioning period selector

The [`position`](https://ej2.syncfusion.com/react/documentation/api/range-navigator/periodSelectorSettingsModel/#position) property allows the users to position the period selector at the **Top** or **Bottom**.

{% tab template="rangenavigator/getting-started", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import {
     AreaSeries, DateTime, Inject, RangeNavigatorComponent, RangenavigatorSeriesCollectionDirective,
     RangenavigatorSeriesDirective,RangeTooltip, PeriodSelector,RangeTooltipSettingsModel, PeriodSelectorSettingsModel
} from '@syncfusion/ej2-react-charts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { bitCoinData } from 'default_data.ts';

class App extends React.Component<{}, {}> {

  public data: object[] = bitCoinData;
  public tooltip: RangeTooltipSettingsModel = { enable: true };
  public periodselector: PeriodSelectorSettingsModel = {
    position: 'Bottom',
    periods: [
      { text: '1M', interval: 1, intervalType: 'Months' },
      { text: '3M', interval: 3, intervalType: 'Months' },
      { text: '6M', interval: 6, intervalType: 'Months' }, { text: 'YTD' },
      { text: '1Y', interval: 1, intervalType: 'Years' },
      { text: '2Y', interval: 2, intervalType: 'Years', selected: true }, { text: 'All' }
    ]
  };

  render() {
    return <RangeNavigatorComponent id='charts'
      valueType='DateTime' labelFormat='MMM-yy' value={[new Date('2017-09-01'), new Date('2018-02-01')]}
      tooltip={this.tooltip}
      periodSelectorSettings={this.periodselector}>
      <Inject services={[AreaSeries, DateTime, RangeTooltip, PeriodSelector]} />
      <RangenavigatorSeriesCollectionDirective>
        <RangenavigatorSeriesDirective dataSource={this.data} xName='x' yName='y' type='Area' width={2} />
      </RangenavigatorSeriesCollectionDirective>
    </RangeNavigatorComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

## Height

The [`height`](https://ej2.syncfusion.com/react/documentation/api/range-navigator/periodSelectorSettingsModel/#height) property allows the users to specify the height of the period selector. The default value of the height property is **43px**.

{% tab template="rangenavigator/getting-started", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import {
     AreaSeries, DateTime, Inject, RangeNavigatorComponent, RangenavigatorSeriesCollectionDirective,
     RangenavigatorSeriesDirective,RangeTooltip, PeriodSelector,RangeTooltipSettingsModel, PeriodSelectorSettingsModel
} from '@syncfusion/ej2-react-charts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { bitCoinData } from 'default_data.ts';

class App extends React.Component<{}, {}> {

  public data: object[] = bitCoinData;
  public tooltip: RangeTooltipSettingsModel = { enable: true };
  public periodselector: PeriodSelectorSettingsModel = {
    position: 'Top',
    height: 65,
    periods: [
      { text: '1M', interval: 1, intervalType: 'Months' },
      { text: '3M', interval: 3, intervalType: 'Months' },
      { text: '6M', interval: 6, intervalType: 'Months' }, { text: 'YTD' },
      { text: '1Y', interval: 1, intervalType: 'Years' },
      { text: '2Y', interval: 2, intervalType: 'Years', selected: true }, { text: 'All' }
    ]
  };

  render() {
    return <RangeNavigatorComponent id='charts'
      valueType='DateTime' labelFormat='MMM-yy' value={[new Date('2017-09-01'), new Date('2018-02-01')]}
      tooltip={this.tooltip}
      periodSelectorSettings={this.periodselector}>
      <Inject services={[AreaSeries, DateTime, RangeTooltip, PeriodSelector]} />
      <RangenavigatorSeriesCollectionDirective>
        <RangenavigatorSeriesDirective dataSource={this.data} xName='x' yName='y' type='Area' width={2} />
      </RangenavigatorSeriesCollectionDirective>
    </RangeNavigatorComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

## Visibility of range navigator

The [`disableRangeSelector`](https://ej2.syncfusion.com/react/documentation/api/range-navigator/#disablerangeselector) property allows the users to display only the period selector and not the Range Selector.

{% tab template="rangenavigator/getting-started", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import {
     AreaSeries, DateTime, Inject, RangeNavigatorComponent, RangenavigatorSeriesCollectionDirective,
     RangenavigatorSeriesDirective,RangeTooltip, PeriodSelector,RangeTooltipSettingsModel, PeriodSelectorSettingsModel
} from '@syncfusion/ej2-react-charts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { bitCoinData } from 'default_data.ts';

class App extends React.Component<{}, {}> {

  public data: object[] = bitCoinData;
  public tooltip: RangeTooltipSettingsModel = { enable: true };
  public periodselector: PeriodSelectorSettingsModel = {
    position: 'Top',
    periods: [
      { text: '1M', interval: 1, intervalType: 'Months' },
      { text: '3M', interval: 3, intervalType: 'Months' },
      { text: '6M', interval: 6, intervalType: 'Months' }, { text: 'YTD' },
      { text: '1Y', interval: 1, intervalType: 'Years' },
      { text: '2Y', interval: 2, intervalType: 'Years', selected: true }, { text: 'All' }
    ]
  };

  render() {
    return <RangeNavigatorComponent id='charts'
      valueType='DateTime' labelFormat='MMM-yy' value={[new Date('2017-09-01'), new Date('2018-02-01')]}
      dataSource={this.data} xName='x' yName='y'
      disableRangeSelector={true}
      tooltip={this.tooltip}
      periodSelectorSettings={this.periodselector}>
      <Inject services={[AreaSeries, DateTime, RangeTooltip, PeriodSelector]} />
    </RangeNavigatorComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}

## See Also

* [LightWeight](./lightweight/)