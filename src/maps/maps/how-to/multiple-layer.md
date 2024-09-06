# Multiple layer

## Adding multiple layers in the Map

The multilayer support allows loading multiple shape files in a single container and enables Maps to display more information. The shape layer is the main layer of the Maps. Multiple layers can be added in a shape layer as **SubLayer** using the [`type`](../api/maps/type/) property.

{% tab template="maps/default-map", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx
import { usa_map } from 'usa.ts';
import { california } from 'california.ts';
import { texas } from 'texas.ts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective } from '@syncfusion/ej2-react-maps';
//tslint:disable
ReactDOM.render(
      <MapsComponent id="maps">
        <LayersDirective>
          <LayerDirective shapeData={usa_map}
                          shapeSettings={ {
                              fill: '#E5E5E5',
                              border: {
                                  color: 'black',
                                  width: 0.1
                              }
                          } }>
          </LayerDirective>
          <LayerDirective shapeData={texas}
                          type='SubLayer'
                          shapeSettings= { {
                              fill: 'rgba(141, 206, 255, 0.6)',
                              border: {
                                  color: '#1a9cff',
                                  width: 0.25
                              }
                          } }>
          </LayerDirective>
          <LayerDirective shapeData={california}
                          type='SubLayer'
                          shapeSettings= { {
                              fill: 'rgba(141, 206, 255, 0.6)',
                              border: {
                                  color: '#1a9cff',
                                  width: 0.25
                              }
                          } }>
          </LayerDirective>
        </LayersDirective>
      </MapsComponent>,
      document.getElementById("maps") as HTMLElement
      );
  ```

{% endtab %}