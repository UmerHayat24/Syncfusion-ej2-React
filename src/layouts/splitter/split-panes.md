---
title: "Split Panes"
component: "Splitter"
description: "This section explain about split panes behaviors."
---

# Split Panes

This section explain about split panes behaviors.

## Horizontal layout

By default, splitter will render in horizontal orientation. Splitter container will be split as panes in horizontal flow direction with vertical separator.

{% tab template="splitter/horizontal", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { PaneDirective, PanesDirective, SplitterComponent } from '@syncfusion/ej2-react-layouts';
import * as React from "react";

class App extends React.Component {
  public leftContent(): JSX.Element {
    return (
      <div>
        <div className="content">
          <h3>Grid </h3>
          The ASP.NET DataGrid control, or DataTable is a feature-rich control used to display data in a tabular format.
        </div>
      </div>
    );
  }
  public middleContent(): JSX.Element {
    return (
      <div>
        <div className="content">
          <h3>Schedule </h3>
          The ASP.NET Scheduler, a.k.a. event calendar, facilitates almost all calendar features, thus allowing users to manage their time efficiently.
        </div>
      </div>
    );
  }
  public rightContent(): JSX.Element {
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
      <SplitterComponent id="horizontal" height="250px" width='600px'>
      <PanesDirective>
        <PaneDirective size='200px' content = {this.leftContent}/>
        <PaneDirective size='200px' content = {this.middleContent}/>
        <PaneDirective size='200px' content = {this.rightContent}/>
      </PanesDirective>
      </SplitterComponent>
  </div>);
  }
}
export default App;
```

{% endtab %}

## Vertical layout

By setting [orientation](../api/splitter/#orientation) property as `Vertical`, splitter will render in vertical orientation. Splitter container will be split as panes in vertical flow direction with horizontal separator.

{% tab template="splitter/vertical", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { PaneDirective, PanesDirective, SplitterComponent } from '@syncfusion/ej2-react-layouts';
import * as React from "react";

class App extends React.Component {
  public leftContent(): JSX.Element {
    return (
      <div>
        <div className="content">
          <h3>Grid </h3>
          The ASP.NET DataGrid control, or DataTable is a feature-rich control used to display data in a tabular format.
        </div>
      </div>
    );
  }
  public middleContent(): JSX.Element {
    return (
      <div>
        <div className="content">
          <h3>Schedule </h3>
          The ASP.NET Scheduler, a.k.a. event calendar, facilitates almost all calendar features, thus allowing users to manage their time efficiently.
        </div>
      </div>
    );
  }
  public rightContent(): JSX.Element {
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
      <SplitterComponent id="vertical" height="300px" width='600px' orientation='Vertical'>
      <PanesDirective>
        <PaneDirective size='100px' content = {this.leftContent}/>
        <PaneDirective size='100px' content = {this.middleContent}/>
        <PaneDirective size='100px' content = {this.rightContent}/>
      </PanesDirective>
      </SplitterComponent>
  </div>);
  }
}
export default App;
```

{% endtab %}

## Multiple panes

You can render the multiple panes with both `Horizontal` and `Vertical` orientations.

{% tab template="splitter/multiple", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { PaneDirective, PanesDirective, SplitterComponent } from '@syncfusion/ej2-react-layouts';
import * as React from "react";

class App extends React.Component {
  public pane1Content(): JSX.Element {
    return (
      <div>
        <div className="content">
          <h3>PARIS </h3>
          Paris, the city of lights and love - this short guide is full of ideas for how to make the most of the romanticism...
        </div>
      </div>
    );
  }
  public pane2Content(): JSX.Element {
    return (
      <div>
        <div className="content">
          <h3>CAMEMBERT </h3>
          The village in the Orne département of Normandy where the famous French cheese is originated from.
        </div>
      </div>
    );
  }
  public pane3Content(): JSX.Element {
    return (
      <div>
        <div className="content">
          <h3>GRENOBLE </h3>
          The capital city of the French Alps and a major scientific center surrounded by many ski resorts, host of the Winter Olympics in 1968.
        </div>
      </div>
    );
  }
  public pane4Content(): JSX.Element {
    return (
      <div>
        <div className="content">
          <h3>AUSTRALIA </h3>
           Australia is a country and continent surrounded by the Indian and Pacific oceans. Its major cities – Sydney, Brisbane, Melbourne, Perth, Adelaide – are coastal. Its capital, Canberra, is inland.
        </div>
      </div>
    );
  }
  public render() {
    return (<div className="App">
      <SplitterComponent id="multiple" height="250px" width='600px'>
      <PanesDirective>
        <PaneDirective size='150px' content = {this.pane1Content}/>
        <PaneDirective size='150px' content = {this.pane2Content}/>
        <PaneDirective size='150px' content = {this.pane3Content}/>
        <PaneDirective size='150px' content = {this.pane4Content}/>
      </PanesDirective>
      </SplitterComponent>
  </div>);
  }
}
export default App;
```

{% endtab %}

## Separator

By default, pane separator will be render with `1px` width/height. You can customize the separator size by using [separatorSize](../api/splitter/#separatorsize) property.

> For Horizontal orientation, it will be considered as separator width.
> For Vertical orientation, it will be considered as separator height.

{% tab template="splitter/separator", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { PaneDirective, PanesDirective, SplitterComponent } from '@syncfusion/ej2-react-layouts';
import * as React from "react";

class App extends React.Component {
  public leftContent(): JSX.Element {
    return (
      <div>
        <div className="content">
          <h3>Grid </h3>
          The ASP.NET DataGrid control, or DataTable is a feature-rich control used to display data in a tabular format.
        </div>
      </div>
    );
  }
  public middleContent(): JSX.Element {
    return (
      <div>
        <div className="content">
          <h3>Schedule </h3>
          The ASP.NET Scheduler, a.k.a. event calendar, facilitates almost all calendar features, thus allowing users to manage their time efficiently.
        </div>
      </div>
    );
  }
  public rightContent(): JSX.Element {
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
      <SplitterComponent id="separator" height="250px" width='600px' separatorSize={5}>
      <PanesDirective>
        <PaneDirective size='200px' content = {this.leftContent as any}/>
        <PaneDirective size='200px' content = {this.middleContent as any}/>
        <PaneDirective size='200px' content = {this.rightContent as any}/>
      </PanesDirective>
      </SplitterComponent>
  </div>);
  }
}
export default App;
```

{% endtab %}

## Nested Splitter

Splitter provides support to render the nested pane to achieve the complex layouts. You can use the same `<div>` element for splitter pane and nested splitter.

> Also you can render the nested splitter using direct child of the splitter pane. For this, nested splitter should have `100%` width and height to match with the parent pane dimensions.

{% tab template="splitter/nested", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { PaneDirective, PanesDirective, SplitterComponent } from '@syncfusion/ej2-react-layouts';
import * as React from "react";

class App extends React.Component {
  private innerSplitterInstance: any;
  private splitterInstance: any;
  public leftPaneContent(): JSX.Element {
    return (
      <div>
          <div className="content">
              <a href="https://www.syncfusion.com/ebooks/neuralnetworks" target="_blank">Neural Networks Using C# Succinctly</a>
              <p>Neural networks are an exciting field of software development used to calculate outputs from input data.
              While the idea seems simple enough, the implications of such networks are staggering—think optical character recognition,
              speech recognition, and regression analysis. With Neural Networks Using C# Succinctly by James McCaffrey, you’ll learn
              how to create your own neural network to solve classification problems, or problems where the outcomes can only be one of
              several values. <br/><br/>Learn about encoding and normalizing data, activation functions and how to choose the right one, and ultimately
              how to train a neural network to find weights and bias values that provide accurate predictions.
              An artificial neural network (sometimes abbreviated ANN, or shortened to just "neural network" when the context is clear) is
              a software system that loosely models biological neurons and synapses. Before explaining exactly how neural networks work, it is
              useful to understand what types of problems they can solve.
          </p>
          </div>
      </div>
    );
  }

  public rightPaneContent1(): JSX.Element {
    return (
      <div>
      <div className="content">
      <a href = "https://www.syncfusion.com/ebooks/data_capture_and_extraction_with_c_sharp_succinctly" target = "_blank" > Data Capture and Extraction with C# Succinctly </a>
      <p>Capturing and extracting information is one of the most important tasks a developer can perform, and making this task more
        engaging without relying entirely on specialized tools is an efficient way to improve productivity.
        In Data Capture and Extraction with C# Succinctly, author Ed Freitas guides readers toward getting more out of C# in minimal time.
        Email has become a pillar of our modern and connected society, and it now serves as a primary means of communication. Because each email
        is filled with valuable information, data extraction has emerged as a worthwhile skill set for developers in today’s business world.
      </p>
      </div >
      </div>
    );
  }

  public rightPaneContent2(): JSX.Element {
    return (
      <div>
        <div className="content">
          <a href="https://www.syncfusion.com/ebooks/spark" target="_blank">Spark Succinctly</a>
          <p>Mastering big data requires an aptitude at every step of information processing.
              Post-processing, one of the most important steps, is where you find Apache Spark frequently employed.
              Spark Succinctly, by Marko Svaljek, addresses Spark’s use in the ultimate step in handling big data. This e-book, the
              third installment in Svaljek’s IoT series, teaches the basics of using Spark and explores how to work with RDDs, Scala and
              Python tasks, JSON files, and Cassandra.Many of the leading companies in the world today face the problem of big data.
          </p>
       </div>
      </div>
    );
  }

  public onCreate(): void {
      // Initialize Splitter component
      const cont = this.innerSplitterInstance.element.querySelectorAll(".e-pane")[1];
      cont.appendChild(this.splitterInstance.element);
  }

  public render(): JSX.Element {
      return (
          <div id="target" className="control-section splitter-expand" >
          <SplitterComponent id="splitter1" separatorSize={3}  height="350px" width="100%" ref={(splitter) => { this.innerSplitterInstance = splitter! }}>
          <PanesDirective>
              <PaneDirective size='48%' content={this.leftPaneContent} />
              <PaneDirective />
          </PanesDirective>
          </SplitterComponent>
          <SplitterComponent id="splitter2" separatorSize={3} orientation="Vertical"  ref={(splitter) => { this.splitterInstance = splitter; }} created={this.onCreate = this.onCreate.bind(this)}>
            <PanesDirective>
                <PaneDirective size='50%' content={this.rightPaneContent1} />
                <PaneDirective content = {this.rightPaneContent2} />
            </PanesDirective>
          </SplitterComponent>
          </div>
      );
  }
}
export default App;
```

{% endtab %}

## Add or remove pane

You can add or remove panes programmatically to the splitter. By using [addPane](../api/splitter#addpane) and [removePane](../api/splitter#removepane) methods.

### Add pane

You can add the panes dynamically in the splitter by passing
[pane properties](https://ej2.syncfusion.com/documentation/api/splitter/panePropertiesModel/) along with index to the addPane method.

{% tab template="splitter/add-pane", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { PaneDirective, PanePropertiesModel, PanesDirective, SplitterComponent } from '@syncfusion/ej2-react-layouts';
import * as React from "react";

class App extends React.Component {
  public splitterInstance: SplitterComponent;
  public paneDetails: PanePropertiesModel = {
    content: 'New Pane',
    max: '250px',
    min: '30px',
    size: '150px',
  }
  public firstPane(): JSX.Element {
    return (
      <div>
        <div className="content">Pane1</div>
      </div>
    );
  }

  public secondPane(): JSX.Element {
    return (
      <div>
        <div className="content">Pane2</div>
      </div>
    );
  }

  public btnClick(): void {
    if ((this.splitterInstance as any).allPanes.length > 1) {
      this.splitterInstance.addPane(this.paneDetails, 1);
    }
  }
  public render() {
    return (<div className="App">
      <SplitterComponent id="separator" height="200px" width='580px' ref={(splitter) => { this.splitterInstance = splitter! }}>
      <PanesDirective>
        <PaneDirective size='200px' content = {this.firstPane}/>
        <PaneDirective size='200px' content = {this.secondPane}/>
      </PanesDirective>
      </SplitterComponent>
      <div id='addButton'>
          <button className='e-control e-btn' onClick={this.btnClick = this.btnClick.bind(this) }>Add Pane</button>
        </div>
  </div>);
  }
}
export default App;
```

{% endtab %}

### Remove pane

You can remove the split panes dynamically by passing the pane index to [removePane](../api/splitter#removepane) method.

{% tab template="splitter/remove-pane", sourceFiles="app/App.tsx", compileJsx=true %}

```typescript
import { PaneDirective, PanesDirective, SplitterComponent } from '@syncfusion/ej2-react-layouts';
import * as React from "react";

class App extends React.Component {
  public splitterInstance: SplitterComponent;
  public firstPane(): JSX.Element {
    return (
      <div>
        <div className="content">Pane1</div>
      </div>
    );
  }

  public secondPane(): JSX.Element {
    return (
      <div>
        <div className="content">Pane2</div>
      </div>
    );
  }

  public thirdPane(): JSX.Element {
    return (
      <div>
        <div className="content">Pane3</div>
      </div>
    );
  }

  public btnClick(): void {
    if ((this.splitterInstance as any).allPanes.length > 1) {
        this.splitterInstance.removePane(1);
    }
  }
  public render() {
    return (
      <div className="App">
        <SplitterComponent id="separator" height="200px" width='600px' ref={(splitter) => { this.splitterInstance = splitter! }}>
          <PanesDirective>
            <PaneDirective size='200px' content = {this.firstPane}/>
            <PaneDirective size='200px' content = {this.secondPane}/>
            <PaneDirective size='200px' content = {this.thirdPane}/>
          </PanesDirective>
        </SplitterComponent>
        <div id='removeButton'>
          <button className='e-control e-btn' onClick={this.btnClick = this.btnClick.bind(this) }>Remove Pane</button>
        </div>
      </div>
    );
  }
}
export default App;
```

{% endtab %}

## See Also

* [Resizable split panes](resize)
* [Collapsible panes](expand-collapse)
* [Define size to a panes](pane-sizing)
* [Specify content to a panes](pane-content)