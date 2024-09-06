---
title: "Pane Content"
component: "Splitter"
description: "This section explains how to provide plain text content or HTML markup or integrate other React UI controls as content of splitter."
---

# Pane Content

This section explains how to provide plain text content or HTML markup or integrate other React UI controls as content of splitter.

## Template

You can render the HTML element directly to the splitter pane content
using [content](../api/splitter/panePropertiesModel/#content) template property.

{% tab template="splitter/html-content", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { PaneDirective, PanesDirective, SplitterComponent } from '@syncfusion/ej2-react-layouts';
import * as React from "react";

class App extends React.Component {
  public firstPaneContent(): JSX.Element {
    return(<div>
      <div className='content'>
        <h3>PARIS </h3>Paris, the city of lights and love - this short guide is full of ideas for how to make the most of the romanticism...
      </div>
      </div>);
  };
  public secondPaneContent(): JSX.Element {
    return(<div>
      <div className='content'>
        <h3>CAMEMBERT </h3>The village in the Orne département of Normandy where the famous French cheese is originated from. </div>
      </div>);
  };
  public thirdPaneContent(): JSX.Element {
    return(<div>
      <div className='content'>
        <h3>GRENOBLE </h3>The capital city of the French Alps and a major scientific center surrounded by many ski resorts, host of the Winter Olympics in 1968.
      </div>
      </div>);
  };
public render() {
  return (<div className="App">
  <SplitterComponent id="collapsed" height="250px" width='600px'>
  <PanesDirective>
    <PaneDirective size='200px' content = {this.firstPaneContent}/>
    <PaneDirective size='200px' content = {this.secondPaneContent}/>
    <PaneDirective size='200px' content = {this.thirdPaneContent}/>
  </PanesDirective>
  </SplitterComponent>
</div>);
}
}
export default App;

```

{% endtab %}

## React UI components

You can render any React UI controls along with their native and control events within splitter as pane content.

You can refer [Accordion within splitter](https://ej2.syncfusion.com/react/demos/#/material/splitter/accordion-navigation-menu) and [Listview within splitter](https://ej2.syncfusion.com/react/demos/#/material/splitter/details-view) samples.

## Plain content

You can add the plain text as a pane contents using either inner HTML or [content](../api/splitter/panePropertiesModel/#content) API

{% tab template="splitter/plain-content", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { PaneDirective, PanesDirective, SplitterComponent } from '@syncfusion/ej2-react-layouts';
import * as React from "react";

class App extends React.Component {
public render() {
  return (<div className="App">
  <SplitterComponent id="plain" height="250px" width='600px'>
  <PanesDirective>
    <PaneDirective size='200px' content = '<div class="content"> Left pane </div>'/>
    <PaneDirective size='200px' content = '<div class="content"> Middle pane </div>'/>
    <PaneDirective size='200px' content = '<div class="content"> Right pane </div>'/>
  </PanesDirective>
  </SplitterComponent>
</div>);
}
}
export default App;

```

{% endtab %}

## HTML Markup

Splitter is a layout based container control. You can render the pane contents from existing HTML markup. Converting HTML markup as splitter pane is easy way to add the panes content dynamically.

{% tab template="splitter/html-content", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { PaneDirective, PanesDirective, SplitterComponent } from '@syncfusion/ej2-react-layouts';
import * as React from "react";

class App extends React.Component {
public render() {
  return (<div className="App">
  <SplitterComponent id="plain" height="250px" width='600px'>
  <PanesDirective>
    <PaneDirective size='200px' content = '<div class="content"><h3 class="h3">PARIS </h3>Paris, the city of lights and love - this short guide is full of ideas for how to make the most of the romanticism...</div>'/>
    <PaneDirective size='200px' content =  '<div class="content"><h3 class="h3">CAMEMBERT </h3>The village in the Orne département of Normandy where the famous French cheese is originated from.</div>'/>
    <PaneDirective size='200px' content = '<div class="content"><h3 class="h3">GRENOBLE </h3>The capital city of the French Alps and a major scientific center surrounded by many ski resorts, host of the Winter Olympics in 1968.</div>'/>
  </PanesDirective>
  </SplitterComponent>
</div>);
}
}
export default App;
```

{% endtab %}

## Pane content using selector

You can set HTML element as pane [content](../api/splitter/panePropertiesModel/#content) using the query selectors such as ID or CSS class selectors.

The following code demonstrates how to fetch an element from the document and load it to pane using its ID.

{% tab template="splitter/selector-content", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { PaneDirective, PanesDirective, SplitterComponent } from '@syncfusion/ej2-react-layouts';
import * as React from "react";

class App extends React.Component {
public render() {
  return (<div className="App">

{ /* <!-- pane contents --> */}

  <div id="left-pane-content" style={{display: "none"}}>
    <div>Left pane<div id='panetext'>size: 25%</div>
        <div id='panetext'>min: 60px</div>
    </div>
</div>

<div id="middle-pane-content" style={{display: "none"}}>
    <span>Middle pane<div id="panetext">size: 50%</div>
        <div id="panetext">min: 60px</div>
    </span>
</div>

<div id="last-pane-content" style={{display: "none"}}>
    <span>Right pane<div id="panetext">size: 25%</div>
        <div id="panetext">min: 60px</div>
    </span>
</div>

  <SplitterComponent id="plain" height="250px" width='600px'>
  <PanesDirective>
    <PaneDirective size='200px' min="60px" content ='#left-pane-content'/>
    <PaneDirective size='200px' min="60px" content ='#middle-pane-content'/>
    <PaneDirective size='200px' min="60px" content ='#last-pane-content'/>
  </PanesDirective>
  </SplitterComponent>
</div>
);
}
}
export default App;
```

{% endtab %}