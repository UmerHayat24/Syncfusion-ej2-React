---
title: " Maps providers in React Maps control | Syncfusion "

component: "Maps"

description: "Learn here all about Maps providers of Syncfusion React Maps control and more."
---

# Map Providers in React Maps control

Maps control support map providers such as OpenStreetMap that can be added to any layers in maps.

## Open Street Map

OpenStreetMap(OSM) is a online map provider. The OpenStreetMap allows you to view, edit and use geographical data in a collaborative way from any place on the Earth. One of the most important features in Maps control is the built-in online map provider support. By using this feature, you can render OpenStreetMaps in the maps component. This provides the ability to visualize street map tiles without using any external shape files.

{% tab compileJsx=true%}

``` tsx
import * as React from 'react';
import { MapsComponent, LayersDirective, LayerDirective } from '@syncfusion/ej2-react-maps';
import './App.css';
class App extends React.Component {
    render() {
        return (
            <MapsComponent id="element">
                <LayersDirective>
                    <LayerDirective layerType="OSM"
                        urlTemplate="http://a.tile.openstreetmap.org/level/tileX/tileY.png">
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent>);
    }
}
export default App;
```

{% endtab %}

## Bing Maps

Bing Maps is a online map provider for accessing the external geospatial imagery services for deep-zoom satellite view which is supported in the Maps control. This provides the ability to visualize satellite, aerial, and street maps without using any external shape files.

{% tab compileJsx=true%}

```tsx
import * as React from 'react';
import { MapsComponent, LayersDirective, LayerDirective } from '@syncfusion/ej2-react-maps';
import './App.css';
class App extends React.Component {
    render() {
        return (
            <MapsComponent id="element">
                <LayersDirective>
                    <LayerDirective layerType="Bing" bingMapType="AerialWithLabel"
                    key="//Place your key"
                    >
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent>);
    }
}
export default App;
```

{% endtab %}