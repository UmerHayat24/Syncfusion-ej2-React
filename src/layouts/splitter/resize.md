---
title: "Resize"
component: "Splitter"
description: "This section explain about split panes resizing behaviors."
---

# Resize

By default, resizing will be enable for split panes. Resizing gripper element will be add to the separator to makes the resize easy.

> Horizontal splitter will allows to resize in horizontal directions.
> Vertical splitter will allows to resize in vertical directions.

While resizing, previous and next panes will be adjust its dimensions automatically.

## Min and Max validation

Splitter allows you to set the minimum and maximum sizes for each pane. Resizing will not be occur over the minimum and maximum values.

{% tab template="splitter/validation", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { PaneDirective, PanesDirective, SplitterComponent } from '@syncfusion/ej2-react-layouts';
import * as React from "react";

class App extends React.Component {
  public leftContent(): JSX.Element {
    return (
      <div>
        <div className="content">
          <h3>PARIS </h3>
          Paris, the city of lights and love - this short guide is full of ideas for how to make the most of the romanticism...
        </div>
      </div>
    );
  }
  public middleContent(): JSX.Element {
    return (
      <div>
        <div className="content">
          <h3>CAMEMBERT </h3>
          The village in the Orne département of Normandy where the famous French cheese is originated from.
        </div>
      </div>
    );
  }
  public rightContent(): JSX.Element {
    return (
      <div>
        <div className="content">
          <h3>GRENOBLE </h3>
          The capital city of the French Alps and a major scientific center surrounded by many ski resorts, host of the Winter Olympics in 1968.
        </div>
      </div>
    );
  }
  public render(): JSX.Element {
    return (<div className="App">
      <SplitterComponent id="percentage" height="250px" width='600px'>
        <PanesDirective>
          <PaneDirective size='200px' content = {this.leftContent} min='20%' max='40%'/>
          <PaneDirective size='200px' content = {this.middleContent} min='30%' max='60%'/>
          <PaneDirective size='200px' content = {this.rightContent} />
        </PanesDirective>
      </SplitterComponent>
  </div>);
  }
}
export default App;

```

{% endtab %}

## Prevent resizing

You can disable the resizing for the pane by setting `false` to
the [resizable](../api/splitter/panePropertiesModel/#resizable) property within paneSettings.

{% tab template="splitter/prevent-resize", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { PaneDirective, PanesDirective, SplitterComponent } from '@syncfusion/ej2-react-layouts';
import * as React from "react";

class App extends React.Component {
  public leftContent(): JSX.Element {
    return (
      <div>
        <div className="content">
          <h3>PARIS </h3>
          Paris, the city of lights and love - this short guide is full of ideas for how to make the most of the romanticism...
        </div>
      </div>
    );
  }
  public middleContent(): JSX.Element {
    return (
      <div>
        <div className="content">
          <h3>CAMEMBERT </h3>
          The village in the Orne département of Normandy where the famous French cheese is originated from.
        </div>
      </div>
    );
  }
  public rightContent(): JSX.Element {
    return (
      <div>
        <div className="content">
          <h3>GRENOBLE </h3>
          The capital city of the French Alps and a major scientific center surrounded by many ski resorts, host of the Winter Olympics in 1968.
        </div>
      </div>
    );
  }
  public render(): JSX.Element {
    return (<div className="App">
      <SplitterComponent id="percentage" height="250px" width='600px'>
      <PanesDirective>
        <PaneDirective size='200px' content = {this.leftContent} resizable={false}/>
        <PaneDirective size='200px' content = {this.middleContent} />
        <PaneDirective size='200px' content = {this.rightContent} />
      </PanesDirective>
      </SplitterComponent>
  </div>);
  }
}
export default App;
```

{% endtab %}

## Refresh content on resizing

While resizing the panes, you can refresh the pane contents by using either [resizeStart](../api/splitter#resizestart),
[resizing](../api/splitter#resizestart) or [resizeStop](../api/splitter#resizestart) events.

## Customize the resize grip and cursor

You can customize the resize gripper icon and cursor in CSS level.

{% tab template="splitter/grip-customization", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { PaneDirective, PanesDirective, SplitterComponent } from '@syncfusion/ej2-react-layouts';
import * as React from "react";

class App extends React.Component {
  public leftContent(): JSX.Element {
    return (
      <div>
        <div className="content">
          <h3>PARIS </h3>
          Paris, the city of lights and love - this short guide is full of ideas for how to make the most of the romanticism...
        </div>
      </div>
    );
  }
  public middleContent(): JSX.Element {
    return (
      <div>
        <div className="content">
          <h3>CAMEMBERT </h3>
          The village in the Orne département of Normandy where the famous French cheese is originated from.
        </div>
      </div>
    );
  }
  public rightContent(): JSX.Element {
    return (
      <div>
        <div className="content">
          <h3>GRENOBLE </h3>
          The capital city of the French Alps and a major scientific center surrounded by many ski resorts, host of the Winter Olympics in 1968.
        </div>
      </div>
    );
  }
  public render(): JSX.Element {
    return (<div className="App">
      <SplitterComponent id="percentage" height="250px" width='600px'>
      <PanesDirective>
        <PaneDirective size='200px' content = {this.leftContent} />
        <PaneDirective size='200px' content = {this.middleContent} />
        <PaneDirective size='200px' content = {this.rightContent}  />
      </PanesDirective>
      </SplitterComponent>
  </div>);
  }
}
export default App;
```

{% endtab %}

## See Also

* [Collapsible panes](expand-collapse)