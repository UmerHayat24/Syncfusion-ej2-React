# Marker type

## Add different types of markers

Different marker objects can be added to the Maps component using the marker settings. To update different marker settings in Maps, please follow the given steps:

**Step 1**:

Initialize the Maps control with marker settings. Here, a marker has been added with specified latitude and longitude of California by using the [`dataSource`](../api/maps/markerSettingsModel/#datasource) property. To customize the shape of the marker using the [`shape`](../api/maps/markerSettingsModel/#shape) property and change the border color and width of the marker using the [`border`](../api/maps/markerSettingsModel/#border) property as mentioned in the following example.

{% tab template="maps/default-map", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx
import { usa_map } from 'usa.ts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import {
  MapsComponent, LayersDirective, LayerDirective, MarkersDirective,
  MarkerDirective, Inject, Marker
} from '@syncfusion/ej2-react-maps';
ReactDOM.render(
      <MapsComponent id="element">
        <Inject services={[Marker]} />
        <LayersDirective>
          <LayerDirective shapeData={usa_map}>
            <MarkersDirective>
              <MarkerDirective visible={true} shape='Circle' fill='white' width={3} animationDuration={0}
                dataSource={[
                  { latitude: 37.0000, longitude: -120.0000, city: 'California' }
                ]}
                border={{ width: 2, color: '#333' }}>
              </MarkerDirective>
            </MarkersDirective>
          </LayerDirective>
        </LayersDirective>
      </MapsComponent>,
       document.getElementById("maps") as HTMLElement
      );
```

{% endtab %}

**Step 2**:

Customize the above option for n number of markers as mentioned in the following example.

{% tab template="maps/default-map", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx
import { usa_map } from 'usa.ts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import {
  MapsComponent, LayersDirective, LayerDirective, MarkersDirective,
  MarkerDirective, Inject, Marker
} from '@syncfusion/ej2-react-maps';
//tslint disable
ReactDOM.render(
      <MapsComponent id="maps">
        <Inject services={[Marker]} />
        <LayersDirective>
          <LayerDirective shapeData={usa_map}>
            <MarkersDirective>
              <MarkerDirective visible={true} shape='Circle' fill='white' width={3} animationDuration={0}
                dataSource={[
                  { latitude: 37.0000, longitude: -120.0000, city: 'California' }
                ]}
                border={
                  { width: 2, color: '#333' }
                  }>
                </MarkerDirective>
              <MarkerDirective visible={true} shape='Rectangle' fill='yellow' width={15} height={4} animationDuration={0}
                dataSource={[
                  { latitude: 40.7127, longitude: -74.0059, city: 'New York' }
                ]}
                border={
                  { width: 2, color: '#333' }
                  }>
                </MarkerDirective>
              <MarkerDirective visible={true} shape='Diamond' fill='white' width={10} height={10} animationDuration={0}
                dataSource={[
                  { latitude: 42, longitude: -93, city: 'Iowa' }
                ]}
                border={
                  { width: 2, color: 'blue' }
                  }>
                </MarkerDirective>
              <MarkerDirective visible={true} shape='Balloon' fill='red' width={10} height={15} animationDuration={0}
                dataSource={[
                  { latitude: 36.499589049395055, longitude: -103.042108197135548, city: 'New Mexico' }
                ]}
                border={
                  { width: 2, color: '#333' }
                  }>
                </MarkerDirective>
              <MarkerDirective visible={true} shape='Triangle' fill='blue' width={10} animationDuration={0}
                dataSource={[
                  { latitude: 36.360624205142919, longitude: -94.595916790727287, city: 'Oklahoma' }
                ]}
                border={
                  { width: 2, color: '#333' }
                  }>
                </MarkerDirective>
            </MarkersDirective>
          </LayerDirective>
        </LayersDirective>
      </MapsComponent>,
      document.getElementById("maps") as HTMLElement
      );
```

{% endtab %}