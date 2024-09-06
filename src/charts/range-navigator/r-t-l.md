---
title: " RangeNavigator Selecting Range | React "

component: "RangeNavigator"

description: "The range navigator provides RTL (right-to-left) support. Axis labels, series types are rendered right to left when we enabled rtl property."
---

# RTL

The Range Selector supports right-to-left (RTL), which can be enabled with the [`enableRtl`](https://ej2.syncfusion.com/react/documentation/api/range-navigator/#enablertl) property.

{% tab template="rangenavigator/getting-started", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import {
     AreaSeries, DateTime, Inject, RangeNavigatorComponent, RangenavigatorSeriesCollectionDirective,
     RangenavigatorSeriesDirective,RangeTooltip,RangeTooltipSettingsModel
} from '@syncfusion/ej2-react-charts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { bitCoinData } from 'default_data.ts';

class App extends React.Component<{}, {}> {

  public data: object[] = bitCoinData;
  public tooltip: RangeTooltipSettingsModel = { enable: true };

  render() {
    return <RangeNavigatorComponent id='charts'
      valueType='DateTime' value={[new Date('2017-09-01'), new Date('2018-02-01')]}
      tooltip={this.tooltip} enableRtl={true}>
      <Inject services={[AreaSeries, DateTime, RangeTooltip]} />
      <RangenavigatorSeriesCollectionDirective>
        <RangenavigatorSeriesDirective dataSource={this.data} xName='x' yName='y' type='Area' width={2} />
      </RangenavigatorSeriesCollectionDirective>
    </RangeNavigatorComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}