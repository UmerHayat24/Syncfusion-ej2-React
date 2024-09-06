---
title: "Expand and Collapse"
component: "Splitter"
description: "This section explains about how to configure collapsible splitter panes, which helps to do expand and collapse action dynamically."
---

# Expand and Collapse

## Collapsible panes

The Splitter panes can be configured with built-in expand and collapse functionalities. By default, the collapsible behavior is disabled. Enable the [collapsible](../api/splitter/panePropertiesModel/#collapsible) behavior in the paneSettings property to show or hide the expand or collapse icons in the panes. You can dynamically expand and collapse the panes by the corresponding icons.

The following code shows how to enable collapsible behavior.

{% tab template="splitter/expand-collapse", sourceFiles="app/App.tsx", compileJsx=true %}

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

  public render(): JSX.Element {
    return (<div className="App">
      <SplitterComponent id="expand-collapse" height="250px" width='600px'>
      <PanesDirective>
        <PaneDirective size='200px' content = {this.firstPaneContent} collapsible={true}/>
        <PaneDirective size='200px' content = {this.secondPaneContent} collapsible={true}/>
        <PaneDirective size='200px' content = {this.thirdPaneContent} collapsible={true}/>
      </PanesDirective>
      </SplitterComponent>
    </div>);
  }
}
export default App;
```

{% endtab %}

## Control the expand and collapse action in programmatic manner

The Splitter provides an option to control the expand and collapse behavior programmatically by using the `expand` and `collapse` methods. Refer to the following code sample.

{% tab template="splitter/expand-collapse-method", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { PaneDirective, PanesDirective, SplitterComponent } from '@syncfusion/ej2-react-layouts';
import * as React from "react";

class App extends React.Component {
  public splitterInstance: SplitterComponent;
  public expandClick(): void {
    this.splitterInstance.expand(0);
  }
  public collapseClick(): void {
    this.splitterInstance.collapse(0);
  }
public render() {
  return (<div className="App">
    <SplitterComponent id="expand-method" height="250px" width='600px' ref={splitter => this.splitterInstance = splitter!}>
    <PanesDirective>
      <PaneDirective size='200px' content = 'Left pane' collapsible={true} />
      <PaneDirective size='200px' content = 'Middle pane' collapsible={true}/>
      <PaneDirective size='200px' content = 'Right pane' collapsible={true}/>
    </PanesDirective>
    </SplitterComponent>
    <div id='btn-container'>
     <button className="e-control e-btn" onClick={this.expandClick=this.expandClick.bind(this)} id="expand"> Expand </button>
     <button className="e-control e-btn"  onClick={this.collapseClick=this.collapseClick.bind(this)} id="collapse"> Collapse </button>
     </div>
</div>);
}
}
export default App;
```

{% endtab %}

## Specify initial state to panes

You can render specific panes with collapsed state on page load. Specify a Boolean value to the [collapsed](../api/splitter/panePropertiesModel/#collapsed) property to control this behavior. The following code explains how to collapse panes on rendering (the second panes renders with collapsed state).

{% tab template="splitter/collapsed", sourceFiles="app/App.tsx", compileJsx=true %}

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
    <PaneDirective size='200px' content = {this.secondPaneContent} collapsed={true}/>
    <PaneDirective size='200px' content = {this.thirdPaneContent}/>
  </PanesDirective>
  </SplitterComponent>
</div>);
}
}
export default App;
```

{% endtab %}

## See Also

* [Resizable split panes](resize)