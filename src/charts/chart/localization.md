---
title: " Chart Localization | React "

component: "Chart"

description: "Localization library allows to localize the default text content of Chart."
---

# Localization

Localization library allows to localize the default text content of Chart. In Chart component,
it has the static text on some features(like zooming toolbars) and this can be changed to any other culture(Arabic, Deutsch, French, etc)
by defining the locale value and translation object.

<!-- markdownlint-disable MD033 -->

<table>
<tr>
<td><b>Locale key words</b></td>
<td><b>Text to display</b></td>
</tr>
<tr>
<td>Zoom</td>
<td>Zoom</td>
</tr>
<tr>
<td>ZoomIn</td>
<td>ZoomIn</td>
</tr>
<tr>
<td>ZoomOut</td>
<td>ZoomOut</td>
</tr>
<tr>
<td>Reset</td>
<td>Reset</td>
</tr>
<tr>
<td>Pan</td>
<td>Pan</td>
</tr>
<tr>
<td>ResetZoom</td>
<td>Reset Zoom</td>
</tr>
</table>

To load translation object in an application use load function of L10n class.

For more information about localization, refer this
[`localization`](http://ej2.syncfusion.com/development/react/documentation/base/localization.html)

{% tab template="chart/getting-started/localization", sourceFiles="app/**/*.tsx", compileJsx=true %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import {
    ChartComponent, SeriesCollectionDirective, AxesDirective, AxisDirective, SeriesDirective, Inject,
    ColumnSeries, Legend, Zoom, DataLabel,ZoomSettingsModel,AxisModel
} from '@syncfusion/ej2-react-charts';
import { L10n } from '@syncfusion/ej2-base';

L10n.load({
    'ar-AR': {
        'chart': {
            ZoomIn: 'تكبير',
            ZoomOut: 'تصغير',
            Zoom: 'زوم',
            Pan: 'مقلاة',
            Reset: 'إعادة تعيين',
        },
    }
});
class App extends React.Component<{}, {}> {

  public data: any[] = [
    { x: 1900, y: 4, y1: 2.6, y2: 2.8 }, { x: 1920, y: 3.0, y1: 2.8, y2: 2.5 },
    { x: 1940, y: 3.8, y1: 2.6, y2: 2.8 }, { x: 1960, y: 3.4, y1: 3, y2: 3.2 },
    { x: 1980, y: 3.2, y1: 3.6, y2: 2.9 }, { x: 2000, y: 3.9, y1: 3, y2: 2 }
  ];
  public primaryxAxis: AxisModel = { edgeLabelPlacement: 'Shift', title: 'Years' };
  public primaryyAxis: AxisModel = { title: 'Sales Amount in Millions' };
  public zoomsettings: ZoomSettingsModel = {
    enableMouseWheelZooming: true, enablePinchZooming: true,
    enableSelectionZooming: true
  };
  public marker = { dataLabel: { visible: true } };

  render() {
    return <ChartComponent id='charts'
      primaryXAxis={this.primaryxAxis}
      primaryYAxis={this.primaryyAxis}
      title='Average Sales Comparison'
      zoomSettings={this.zoomsettings}
      locale='ar-AR'>
      <Inject services={[ColumnSeries, Legend, Zoom, DataLabel]} />
      <SeriesCollectionDirective>
        <SeriesDirective dataSource={this.data} xName='x' yName='y' name='Product X' type='Column'
          marker={this.marker}>
        </SeriesDirective>
        <SeriesDirective dataSource={this.data} xName='x' yName='y1' name='Product Y' type='Column'
          marker={this.marker}>
        </SeriesDirective>
      </SeriesCollectionDirective>
    </ChartComponent>
  }

};
ReactDOM.render(<App />, document.getElementById("charts"));

```

{% endtab %}