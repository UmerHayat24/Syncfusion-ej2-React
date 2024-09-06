---
title: " Navigation Lines in React Maps control | Syncfusion "

component: "Maps"

description: "Learn here all about Navigation Lines feature of Syncfusion React Maps control and more."
---

# Navigation Lines in React Maps control

The navigation lines are used to denote the path between two locations. This feature can be used to draw flight or sea routes. Navigation lines are enabled by setting the [`visible`](../api/maps/navigationLineSettingsModel/#visible) property of the [`navigationLineSettings`](../api/maps/navigationLineSettingsModel) to **true**.

## Customization

The following properties are available in [`navigationLineSettings`](../api/maps/navigationLineSettingsModel/) to customize the navigation line of the Maps component.

* [`color`](../api/maps/navigationLineSettingsModel/#color) - To apply the color for navigation lines in Maps.
* [`dashArray`](../api/maps/navigationLineSettingsModel/#dasharray) - To define the pattern of dashes and gaps that is applied to the outline of the navigation lines.
* [`width`](../api/maps/navigationLineSettingsModel/#width) - To customize the width of the navigation lines.
* [`angle`](../api/maps/navigationLineSettingsModel/#angle) - To customize the angle of the navigation lines.
* [`highlightSettings`](../api/maps/navigationLineSettingsModel/#highlightsettings) - To customize the highlight settings of the navigation line.
* [`selectionSettings`](../api/maps/navigationLineSettingsModel/#selectionsettings) - To customize the selection settings of the navigation line.

To navigate the line between two cities on the world map, [`latitude`](../api/maps/navigationLineSettingsModel/#latitude) and [`longitude`](../api/maps/navigationLineSettingsModel/#longitude) values are used to indicate the start and end points of navigation lines drawn on Maps.

{% tab template="maps/default-map", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx
import { world_map } from 'world-map.ts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective, Inject, NavigationLine, NavigationLinesDirective, NavigationLineDirective } from '@syncfusion/ej2-react-maps';

ReactDOM.render(
            <MapsComponent id="element">
                <Inject services={[NavigationLine]} />
                <LayersDirective>
                    <LayerDirective shapeData={world_map}>
                        <NavigationLinesDirective>
                            <NavigationLineDirective visible={true}
                                                     latitude={[37.6276571, -122.4276688]}
                                                     longitude={[-74.0060, -117.7418381]}
                                                     color="black"
                                                     angle={90}
                                                     width={2}
                                                     dashArray="4"/>
                        </NavigationLinesDirective>
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent>,
document.getElementById("maps") as HTMLElement
);
```

{% endtab %}

## Enabling the arrows

To enable the arrow in the navigation line, set the [`showArrow`](../api/maps/arrowModel/#showarrow) property of [`arrowSettings`](../api/maps/navigationLineSettingsModel/#arrowsettings) to **true**. The following properties are available in [`arrowSettings`](../api/maps/navigationLineSettingsModel/#arrowsettings) to customize the arrow of the navigation lines.

* [`color`](../api/maps/arrowModel/#color) - To apply the color for arrow of the navigation line.
* [`offset`](../api/maps/arrowModel/#offset) - To customize the offset position of the arrow of the navigation line.
* [`position`](../api/maps/arrowModel/#position) - To customize the position of the arrow in navigation line. The possible values can be **Start** and **End**.
* [`size`](../api/maps/arrowModel/#size) - To customize the size of the arrow in pixels.

{% tab template="maps/default-map", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx
import { world_map } from 'world-map.ts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective, Inject, NavigationLine, NavigationLinesDirective, NavigationLineDirective } from '@syncfusion/ej2-react-maps';

ReactDOM.render(
            <MapsComponent id="element">
                <Inject services={[NavigationLine]} />
                <LayersDirective>
                    <LayerDirective shapeData={world_map}>
                        <NavigationLinesDirective>
                            <NavigationLineDirective visible={true}
                                                     latitude={[37.6276571, -122.4276688]}
                                                     longitude={[-74.0060, -117.7418381]}
                                                     color="black"
                                                     angle={90}
                                                     width={2}
                                                     dashArray="4"
                                                     arrowSettings={{
                                                         showArrow: true,
                                                         size: 15,
                                                         position: 'Start'
                                                    }}/>
                        </NavigationLinesDirective>
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent>,
document.getElementById("maps") as HTMLElement
);
```

{% endtab %}