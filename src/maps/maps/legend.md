---
title: "Legend in React Maps control | Syncfusion"

component: "Maps"

description: "Learn here all about Legend feature of Syncfusion React Maps control and more."
---

# Legend in React Maps control

A Legend is a visual representation of the symbols used on the Maps. It can be represented in various colors, shapes or other identifiers based on the data and provides valuable information for interpreting what the Maps are displaying. It explains what each symbol in the Maps represents. Legends are enabled by setting the [`visible`](../api/maps/legendSettingsModel/#visible) property of [`legendSettings`](../api/maps/legendSettingsModel)  to **true**.

## Modes of legend

Legend had two types of mode.
1. **Default** mode
2. **Interactive** mode

### Default mode

Default mode legends having symbols with legend labels, used to identify the shape or bubble or marker color. To enable this option by setting the [`mode`](../api/maps/legendSettingsModel/#mode) property of [`legendSettings`](../api/maps/legendSettingsModel) as **Default**.

### Interactive mode

The legends can be made interactive with an arrow mark indicating the exact range color in the legend when the mouse hovers over the corresponding shapes. To enable this type of mode by setting the [`mode`](../api/maps/legendSettingsModel/#mode) property of [`legendSettings`](../api/maps/legendSettingsModel) as **Interactive**. The [`invertedPointer`](../api/maps/legendSettingsModel/#invertedpointer) property is used to enable or disable the visibility of the inverted pointer in interactive legend in Maps.

{% tab template="maps/default-map", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx
import { world_map } from 'world-map.ts';
import { uncountries } from 'data.ts'
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective, Inject, Legend } from '@syncfusion/ej2-react-maps';

ReactDOM.render(
            <MapsComponent id="maps" legendSettings={ {
                                        visible: true,
                                        mode: 'Interactive',
                                        invertedPointer: true
                                    } } >
            <Inject services={[Legend]} />
                <LayersDirective>
                    <LayerDirective shapeData={world_map} shapeDataPath='Country' shapePropertyPath='name' dataSource={uncountries}
                        shapeSettings={ {
                            colorValuePath: 'Membership',
                            colorMapping: [
                                { value: 'Permanent', color: '#D84444' },
                                { value: 'Non-Permanent', color: '#316DB5'}
                            ]
                        } }>
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent>,
document.getElementById("maps") as HTMLElement
);
```

{% endtab %}

## Positioning of the legend

The legend can be positioned in the following two ways:

* Absolute position
* Dock position

<b>Absolute position</b>

The legend of the Maps can be positioned using the [`location`](../api/maps/legendSettingsModel/#location) property in the [`legendSettings`](../api/maps/legendSettingsModel). For positioning the legend based on co-ordinates corresponding to a Maps, the [`position`](../api/maps/legendSettingsModel/#position) property is set as **Float**.

<b>Dock position</b>

Legends are positioned in the following locations within the container. The [`position`](../api/maps/legendSettingsModel/#position) property in [`legendSettings`](../api/maps/legendSettingsModel) is used to set these options in Maps.

* Top
* Left
* Bottom
* Right

The above four positions can be aligned with combination of **Near**, **Center** and **Far** using [`alignment`](../api/maps/legendSettingsModel/#alignment) property in [`legendSettings`](../api/maps/legendSettingsModel). So, the legend can be aligned to 12 positions.

{% tab template="maps/default-map", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx
import { world_map } from 'world-map.ts';
import { uncountries } from 'data.ts'
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective, Inject, Legend } from '@syncfusion/ej2-react-maps';

ReactDOM.render(
            <MapsComponent id="maps" legendSettings={ {
                                        visible: true,
                                        position: 'Top',
                                        alignment: 'Near'
                                    } } >
            <Inject services={[Legend]} />
                <LayersDirective>
                    <LayerDirective shapeData={world_map} shapeDataPath='Country' shapePropertyPath='name' dataSource={uncountries}
                        shapeSettings={ {
                            colorValuePath: 'Membership',
                            colorMapping: [
                                { value: 'Permanent', color: '#D84444' },
                                { value: 'Non-Permanent', color: '#316DB5'}
                            ]
                        } }>
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent>,
document.getElementById("maps") as HTMLElement
);
```

{% endtab %}

## Legend for shapes

Legend for shapes can be generated from color mapping types such as equal color mapping, range color mapping and desaturation color mapping.

The below code snippet demonstrate the equal color mapping legends for the shapes. To bind the given data source to the [`dataSource`](../api/maps/layerSettingsModel/#datasource) property of [`layerSettings`](../api/maps/layerSettingsModel/). Set the value of [`shapePropertyPath`](../api/maps/layerSettingsModel/#shapepropertypath) to **name** and [`shapeDataPath`](../api/maps/layerSettingsModel/#shapedatapath) to **Country**. To enable equal color mapping, set the [`colorMapping`](../api/maps/colorMappingSettingsModel/) as an array in [`shapeSettings`](../api/maps/shapeSettingsModel/). Finally, set the [`visible`](../api/maps/legendSettingsModel/#visible) property of [`legendSettings`](../api/maps/legendSettingsModel) as **true**. The [`label`](../api/maps/colorMappingSettingsModel/#label) property in [`colorMapping`](../api/maps/colorMappingSettingsModel/) is used to set the text name for legend in Maps.

{% tab template="maps/default-map", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx
import { world_map } from 'world-map.ts';
import { uncountries } from 'data.ts'
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective, Inject, Legend } from '@syncfusion/ej2-react-maps';

ReactDOM.render(
            <MapsComponent id="maps" legendSettings={ { visible: true } } >
            <Inject services={[Legend]} />
                <LayersDirective>
                    <LayerDirective shapeData={world_map} shapeDataPath='Country' shapePropertyPath='name' dataSource={uncountries}
                        shapeSettings={ {
                            colorValuePath: 'Membership',
                            colorMapping: [
                                { value: 'Permanent', color: '#D84444' },
                                { value: 'Non-Permanent', color: '#316DB5'}
                            ]
                        } }>
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent>,
document.getElementById("maps") as HTMLElement
);
```

{% endtab %}

### Legend shape

Maps supports the following types of legend shapes. The [`shape`](../api/maps/legendSettingsModel/#shape) property in the [`legendSettings`](../api/maps/legendSettingsModel) can be used to change the type of legend shapes.

* Circle
* Rectangle
* Triangle
* Diamond
* Cross
* Star
* HorizontalLine
* VerticalLine
* Pentagon
* InvertedTriangle

The shape of legends can be customized by using the [`shapeWidth`](../api/maps/legendSettingsModel/#shapewidth), [`shapeHeight`](../api/maps/legendSettingsModel/#shapeheight), [`shapeBorder`](../api/maps/legendSettingsModel/#shapeborder) and [`shapePadding`](../api/maps/legendSettingsModel/#shapepadding) properties.

### Customization

The following properties are available in legend to customize the legend shape and legend text in Maps.

* [`background`](../api/maps/legendSettingsModel/#background) - To customize the background color of the Legend.
* [`border`](../api/maps/legendSettingsModel/#border) - To customize the color, width and opacity of the border for the Legend.
* [`fill`](../api/maps/legendSettingsModel/#fill) - To apply the color for the Legend.
* [`labelDisplayMode`](../api/maps/legendSettingsModel/#labeldisplaymode) - To customize the display mode for the Legend text.
* [`labelPosition`](../api/maps/legendSettingsModel/#labelposition) - To customize the position of the Legend text.
* [`orientation`](../api/maps/legendSettingsModel/#orientation) - To customize the orientation of the Legend.
* [`textStyle`](../api/maps/legendSettingsModel/#textstyle) - To customize the text style for Legend.
* [`title`](../api/maps/legendSettingsModel/#title) - To apply the title for the Legend.
* [`titleStyle`](../api/maps/legendSettingsModel/#titlestyle) - To customize the style of the title for the Legend.
* [`height`](../api/maps/legendSettingsModel/#height) - To customize the height of the Legend.
* [`width`](../api/maps/legendSettingsModel/#width) - To customize the width of the Legend.
* [`opacity`](../api/maps/legendSettingsModel/#opacity) - To apply the opacity to the Legend.

{% tab template="maps/default-map", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx
import { world_map } from 'world-map.ts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective, Inject, Legend } from '@syncfusion/ej2-react-maps';

ReactDOM.render(
            <MapsComponent id="maps" legendSettings={ {
                                        visible: true,
                                        background: 'green',
                                        border: {
                                            color: 'blue',
                                            width: 2
                                        },
                                        fill: 'orange',
                                        labelPosition: 'Before',
                                        orientation: 'Vertical',
                                        textStyle: {
                                            size: '12px',
                                            color: 'red',
                                            fontStyle: 'italic'
                                        },
                                        title: {
                                            description: 'Legend title',
                                            text: 'Legend'
                                        },
                                        titleStyle: {
                                            size: '12px',
                                            color: '#d6e341',
                                            fontStyle: 'italic'
                                        }
                                    } } >
            <Inject services={[Legend]} />
                <LayersDirective>
                    <LayerDirective shapeData={world_map} shapeDataPath='Country' shapePropertyPath='name' dataSource={[
                        {  "Country": "China", "Membership": "Permanent" },
                        { "Country": "France", "Membership": "Permanent" },
                        { "Country": "Russia", "Membership": "Permanent" },
                        { "Country": "Kazakhstan", "Membership": "Non-Permanent" },
                        { "Country": "Poland", "Membership": "Non-Permanent" },
                        { "Country": "Sweden", "Membership": "Non-Permanent" }
                    ]}
                        shapeSettings={ {
                            colorValuePath: 'Membership',
                            colorMapping: [
                               { value: 'Permanent', color: '#D84444' },
                               { value: 'Non-Permanent', color: '#316DB5' }]
                            } }>
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent>,
document.getElementById("maps") as HTMLElement
);
```

{% endtab %}

### Legend for items excluded from color mapping

The legend can be enabled for items excluded from the color mapping using the [`color`](../api/maps/colorMappingSettingsModel/#color) property in [`colorMapping`](../api/maps/colorMappingSettingsModel/). Refer to the **population_density** data which demonstrates the population density of some countries.

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

In the following example, color mapping is added for the ranges from **0** to **200**. If there are any records in the data source that are outside of this range, the color mapping will not be applied. To apply the color for these excluded items, set the [`color`](../api/maps/colorMappingSettingsModel/#color) property alone in the [`colorMapping`](../api/maps/colorMappingSettingsModel/). To enable legend for these items, set the [`visible`](../api/maps/legendSettingsModel/#visible) property of [`legendSettings`](../api/maps/legendSettingsModel/) to **true**.

{% tab template="maps/default-map", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx
import { world_map } from 'world-map.ts';
import { uncountries } from 'data.ts'
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective, Inject, Legend } from '@syncfusion/ej2-react-maps';

ReactDOM.render(
            <MapsComponent id="maps" legendSettings={ { visible: true } } >
            <Inject services={[Legend]} />
                <LayersDirective>
                    <LayerDirective shapeData={world_map} shapeDataPath='Country' shapePropertyPath='name' dataSource={uncountries}
                        shapeSettings={ {
                            colorValuePath: 'Membership',
                            colorMapping: [
                                { from: 0, to: 100, color: 'rgb(153,174,214)' },
                                { from: 101, to: 200, color: 'rgb(115,143,199)' },
                                { color: 'rgb(77,112,184)' }
                            ]
                        } }>
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent>,
document.getElementById("maps") as HTMLElement
);
```

{% endtab %}

### Hide desired legend items

Use the [`showLegend`](../api/maps/colorMappingSettingsModel/#showlegend) in the [`colorMapping`](../api/maps/colorMappingSettingsModel/) property to show or hide the desired legend items in Maps. If the [`showLegend`](../api/maps/colorMappingSettingsModel/#showlegend) property is set to **false**, the legend item will be hidden. otherwise, it will be visible.

{% tab template="maps/default-map", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx
import { world_map } from 'world-map.ts';
import { uncountries } from 'data.ts'
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective, Inject, Legend } from '@syncfusion/ej2-react-maps';

ReactDOM.render(
            <MapsComponent id="maps" legendSettings={ { visible: true } } >
            <Inject services={[Legend]} />
                <LayersDirective>
                    <LayerDirective shapeData={world_map} shapeDataPath='Country' shapePropertyPath='name' dataSource={uncountries}
                        shapeSettings={ {
                            colorValuePath: 'Membership',
                            colorMapping: [
                                {
                                    from: 0, to: 100, color: 'rgb(153,174,214)', showLegend: true
                                },
                                {
                                    from: 101, to: 200, color: 'rgb(115,143,199)', showLegend: false
                                },
                                {
                                    color: 'rgb(77,112,184)', showLegend: false
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

### Hide legend items based on data source value

Depending on the boolean values provided in the data source, the legend items will be hidden or visible. Bind the field name that contains the visibility state in the data source to the [`showLegendPath`](../api/maps/legendSettingsModel/#showlegendpath) property of the [`legendSettings`](../api/maps/legendSettingsModel/) to achieve this.

{% tab template="maps/default-map", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx
import { world_map } from 'world-map.ts';
import { dafaultData } from 'data.ts'
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective, Inject, Legend } from '@syncfusion/ej2-react-maps';

ReactDOM.render(
            <MapsComponent id="maps" legendSettings={ { visible: true , showLegendPath: 'visibility'} } >
            <Inject services={[Legend]} />
                <LayersDirective>
                    <LayerDirective shapeData={world_map} shapeDataPath='continent' shapePropertyPath='continent' dataSource={dafaultData}
                        shapeSettings={ {
                            colorValuePath: 'color',
                        } }>
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent>,
document.getElementById("maps") as HTMLElement
);
```

{% endtab %}

### Binding legend item text from data source

To show the legend text based on values provided in the data source, use the [`valuePath`](../api/maps/legendSettingsModel/#valuepath) property in the [`legendSettings`](../api/maps/legendSettingsModel/).

{% tab template="maps/default-map", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx
import { world_map } from 'world-map.ts';
import { dafaultData } from 'data.ts'
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective, Inject, Legend } from '@syncfusion/ej2-react-maps';

ReactDOM.render(
            <MapsComponent id="maps" legendSettings={ { visible: true , valuePath: 'continent' } } >
            <Inject services={[Legend]} />
                <LayersDirective>
                    <LayerDirective shapeData={world_map} shapeDataPath='continent' shapePropertyPath='continent' dataSource={dafaultData}
                        shapeSettings={ {
                            colorValuePath: 'color',
                        } }>
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent>,
document.getElementById("maps") as HTMLElement
);
```

{% endtab %}

### Hide duplicate legend items

To hide the duplicate legend items in Maps, set the [`removeDuplicateLegend`](../api/maps/legendSettingsModel/#removeduplicatelegend) property to **true** in the [`legendSettings`](../api/maps/legendSettingsModel/).

{% tab template="maps/default-map", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx
import { world_map } from 'world-map.ts';
import { dafaultData } from 'data.ts'
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective, Inject, Legend } from '@syncfusion/ej2-react-maps';

ReactDOM.render(
            <MapsComponent id="maps" legendSettings={ { visible: true, valuePath: 'continent', removeDuplicateLegend: true} } >
            <Inject services={[Legend]} />
                <LayersDirective>
                    <LayerDirective shapeData={world_map} shapeDataPath='continent' shapePropertyPath='continent' dataSource={dafaultData}
                        shapeSettings={ {
                            colorValuePath: 'color',
                        } }>
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent>,
document.getElementById("maps") as HTMLElement
);
```

{% endtab %}

### Toggle option in legend

The toggle option has been provided for legend. If the legend can be toggled, the given color will be changed to the corresponding Maps shape item. To enable the toggle options in Legend, set the [`enable`](../api/maps/toggleLegendSettingsModel/#enable) property of the [`toggleLegendSettings`](../api/maps/toggleLegendSettingsModel) to **true**.

The following properties are available to customize the toggle option in legend.

* [`applyShapeSettings`](../api/maps/toggleLegendSettingsModel/#applyshapesettings) – To apply the [`fill`](../api/maps/shapeSettingsModel/#fill) property value to the shape of the Maps when toggling the legend items.
* [`fill`](../api/maps/toggleLegendSettingsModel/#fill) - To apply the color to the shape of the Maps for which legend item is toggled.
* [`opacity`](../api/maps/toggleLegendSettingsModel/#opacity) – To customize the transparency for the shapes for which legend item is toggled.
* [`border`](../api/maps/toggleLegendSettingsModel/#border) – To customize the color, width and opacity of the border of the shapes in Maps.

{% tab template="maps/default-map", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx
import { world_map } from 'world-map.ts';
import { population_density } from 'data.ts'
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective, Inject, Legend } from '@syncfusion/ej2-react-maps';

ReactDOM.render(
            <MapsComponent id="maps" legendSettings={ { visible: true, toggleLegendSettings: { enable: true } } } >
            <Inject services={[Legend]} />
                <LayersDirective>
                    <LayerDirective shapeData={world_map} shapeDataPath='name' shapePropertyPath='name'
                        dataSource={population_density}
                        shapeSettings={ {
                            colorValuePath: 'density',
                            colorMapping: [
                                {
                                    from: 0, to: 100, color: 'rgb(153,174,214)',
                                },
                                {
                                    from: 101, to: 200, color: 'rgb(115,143,199)',
                                },
                                {
                                    color: 'rgb(77,112,184)'
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

## Enable Legend for bubbles

To enable the legend for the bubble by setting the [`visible`](../api/maps/legendSettingsModel/#visible) property of [`legendSettings`](../api/maps/legendSettingsModel) as **true** and [`type`](../api/maps/legendSettingsModel/#type) of [`legendSettings`](../api/maps/legendSettingsModel) as **Bubbles**.

{% tab template="maps/default-map", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx
import { world_map } from 'world-map.ts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective, Inject } from '@syncfusion/ej2-react-maps';
import { BubblesDirective, BubbleDirective, Bubble, Legend } from '@syncfusion/ej2-react-maps';


ReactDOM.render(
            <MapsComponent id="maps" legendSettings= {{visible: true, type: 'Bubbles'}}>
            <Inject services={[Bubble, Legend]}/>
                <LayersDirective>
                    <LayerDirective shapeData={world_map} shapeDataPath="name" shapePropertyPath="name">
                        <BubblesDirective>
                            <BubbleDirective visible={true}
                                             valuePath="population"
                                             colorValuePath="color"
                                             dataSource= {[
                                                { color: 'green', name: 'India', population: '38332521' },
                                                { color: 'purple', name: 'New Zealand', population: '19651127' },
                                                { color: 'blue', name: 'Pakistan', population: '3090416' }
                                             ]}
                                            minRadius={20} maxRadius={40} />
                        </BubblesDirective>
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent>,
            document.getElementById("maps") as HTMLElement
);
```

{% endtab %}

## Enable legend for markers

To enable legend for marker by setting the [`visible`](../api/maps/legendSettingsModel/#visible) property of [`legendSettings`](../api/maps/legendSettingsModel) as **true** and [`type`](../api/maps/legendSettingsModel/#type) property of [`legendSettings`](../api/maps/legendSettingsModel) as **Markers**. The [`legendText`](../api/maps/markerSettingsModel/#legendtext) property in the [`markerSettings`](../api/maps/markerSettingsModel) can be used to show the legend text based on values provided in the data source.

{% tab template="maps/default-map", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx
import { world_map } from 'world-map.ts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective, MarkersDirective, Legend,MarkerDirective, Marker, Inject } from '@syncfusion/ej2-react-maps';

ReactDOM.render(
                <MapsComponent id="maps" legendSettings= {{visible: true, type: 'Markers'}}>
                <Inject services={[Marker, Legend]} />
                    <LayersDirective>
                        <LayerDirective shapeData={world_map}>
                        <MarkersDirective>
                            <MarkerDirective
                                    visible={true}
                                    legendText= 'city'
                                    dataSource={[
                                        { latitude: 37.0000, longitude: -120.0000, city: 'California' },
                                        { latitude: 40.7127, longitude: -74.0059, city: 'New York' },
                                        { latitude: 42, longitude: -93, city: 'Iowa' }
                                    ]}>
                            </MarkerDirective>
                        </MarkersDirective>
                        </LayerDirective>
                    </LayersDirective>
                </MapsComponent>,
            document.getElementById("maps") as HTMLElement
);
```

{% endtab %}