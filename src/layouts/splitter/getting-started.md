---
title: "Getting Started"
component: "Splitter"
description: "Explains to get started with Syncfusion React Splitter component with its key features such as resizable,validation and nested Splitter, etc."
---

# Getting Started

The following section explains the steps required to build the Splitter component with step-by-step procedure.

## Dependencies

The following list of dependencies required to use the Splitter component in your application:

```js
|-- @syncfusion/ej2-layouts
    |-- @syncfusion/ej2-base
|-- @syncfusion/ej2-react-layouts
    |-- @syncfusion/ej2-react-base

```

## Installation and configuration

You can use [`Create-react-app`](https://github.com/facebookincubator/create-react-app) to setup the
applications.
To install `create-react-app` run the following command.

```bash
npm install -g create-react-app
```

Start a new project using create-react-app command as follows

<div class='tsx'>

```bash
create-react-app quickstart --scripts-version=react-scripts-ts

cd quickstart

```

</div>

<div class='jsx'>

```sh

create-react-app quickstart

cd quickstart

```

</div>

Install the below required dependency package in order to use the `Splitter` component in your application.

```bash
npm install @syncfusion/ej2-react-layouts --save
```

* The Splitter CSS files are available in the `ej2-layouts` package folder.
This can be referred in your application using the following code.

`[src/App.css]`

```css
@import '../../node_modules/@syncfusion/ej2-base/styles/material.css';
@import '../../node_modules/@syncfusion/ej2-layouts/styles/material.css';
```

## Adding Splitter to the project

The Splitter can be initialized through `<SplitterComponent>` tag-directive with `<PanesDirective>` and `<PaneDirective>` as child elements respectively.

Please refer the below code snippet,

{% tab compileJsx=true %}

```typescript
import { PaneDirective, PanesDirective, SplitterComponent } from '@syncfusion/ej2-react-layouts';
import * as React from "react";

class App extends React.Component {
  public render() {
    return (
      <div className="App">
      <SplitterComponent id="splitter" height="250px" width="600px">
          <PanesDirective>
            <PaneDirective/>
            <PaneDirective/>
            <PaneDirective/>
          </PanesDirective>
      </SplitterComponent>
      </div>
    );
  }
}

export default App;

```

{% endtab %}

After completing the configurations to render the Splitter, use the following command to display
the output in your default browser.

```shell
npm start
```

Output will be as follows:

{% tab template="splitter/getting-started", sourceFiles="app/App.tsx", isDefaultActive=true, compileJsx=true   %}

```typescript
import { PaneDirective, PanesDirective, SplitterComponent } from '@syncfusion/ej2-react-layouts';
import * as React from "react";

class App extends React.Component {
  public render() {
    return (
      <div className="App">
        <SplitterComponent id="splitter" height="250px" width="600px">
          <PanesDirective>
            <PaneDirective/>
            <PaneDirective/>
            <PaneDirective/>
          </PanesDirective>
        </SplitterComponent>
      </div>
    );
  }
}

export default App;
```

{% endtab %}

## Orientation

Splitter supports both `Horizontal` and `Vertical` orientation for the panes. By default, it will be rendered in `Horizontal` orientation. You can change it by using [orientation](../api/splitter#orientation) property.

{% tab template="splitter/getting-started", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { PaneDirective, PanesDirective, SplitterComponent } from '@syncfusion/ej2-react-layouts';
import * as React from "react";

class App extends React.Component {
  public render() {
    return (<div className="App">
            <SplitterComponent id="splitter-vertical" height="250px" width="50%" orientation = {'Vertical'}>
              <PanesDirective>
                <PaneDirective/>
                <PaneDirective/>
              </PanesDirective>
            </SplitterComponent>
          </div>
    );
  }
}

export default App;
```

{% endtab %}

## Load content to the pane

You can load the pane contents in either HTML element or string types
using [content](../api/splitter/panePropertiesModel/#content) property.

For detailed information, refer to the [Pane Content](./pane-content/) section

{% tab template="splitter/getting-started", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { PaneDirective, PanesDirective, SplitterComponent } from '@syncfusion/ej2-react-layouts';
import * as React from "react";

class App extends React.Component {
public firstPane() {
  return (
    <div>
    <div className="content">
      <h3 className="h3">HTML</h3>
      <div className="code-preview">
        &lt;<span>!DOCTYPE html&gt;</span>
        <div>&lt;<span>html&gt;</span></div>
        <div>&lt;<span>body&gt;</span></div>
        &lt;<span>div</span> id="custom-image"&gt;
        <div>&lt;<span>img</span> src="src/albert.png"&gt;</div>
        <div>&lt;<span>div</span>&gt;</div>
        <div>&lt;<span>/body&gt;</span></div>
        <div>&lt;<span>/html&gt;</span></div>
      </div>
    </div>
    </div>
  );
}

public secondPane() {
  const openBrace: string = '{';
  const closeBrace: string = '}';
  return (
    <div>
    <div className="content">
      <h3 className="h3">CSS</h3>
      <div className="code-preview">
      <span>img {openBrace} </span>
      <div id="code-text">margin:<span>0 auto;</span></div>
      <div id="code-text">display:<span>flex;</span></div>
      <div id="code-text">height:<span>70px;</span></div>
      <span>{closeBrace}</span>
      </div>
    </div>
    </div>
  );
}

public thirdPane() {
  const openBrace: string = '{';
  const closeBrace: string = '}';
  return (
    <div>
      <div className="content">
        <h3 className="h3">JavaScript</h3>
        <div className="code-preview">
        <span>var</span> image = document.getElementById("custom-image");
        <div>image.addEventListener("click", function() { openBrace }</div>
          <div>// Code block for click action</div>
        <span> {closeBrace }) </span>
        </div>
      </div>
    </div>
  );
}

public render() {
  return (<div className="App">
  <SplitterComponent id="splitter" height="250px" width="550px">
  <PanesDirective>
  <PaneDirective content = {this.firstPane}/>
  <PaneDirective content = {this.secondPane}/>
  <PaneDirective content = {this.thirdPane}/>
  </PanesDirective>
  </SplitterComponent>
  </div>);
}
}

export default App;

```

{% endtab %}

## See Also

* [Construct different layouts using Splitter](different-layouts)
