---
title: "Pane Sizing"
component: "Splitter"
description: "This section explains about user can feed pane sizes."
---

# Pane sizing

Splitter allows you to provide pane sizes either in pixel or percentage formats.

## Pane size in pixel

{% tab template="splitter/pane-sizes", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { PaneDirective, PanesDirective, SplitterComponent } from '@syncfusion/ej2-react-layouts';
import * as React from "react";

class App extends React.Component {
public render() {
  return (<div className="App">
  <SplitterComponent id="pixel_size" height="250px" width='600px'>
  <PanesDirective>
    <PaneDirective size='200px' content = 'Left pane'/>
    <PaneDirective size='200px' content = 'Middle pane'/>
    <PaneDirective size='200px' content = 'Right pane'/>
  </PanesDirective>
  </SplitterComponent>
</div>);
}
}
export default App;
```

{% endtab %}

## Pane size in percentage

{% tab template="splitter/pane-sizes", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { PaneDirective, PanesDirective, SplitterComponent } from '@syncfusion/ej2-react-layouts';
import * as React from "react";

class App extends React.Component {
public render() {
  return (<div className="App">
  <SplitterComponent id="percentage" height="250px" width='600px'>
  <PanesDirective>
    <PaneDirective size='30%' content = 'Left pane'/>
    <PaneDirective size='40%' content = 'Middle pane'/>
    <PaneDirective size='30%' content = 'Right pane'/>
  </PanesDirective>
  </SplitterComponent>
</div>);
}
}
export default App;
```

{% endtab %}

## Auto size panes

You can render the split panes without providing the size values. It will split up the sizes automatically.

{% tab template="splitter/template", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { PaneDirective, PanesDirective, SplitterComponent } from '@syncfusion/ej2-react-layouts';
import * as React from "react";

class App extends React.Component {
  public leftContent(data: any): JSX.Element {
    return (
      <div>
        <div className="content">
          <h3>Grid </h3>
          The ASP.NET DataGrid control, or DataTable is a feature-rich control used to display data in a tabular format.
        </div>
      </div>
    );
  }
  public middleContent(data: any): JSX.Element {
    return (
      <div>
        <div className="content">
          <h3>Schedule </h3>
          The ASP.NET Scheduler, a.k.a. event calendar, facilitates almost all calendar features, thus allowing users to manage their time efficiently.
        </div>
      </div>
    );
  }
  public rightContent(data: any): JSX.Element {
    return (
      <div>
        <div className="content">
          <h3>Chart </h3>
          ASP.NET charts, a well-crafted easy-to-use charting package, is used to add beautiful charts in web and mobile applications.
        </div>
      </div>
    );
  }
public render() {
  return (<div className="App">
  <SplitterComponent id="plain" height="200px" width='600px'>
  <PanesDirective>
    <PaneDirective content = {this.leftContent}/>
    <PaneDirective content = {this.middleContent}/>
    <PaneDirective content = {this.rightContent}/>
  </PanesDirective>
  </SplitterComponent>
</div>);
}
}
export default App;
```

{% endtab %}

## Fixed pane

You can render the split panes with fixed sizes. Since last pane is a flexible pane, fixed size will not be applied.

{% tab template="splitter/fixed-pane", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { PaneDirective, PanesDirective, SplitterComponent } from '@syncfusion/ej2-react-layouts';
import * as React from "react";

export default class App extends React.Component<{}, {}> {
  public leftContent(data: any): JSX.Element {
    return (
      <div>
        <div className="content">
          <h3>Grid </h3>
          The ASP.NET DataGrid control, or DataTable is a feature-rich control used to display data in a tabular format.
        </div>
      </div>
    );
  }
  public middleContent(data: any): JSX.Element {
    return (
      <div>
        <div className="content">
          <h3>Schedule </h3>
          The ASP.NET Scheduler, a.k.a. event calendar, facilitates almost all calendar features, thus allowing users to manage their time efficiently.
        </div>
      </div>
    );
  }
  public rightContent(data: any): JSX.Element {
    return (
      <div>
        <div className="content">
          <h3>Chart </h3>
          ASP.NET charts, a well-crafted easy-to-use charting package, is used to add beautiful charts in web and mobile applications.
        </div>
      </div>
    );
  }
  public render() {
    return (<div className="App">
      <SplitterComponent id="percentage" height="200px" width='600px'>
      <PanesDirective>
        <PaneDirective size='200px' content = {this.leftContent as any} resizable={false} />
        <PaneDirective size='200px' content = {this.middleContent as any} />
        <PaneDirective size='200px' content = {this.rightContent as any} />
      </PanesDirective>
      </SplitterComponent>
  </div>);
  }
}
```

{% endtab %}
