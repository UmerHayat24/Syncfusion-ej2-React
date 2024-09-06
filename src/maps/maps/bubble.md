---
title: " Bubbles in React Maps control | Syncfusion "

component: "Maps"

description: "Learn here all about Bubbles feature of Syncfusion React Maps control and more."
---

# Bubbles in React Maps

Bubbles in the Maps control represent the underlying data values of the Maps. It can be scattered throughout the Maps shapes that contain values in the data source. Bubbles are enabled by setting the [`visible`](../api/maps/bubbleSettingsModel/#visible) property of [`bubbleSettings`](../api/maps/bubbleSettingsModel) to **true**. To add bubbles to the Maps, bind the data source to the [`dataSource`](../api/maps/bubbleSettingsModel/#datasource) property of [`BubbleDirective`](../api/maps/bubbleSettingsModel) and set the field name, that contains the numerical data, in the data source to the [`valuePath`](../api/maps/bubbleSettingsModel/#valuepath) property.

```tsx
export let world_map = // paste the World map from World.json GeoJSON file.
```

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
                            <BubbleDirective visible={true} valuePath="population" dataSource={[{color: 'green', name: 'India', population: '38332521' },
                {color: 'purple', name: 'New Zealand', population: '19651127' },
                {color: 'blue', name: 'Pakistan', population: '3090416' }]} minRadius={20} maxRadius={40} />
                        </BubblesDirective>
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent>,
            document.getElementById("maps") as HTMLElement
);
```

{% endtab %}

## Bubble shapes

The following types of shapes are available to render the bubbles in Maps.

* Circle
* Square

By default, bubbles are rendered in the **Circle** type. To change the type of the bubble, set the [`bubbleType`](../api/maps/bubbleSettingsModel/#bubbletype) property of [`BubbleDirective`](../api/maps/bubbleSettingsModel) as **Square** to render the square shape bubbles.

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
                            <BubbleDirective visible={true} valuePath="population" bubbleType="Square" dataSource={[{ name: 'India', population: '38332521' },
                            { name: 'Pakistan', population: '3090416' }]} minRadius={20} maxRadius={40} />
                        </BubblesDirective>
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent>,
            document.getElementById("maps") as HTMLElement
);
```

{% endtab %}

## Customization

The following properties are available in [`BubbleDirective`](../api/maps/bubbleSettingsModel) to customize the bubbles of the Maps component.

* [`border`](../api/maps/bubbleSettingsModel/#border) – To customize the color, width and opacity of the border of the bubbles in Maps.
* [`fill`](../api/maps/bubbleSettingsModel/#fill) – To apply the color for bubbles in Maps.
* [`opacity`](../api/maps/bubbleSettingsModel/#opacity) – To apply opacity to the bubbles in Maps.
* [`animationDelay`](../api/maps/bubbleSettingsModel/#animationdelay) - To change the time delay in the transition for bubbles.
* [`animationDuration`](../api/maps/bubbleSettingsModel/#animationduration) - To change the time duration of animation for bubbles.

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
                            <BubbleDirective visible={true} valuePath="population"
                                             dataSource={[
                                                { name: 'India', population: '38332521' },
                                                { name: 'Pakistan', population: '3090416' },
                                                { name: 'New Zealand', population: '19651127' }
                                             ]}
                                             minRadius={5} maxRadius={40} fill="green"
                                             animationDelay={100} animationDuration={1000} opacity={1}
                                             border={{color: "blue", width: 2}} />
                        </BubblesDirective>
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent>,
            document.getElementById("maps") as HTMLElement
);
```

{% endtab %}

## Setting colors to the bubbles from the data source

The color for each bubble in the Maps can be set using the [`colorValuePath`](../api/maps/bubbleSettingsModel/#colorvaluepath) property of [`BubbleDirective`](../api/maps/bubbleSettingsModel). The value for the [`colorValuePath`](../api/maps/bubbleSettingsModel/#colorvaluepath) property is the field name from the data source of the [`BubbleDirective`](../api/maps/bubbleSettingsModel) which contains the color values.

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
                            <BubbleDirective visible={true} valuePath="population"
                                             dataSource={[
                                                { name: 'India', population: '38332521', color: 'blue' },
                                                { name: 'New Zealand', population: '19651127', color: '#c2d2d6' },
                                                { name: 'Pakistan', population: '3090416', color: '#09156d' }
                                             ]}
                                             minRadius={20} maxRadius={40} colorValuePath="color"/>
                        </BubblesDirective>
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent>,
            document.getElementById("maps") as HTMLElement
);
```

{% endtab %}

## Setting the range of the bubble size

The size of the bubbles is calculated from the values got from the [`valuePath`](../api/maps/bubbleSettingsModel/#valuepath) property. The range for the radius of the bubbles can be modified using [`minRadius`](../api/maps/bubbleSettingsModel/#minradius) and [`maxRadius`](../api/maps/bubbleSettingsModel/#maxradius) properties.

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
                            <BubbleDirective visible={true} valuePath="population" dataSource={[{name: 'India', population: '38332521' },
                {name: 'New Zealand', population: '19651127' },
                {name: 'Pakistan', population: '3090416' }]} minRadius={5} maxRadius={80} />
                        </BubblesDirective>
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent>,
            document.getElementById("maps") as HTMLElement
);
```

{% endtab %}

## Multiple bubble groups

Multiple groups of bubbles can be added to the Maps using the [`BubbleDirective`](../api/maps/bubbleSettingsModel) in which the properties of bubbles are added as an array. The customization for the bubbles can be done with the [`BubbleDirective`](../api/maps/bubbleSettingsModel). In the following example, the gender-wise population ratio is demonstrated with two different bubble groups.

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
                            <BubbleDirective visible={true}
                                             valuePath="femaleRatio"
                                             colorValuePath="femaleRatioColor"
                                             dataSource={[
                                                 {country: "United States", femaleRatio: 50.50442726, maleRatio: 49.49557274, femaleRatioColor: "green", maleRatioColor: "blue" },
                                                 {country: "India", femaleRatio: 48.18032713, maleRatio: 51.81967287, femaleRatioColor: "blue", maleRatioColor: "#c2d2d6" },
                                                 {country: "Oman", femaleRatio: 34.15597234, maleRatio: 65.84402766, femaleRatioColor: "#09156d", maleRatioColor: "orange" }, {country: "United Arab Emirates", femaleRatio: 27.59638942, maleRatio: 72.40361058, femaleRatioColor: "#09156d", maleRatioColor: "orange"}]} minRadius={5} maxRadius={20} />
                            <BubbleDirective visible={true}
                                             bubbleType="Circle"
                                             valuePath="maleRatio"
                                             colorValuePath="maleRatioColor"
                                             dataSource={[
                                                 {country: "United States", femaleRatio: 50.50442726, maleRatio: 49.49557274, femaleRatioColor: "green", maleRatioColor: "blue" },
                                                 {country: "India", femaleRatio: 48.18032713, maleRatio: 51.81967287, femaleRatioColor: "blue", maleRatioColor: "#c2d2d6" },
                                                 {country: "Oman", femaleRatio: 34.15597234, maleRatio: 65.84402766, femaleRatioColor: "#09156d", maleRatioColor: "orange" }, {country: "United Arab Emirates", femaleRatio: 27.59638942, maleRatio: 72.40361058, femaleRatioColor: "#09156d", maleRatioColor: "orange"}]} minRadius={15} maxRadius={25} opacity={0.4} />
                        </BubblesDirective>
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent>,
            document.getElementById("maps") as HTMLElement
);
```

{% endtab %}

## Enable tooltip for bubble

The tooltip for the bubbles can be enabled by setting the [`visible`](../api/maps/tooltipSettingsModel/#visible) property of the [`tooltipSettings`](../api/maps/tooltipSettingsModel) as **true**. The content for the tooltip can be set using the [`valuePath`](../api/maps/tooltipSettingsModel/#valuepath) property in the [`tooltipSettings`](../api/maps/tooltipSettingsModel) of the [`BubbleDirective`](../api/maps/bubbleSettingsModel) where the value for the [`valuePath`](../api/maps/tooltipSettingsModel/#valuepath) property is the field name from the data source of the [`BubbleDirective`](../api/maps/bubbleSettingsModel). Also added any HTML element as the template in tooltip using the [`template`](../api/maps/tooltipSettingsModel/#template) property.

{% tab template="maps/default-map", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx
import { world_map } from 'world-map.ts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective, Inject } from '@syncfusion/ej2-react-maps';
import { BubblesDirective, BubbleDirective, Bubble, MapsTooltip } from '@syncfusion/ej2-react-maps';


ReactDOM.render(
            <MapsComponent id="maps">
            <Inject services={[Bubble, MapsTooltip]}/>
                <LayersDirective>
                    <LayerDirective shapeData={world_map} shapeDataPath="name" shapePropertyPath="name">
                        <BubblesDirective>
                            <BubbleDirective visible={true} valuePath="population" dataSource={[
                                            { name: 'India', population: '38332521' },
                                            { name: 'New Zealand', population: '19651127' },
                                            { name: 'Pakistan', population: '3090416' }]}
                                            minRadius={5} maxRadius={80}
                                            tooltipSettings={{
                                                visible: true,
                                                valuePath: 'population'
                                            }} />
                        </BubblesDirective>
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent>,
            document.getElementById("maps") as HTMLElement
);
```

{% endtab %}