---
title: "Tooltip"
component: "Diagram"
description: "The tooltip is a message that is displayed when mouse hovers over an element."
---

# Tooltip

<!-- markdownlint-disable MD010 -->

In Graphical User Interface (GUI), the tooltip is a message that is displayed when mouse hovers over an element. The diagram provides tooltip support while dragging, resizing, rotating a node, and when the mouse hovers any diagram element.

## Default tooltip

By default, diagram displays a tooltip to provide the size, position, and angle related information while dragging, resizing, and rotating. The following images illustrate how the diagram displays the node information during an interaction.

| Drag | Resize | Rotate |
|---|---|---|
| ![ToolTip During Drag](images/Tooltip_img1.png) | ![ToolTip During Resize](images/Tooltip_img2.png) | ![ToolTip During Rotate](images/Tooltip_img3.png) |

## Common tooltip for all nodes and connectors

The diagram provides support to show tooltip when the mouse hovers over any node/connector.
To show tooltip on mouse over, the [`tooltip`](../api/diagram#tooltip) property of diagram model needs to be set with the tooltip [`content`](../api/diagram/diagramTooltip/#content) and [`position`](../api/diagram/diagramTooltip/#position) as shown in the following example.

{% tab template= "diagram/tooltip/es5tooltip", sourceFiles="app/**/*.tsx" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import {
    Diagram,
    NodeModel,
    DiagramComponent,
    DiagramConstraints,
    NodeConstraints
} from "@syncfusion/ej2-react-diagrams";
import { TooltipComponent, TooltipEventArgs } from '@syncfusion/ej2-react-popups';
import {
    NodeAnimationSettings
} from '@syncfusion/ej2-navigations';

// A node is created and stored in nodes array.
let node: NodeModel[] = [{
                id: "node1",
                width: 100,
                height: 100,
                annotations: [{
                    id: 'label',
                    content: 'Rectangle',
                    offset: {
                        x: 0.5,
                        y: 0.5
                    },
                    style: {
                        color: 'white',
                    },
                }],
                offsetX: 200,
                offsetY: 200,
                style: {
                    strokeColor: '#6BA5D7',
                    fill: '#6BA5D7',
                },
                constraints: NodeConstraints.Default | NodeConstraints.Tooltip,
            }];

//Initializes the Diagram component
ReactDOM.render( < DiagramComponent id = "diagram"
        width = {
            '650px'
        }
        height = {
            '350px'
        }
        constraints = {
            DiagramConstraints.Default | DiagramConstraints.Tooltip
        }
        //Defines nodes
        nodes = {
            node
        }
        //Defines mouse over tooltip
        tooltip = {
            {
                content: 'Nodes',
                position: 'TopLeft'
            }
        }
        />,   document.getElementById("diagram") );

```

{% endtab %}

### Disable tooltip at runtime

The tooltip on mouse over can be disabled by assigning the [`tooltip`](../api/diagram#tooltip) property as `null`. The following code example illustrates how to disable the mouse over tooltip at runtime.

```typescript

//Initializes the Diagram component
ReactDOM.render( < DiagramComponent id = "diagram"
        width = {
            '650px'
        }
        height = {
            '350px'
        }
        //Disables mouse over tooltip at runtime
        tooltip = {
            null
        }
        />,   document.getElementById("diagram") );

```

## Tooltip for a specific node/connector

The tooltip can be customized for each node and connector. Remove the **InheritTooltip** option from the [`constraints`](../api/diagram#constraints) of that node/connector. The following code example illustrates how to customize the tooltip for individual elements.

{% tab template= "diagram/tooltip/es5TooltipNodes", sourceFiles="app/**/*.tsx" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import {
    Diagram,
    NodeModel,
    DiagramComponent,
    DiagramConstraints,
    NodeConstraints
} from "@syncfusion/ej2-react-diagrams";
import {
    NodeAnimationSettings
} from '@syncfusion/ej2-navigations';

// A node is created and stored in nodes array.
let node: NodeModel[] = [{
                id: "node1",
                width: 100,
                height: 100,
                annotations: [{
                    id: 'label',
                    content: 'Rectangle',
                    offset: {
                        x: 0.5,
                        y: 0.5
                    },
                    style: {
                        color: 'white'
                    },
                }],
                offsetX: 200,
                offsetY: 200,
                style: {
                    strokeColor: '#6BA5D7',
                    fill: '#6BA5D7'
                },
                constraints: NodeConstraints.Default | NodeConstraints.Tooltip,
                //Defines mouse over tooltip for a node
                tooltip: {
                    //Sets the content of the Tooltip
                    content: 'Node1',
                    //Sets the position of the Tooltip
                    position: 'BottomRight',
                    //Sets the tooltip position relative to the node
                    relativeMode: 'Object'
                },
            }];

//Initializes the Diagram component
ReactDOM.render( < DiagramComponent id = "diagram"
        width = {
            '650px'
        }
        height = {
            '350px'
        }
        constraints = {
            DiagramConstraints.Default | DiagramConstraints.Tooltip
        }
        //Defines nodes
        nodes = {
            node
        }
        />,   document.getElementById("diagram") );

```

{% endtab %}

## Tooltip template content

Any text or image can be added to the tooltip, by default. To customize the tooltip layout or to create your own visualized element on the tooltip, template can be used.

The following code example illustrates how to add formatted HTML content to the tooltip.

{% tab template= "diagram/tooltip/es5TooltipTemplate", sourceFiles="app/**/*.tsx" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import {
    Diagram,
    NodeModel,
    DiagramComponent,
    DiagramConstraints,
    NodeConstraints
} from "@syncfusion/ej2-react-diagrams";
import {
    NodeAnimationSettings
} from '@syncfusion/ej2-navigations';

// A node is created and stored in nodes array.
let node: NodeModel[] = [{
                id: "node1",
                width: 100,
                height: 100,
                annotations: [{
                    id: 'label',
                    content: 'Rectangle',
                    offset: {
                        x: 0.5,
                        y: 0.5
                    },
                    style: {
                        color: 'white'
                    },
                }],
                offsetX: 200,
                offsetY: 200,
                style: {
                    strokeColor: '#6BA5D7',
                    fill: '#6BA5D7'
                },
                constraints: NodeConstraints.Default | NodeConstraints.Tooltip,
                //Defines mouse over tooltip for a node
                tooltip: {
                    //Sets the content of the Tooltip
                    content: getContent(),
                    //Sets the position of the Tooltip
                    position: 'TopLeft',
                    //Sets the tooltip position relative to the node
                    relativeMode: 'Object'
                }
            }];
            ReactDOM.render( < DiagramComponent id = "diagram"
        width = {
            '650px'
        }
        height = {
            '350px'
        }
        constraints = {
            DiagramConstraints.Default | DiagramConstraints.Tooltip
        }
        // Add node
        nodes = {
            node
        }
        // render initialized Diagram
        />,   document.getElementById("diagram") );

function getContent(): HTMLElement {
    let tooltipContent: HTMLElement = document.createElement('div');
    tooltipContent.innerHTML = '<div style="background-color: #f4f4f4; color: black; border-width:1px;border-style: solid;border-color: #d3d3d3; border-radius: 8px;white-space: nowrap;"> <span style="margin: 10px;"> Tooltip !!! </span> </div>';
    return tooltipContent;
}

```

{% endtab %}

## Tooltip alignments

### Tooltip relative to object

The diagram provides support to show tooltip around the node/connector that is hovered by the mouse. The tooltip can be aligned by using the [`position`](../api/diagram/diagramTooltip#position) property of the tooltip.
The [`relativeMode`](../api/diagram/diagramTooltip#relativemode) property of the tooltip defines whether the tooltip has to be displayed around the object or at the mouse position.

The following code example illustrates how to position the tooltip around object.

{% tab template= "diagram/tooltip/es5TooltipObject", sourceFiles="app/**/*.tsx" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import {
    Diagram,
    NodeModel,
    DiagramComponent,
    DiagramConstraints,
    NodeConstraints
} from "@syncfusion/ej2-react-diagrams";
import {
    NodeAnimationSettings
} from '@syncfusion/ej2-navigations';

// A node is created and stored in nodes array.
let node: NodeModel[] = [{
                id: "node1",
                width: 100,
                height: 100,
                annotations: [{
                    id: 'label',
                    content: 'Rectangle',
                    offset: {
                        x: 0.5,
                        y: 0.5
                    },
                    style: {
                        color: 'white'
                    }
                }],
                offsetX: 200,
                offsetY: 200,
                style: {
                    strokeColor: '#6BA5D7',
                    fill: '#6BA5D7'
                },
                constraints: NodeConstraints.Default | NodeConstraints.Tooltip,
                //Defines mouse over tooltip for a node
                tooltip: {
                    content: 'Node1',
                    //Sets the alignment properties
                    position: 'BottomRight',
                    //Sets to show tooltip around the element
                    relativeMode: 'Object',
                },
            }];

//Initializes the Diagram component
ReactDOM.render( < DiagramComponent id = "diagram"
        width = {
            '650px'
        }
        height = {
            '350px'
        }
        constraints = {
            DiagramConstraints.Default | DiagramConstraints.Tooltip
        }
        //Defines nodes
        nodes = {
            node
        }
        />,   document.getElementById("diagram") );

```

{% endtab %}

### Tooltip relative to mouse position

To display the tooltip at mouse position, need to set **mouse** option to the [`relativeMode`](../api/diagram/diagramTooltip#relativemode) property of the tooltip.
The following code example illustrates how to show tooltip at mouse position.

{% tab template= "diagram/tooltip/es5TooltipMouse", sourceFiles="app/**/*.tsx" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import {
    Diagram,
    NodeModel,
    DiagramComponent,
    DiagramConstraints,
    NodeConstraints
} from "@syncfusion/ej2-react-diagrams";
import {
    NodeAnimationSettings
} from '@syncfusion/ej2-navigations';

let node: NodeModel[] = [{
                id: "node1",
                width: 100,
                height: 100,
                annotations: [{
                    id: 'label',
                    content: 'Rectangle',
                    offset: {
                        x: 0.5,
                        y: 0.5
                    },
                    style: {
                        color: 'white'
                    }
                }],
                offsetX: 200,
                offsetY: 200,
                style: {
                    strokeColor: '#6BA5D7',
                    fill: '#6BA5D7'
                },
                constraints: NodeConstraints.Default | NodeConstraints.Tooltip,
                //Defines mouse over tooltip for a node
                tooltip: {
                    content: 'Node1',
                    //Sets to show tooltip at mouse position
                    relativeMode: 'Mouse',
                },
            }];

//Initializes the Diagram component
ReactDOM.render( < DiagramComponent id = "diagram"
        width = {
            '650px'
        }
        height = {
            '350px'
        }
        constraints = {
            DiagramConstraints.Default | DiagramConstraints.Tooltip
        }
        //Defines nodes
        nodes = {
            node
        }
        />,   document.getElementById("diagram") );

```

{% endtab %}

## Tooltip animation

To animate the tooltip, a set of specific animation effects are available, and it can be controlled by using the [`animation`](../api/diagram/diagramTooltip#animation) property. The animation property also allows you to set delay, duration, and various other effects of your choice.

{% tab template= "diagram/tooltip/es5TooltipAnimation", sourceFiles="app/**/*.tsx" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
    import {
        Diagram,
        DiagramComponent,
        NodeModel,
        DiagramConstraints,
        NodeConstraints
    } from "@syncfusion/ej2-react-diagrams";
    import {
        NodeAnimationSettings
    } from '@syncfusion/ej2-navigations';

let node: NodeModel[] = [{
                    id: "node1",
                    width: 100,
                    height: 100,
                    annotations: [{
                        id: 'label',
                        content: 'Rectangle',
                        offset: {
                            x: 0.5,
                            y: 0.5
                        },
                        style: {
                            color: 'white'
                        },
                    }],
                    offsetX: 200,
                    offsetY: 200,
                    style: {
                        strokeColor: '#6BA5D7',
                        fill: '#6BA5D7'
                    },
                    constraints: NodeConstraints.Default | NodeConstraints.Tooltip,
                    //Defines mouse over tooltip for a node
                    tooltip: {
                        content: 'Node1',
                        position: 'BottomCenter',
                        relativeMode: 'Object',
                        animation: {
                            //Animation settings to be applied on the Tooltip, while it is being shown over the target.
                            open: {
                                //Animation effect on the Tooltip is applied during open and close actions.
                                effect: 'ZoomIn',
                                //Duration of the animation that is completed per animation cycle.
                                duration: 1000,
                                //Indicating the waiting time before animation begins.
                                delay: 0
                            },
                            //Animation settings to be applied on the Tooltip, when it is closed.
                            close: {
                                effect: 'ZoomOut',
                                duration: 500,
                                delay: 0
                            },
                        },
                    },
                }];

    //Initializes the Diagram component
    ReactDOM.render( < DiagramComponent id = "diagram"
            width = {
                '650px'
            }
            height = {
                '350px'
            }
            constraints = {
                DiagramConstraints.Default | DiagramConstraints.Tooltip
            }
            //Defines nodes
            nodes = {
                node
            }
            />,   document.getElementById("diagram") );

```

{% endtab %}