---
title: "Getting Started"
component: "Diagram"
description: "Diagram getting started creates your first flow diagram and organizational chart diagram."
---

# Getting started

This section explains the steps required to create a simple diagram and demonstrates the basic usage of the diagram control.

## Dependencies

The following list of dependencies are required to use the `Diagram` component in your application.

```javascript
|-- @syncfusion/ej2-react-diagrams
    |-- @syncfusion/ej2-base
    |-- @syncfusion/ej2-data
    |-- @syncfusion/ej2-navigations
    |-- @syncfusion/ej2-inputs
    |-- @syncfusion/ej2-popups
    |-- @syncfusion/ej2-buttons
    |-- @syncfusion/ej2-lists
    |-- @syncfusion/ej2-splitbuttons
    |-- @syncfusion/ej2-diagrams
    |-- @syncfusion/ej2-react-base
```

## Installation and configuration

You can use [`create-react-app`](https://github.com/facebookincubator/create-react-app) to setup the applications.
To install `create-react-app` run the following command.

```sh
npm install -g create-react-app
```

* To setup basic `React` sample use following commands.

```sh
create-react-app quickstart --scripts-version=react-scripts-ts

cd quickstart
```

### Adding Syncfusion packages

All the available Essential JS 2 packages are published in [`Node Package Manager`](https://www.npmjs.com/~syncfusionorg) public registry.
You can choose the component that you want to install. For this application, we are going to use `Diagram` component.

To install Diagram component, use the following command

```bash
npm install @syncfusion/ej2-react-diagrams –save
```

### Adding Style sheet to the Application

Add Diagram component's styles as given below in `App.css`.

```css
@import "../node_modules/@syncfusion/ej2-react-diagrams/styles/material.css";
@import "../node_modules/@syncfusion/ej2-react-base/styles/material.css";
@import "../node_modules/@syncfusion/ej2-react-buttons/styles/material.css";
@import "../node_modules/@syncfusion/ej2-react-popups/styles/material.css";
@import "../node_modules/@syncfusion/ej2-react-splitbuttons/styles/material.css";
@import "../node_modules/@syncfusion/ej2-react-navigations/styles/material.css";
```

### Adding Diagram component to the Application

* To include the Diagram component in application import the `DiagramComponent` from `ej2-react-diagrams` package.

* Then add the Diagram component as shown in below code example.

`[src/App.tsx]`

```typescript
import * as React from "react";
import "./App.css";
// import the DiagramComponent
import { DiagramComponent } from "@syncfusion/ej2-react-diagrams";

export default class App extends React.Component<{}, {}> {
  render() {
    return <DiagramComponent id="diagram" />;
  }
}
```

### Run the application

Now run the `npm start` command in the console, it will run your application and open the browser window.

```cmd
npm start
```

The below examples shows the basic Diagram component.

{% tab template="diagram/getting-started/initialize", sourceFiles="app/**/*.tsx",  isDefaultActive=true %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import { DiagramComponent } from "@syncfusion/ej2-react-diagrams";

ReactDOM.render(
  <DiagramComponent id="diagram" width={"100%"} height={"350px"} />,
  document.getElementById("diagram")
);
```

{% endtab %}

## Module Injection

The diagram component is divided into individual feature-wise modules. In order to use a particular feature, inject the required module. The following list describes the module names and their description.

* `BpmnDiagrams` - Inject this provider to add built-in BPMN Shapes to diagrams.
* `ConnectorBridging` - Inject this provider to add bridges to connectors.
* `ConnectorEditing` - Inject this provider to edit the segments for connector.
* `ComplexHierarchicalTree` - Inject this provider to complex hierarchical tree like structure.
* `DataBinding` - Inject this provider to populate nodes from given data source.
* `DiagramContextMenu` - Inject this provider to manipulate context menu.
* `HierarchicalTree` - Inject this provider to use hierarchical tree like structure.
* `LayoutAnimation` - Inject this provider animation to layouts.
* `MindMap` - Inject this provider to use mind map.
* `PrintAndExport` - Inject this provider to print or export the objects.
* `RadialTree` - Inject this provider to use Radial tree like structure.
* `Snapping` - Inject this provider to Snap the objects.
* `SymmetricLayout` - Inject this provider to render layout in symmetrical method.
* `UndoRedo` - Inject this provider to revert and restore the changes.

These modules should be imported and injected into the Diagram component using `Diagram.Inject` method as follows.

```javascript
import * as React from "react";
import * as ReactDOM from "react-dom";
import {
  DiagramComponent,
  HierarchicalTree,
  MindMap,
  RadialTree,
  ComplexHierarchicalTree,
  DataBinding,
  Snapping,
  PrintAndExport,
  BpmnDiagrams,
  SymmetricLayout,
  ConnectorBridging,
  UndoRedo,
  LayoutAnimation,
  DiagramContextMenu,
  ConnectorEditing
} from "@syncfusion/ej2-react-diagrams";

ReactDOM.render(
  <DiagramComponent id="diagram">
    <Inject
      services={[
        HierarchicalTree,
        MindMap,
        RadialTree,
        ComplexHierarchicalTree,
        DataBinding,
        Snapping,
        PrintAndExport,
        BpmnDiagrams,
        SymmetricLayout,
        ConnectorBridging,
        UndoRedo,
        LayoutAnimation,
        DiagramContextMenu,
        ConnectorEditing
      ]}
    />
  </DiagramComponent>,
  document.getElementById("diagram")
);
```

## Flow Diagram

### Create and Add Node

Create and add a `node` (JSON data) with specific position, size, label, and shape.

{% tab template="diagram/getting-started/addnode", sourceFiles="app/**/*.tsx",  isDefaultActive=true %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import { DiagramComponent, NodeModel } from "@syncfusion/ej2-react-diagrams";

let nodes: NodeModel[] = [
  {
    id: "node1",
    height: 100,
    width: 100,
    offsetX: 100,
    offsetY: 200
  }
];

ReactDOM.render(
  <DiagramComponent
    id="diagram"
    width={"100%"}
    height={"350px"}
    nodes={nodes}
  />,
  document.getElementById("diagram")
);
```

{% endtab %}

### Connect two Nodes with a Connector

Add two node to the diagram as shown in the previous example. Connect these nodes by adding a connector using the `connector` property and refer the source and target end by using the `sourceNode` and `targetNode` properties.

{% tab template="diagram/getting-started/connectnode", sourceFiles="app/**/*.tsx",  isDefaultActive=true %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import {
  DiagramComponent,
  NodeModel,
  ConnectorModel
} from "@syncfusion/ej2-react-diagrams";

let nodes: NodeModel[] = [
  {
    id: "node1",
    height: 100,
    width: 100,
    offsetX: 200,
    offsetY: 100
  },
  {
    id: "node2",
    height: 100,
    width: 100,
    offsetX: 200,
    offsetY: 250
  }
];

let connectors: ConnectorModel[] = [
  {
    id: "connector1",
    sourceID: "node1",
    targetID: "node2"
  }
];

ReactDOM.render(
  <DiagramComponent
    id="diagram"
    width={"100%"}
    height={"350px"}
    nodes={nodes}
    connectors={connectors}
  />,
  document.getElementById("diagram")
);
```

{% endtab %}

Default values for all `nodes` and `connectors` can be set using the `getNodeDefaults` and `getConnectorDefaults` properties, respectively. For example, if all nodes have the same width and height, such properties can be moved into `getNodeDefaults`.

### Complete Flow Diagram

Similarly we can add required nodes and connectors to form a complete flow diagram.

{% tab template="diagram/getting-started/flowdiagram", sourceFiles="app/**/*.tsx",  isDefaultActive=true %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import {
  DiagramComponent,
  NodeModel,
  ConnectorModel
} from "@syncfusion/ej2-react-diagrams";

let nodes: NodeModel[] = [
  {
    id: "node1",
    offsetY: 50,
    shape: { type: "Flow", shape: "Terminator" },
    annotations: [
      {
        content: "Start"
      }
    ]
  },
  {
    id: "node2",
    offsetY: 140,
    shape: { type: "Flow", shape: "Process" },
    annotations: [
      {
        content: "var i = 0;"
      }
    ]
  },
  {
    id: "node3",
    offsetY: 230,
    shape: { type: "Flow", shape: "Decision" },
    annotations: [
      {
        content: "i < 10?"
      }
    ]
  },
  {
    id: "node4",
    offsetY: 320,
    shape: { type: "Flow", shape: "PreDefinedProcess" },
    annotations: [
      {
        content: 'print("Hello!!");'
      }
    ]
  },
  {
    id: "node5",
    offsetY: 410,
    shape: { type: "Flow", shape: "Process" },
    annotations: [
      {
        content: "i++;"
      }
    ]
  },
  {
    id: "node6",
    offsetY: 500,
    shape: { type: "Flow", shape: "Terminator" },
    annotations: [
      {
        content: "End"
      }
    ]
  }
];

let connectors: ConnectorModel[] = [
  {
    id: "connector1",
    sourceID: "node1",
    targetID: "node2"
  },
  {
    id: "connector2",
    sourceID: "node2",
    targetID: "node3"
  },
  {
    id: "connector3",
    sourceID: "node3",
    targetID: "node4",
    annotations: [{ text: "Yes" }]
  },
  {
    id: "connector4",
    sourceID: "node3",
    targetID: "node6",
    labels: [{ text: "No" }],
    segments: [
      { length: 30, direction: "Right" },
      { length: 300, direction: "Bottom" }
    ]
  },
  {
    id: "connector5",
    sourceID: "node4",
    targetID: "node5"
  },
  {
    id: "connector6",
    sourceID: "node5",
    targetID: "node3",
    segments: [
      { length: 30, direction: "Left" },
      { length: 200, direction: "Top" }
    ]
  }
];

ReactDOM.render(
  <DiagramComponent
    id="diagram"
    width={"100%"}
    height={"600px"}
    nodes={nodes}
    connectors={connectors}
    getNodeDefaults={(node: NodeModel): NodeModel => {
      node.height = 50;
      node.width = 140;
      node.offsetX = 300;
      return node;
    }}
    getConnectorDefaults={(obj: ConnectorModel): ConnectorModel => {
      obj.type = "Orthogonal";
    }}
  />,
  document.getElementById("diagram")
);
```

{% endtab %}

## Automatic Organization Chart

In ‘Flow Diagram’ section we saw how to create a diagram manually, now let us see how to create and position diagram automatically.

### Business object (Employee information)

Define Employee Information as JSON data. The following code example shows an employee array whose, `Name` is used as an unique identifier and `ReportingPerson` is used to identify the person to whom an employee report to, in the organization.

```typescript
    public data: Object[] = [
        {
            Name: "Elizabeth",
            Role: "Director"
        },
        {
            Name: "Christina",
            ReportingPerson: "Elizabeth",
            Role: "Manager"
        },
        {
            Name: "Yoshi",
            ReportingPerson: "Christina",
            Role: "Lead"
        },
        {
            Name: "Philip",
            ReportingPerson: "Christina",
            Role: "Lead"
        },
        {
            Name: "Yang",
            ReportingPerson: "Elizabeth",
            Role: "Manager"
        },
        {
            Name: "Roland",
            ReportingPerson: "Yang",
            Role: "Lead"
        },
        {
            Name: "Yvonne",
            ReportingPerson: "Yang",
            Role: "Lead"
        }
    ];
```

### Map data source

You can configure the above "Employee Information" with diagram, so that the nodes and connectors are automatically generated using the mapping properties. The following code example show how `dataSourceSettings` is used to map ID and parent with property name identifiers for employee information.

```typescript

export let data: Object[] = [
  {
    Name: "Elizabeth",
    Role: "Director"
  },
  {
    Name: "Christina",
    ReportingPerson: "Elizabeth",
    Role: "Manager"
  },
  {
    Name: "Yoshi",
    ReportingPerson: "Christina",
    Role: "Lead"
  },
  {
    Name: "Philip",
    ReportingPerson: "Christina",
    Role: "Lead"
  },
  {
    Name: "Yang",
    ReportingPerson: "Elizabeth",
    Role: "Manager"
  },
  {
    Name: "Roland",
    ReportingPerson: "Yang",
    Role: "Lead"
  },
  {
    Name: "Yvonne",
    ReportingPerson: "Yang",
    Role: "Lead"
  }
];

let dataSettings: object = {
  id: "Name",
  parentId: "ReportingPerson",
  dataManager: new DataManager(data as JSON[])
}

ReactDOM.render(<DiagramComponent
id="diagram"
width={"100%"}
height={"350px"}
dataSourceSettings={dataSettings}><Inject services={[HierarchicalTree, DataBinding]} /></DiagramComponent>,
document.getElementById("diagram")
);
```

### Visualize employee

Following code examples indicate how to define the default appearance of node and connector using default settings.

{% tab template="diagram/getting-started/orgchart", sourceFiles="app/**/*.tsx",  isDefaultActive=true %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import { DiagramComponent } from "@syncfusion/ej2-react-diagrams";
import {
  Node,
  HierarchicalTree,
  Diagram,
  NodeModel,
  ConnectorModel,
  Inject,
  DataBinding
} from "@syncfusion/ej2-react-diagrams";
import { DataManager } from "@syncfusion/ej2-data";

export interface EmployeeInfo {
  Name: string;
  Role: string;
  color: string;
}

export let data: Object[] = [
  {
    Name: "Elizabeth",
    Role: "Director"
  },
  {
    Name: "Christina",
    ReportingPerson: "Elizabeth",
    Role: "Manager"
  },
  {
    Name: "Yoshi",
    ReportingPerson: "Christina",
    Role: "Lead"
  },
  {
    Name: "Philip",
    ReportingPerson: "Christina",
    Role: "Lead"
  },
  {
    Name: "Yang",
    ReportingPerson: "Elizabeth",
    Role: "Manager"
  },
  {
    Name: "Roland",
    ReportingPerson: "Yang",
    Role: "Lead"
  },
  {
    Name: "Yvonne",
    ReportingPerson: "Yang",
    Role: "Lead"
  }
];

let dataSettings: object = {
  id: "Name",
  parentId: "ReportingPerson",
  dataManager: new DataManager(data as JSON[])
}

let layoutSetting: object= { type: "OrganizationalChart" }

ReactDOM.render(<DiagramComponent
id="diagram"
width={"100%"}
height={"350px"}
dataSourceSettings={dataSettings}
layout={layoutSetting}
getNodeDefaults={(node: NodeModel): NodeModel => {
let codes: Object = {
    Director: "rgb(0, 139,139)",
    Manager: "rgb(30, 30,113)",
    Lead: "rgb(0, 100,0)"
};
node.width = 70;
node.height = 30;
node.annotations = [
{ content: (node.data as EmployeeInfo).Name, style: { color: "white" } }
];
node.style.fill = codes[(node.data as EmployeeInfo).Role];
return node;
}}
getConnectorDefaults={(connector: ConnectorModel): ConnectorModel => {
    connector.type = "Orthogonal";
    connector.cornerRadius = 7;
    return connector;
}}><Inject services={[HierarchicalTree, DataBinding]} /></DiagramComponent>,
document.getElementById("diagram")
);
```

{% endtab %}
