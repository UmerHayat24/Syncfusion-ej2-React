---
title: " Annotations in React Maps control | Syncfusion "

component: "Maps"

description: "Learn here all about Annotations feature of Syncfusion React Maps control and more."
---

# Annotations in React Maps

<!-- markdownlint-disable MD013 -->

Annotations are used to mark the specific area of interest in the Maps with texts, shapes, or images. Any number of annotations can be added to the Maps control.

## Annotation

By using the [`content`](../api/maps/annotationModel/#content) property of [`AnnotationsDirective`](../api/maps/annotationModel), text content or id of an element or an HTML string can be specified to render a new HTML element in Maps.

<!-- markdownlint-disable MD036 -->

 ```html
<script id='annotation' type="text/x-template">
    <div id='template'>
        <img src='src/maps/images/flight.png'>
    </div>
</script>

```

```tsx
import { world_map } from 'world-map.ts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective, Inject } from '@syncfusion/ej2-react-maps';
import { AnnotationsDirective, AnnotationDirective, Annotations} from '@syncfusion/ej2-react-maps';


ReactDOM.render(
            <MapsComponent id="maps">
            <Inject services={[Annotations]}/>
                <AnnotationsDirective>
                    <AnnotationDirective content="#annotation" x="0%" y="50%"/>
                </AnnotationsDirective>
                <LayersDirective>
                    <LayerDirective shapeData={world_map}>
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent>,
            document.getElementById("maps") as HTMLElement
);
```

## Annotation customization

### Changing the z-index

The stack order of an annotation element can be changed using the [`zIndex`](../api/maps/annotationModel/#zindex) property in the [`AnnotationsDirective`](../api/maps/annotationModel).

{% tab template="maps/default-map", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx
import { world_map } from 'world-map.ts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective, Inject } from '@syncfusion/ej2-react-maps';
import { AnnotationsDirective, AnnotationDirective, Annotations} from '@syncfusion/ej2-react-maps';


ReactDOM.render(
            <MapsComponent id="maps">
            <Inject services={[Annotations]}/>
                <AnnotationsDirective>
                    <AnnotationDirective content='<div id="first"><h1>Maps</h1></div>' x="0%" y="50%" zIndex="-1"/>
                </AnnotationsDirective>
                <LayersDirective>
                    <LayerDirective shapeData={world_map}>
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent>,
            document.getElementById("maps") as HTMLElement
);
```

{% endtab %}

<!-- markdownlint-disable MD036 -->

### Positioning an annotation

Annotations can be placed anywhere in the Maps by specifying pixel or percentage values to the [`x`](../api/maps/annotationModel/#x) and [`y`](../api/maps/annotationModel/#y) properties in the [`AnnotationsDirective`](../api/maps/annotationModel).

{% tab template="maps/default-map", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx
import { world_map } from 'world-map.ts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective, Inject } from '@syncfusion/ej2-react-maps';
import { AnnotationsDirective, AnnotationDirective, Annotations} from '@syncfusion/ej2-react-maps';


ReactDOM.render(
            <MapsComponent id="maps">
            <Inject services={[Annotations]}/>
                <AnnotationsDirective>
                    <AnnotationDirective content='<div id="first"><h1>Maps</h1></div>' x="20%" y="50%" zIndex="-1"/>
                </AnnotationsDirective>
                <LayersDirective>
                    <LayerDirective shapeData={world_map}>
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent>,
            document.getElementById("maps") as HTMLElement
);
```

{% endtab %}

<!-- markdownlint-disable MD036 -->

### Alignment of an annotation

Annotations can be aligned using the [`horizontalAlignment`](../api/maps/annotationModel/#horizontalalignment) and [`verticalAlignment`](../api/maps/annotationModel/#verticalalignment) properties in the [`AnnotationsDirective`](../api/maps/annotationModel). The possible values can be **Center**, **Far**, **Near** and **None**.

{% tab template="maps/default-map", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx
import { world_map } from 'world-map.ts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective, Inject } from '@syncfusion/ej2-react-maps';
import { AnnotationsDirective, AnnotationDirective, Annotations} from '@syncfusion/ej2-react-maps';


ReactDOM.render(
            <MapsComponent id="maps">
            <Inject services={[Annotations]}/>
                <AnnotationsDirective>
                    <AnnotationDirective content='<div id="first"><h1>Maps</h1></div>' x="20%" y="50%" zIndex="-1"
                                         verticalAlignment="Center" horizontalAlignment="Center"/>
                </AnnotationsDirective>
                <LayersDirective>
                    <LayerDirective shapeData={world_map}>
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent>,
            document.getElementById("maps") as HTMLElement
);
```

{% endtab %}

## Multiple Annotation

Multiple annotations can be added to the Maps by adding multiple [`AnnotationDirective`](../api/maps/annotationModel) in the [`AnnotationsDirective`](../api/maps/#annotations) and customization for the annotations can be done with the [`AnnotationDirective`](../api/maps/annotationModel).

{% tab template="maps/default-map", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx
import { world_map } from 'world-map.ts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { MapsComponent, LayersDirective, LayerDirective, Inject } from '@syncfusion/ej2-react-maps';
import { AnnotationsDirective, AnnotationDirective, Annotations} from '@syncfusion/ej2-react-maps';


ReactDOM.render(
            <MapsComponent id="maps">
            <Inject services={[Annotations]}/>
                <AnnotationsDirective>
                    <AnnotationDirective content='<div id="first"><h1>Maps-Annotation</h1></div>' x="50%" y="0%" zIndex="-1"/>
                    <AnnotationDirective content='<div id="first"><h1>Maps</h1></div>' x="20%" y="50%" zIndex="-1"/>
                </AnnotationsDirective>
                <LayersDirective>
                    <LayerDirective shapeData={world_map}>
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent>,
            document.getElementById("maps") as HTMLElement
);
```

{% endtab %}