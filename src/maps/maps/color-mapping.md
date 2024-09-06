---
title: " Color Mapping in React Maps control | Syncfusion "

component: "Maps"

description: "Learn here all about Color Mapping feature of Syncfusion React Maps control and more."
---

# Color Mapping in React Maps control

Color mapping is used to customize the shape colors based on the given values. It has three types.

1. Range color mapping
2. Equal color mapping
3. Desaturation color mapping.

To add color mapping to the shapes of the Maps, bind the data source to the [`dataSource`](../api/maps/layerSettingsModel/#datasource) property of [`layerSettings`](../api/maps/layerSettingsModel) and set the field name which contains the color value in the data source to the [`colorValuePath`](../api/maps/shapeSettingsModel/#colorvaluepath) property.

## Types of color mapping

### Range color mapping

Range color mapping applies the color to the shapes of the Maps which matches the numeric values in the data source within the given color mapping ranges. The [`from`](../api/maps/colorMappingSettingsModel/#from) and [`to`](../api/maps/colorMappingSettingsModel/#to) properties in the [`colorMapping`](../api/maps/colorMappingSettingsModel/) are used to specify the color mapping ranges in the Maps.

{% tab compileJsx=true%}

```tsx
export let population_density = [
    ...
    {
        'code': 'AE',
        'value': 90,
        'name': 'United Arab Emirates',
        'population': 8264070,
        'density': 99
    },
    {
        'code': 'GB',
        'value': 257,
        'name': 'United Kingdom',
        'population': 62041708,
        'density': 255
    },
    {
        'code': 'US',
        'value': 34,
        'name': 'United States',
        'population': 325020000,
        'density': 33
    }
    ...
    ];
```

{% endtab %}

Bind the **population_density** data to the [`dataSource`](../api/maps/layerSettingsModel/#datasource) property of [`layerSettings`](../api/maps/layerSettingsModel/) and set the [`colorValuePath`](../api/maps/shapeSettingsModel/#colorvaluepath) property of [`shapeSettings`](../api/maps/shapeSettingsModel/) as **density**. The range values can be set using the [`from`](../api/maps/colorMappingSettingsModel/#from) and [`to`](../api/maps/colorMappingSettingsModel/#to) properties of [`colorMapping`](../api/maps/colorMappingSettingsModel/).

{% tab template="maps/default-map", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx
import { world_map } from 'world-map.ts';
import { population_density } from 'data.ts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective } from '@syncfusion/ej2-react-maps';

ReactDOM.render(
            <MapsComponent id="maps">
                <LayersDirective>
                    <LayerDirective shapeData={world_map} shapeDataPath='name' shapePropertyPath='name'
                        dataSource={population_density}
                        shapeSettings={ {
                            colorValuePath: 'density',
                            fill: '#E5E5E5',
                            colorMapping: [
                                {
                                    from: 0.00001, to: 100, color: 'rgb(153,174,214)'
                                },
                                {
                                    from: 100, to: 200, color: 'rgb(115,143,199)'
                                },
                                {
                                    from: 200, to: 300, color: 'rgb(77,112,184)'
                                },
                                {
                                    from: 300, to: 500, color: 'rgb(38,82,168)'
                                },
                                {
                                    from: 500, to: 19000, color: 'rgb(0,51,153)'
                                }
                            ]
                        } }>
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent>,
            document.getElementById("maps") as HTMLElement
);
```

{% endtab %}

### Equal color mapping

Equal color mapping applies the color to the shapes of the Maps when the [`value`](../api/maps/colorMappingSettingsModel/#value) property of [`colorMapping`](../api/maps/colorMappingSettingsModel/) matches with the values provided in the data source. The following example shows how to apply equal color mapping to the shapes with the data source **unCountries** which illustrates the permanent and non-permanent countries in the UN security council.

{% tab compileJsx=true%}

```tsx
export let unCountries: object[] = [
{ Country: 'China', Membership: 'Permanent' },
{ Country: 'France', Membership: 'Permanent' },
{ Country: 'Russia', Membership: 'Permanent' },
{ Country: 'United Kingdom', Membership: 'Permanent' },
{ Country: 'United States', Membership: 'Permanent' },
{ Country: 'Bolivia', Membership: 'Non-Permanent' },
{ Country: 'Eq. Guinea', Membership: 'Non-Permanent' },
{ Country: 'Ethiopia', Membership: 'Non-Permanent' },
{ Country: "Côte d'Ivoire", Membership: 'Permanent' },
{ Country: 'Kazakhstan', Membership: 'Non-Permanent' },
{ Country: 'Kuwait', Membership: 'Non-Permanent' },
{ Country: 'Netherlands', Membership: 'Non-Permanent' },
{ Country: 'Peru', Membership: 'Non-Permanent' },
{ Country: 'Poland', Membership: 'Non-Permanent' },
{ Country: 'Sweden', Membership: 'Non-Permanent' },
];
```

{% endtab %}

Bind the **unCountries** data to the [`dataSource`](../api/maps/layerSettingsModel/#datasource) property of [`layerSettings`](../api/maps/layerSettingsModel/) and set the [`colorValuePath`](../api/maps/shapeSettingsModel/#colorvaluepath) property of [`shapeSettings`](../api/maps/shapeSettingsModel/) as **Membership**. Set the [`value`](../api/maps/colorMappingSettingsModel/#value) property in the [`colorMapping`](../api/maps/colorMappingSettingsModel/) to **Permanent** and **Non-Permanent** in the different set of color mapping properties. If the corresponding value of the [`colorValuePath`](../api/maps/shapeSettingsModel/#colorvaluepath) property matches with the corresponding field name in the data source, then the given color will be applied.

{% tab template="maps/default-map", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx
import { world_map } from 'world-map.ts';
import { uncountries } from 'data.ts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective } from '@syncfusion/ej2-react-maps';

ReactDOM.render(
            <MapsComponent id="maps">
                <LayersDirective>
                    <LayerDirective shapeData={world_map} shapeDataPath='Country' shapePropertyPath='name'
                        dataSource={uncountries}
                        shapeSettings={ {
                            fill: '#E5E5E5',
                            colorMapping: [
                                {
                                    value: 'Permanent',
                                    color: '#EDB46F'
                                },
                                {
                                    color: '#F1931B',
                                    value: 'Non-Permanent'
                                }
                            ],
                            colorValuePath: 'Membership'
                        } }>
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent>,
            document.getElementById("maps") as HTMLElement
);
```

{% endtab %}

### Desaturation color mapping

Desaturation color mapping applies the color to the shapes of the Maps, similar to the range color mapping. The opacity will be applied in this color mapping based on the [`minOpacity`](../api/maps/colorMappingSettingsModel/#minopacity) and [`maxOpacity`](../api/maps/colorMappingSettingsModel/#maxopacity) properties in the [`colorMapping`](../api/maps/colorMappingSettingsModel/) property.

>The following example shows how to apply desaturation color mapping to the shapes with the data source  **population_density** that is available in the [Range color mapping](#range-color-mapping) section.

Bind the **population_density** data to the [`dataSource`](../api/maps/layerSettingsModel/#datasource) property of [`layerSettings`](../api/maps/layerSettingsModel/) and set the [`colorValuePath`](../api/maps/shapeSettingsModel/#colorvaluepath) property of [`shapeSettings`](../api/maps/shapeSettingsModel/) as **density**. The range values can be set using the [`from`](../api/maps/colorMappingSettingsModel/#from) and [`to`](../api/maps/colorMappingSettingsModel/#to) properties of [`colorMapping`](../api/maps/colorMappingSettingsModel/).

{% tab template="maps/default-map", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx
import { world_map } from 'world-map.ts';
import { population_density } from 'data.ts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective } from '@syncfusion/ej2-react-maps';

ReactDOM.render(
            <MapsComponent id="maps">
                <LayersDirective>
                    <LayerDirective shapeData={world_map} shapeDataPath='name' shapePropertyPath='name'
                        dataSource={population_density}
                        shapeSettings={ {
                            colorValuePath: 'density',
                            colorMapping: [
                                {
                                    from: 0, to: 100, color: 'rgb(153,174,214)',
                                    minOpacity: 0.2, maxOpacity: 1
                                },
                                {
                                    from: 101, to: 260, color: 'rgb(115,143,199)',
                                    minOpacity: 0.3, maxOpacity: 1
                                }
                            ]
                        } }>
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent>,
            document.getElementById("maps") as HTMLElement
);
```

{% endtab %}

## Multiple colors for a single shape

Multiple colors can be added to the color mapping which can be used as gradient effect to a specific shape based on the ranges in the data source. By using the [`color`](../api/maps/colorMappingSettingsModel/#color) property of [`colorMapping`](../api/maps/colorMappingSettingsModel/), any number of colors can be set to the shapes as a gradient.

>The following example demonstrates how to use multiple colors in color mapping with the data source  **population_density** that is available in the [Range color mapping](#range-color-mapping) section.

Bind the **population_density** data to the [`dataSource`](../api/maps/layerSettingsModel/#datasource) property of [`layerSettings`](../api/maps/layerSettingsModel/) and set the [`colorValuePath`](../api/maps/shapeSettingsModel/#colorvaluepath) property of [`shapeSettings`](../api/maps/shapeSettingsModel/) as **density**. The range values can be set using the [`from`](../api/maps/colorMappingSettingsModel/#from) and [`to`](../api/maps/colorMappingSettingsModel/#to) properties of [`colorMapping`](../api/maps/colorMappingSettingsModel/).

{% tab template="maps/default-map", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx
import { world_map } from 'world-map.ts';
import { population_density } from 'data.ts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective } from '@syncfusion/ej2-react-maps';

ReactDOM.render(
            <MapsComponent id="maps">
                <LayersDirective>
                    <LayerDirective shapeData={world_map} shapeDataPath='name' shapePropertyPath='name'
                        dataSource={population_density}
                        shapeSettings={ {
                            colorValuePath: 'density',
                            colorMapping: [
                                {
                                    from: 0, to: 100, color: ['red','blue']
                                },
                                {
                                    from: 101, to: 260, color: ['green','yellow']
                                }
                            ]
                        } }>
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent>,
            document.getElementById("maps") as HTMLElement
);
```

{% endtab %}

## Color for items excluded from color mapping

Color mapping can be applied to the shapes in the Maps which does not match color mapping criteria such as range or equal values using the [`color`](../api/maps/colorMappingSettingsModel/#color) property of [`colorMapping`](../api/maps/colorMappingSettingsModel/).

>The following example shows how to set the color for items excluded from the color mapping with the data source **population_density** that is available in the [Range color mapping](#range-color-mapping) section.

In the following example, color mapping is added for the ranges from 0 to 200. If there are any records in the data source that are outside of this range, the color mapping will not be applied. To apply the color for these excluded items, set the [`color`](../api/maps/colorMappingSettingsModel/#color) property alone in the [`colorMapping`](../api/maps/colorMappingSettingsModel/).

{% tab template="maps/default-map", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import { world_map } from 'world-map.ts';
import { population_density } from 'data.ts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective } from '@syncfusion/ej2-react-maps';

ReactDOM.render(
            <MapsComponent id="maps">
                <LayersDirective>
                    <LayerDirective shapeData={world_map} shapeDataPath='name' shapePropertyPath='name'
                        dataSource={population_density}
                        shapeSettings={ {
                            colorValuePath: 'density',
                            colorMapping: [
                            {
                                from: 0, to: 100, color: 'skyblue',
                            },
                            {
                                from: 101, to: 200, color: 'blue',
                            },
                            {
                                color: 'green'
                            } ]
                        } }>
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent>,
            document.getElementById("maps") as HTMLElement
);
```

{% endtab %}

## Color mapping for bubbles

The color mapping types such as range color mapping, equal color mapping and desaturation color mapping are applicable for bubbles in the Maps. To add color mapping for bubbles of the Maps, bind the data source to the [`dataSource`](../api/maps/bubbleSettingsModel/#datasource) property of [`bubbleSettings`](../api/maps/bubbleSettingsModel) and set the field name which contains the color value in the data source to the [`colorValuePath`](../api/maps/bubbleSettingsModel/#colorvaluepath) property. Multiple colors for a single set of bubbles and color for excluded items from [`colorMapping`](../api/maps/colorMappingSettingsModel/) are also applicable for bubbles.

{% tab template="maps/default-map", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx
import { world_map } from 'world-map.ts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective, Inject } from '@syncfusion/ej2-react-maps';
import { BubblesDirective, BubbleDirective, Bubble } from '@syncfusion/ej2-react-maps';


ReactDOM.render(
            <MapsComponent id="maps">
            <Inject services={[Bubble]}/>
                <LayersDirective>
                    <LayerDirective shapeData={world_map} shapeDataPath="name" shapePropertyPath="name">
                        <BubblesDirective>
                            <BubbleDirective visible={true} valuePath="population" dataSource={[
                                            { name: 'India', population: '38332521' },
                                            { name: 'New Zealand', population: '19651127' },
                                            { name: 'Pakistan', population: '3090416' }]}
                                            minRadius={5} colorValuePath= "population"  colorMapping={[
                                                { value: '38332521', color: '#C3E6ED' },
                                                { value: '19651127', color: '#F1931B' },
                                                { value: '3090416', color: 'blue'}]}/>
                        </BubblesDirective>
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent>,
            document.getElementById("maps") as HTMLElement
);
```

{% endtab %}