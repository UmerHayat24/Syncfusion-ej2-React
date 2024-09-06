---
title: " User interactions in React Maps control | Syncfusion "

component: "Maps"

description: "Learn here all about User interactions of Syncfusion React Maps control and more."
---

# User Interactions in React Maps control

## Zooming

The zooming feature is used to zoom in and out of Maps to show in-depth information. It is controlled by the [`zoomFactor`](../api/maps/zoomSettingsModel/#zoomfactor) property of the [`zoomSettings`](../api/maps/zoomSettingsModel) of the Maps. The Map is zoomed in when the [`zoomFactor`](../api/maps/zoomSettingsModel/#zoomfactor) is increased. The [`zoomFactor`](../api/maps/zoomSettingsModel/#zoomfactor) is increased or decrease dynamically based on zoom in and out interaction.

<b>Enable zooming</b>

Zooming of Maps is enabled by setting the [`enable`](../api/maps/zoomSettingsModel/#enable) property of [`zoomSettings`](../api/maps/zoomSettingsModel/) to **true**.

<b>Enable panning</b>

To enable the panning feature, set the [`enablePanning`](../api/maps/zoomSettingsModel/#enablepanning) property of [`zoomSettings`](../api/maps/zoomSettingsModel) to **true**.

{% tab template="maps/default-map", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import { world_map } from 'world-map.ts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective, Zoom, Inject } from '@syncfusion/ej2-react-maps';

ReactDOM.render(
            <MapsComponent id="maps" zoomSettings={ { enable: true, enablePanning: true } }>
            <Inject services={[Zoom]}/>
                <LayersDirective>
                    <LayerDirective shapeData={world_map}>
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent>,
document.getElementById("maps") as HTMLElement
);

```

{% endtab %}

### Various type of zooming

Zooming can be performed in following types:

#### Zooming toolbar

By default, the toolbar is rendered with **zoom-in**, **zoom-out**, and **reset** options when it is set to **true** in the [`enable`](../api/maps/zoomSettingsModel/#enable) property of [`zoomSettings`](../api/maps/zoomSettingsModel/).

The following options are available in toolbar.

1. Zoom - Provides rectangular zoom support.
2. ZoomIn - Zooms in the Maps.
3. ZoomOut - Zooms out the Maps.
4. Pan - Switches to panning if rectangular zoom is activated.
5. Reset - Restores the Maps to the default view.

The following properties are available in toolbars to customize the zooming toolbars.

* [`color`](../api/maps/zoomSettingsModel/#color) - To apply the color for toolbars in Maps.
* [`highlightColor`](../api/maps/zoomSettingsModel/#highlightcolor) - To apply the color for the zooming toolbar when the mouse has hovered on the toolbar element in Maps.
* [`horizontalAlignment`](../api/maps/zoomSettingsModel/#horizontalalignment) - To customize the position type of toolbar when it is placed horizontally.
* [`selectionColor`](../api/maps/zoomSettingsModel/#selectioncolor) - To apply the color for the zooming toolbar when clicking the zooming toolbar in Maps.
* [`toolBarOrientation`](../api/maps/zoomSettingsModel/#toolbarorientation) - To customize the orientation of the zooming toolbar.
* [`toolbars`](../api/maps/zoomSettingsModel/#toolbars) - To customize the items that are to be shown in the zooming toolbar in Maps.
* [`verticalAlignment`](../api/maps/zoomSettingsModel/#verticalalignment) - To customize the position type of toolbar when it is placed vertically.

{% tab template="maps/default-map", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import { world_map } from 'world-map.ts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective, Zoom, Inject } from '@syncfusion/ej2-react-maps';

ReactDOM.render(
            <MapsComponent id="maps" zoomSettings={ {
                                        enable: true,
                                        color: 'green',
                                        highlightColor: 'blue',
                                        selectionColor: 'orange',
                                        horizontalAlignment: 'Center',
                                        toolbars: ['ZoomIn', 'ZoomOut', 'Pan', 'Reset']} }>
            <Inject services={[Zoom]}/>
                <LayersDirective>
                    <LayerDirective shapeData={world_map}>
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent>,
document.getElementById("maps") as HTMLElement
);

```

{% endtab %}

#### Pinch zooming

To enable or disable the pinch zooming, use the [`pinchZooming`](../api/maps/zoomSettingsModel/#pinchzooming) property in [`zoomSettings`](../api/maps/zoomSettingsModel).

```tsx

import { world_map } from 'world-map.ts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective, Zoom, Inject } from '@syncfusion/ej2-react-maps';

ReactDOM.render(
            <MapsComponent id="maps" zoomSettings={ { enable: true, pinchZooming: true } }>
            <Inject services={[Zoom]}/>
                <LayersDirective>
                    <LayerDirective shapeData={world_map}>
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent>,
document.getElementById("maps") as HTMLElement
);

```

#### Single-click zooming

To enable or disable the single-click zooming, use the [`zoomOnClick`](../api/maps/zoomSettingsModel/#zoomonclick) property in [`zoomSettings`](../api/maps/zoomSettingsModel).

```tsx

import { world_map } from 'world-map.ts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective, Zoom, Inject } from '@syncfusion/ej2-react-maps';

ReactDOM.render(
            <MapsComponent id="maps" zoomSettings={ { enable: true, zoomOnClick: true } }>
            <Inject services={[Zoom]}/>
                <LayersDirective>
                    <LayerDirective shapeData={world_map}>
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent>,
document.getElementById("maps") as HTMLElement
);

```

#### Double-click zooming

To enable or disable the double-click zooming, use the [`doubleClickZoom`](../api/maps/zoomSettingsModel/#doubleclickzoom) property in [`zoomSettings`](../api/maps/zoomSettingsModel/).

```tsx

import { world_map } from 'world-map.ts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective, Zoom, Inject } from '@syncfusion/ej2-react-maps';

ReactDOM.render(
            <MapsComponent id="maps" zoomSettings={ { enable: true, doubleClickZoom: true } }>
            <Inject services={[Zoom]}/>
                <LayersDirective>
                    <LayerDirective shapeData={world_map}>
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent>,
document.getElementById("maps") as HTMLElement
);

```

#### Mouse wheel zooming

To enable or disable mouse wheel zooming, use the [`mouseWheelZoom`](../api/maps/zoomSettingsModel/#mousewheelzoom) property in [`zoomSettings`](../api/maps/zoomSettingsModel/).

```tsx

import { world_map } from 'world-map.ts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective, Zoom, Inject } from '@syncfusion/ej2-react-maps';

ReactDOM.render(
            <MapsComponent id="maps" zoomSettings={ { enable: true, mouseWheelZoom: true } }>
            <Inject services={[Zoom]}/>
                <LayersDirective>
                    <LayerDirective shapeData={world_map}>
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent>,
document.getElementById("maps") as HTMLElement
);

```

#### Selection zooming

To enable or disable selection zooming, use the [`enableSelectionZooming`](../api/maps/zoomSettingsModel/#enableselectionzooming) property in [`zoomSettings`](../api/maps/zoomSettingsModel/). The [`enablePanning`](../api/maps/zoomSettingsModel/#enablepanning) property must be set to **false** to enable the selection zooming in Maps.

```tsx

import { world_map } from 'world-map.ts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective, Zoom, Inject } from '@syncfusion/ej2-react-maps';

ReactDOM.render(
            <MapsComponent id="maps" zoomSettings={ { enable: true, enableSelectionZooming: true,
                                                      enablePanning: false } }>
            <Inject services={[Zoom]}/>
                <LayersDirective>
                    <LayerDirective shapeData={world_map}>
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent>,
document.getElementById("maps") as HTMLElement
);

```

### Setting minimum and maximum values for zoom factor

The zooming range can be adjusted using the [`minZoom`](../api/maps/zoomSettingsModel/#minzoom) and [`maxZoom`](../api/maps/zoomSettingsModel/#maxzoom) properties in [`zoomSettings`](../api/maps/zoomSettingsModel/). The minZoom value is set to 1 by default, and the maxZoom value is set to 10.

```tsx

import { world_map } from 'world-map.ts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective, Zoom, Inject } from '@syncfusion/ej2-react-maps';

ReactDOM.render(
            <MapsComponent id="maps" zoomSettings={ { enable: true, minZoom: 2,
                                                      maxZoom: 12 } }>
            <Inject services={[Zoom]}/>
                <LayersDirective>
                    <LayerDirective shapeData={world_map}>
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent>,
document.getElementById("maps") as HTMLElement
);

```

### Zooming with animation

To zoom in or zoom out the Maps with animation, use the [`animationDuration`](../api/maps/layerSettingsModel/#animationduration) property in [`layers`](../api/maps/layerSettingsModel).

```tsx

import { world_map } from 'world-map.ts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective, Zoom, Inject } from '@syncfusion/ej2-react-maps';

ReactDOM.render(
            <MapsComponent id="maps" zoomSettings={ { enable: true } }>
            <Inject services={[Zoom]}/>
                <LayersDirective>
                    <LayerDirective shapeData={world_map} animationDuration={500}>
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent>,
document.getElementById("maps") as HTMLElement
);

```

## Selection

Each shape in the Maps can be selected and deselected during interaction with the shapes. Selection is enabled by setting the [`enable`](../api/maps/selectionSettingsModel/#enable) property of [`selectionSettings`](../api/maps/selectionSettingsModel) to **true**.

The following properties are available to customize the selection of Maps elements such as shapes, bubbles, markers and legends.

* [`border`](../api/maps/selectionSettingsModel/#border) - To customize the color, width and opacity of the border of which element is selected in Maps.
* [`fill`](../api/maps/selectionSettingsModel/#fill) - Applies the color for the element that is selected.
* [`opacity`](../api/maps/selectionSettingsModel/#opacity) - To customize the transparency for the element that is selected.
* [`enableMultiSelect`](../api/maps/selectionSettingsModel/#enablemultiselect) - To enable or disable the selection for multiple shapes or markers or bubbles in the Maps.

By tapping on the specific legend, the shapes which are bounded to the selected legend is also selected and vice versa.

{% tab template="maps/default-map", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import { world_map } from 'world-map.ts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective, Selection, Inject, Legend  } from '@syncfusion/ej2-react-maps';

ReactDOM.render(
            <MapsComponent id="maps" legendSettings={{visible: true}}>
            <Inject services={[Selection, Legend]} />
                <LayersDirective>
                    <LayerDirective shapeData={world_map} selectionSettings={ {
                        enable: true,
                        fill: 'blue',
                        border: { color: 'white', width: 2 }
                    } } dataSource={[
                        {"Country": "China", "Membership": "Permanent"},
                        {"Country": "France","Membership": "Permanent" },
                        { "Country": "Russia","Membership": "Permanent"},
                        {"Country": "Kazakhstan","Membership": "Non-Permanent"},
                        { "Country": "Poland","Membership": "Non-Permanent"},
                        {"Country": "Sweden","Membership": "Non-Permanent"}
                       ]} shapePropertyPath="name" shapeDataPath="Country"
                        shapeSettings={{
                           colorValuePath: 'Membership',
                           colorMapping: [
                               { value: 'Permanent', color: '#D84444' },
                               { value: 'Non-Permanent', color: '#316DB5'}]
                        }}>
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent>,
document.getElementById("maps") as HTMLElement
);

```

{% endtab %}

### Enable selection for bubbles

To enable the selection for bubbles in Maps, set the [`selectionSettings`](../api/maps/selectionSettingsModel) in [`bubbleSettings`](../api/maps/bubbleSettingsModel/) and set the [`enable`](../api/maps/selectionSettingsModel/#enable) property of [`selectionSettings`](../api/maps/selectionSettingsModel) as **true**.

>To use the bubble feature, the Bubble module must be injected.

{% tab template="maps/default-map", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx
import { world_map } from 'world-map.ts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective, Inject } from '@syncfusion/ej2-react-maps';
import { BubblesDirective, BubbleDirective, Bubble, Selection } from '@syncfusion/ej2-react-maps';


ReactDOM.render(
            <MapsComponent id="maps">
            <Inject services={[Bubble, Selection]}/>
                <LayersDirective>
                    <LayerDirective shapeData={world_map} shapeDataPath="name" shapePropertyPath="name">
                        <BubblesDirective>
                            <BubbleDirective visible={true} valuePath="population"
                                             dataSource={[
                                                { name: 'India', population: '38332521' },
                                                { name: 'Pakistan', population: '3090416' },
                                                { name: 'New Zealand', population: '19651127' }
                                             ]}
                                             selectionSettings={{
                                                enable: true,
                                                fill: 'green',
                                                border: { color: 'white', width: 2}
                                             }} />
                        </BubblesDirective>
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent>,
            document.getElementById("maps") as HTMLElement
);
```

{% endtab %}

### Enable selection for markers

To enable the selection for markers in Maps, set the [`selectionSettings`](../api/maps/selectionSettingsModel) in the [`markerSettings`](../api/maps/markerSettingsModel) and set the [`enable`](../api/maps/selectionSettingsModel/#enable) property of the [`selectionSettings`](../api/maps/selectionSettingsModel) as **true**.

>To use the marker feature, the Marker module must be injected.

{% tab template="maps/default-map", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx
import { world_map } from 'world-map.ts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective, MarkersDirective, MarkerDirective, Selection, Marker, Inject } from '@syncfusion/ej2-react-maps';

ReactDOM.render(
                <MapsComponent id="maps">
                <Inject services={[Marker, Selection]} />
                    <LayersDirective>
                        <LayerDirective shapeData={world_map}>
                        <MarkersDirective>
                            <MarkerDirective visible={true}
                                            height={20}
                                            width={20}
                                            animationDuration={0}
                                            fill="green"
                                            shape="Balloon"
                                            dataSource={[
                                                { latitude: 49.95121990866204, longitude: 18.468749999999998, name:'Europe' },
                                                { latitude: 59.88893689676585, longitude: -109.3359375, name:'North America'},
                                                { latitude: -6.64607562172573, longitude: -55.54687499999999, name:'South America'}
                                            ]}
                                            selectionSettings={{
                                                enable: true,
                                                fill: 'blue',
                                                border: { color: 'white', width: 2}
                                            }}>
                            </MarkerDirective>
                        </MarkersDirective>
                        </LayerDirective>
                    </LayersDirective>
                </MapsComponent>,
            document.getElementById("maps") as HTMLElement
);
```

{% endtab %}

### Public method for the shape selection

The [`shapeSelection`](../api/maps/#shapeselection) method can be used to select each shape in the Maps.
LayerIndex, propertyName, country name, and selected value as a boolean state(true / false) are the input parameters for this method.

{% tab template="maps/default-map", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import { world_map } from 'world-map.ts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective, Selection, Inject } from '@syncfusion/ej2-react-maps';

class App extends React.Component<{}, {}>{

  public mapsInstance: MapsComponent;
  public selectclickHandler() {
    this.mapsInstance.shapeSelection(0, "continent", "Asia", true);
  }
  public unselectclickHandler() {
    this.mapsInstance.shapeSelection(0, "continent", "Asia", false);
  }
  render() {
    return (<div>
      <MapsComponent id="maps" ref={maps => this.mapsInstance = maps}>
            <Inject services={[Selection]} />
                <LayersDirective>
                    <LayerDirective shapeData={world_map} selectionSettings={ {
                        enable: true,
                        fill: 'green',
                        border: { color: 'white', width: 2 }
                    } }>
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent>
            <button value='select' onClick={this.selectclickHandler.bind(this)}>select</button>
            <button value='unselect' onClick={this.unselectclickHandler.bind(this)}>unselect</button></div>)
  }
};
ReactDOM.render(<App />, document.getElementById('maps'));

```

{% endtab %}

### Initial shape selection

The shape is initially selected using the [`initialShapeSelection`](../api/maps/initialShapeSelectionSettingsModel/), and the values are mapped to the [`shapePath`](../api/maps/initialShapeSelectionSettingsModel/#shapepath) and [`shapeValue`](../api/maps/initialShapeSelectionSettingsModel/#shapevalue).

>initialShapeSelection is an Array property.

{% tab template="maps/default-map", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import { world_map } from 'world-map.ts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, InitialShapeSelectionsDirective, InitialShapeSelectionDirective, LayerDirective, Selection, Inject } from '@syncfusion/ej2-react-maps';

ReactDOM.render(
            <MapsComponent id="maps">
            <Inject services={[Selection]} />
                <LayersDirective>
                    <LayerDirective shapeData={world_map}  selectionSettings={{
                        enable: true,
                        fill: 'green',
                        border: { color: 'white', width: 2 }
                    }}>
        <InitialShapeSelectionsDirective>
            <InitialShapeSelectionDirective shapePath={'continent'} shapeValue={'Africa'}>
            </InitialShapeSelectionDirective>
            <InitialShapeSelectionDirective shapePath={'name'} shapeValue={'India'}>
            </InitialShapeSelectionDirective>
        </InitialShapeSelectionsDirective>
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent>,
document.getElementById("maps") as HTMLElement
);

```

{% endtab %}

### Initial marker selection

Using the [`initialMarkerSelection`](../api/maps/initialMarkerSelectionSettingsModel), the marker shape can be selected initially. Markers render based on the [`latitude`](../api/maps/initialMarkerSelectionSettingsModel/#latitude) and [`longitude`](../api/maps/initialMarkerSelectionSettingsModel/#longitude) values.

>initialMarkerSelection is an Array property.

{% tab template="maps/default-map", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx
import { world_map } from 'world-map.ts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective, MarkersDirective, MarkerDirective, Selection, Marker, Inject } from '@syncfusion/ej2-react-maps';

ReactDOM.render(
                <MapsComponent id="maps">
                <Inject services={[Marker, Selection]} />
                    <LayersDirective>
                        <LayerDirective shapeData={world_map}>
                        <MarkersDirective>
                            <MarkerDirective visible={true}
                                            height={20}
                                            width={20}
                                            animationDuration={0}
                                            fill="green"
                                            shape="Balloon"
                                            dataSource={[
                                                { latitude: 49.95121990866204, longitude: 18.468749999999998, name:'Europe' },
                                                { latitude: 59.88893689676585, longitude: -109.3359375, name:'North America'},
                                                { latitude: -6.64607562172573, longitude: -55.54687499999999, name:'South America'}
                                            ]}
                                            initialMarkerSelection={{
                                                latitude: -6.64607562172573, longitude: -55.54687499999999
                                            }}
                                            selectionSettings={{
                                                enable: true,
                                                fill: 'blue',
                                                border: { color: 'white', width: 2}
                                            }}>
                            </MarkerDirective>
                        </MarkersDirective>
                        </LayerDirective>
                    </LayersDirective>
                </MapsComponent>,
            document.getElementById("maps") as HTMLElement
);
```

{% endtab %}

## Highlight

Each shape in the Maps can be highlighted during mouse hover on the Maps elements such as shapes, bubbles, markers and legends. Highlight is enabled by setting the [`enable`](../api/maps/highlightSettingsModel/#enable) property of [`highlightSettings`](../api/maps/highlightSettingsModel) to **true**.

The following properties are available to customize the highlight of Maps elements such as shapes, bubbles, markers and legends.

* [`border`](../api/maps/highlightSettingsModel/#border) - To customize the color, width and opacity of the border of which element is highlighted in Maps.
* [`fill`](../api/maps/highlightSettingsModel/#fill) - Applies the color for the element that is highlighted.
* [`opacity`](../api/maps/highlightSettingsModel/#opacity) - To customize the transparency for the element that is highlighted.

Hovering on the specific legend, the shapes which are bounded to the selected legend is also highlighted and vice versa.

{% tab template="maps/default-map", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import { world_map } from 'world-map.ts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective, Highlight, Inject, Legend } from '@syncfusion/ej2-react-maps';

ReactDOM.render(
            <MapsComponent id="maps" legendSettings={{visible: true}}>
            <Inject services={[Highlight, Legend]} />
                <LayersDirective>
                    <LayerDirective shapeData={world_map}  highlightSettings={ {
                        enable: true,
                        fill: 'green',
                        border: { color: 'white', width: 2 }
                    } }
                        dataSource={[
                            { "Country": "China", "Membership": "Permanent"},
                            { "Country": "France", "Membership": "Permanent" },
                            { "Country": "Russia", "Membership": "Permanent"},
                            { "Country": "Kazakhstan", "Membership": "Non-Permanent"},
                            { "Country": "Poland", "Membership": "Non-Permanent"},
                            { "Country": "Sweden", "Membership": "Non-Permanent"}
                        ]} shapePropertyPath="name" shapeDataPath="Country"
                         shapeSettings={{
                            colorValuePath: 'Membership',
                            colorMapping: [
                                { value: 'Permanent', color: '#D84444' },
                                { value: 'Non-Permanent', color: '#316DB5'}]
                         }}>
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent>,
document.getElementById("maps") as HTMLElement
);

```

{% endtab %}

### Enable highlight for bubbles

To enable the highlight for bubbles in Maps, set the [`highlightSettings`](../api/maps/highlightSettingsModel) in [`bubbleSettings`](../api/maps/bubbleSettingsModel) and set the [`enable`](../api/maps/highlightSettingsModel/#enable) property of [`highlightSettings`](../api/maps/highlightSettingsModel) as **true**.

>To use the bubble feature, the Bubble module must be injected.

{% tab template="maps/default-map", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx
import { world_map } from 'world-map.ts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective, Inject } from '@syncfusion/ej2-react-maps';
import { BubblesDirective, BubbleDirective, Bubble, Highlight } from '@syncfusion/ej2-react-maps';


ReactDOM.render(
            <MapsComponent id="maps">
            <Inject services={[Bubble, Highlight]}/>
                <LayersDirective>
                    <LayerDirective shapeData={world_map} shapeDataPath="name" shapePropertyPath="name">
                        <BubblesDirective>
                            <BubbleDirective visible={true} valuePath="population"
                                             dataSource={[
                                                { name: 'India', population: '38332521' },
                                                { name: 'Pakistan', population: '3090416' },
                                                { name: 'New Zealand', population: '19651127' }
                                             ]}
                                             highlightSettings={{
                                                enable: true,
                                                fill: 'green',
                                                border: { color: 'white', width: 2}
                                             }} />
                        </BubblesDirective>
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent>,
            document.getElementById("maps") as HTMLElement
);
```

{% endtab %}

### Enable highlight for markers

To enable the highlight for markers in Maps, set the [`highlightSettings`](../api/maps/highlightSettingsModel) in [`markerSettings`](../api/maps/markerSettingsModel) and set the [`enable`](../api/maps/highlightSettingsModel/#enable) property of [`highlightSettings`](../api/maps/highlightSettingsModel) as **true**.

>To use the marker feature, the Marker module must be injected.

{% tab template="maps/default-map", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx
import { world_map } from 'world-map.ts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective, MarkersDirective, MarkerDirective, Highlight , Marker, Inject } from '@syncfusion/ej2-react-maps';

ReactDOM.render(
                <MapsComponent id="maps">
                <Inject services={[Marker, Highlight]} />
                    <LayersDirective>
                        <LayerDirective shapeData={world_map}>
                        <MarkersDirective>
                            <MarkerDirective visible={true}
                                            height={20}
                                            width={20}
                                            animationDuration={0}
                                            fill="green"
                                            shape="Balloon"
                                            dataSource={[
                                                { latitude: 49.95121990866204, longitude: 18.468749999999998, name:'Europe' },
                                                { latitude: 59.88893689676585, longitude: -109.3359375, name:'North America'},
                                                { latitude: -6.64607562172573, longitude: -55.54687499999999, name:'South America'}
                                            ]}
                                            highlightSettings={{
                                                enable: true,
                                                fill: 'blue',
                                                border: { color: 'white', width: 2}
                                            }}>
                            </MarkerDirective>
                        </MarkersDirective>
                        </LayerDirective>
                    </LayersDirective>
                </MapsComponent>,
            document.getElementById("maps") as HTMLElement
);
```

{% endtab %}

## Tooltip

On mouse over or touch end event, the tooltip is used to get more information about the layer, bubble, or marker. To enable tooltip in Maps, the **Tooltip** module must be injected into Maps using **Inject services={[Tooltip]}** tag. It can be enabled separately for layer or bubble or marker by using the [`visible`](../api/maps/tooltipSettingsModel/#visible) property of [`tooltipSettings`](../api/maps/tooltipSettingsModel/) as **true**. The [`valuePath`](../api/maps/tooltipSettingsModel/#valuepath) property in the tooltip takes the field name that presents in data source and displays that value as tooltip text. The [`tooltipDisplayMode`](../api/maps/mapsModel/#tooltipdisplaymode) property is used to change the display mode of the tooltip in Maps. Following display modes of tooltip are available in the Maps component. By default,  [`tooltipDisplayMode`](../api/maps/mapsModel/#tooltipdisplaymode) is set to **MouseMove**.

* MouseMove
* Click
* DoubleClick

{% tab template="maps/default-map", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import { world_map } from 'world-map.ts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective, MapsTooltip, Inject } from '@syncfusion/ej2-react-maps';

ReactDOM.render(
            <MapsComponent id="maps">
                        <Inject services={[MapsTooltip]} />
                <LayersDirective>
                    <LayerDirective shapeData={world_map}  tooltipSettings={ {
                            visible: true,
                            valuePath: 'name'
                        } }>
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent>,
document.getElementById("maps") as HTMLElement
);

```

{% endtab %}

### Customization

The following properties are available in the [`tooltipSettings`](../api/maps/tooltipSettingsModel/) to customize the tooltip of the Maps component.

* [`border`](../api/maps/tooltipSettingsModel/#border) - To customize the color, width and opacity of the border of the tooltip in layers, markers, and bubbles of Maps.
* [`fill`](../api/maps/tooltipSettingsModel/#fill) - Applies the color of the tooltip in layers, markers, and bubbles of Maps.
* [`format`](../api/maps/tooltipSettingsModel/#format) - To customize the format of the tooltip in layers, markers, and bubbles of Maps
* [`textStyle`](../api/maps/tooltipSettingsModel/#textstyle) - To customize the style of the text in the tooltip for layers, markers, and bubbles of Maps.

{% tab template="maps/default-map", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import { world_map } from 'world-map.ts';
import { default_data } from 'data.ts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective, MapsTooltip, Inject } from '@syncfusion/ej2-react-maps';

class App extends React.Component {
    render() {
        return(<div><MapsComponent id="maps">
        <Inject services={[MapsTooltip]}/>
            <LayersDirective>
              <LayerDirective shapeData={world_map} dataSource={default_data} shapeDataPath='continent'
              shapePropertyPath='continent'
              tooltipSettings={{
                  visible: true,
                  valuePath: 'continent',
                  format: '${continent}',
                  fill: '#D0D0D0',
                  textStyle: {
                    color: 'green',
                    fontFamily: 'Times New Roman',
                    fontStyle: 'Sans-serif'
                }
              }}/>
            </LayersDirective>
           </MapsComponent></div>);
    }
}
ReactDOM.render(<App/>, document.getElementById('maps'));

```

{% endtab %}

### Tooltip template

The HTML element can be rendered in the tooltip of the Maps using the [`template`](../api/maps/tooltipSettingsModel/#template) property of the [`tooltipSettings`](../api/maps/tooltipSettingsModel/).

{% tab template="maps/default-map", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import { world_map } from 'world-map.ts';
import { default_data } from 'data.ts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective, MapsTooltip, Inject } from '@syncfusion/ej2-react-maps';

class App extends React.Component {
    render() {
        return(<div><MapsComponent id="maps">
        <Inject services={[MapsTooltip]}/>
            <LayersDirective>
              <LayerDirective shapeData={world_map} dataSource={default_data} shapeDataPath='continent'
              shapePropertyPath='continent'
              tooltipSettings={{
                  visible: true,
                  valuePath: 'continent',
                  template: '<div style="width:60px; text-align:center; background-color: white; border: 2px solid black; padding-bottom: 10px;padding-top: 10px;padding-left: 10px;padding-right: 10px;"><span>${continent}</span></div>',
                  textStyle: {
                      color: 'black'
                  }
              }}/>
            </LayersDirective>
           </MapsComponent></div>);
    }
}
ReactDOM.render(<App/>, document.getElementById('maps'));

```

{% endtab %}