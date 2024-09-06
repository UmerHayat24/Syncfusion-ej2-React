---
title: "Data Labels in React Maps control | Syncfusion"

component: "Maps"

description: "Learn here all about Data Labels of Syncfusion React Maps control and more."
---

# Data labels in React Maps control

Data labels provide information to users about the shapes of the Maps component. It can be enabled by setting the [`visible`](../api/maps/dataLabelSettingsModel/#visible) property of the [`dataLabelSettings`](../api/maps/dataLabelSettingsModel/) to **true**.

## Adding data labels

To display data labels in the Maps, the [`labelPath`](../api/maps/dataLabelSettingsModel/#labelpath) property of [`dataLabelSettings`](../api/maps/dataLabelSettingsModel/) must be used. The value of the [`labelPath`](../api/maps/dataLabelSettingsModel/#labelpath) property can be taken from the field name in the shape data or data source. In the following example, the value of the [`labelPath`](../api/maps/dataLabelSettingsModel/#labelpath) property is the field name in the shape data of the Maps layer.

{% tab template="maps/default-map", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import { usa_map } from 'usa.ts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective, Inject, DataLabel } from '@syncfusion/ej2-react-maps';

ReactDOM.render(
            <MapsComponent id="maps">
            <Inject services={[DataLabel]} />
                <LayersDirective>
                    <LayerDirective shapeData={usa_map}
                                    shapeSettings= { {
                                        autofill: true
                                    } }
                                   dataLabelSettings={ {
                                       visible: true,
                                       labelPath: 'name'
                                    } }>
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent>,
document.getElementById("maps") as HTMLElement
);

```

{% endtab %}

In the following example, the value of [`labelPath`](../api/maps/dataLabelSettingsModel/#labelpath) property is set from the field name in the data source of the layer settings.

{% tab template="maps/default-map", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import { world_map } from 'world-map.ts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective, Inject, DataLabel } from '@syncfusion/ej2-react-maps';

ReactDOM.render(
            <MapsComponent id="maps">
            <Inject services={[DataLabel]} />
                <LayersDirective>
                    <LayerDirective shapeData={world_map} shapePropertyPath="name" shapeDataPath="name"
                                    shapeSettings= { {
                                        autofill: true
                                    } }
                                    dataSource ={ [
                                        { "name": "Afghanistan", "value": 53, "countryCode": "AF", "population": "29863010", "color": "red", "density": "119", "continent": "Asia" },
                                        { "name": "Albania", "value": 117, "countryCode": "AL", "population": "3195000", "color": "Blue", "density": "111", "continent": "Europe" },
                                        { "name": "Algeria", "value": 15, "countryCode": "DZ", "population": "34895000", "color": "Green", "density": "15", "continent": "Africa" }
                                    ] }
                                    dataLabelSettings={ {
                                        visible: true,
                                        labelPath: 'continent',
                                        smartLabelMode: 'Trim'
                                    } }>
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent>,
document.getElementById("maps") as HTMLElement
);

```

{% endtab %}

## Customization

The following properties are available in the [`dataLabelSettings`](../api/maps/dataLabelSettingsModel/) to customize the data label of the Maps control.

* [`border`](../api/maps/dataLabelSettingsModel/#border) - To customize the color, width and opacity for the border of the data labels in Maps.
* [`fill`](../api/maps/dataLabelSettingsModel/#fill) - To apply the color of the data labels in Maps.
* [`opacity`](../api/maps/dataLabelSettingsModel/#opacity) - To customize the transparency of the data labels in Maps.
* [`textStyle`](../api/maps/dataLabelSettingsModel/#textstyle) - To customize the text style of the data labels in Maps.

{% tab template="maps/default-map", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import { usa_map } from 'usa.ts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective, Inject, DataLabel } from '@syncfusion/ej2-react-maps';

ReactDOM.render(
            <MapsComponent id="maps">
            <Inject services={[DataLabel]} />
                <LayersDirective>
                    <LayerDirective shapeData={usa_map}
                                    shapeSettings= {{
                                        autofill: true
                                    }}
                                    dataLabelSettings={ {
                                        visible: true,
                                        labelPath: 'name',
                                        border: {
                                            color: 'green',
                                            width: 2
                                        },
                                        fill: 'red',
                                        opacity: 0.9,
                                        textStyle: {
                                            color: 'blue',
                                            size: '10px',
                                            fontStyle: 'Sans-serif',
                                            fontWeight: 'normal'
                                        }
                                    } }>
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent>,
document.getElementById("maps") as HTMLElement
);

```

{% endtab %}

## Smart labels

The Maps control provides an option to handle the labels when they intersect with the corresponding shape borders using the [`smartLabelMode`](../api/maps/dataLabelSettingsModel/#smartlabelmode) property. The following options are available in the [`smartLabelMode`](../api/maps/dataLabelSettingsModel/#smartlabelmode) property.

* None
* Hide
* Trim

{% tab template="maps/default-map", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import { usa_map } from 'usa.ts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective, Inject, DataLabel } from '@syncfusion/ej2-react-maps';

ReactDOM.render(
            <MapsComponent id="maps">
            <Inject services={[DataLabel]} />
                <LayersDirective>
                    <LayerDirective shapeData={usa_map}
                                    shapeSettings= { {
                                        autofill: true
                                    } }
                                    dataLabelSettings={ {
                                        visible: true,
                                        labelPath: 'name',
                                        smartLabelMode: 'Hide'
                                    } }>
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent>,
document.getElementById("maps") as HTMLElement
);

```

{% endtab %}

## Intersect action

The Maps component provides an option to handle the labels when a label intersects with another label using the [`intersectionAction`](../api/maps/dataLabelSettingsModel/#intersectionaction) property. The following options are available in the [`intersectionAction`](../api/maps/dataLabelSettingsModel/#intersectionaction) property.

* None
* Hide
* Trim

{% tab template="maps/default-map", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import { usa_map } from 'usa.ts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective, Inject, DataLabel } from '@syncfusion/ej2-react-maps';

ReactDOM.render(
            <MapsComponent id="maps">
            <Inject services={[DataLabel]} />
                <LayersDirective>
                    <LayerDirective shapeData={usa_map}
                                    shapeSettings= { {
                                        autofill: true
                                    } }
                                    dataLabelSettings= { {
                                        visible: true,
                                        labelPath: 'name',
                                        intersectionAction: 'Trim'
                                    } }>
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent>,
document.getElementById("maps") as HTMLElement
);

```

{% endtab %}

## Adding data label as a template

The data label can be added as a template in the Maps component. The [`template`](../api/maps/dataLabelSettingsModel/#template) property of [`dataLabelSettings`](../api/maps/dataLabelSettingsModel) is used to set the data label as a template. Any text or HTML element can be added as the template in data labels.

>The customization properties of data label, [`smartLabelMode`](../api/maps/dataLabelSettingsModel/#smartlabelmode) and [`intersectionAction`](../api/maps/dataLabelSettingsModel/#intersectionaction) properties are not applicable to [`template`](../api/maps/dataLabelSettingsModel/#template) property. The styles can be applied to the label template using the CSS styles of the template element.

{% tab template="maps/default-map", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import { usa_map } from 'usa.ts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective, Inject, DataLabel } from '@syncfusion/ej2-react-maps';

ReactDOM.render(
            <MapsComponent id="maps">
            <Inject services={[DataLabel]} />
                <LayersDirective>
                    <LayerDirective shapeData={usa_map}
                                    shapeSettings= {{
                                        autofill: true
                                    }}
                                    dataLabelSettings={ {
                                        visible: true,
                                        template: 'Label'
                                    } }>
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent>,
document.getElementById("maps") as HTMLElement
);

```

{% endtab %}