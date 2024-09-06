---
title: " Layers in React Maps control | Syncfusion "

component: "Maps"

description: "Learn here all about Layers feature of Syncfusion React Maps control and more."
---

# Layers in React Maps control

The Maps control is rendered through [`layers`](../api/maps/#layers) and any number of layers can be added to the Maps.

## Multilayer

The Multilayer support allows loading multiple shape files and map providers in a single container, enabling Maps to display more information. The shape layer or map providers are the main layers of the Maps. Multiple layers can be added as **SubLayer** over the main layers using the [`type`](../api/maps/layerSettingsModel/#type) property of [`layers`](../api/maps/#layers).

## Sublayer

Sublayer is a type of shape file layer. It allows loading multiple shape files in a single map view. For example, a sublayer can be added over the main layer to view geographic features such as rivers, valleys and cities in a map of a country. Similar to the main layer, elements in the Maps such as markers, bubbles, color mapping and legends can be added to the sub-layer.

In this example, the United States map shape is used as shape data by utilizing **usa.ts** file, and **texas.ts** and **california.ts** files are used as sub-layers in the United States map.

{% tab template="maps/default-map", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx
//tslint:disable
import { texas } from 'texas.ts';
import { usa_map } from 'usa.ts';
import { california } from 'california.ts'
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective } from '@syncfusion/ej2-react-maps';

ReactDOM.render(
            <MapsComponent id="maps">
                <LayersDirective>
                    <LayerDirective shapeData={usa_map}
                        shapeSettings={ {
                            fill: '#E5E5E5',
                            border: { width: 0.1, color: 'Black' },
                        } } />
                    <LayerDirective shapeData={texas} type="SubLayer"
                        shapeSettings={ {
                            fill: 'rgba(141, 206, 255, 0.6)',
                            border: { width: 0.25, color: '#1a9cff' },
                        } } />
                    <LayerDirective shapeData={california} type="SubLayer"
                        shapeSettings={ {
                            fill: 'rgba(141, 206, 255, 0.6)',
                            border: { width: 0.25, color: '#1a9cff' },
                        } } />
                </LayersDirective>
            </MapsComponent>,
document.getElementById("maps") as HTMLElement
);

```

{% endtab %}

## Displaying different layer in the view

Multiple shape files and map providers can be loaded simultaneously in Maps. The [`baseLayerIndex`](../api/maps/mapsModel/#baselayerindex) property is used to determine which layer on the user interface should be displayed. This property is used for the Maps drill-down feature, so when the [`baseLayerIndex`](../api/maps/mapsModel/#baselayerindex) value is changed, the corresponding shape is loaded. In this example, two layers can be loaded with the World map and the United States map. Based on the given [`baseLayerIndex`](../api/maps/mapsModel/#baselayerindex) value the corresponding shape will be loaded in the user interface. If the [`baseLayerIndex`](../api/maps/mapsModel/#baselayerindex) value is set to **0**, then the world map will be loaded.

{% tab template="maps/default-map", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx
//tslint:disable
import { world_map } from 'world-map.ts';
import { usa_map } from 'usa.ts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective } from '@syncfusion/ej2-react-maps';

ReactDOM.render(
            <MapsComponent id="maps" baseLayerIndex={1}>
                <LayersDirective>
                    <LayerDirective shapeData={world_map} />
                    <LayerDirective shapeData={usa_map} />
                </LayersDirective>
            </MapsComponent>,
document.getElementById("maps") as HTMLElement
);

```

{% endtab %}