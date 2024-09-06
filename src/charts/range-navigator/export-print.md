---
title: " RangeNavigator Export and Print | React "

component: "RangeNavigator"

description: "The rendered rangenavigator can be printed or exported directly from the browser by calling the public method print and export."
---

# Export and print

## Export

The rendered Range Selector can be exported to **JPEG**, **PNG**, **SVG**, or **PDF** format by using the [`export`](https://ej2.syncfusion.com/react/documentation/api/range-navigator/#export) method in the Range Selector. This method contains the following parameters:

* **Type** - To specify the export type. The component can be exported to **JPEG**, **PNG**, **SVG**, or **PDF** format.
* **File name** - To specify the file name to export.
* **Orientation** - To specify the orientation type. This is applicable only for PDF export type.

{% tab template="rangenavigator/export", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import {
     AreaSeries, DateTime, Inject, RangeNavigatorComponent, RangenavigatorSeriesCollectionDirective,
     RangenavigatorSeriesDirective,RangeTooltip, RangeNavigator,RangeTooltipSettingsModel
} from '@syncfusion/ej2-react-charts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { bitCoinData } from 'default_data.ts';

class App extends React.Component<{}, {}>{

  public data: object[] = bitCoinData;
  public tooltip: RangeTooltipSettingsModel = { enable: true };
  public clickHandler() {
    this.range.export('PNG', 'sample');
  }
  private range: RangeNavigator;

  render() {
    return (<div>
      <ButtonComponent value='export' onClick={this.clickHandler.bind(this)}>Export</ButtonComponent>
      <RangeNavigatorComponent id='charts' ref={g => this.range = g}
        valueType='DateTime' labelFormat='MMM-yy' value={[new Date('2017-09-01'), new Date('2018-02-01')]}
        tooltip={this.tooltip}>
        <Inject services={[AreaSeries, DateTime, RangeTooltip]} />
        <RangenavigatorSeriesCollectionDirective>
          <RangenavigatorSeriesDirective dataSource={this.data} xName='x' yName='y' type='Area' width={2} />
        </RangenavigatorSeriesCollectionDirective>
      </RangeNavigatorComponent></div>)
  }

};
ReactDOM.render(<App />, document.getElementById('charts'));

```

{% endtab %}

## Print

The rendered Range Selector can be printed directly from the browser by calling the public method [`print`](https://ej2.syncfusion.com/react/documentation/api/range-navigator/#print).

{% tab template="rangenavigator/print", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx

import {
     AreaSeries, DateTime, Inject, RangeNavigatorComponent, RangenavigatorSeriesCollectionDirective,
     RangenavigatorSeriesDirective,RangeTooltip, RangeNavigator,RangeTooltipSettingsModel
} from '@syncfusion/ej2-react-charts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { bitCoinData } from 'default_data.ts';

class App extends React.Component<{}, {}>{

  public data: object[] = bitCoinData;
  public tooltip: RangeTooltipSettingsModel = { enable: true };
  public clickHandler() {
    this.range.print();
  }
  private range: RangeNavigator;

  render() {
    return (<div> <ButtonComponent value='print' onClick={this.clickHandler.bind(this)}>Print</ButtonComponent>
      <RangeNavigatorComponent id='charts' ref={g => this.range = g}
        valueType='DateTime' labelFormat='MMM-yy' value={[new Date('2017-09-01'), new Date('2018-02-01')]}
        tooltip={this.tooltip}>
        <Inject services={[AreaSeries, DateTime, RangeTooltip]} />
        <RangenavigatorSeriesCollectionDirective>
          <RangenavigatorSeriesDirective dataSource={this.data} xName='x' yName='y' type='Area' width={2} />
        </RangenavigatorSeriesCollectionDirective>
      </RangeNavigatorComponent></div>)
  }

};
ReactDOM.render(<App />, document.getElementById('charts'));
```

{% endtab %}