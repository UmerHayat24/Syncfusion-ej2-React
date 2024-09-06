---
title: "Bing Maps in React Maps control | Syncfusion"

component: "Maps"

description: "Learn here all about Bing Maps of Syncfusion React Maps control and more."
---

# Bing Maps in React Maps

Bing Maps is a online Maps provider, owned by Microsoft. As like OSM, it provide Maps tile images based on our requests and combines those images into a single one to display Maps area.

## Adding Bing Maps

The Bing Maps can be rendered by setting the [`layerType`](../api/maps/layerSettingsModel/#layertype) property as **Bing** and the key for the Bing Maps must be set in the [`key`](../api/maps/layerSettingsModel/#key) property. The Bing Maps key can be obtained from [here](https://www.microsoft.com/en-us/maps/create-a-bing-maps-key).

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective } from '@syncfusion/ej2-react-maps';

ReactDOM.render(
            <MapsComponent id="maps">
                <LayersDirective>
                    <LayerDirective layerType='Bing'
                                    bingMapType= 'AerialWithLabel'
                                    key= '//bingmapkey'
                    />
                </LayersDirective>
            </MapsComponent>,
document.getElementById("maps") as HTMLElement
);


```

>Specify Bing Maps key in the `key` property.

## Types of Bing Maps

Bing Maps provides different types of Maps and it is supported in the Maps control.

* **Aerial** - Displays satellite images to highlight roads and major landmarks for easy identification.
* **AerialWithLabel** - Displays aerial Maps with labels for the continent, country, ocean, etc.
* **Road** - Displays the default Maps view of roads, buildings, and geography.
* **CanvasDark** - Displays dark version of the road Maps.
* **CanvasLight** - Displays light version of the road Maps.
* **CanvasGray** - Displays grayscale version of the road Maps.

To render the light version of the road Maps, set the `bingMapType` to `CanvasLight` as demonstrated in the following code sample.

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective, Zoom, Inject } from '@syncfusion/ej2-react-maps';

ReactDOM.render(
            <MapsComponent id="maps" zoomSettings= {{ zoomFactor: 4 }}
                                    centerPosition = {{
                                        latitude : 38.8951,
                                        longitude : -77.0364
                                    }}>
                <Inject services={[Zoom]} />
                <LayersDirective>
                    <LayerDirective layerType='Bing'
                                    bingMapType= 'CanvasLight'
                                    key= '// ...bingMapKey'
                    />
                </LayersDirective>
            </MapsComponent>,
document.getElementById("maps") as HTMLElement
);

```

>Specify Bing Maps key in the `key` property.

## Zooming and Panning

Bing Maps layer can be zoomed and panned. Zooming helps to get a closer look at a particular area on a Maps for in-depth analysis. Panning helps to move a Maps around to focus the targeted area.

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective, Zoom, Inject } from '@syncfusion/ej2-react-maps';

ReactDOM.render(
            <MapsComponent id="maps" zoomSettings= {{
                                        enable : true,
                                        toolbars:[ "Zoom", "ZoomIn", "ZoomOut", "Pan", "Reset" ]}}>
                <Inject services={[Zoom]} />
                <LayersDirective>
                    <LayerDirective layerType='Bing'
                                    key='// ...bingMapKey'
                    />
                </LayersDirective>
            </MapsComponent>,
document.getElementById("maps") as HTMLElement
);

```

>Specify Bing Maps key in the `key` property.

## Adding markers and navigation line

Markers can be added to the layers of Bing Maps by setting the corresponding location's coordinates of latitude and longitude using [`markerSettings`](../api/maps/layerSettingsModel/#markersettings). Navigation lines can be added on top of an Bing Maps layer for highlighting a path among various places by setting the corresponding location's coordinates of latitude and longitude in the [`navigationLineSettings`](../api/maps/layerSettingsModel/#navigationlinesettings).

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, MarkersDirective, NavigationLineDirective, NavigationLinesDirective, MarkerDirective, LayersDirective, LayerDirective, Inject, Zoom, Marker, NavigationLine } from '@syncfusion/ej2-react-maps';

ReactDOM.render(
            <MapsComponent id="maps" zoomSettings= {{
                                        zoomFactor : 4
                                        }}
                                        centerPosition = {{
                                            latitude: 29.394708,
                                            longitude: -94.954653
                                        }}>
            <Inject services={[Zoom, Marker, NavigationLine]} />
                <LayersDirective>
                    <LayerDirective layerType='OSM'>
                        <MarkersDirective>
                            <MarkerDirective visible={true}
                                            height={25}
                                            width={15}
                                            dataSource={[
                                                {
                                                    latitude: 34.060620,
                                                    longitude: -118.330491,
                                                    name: "California"
                                                },
                                                {
                                                    latitude: 40.724546,
                                                    longitude: -73.850344,
                                                    name: "New York"
                                                }
                                            ]}
                                        >
                            </MarkerDirective>
                        </MarkersDirective>
                        <NavigationLinesDirective>
                            <NavigationLineDirective visible={true}
                                                     latitude={[34.060620, 40.724546]}
                                                     longitude={[-118.330491,-73.850344]}
                                                     color="blue"
                                                     angle={90}
                                                     width={5} />
                        </NavigationLinesDirective>
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent>,
document.getElementById("maps") as HTMLElement
);

```

>Specify Bing Maps key in the `Key` property.

## Sublayer

Any GeoJSON shape can be rendered as a sublayer on top of the Bing Maps layer for highlighting a particular continent or country in Bing Maps by adding another layer and specifying the [`type`](../api/maps/layerSettingsModel/#type) property of Maps layer to **SubLayer**.