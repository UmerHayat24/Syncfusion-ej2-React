---
title: "Gridlines"
component: "Diagram"
description: "Diagram gridlines are the lines that are draw behind the nodes and connectors."
---

# Gridlines

Gridlines are the pattern of lines drawn behind the diagram elements. It provides a visual guidance while dragging or arranging the objects on the diagram surface.

The model’s [`snapSettings`](../api/diagram#snapsettings-SnapSettingsModel) property is used to customize the gridlines and control the snapping behavior in the diagram.

## Customize the gridlines visibility

The [`snapSettings.snapConstraints`](../api/diagram/snapSettings#constraints-SnapConstraints) enables you to show/hide the gridlines. The following code example illustrates how to show or hide gridlines.

If you need to enable snapping, then inject snapping module into the diagram.

{% tab template= "diagram/nodes/es5Node", sourceFiles="app/**/*.tsx" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import {
    Diagram,
    NodeModel,
    DiagramComponent,
    SnapSettingsModel,
    SnapConstraints,
    UndoRedo,
    GridlinesModel,
    Snapping,
    Inject
} from "@syncfusion/ej2-react-diagrams";

let snapSettings: SnapSettingsModel = {
  constraints: SnapConstraints.ShowLines,
};
// A node is created and stored in nodes array.

let node: NodeModel[] = [{
    // Position of the node
    offsetX: 250,
    offsetY: 250,
    // Size of the node
    width: 100,
    height: 100,
    style: {
        fill: '#6BA5D7',
        strokeColor: 'white'
    },
    // Text(label) added to the node
}];

// initialize Diagram component

ReactDOM.render( < DiagramComponent id = "diagram"
        width = {
            '100%'
        }
        height = {
            '600px'
        }
        // Add node
        nodes = {
            node
        }
        snapSettings={snapSettings}
        // render initialized Diagram
        />,   document.getElementById("diagram") );

```

{% endtab %}

To show only horizontal/vertical gridlines or to hide gridlines, refer to [`Constraints`](../api/diagram/snapSettings#constraints-SnapConstraints).

## Appearance

The appearance of the gridlines can be customized by using a set of predefined properties.

* The [`horizontalGridLines`](../api/diagram/snapSettings#horizontalgridlines-GridlinesModel) and the [`verticalGridLines`](../api/diagram/snapSettings#verticalgridlines-GridlinesModel) properties allow to customize the appearance of the horizontal and vertical gridlines respectively.

* The horizontal gridlines [`lineColor`](../api/diagram/gridlines#linecolor-string) and [`lineDashArray`](../api/diagram/gridlines#linedasharray-string) properties are used to customizes the line color and line style of the horizontal gridlines.

* The vertical gridlines [`lineColor`](../api/diagram/gridlines#linecolor-string) and [`lineDashArray`](../api/diagram/gridlines#linedasharray-string) properties are used to customizes the line color and line style of the vertical gridlines.

The following code example illustrates how to customize the appearance of gridlines.

{% tab template= "diagram/nodes/es5Node", sourceFiles="app/**/*.tsx" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import {
    Diagram,
    NodeModel,
    DiagramComponent,
    SnapSettingsModel,
    SnapConstraints,
    UndoRedo,
    GridlinesModel,
    Snapping,
    Inject
} from "@syncfusion/ej2-react-diagrams";
let gridlines: GridlinesModel = {
  lineColor: "blue",
  lineDashArray: '2 2'
};
let snapSettings: SnapSettingsModel = {
  constraints: SnapConstraints.ShowLines,
  horizontalGridlines: gridlines,
  verticalGridlines: gridlines
};
// A node is created and stored in nodes array.

let node: NodeModel[] = [{
    // Position of the node
    offsetX: 250,
    offsetY: 250,
    // Size of the node
    width: 100,
    height: 100,
    style: {
        fill: '#6BA5D7',
        strokeColor: 'white'
    },
    // Text(label) added to the node
}];

// initialize Diagram component

ReactDOM.render( < DiagramComponent id = "diagram"
        width = {
            '100%'
        }
        height = {
            '600px'
        }
        // Add node
        nodes = {
            node
        }
        snapSettings={snapSettings}
        // render initialized Diagram
        />,   document.getElementById("diagram") );

```

{% endtab %}

## Line intervals

Thickness and the space between gridlines can be customized by using horizontal gridlines’s [`linesInterval`](../api/diagram/gridlines#lineintervals-number) and vertical gridlines’s [`linesInterval`](../api/diagram/gridlines#lineintervals-number) properties. In the lines interval collections, values at the odd places are referred as the thickness of lines and values at the even places are referred as the space between gridlines.
The following code example illustrates how to customize the thickness of lines and the line intervals.

{% tab template= "diagram/nodes/es5Node", sourceFiles="app/**/*.tsx" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import {
    Diagram,
    NodeModel,
    DiagramComponent,
    SnapSettingsModel,
    SnapConstraints,
    UndoRedo,
    GridlinesModel,
    Snapping,
    Inject
} from "@syncfusion/ej2-react-diagrams";
let interval: number[];
interval = [
  1,
  9,
  0.25,
  9.75,
  0.25,
  9.75,
  0.25,
  9.75,
  0.25,
  9.75,
  0.25,
  9.75,
  0.25,
  9.75,
  0.25,
  9.75,
  0.25,
  9.75,
  0.25,
  9.75
];
let gridlines: GridlinesModel = {
  lineColor: 'blue',
  lineDashArray: '2 2',
  lineIntervals: interval
};
let snapSettings: SnapSettingsModel = {
  constraints: SnapConstraints.ShowLines,
  horizontalGridlines: gridlines,
  verticalGridlines: gridlines
};
// A node is created and stored in nodes array.

let node: NodeModel[] = [{
    // Position of the node
    offsetX: 250,
    offsetY: 250,
    // Size of the node
    width: 100,
    height: 100,
    style: {
        fill: '#6BA5D7',
        strokeColor: 'white'
    },
    // Text(label) added to the node
}];

// initialize Diagram component

ReactDOM.render( < DiagramComponent id = "diagram"
        width = {
            '100%'
        }
        height = {
            '600px'
        }
        // Add node
        nodes = {
            node
        }
        snapSettings={snapSettings}
        // render initialized Diagram
        />,   document.getElementById("diagram") );

```

{% endtab %}

## Snapping

## Snap to lines

This feature allows the diagram objects to snap to the nearest intersection of gridlines while being dragged or resized. This feature enables easier alignment during layout or design.

Snapping to gridlines can be enabled/disabled with the [`snapSettings.snapConstraints`](../api/diagram/snapSettings#constraints-SnapConstraints). The following code example illustrates how to enable/disable the snapping to gridlines.

{% tab template= "diagram/nodes/es5Node", sourceFiles="app/**/*.tsx" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import {
    Diagram,
    NodeModel,
    DiagramComponent,
    SnapSettingsModel,
    SnapConstraints,
    UndoRedo,
    GridlinesModel,
    Snapping,
    Inject
} from "@syncfusion/ej2-react-diagrams";
let snapSettings: SnapSettingsModel = {
    constraints: SnapConstraints.SnapToLines | SnapConstraints.ShowLines
};
// A node is created and stored in nodes array.

let node: NodeModel[] = [{
    // Position of the node
    offsetX: 250,
    offsetY: 250,
    // Size of the node
    width: 100,
    height: 100,
    style: {
        fill: '#6BA5D7',
        strokeColor: 'white'
    },
    // Text(label) added to the node
}];

// initialize Diagram component

ReactDOM.render( < DiagramComponent id = "diagram"
        width = {
            '100%'
        }
        height = {
            '600px'
        }
        // Add node
        nodes = {
            node
        }
        snapSettings={snapSettings}
        // render initialized Diagram
        ><Inject services = {[Snapping]}/>
        </DiagramComponent>,   document.getElementById("diagram") );

```

{% endtab %}

## Customization of snap intervals

By default, the objects are snapped towards the nearest gridline. The gridline or position towards where the diagram object snaps can be customized with the horizontal gridlines’s [`snapInterval`](../api/diagram/gridlines#snapintervals-number) and the vertical gridlines’s [`snapInterval`](../api/diagram/gridlines#snapintervals-number) properties.

{% tab template= "diagram/nodes/es5Node", sourceFiles="app/**/*.tsx" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import {
    Diagram,
    NodeModel,
    DiagramComponent,
    SnapSettingsModel,
    SnapConstraints,
    UndoRedo,
    GridlinesModel,
    Snapping,
    Inject
} from "@syncfusion/ej2-react-diagrams";
let gridlines: GridlinesModel = {
  // Defines the snap interval for object
  snapIntervals: [10],
};
let snapSettings: SnapSettingsModel = {
  constraints: SnapConstraints.All,
  horizontalGridlines: gridlines,
  verticalGridlines: gridlines
};
// A node is created and stored in nodes array.

let node: NodeModel[] = [{
    // Position of the node
    offsetX: 250,
    offsetY: 250,
    // Size of the node
    width: 100,
    height: 100,
    style: {
        fill: '#6BA5D7',
        strokeColor: 'white'
    },
    // Text(label) added to the node
}];

// initialize Diagram component

ReactDOM.render( < DiagramComponent id = "diagram"
        width = {
            '100%'
        }
        height = {
            '600px'
        }
        // Add node
        nodes = {
            node
        }
        snapSettings={snapSettings}
        // render initialized Diagram
        ><Inject services = {[Snapping]}/>
    </DiagramComponent>,   document.getElementById("diagram") );

```

{% endtab %}

## Snap to objects

The snap to object provides visual cues to assist with aligning and spacing diagram elements. A node can be snapped with its neighboring objects based on certain alignments. Such alignments are visually represented as smart guides.

The [`snapObjectDistance`](../api/diagram/snapSettings/#snapobjectdistance) property allows you to define minimum distance between the selected object and the nearest object.

The [`snapAngle`](../api/diagram/snapSettings/#snapangle) property allows you to define the snap angle by which the object needs to be rotated.

The [`snapConstraints`](../api/diagram/snapSettings/#constraints) property allows you to enable or disable the certain features of the snapping, refer to `snapConstraints`.

{% tab template= "diagram/nodes/es5Node", sourceFiles="app/**/*.tsx" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import {
    Diagram,
    NodeModel,
    DiagramComponent,
    SnapSettingsModel,
    SnapConstraints,
    UndoRedo,
    GridlinesModel,
    Snapping,
    Inject
} from "@syncfusion/ej2-react-diagrams";
let snapSettings: SnapSettingsModel = {
  snapObjectDistance: 10,
  snapAngle: 10,
  constraints: SnapConstraints.SnapToObject | SnapConstraints.ShowLines,
};
// A node is created and stored in nodes array.

let node: NodeModel[] = [{
    // Position of the node
    offsetX: 250,
    offsetY: 250,
    // Size of the node
    width: 100,
    height: 100,
    style: {
        fill: '#6BA5D7',
        strokeColor: 'white'
    },
    // Text(label) added to the node
}];

// initialize Diagram component

ReactDOM.render( < DiagramComponent id = "diagram"
        width = {
            '100%'
        }
        height = {
            '600px'
        }
        // Add node
        nodes = {
            node
        }
        snapSettings={snapSettings}
        // render initialized Diagram
        ><Inject services = {[Snapping]}/>
    </DiagramComponent>,   document.getElementById("diagram") );

```

{% endtab %}