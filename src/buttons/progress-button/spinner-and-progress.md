---
title: "ProgressButton Spinner and Progress"
component: "ProgressButton"
description: "React ProgressButton allows the user to change size & position of the spinner, customize spinner using template and to change the progress."
---

<!-- markdownlint-disable MD002 MD022 -->
## Spinner

### Change spinner position

Spinner position can be changed by modifying the [`position`](../api/progress-button/spinSettingsModel#position) property of [`spinSettingsModel`](../api/progress-button/spinSettingsModel). By default, the spinner is positioned at the left of the ProgressButton. You can position it at the `left`, `right`, `top`, `bottom`, or `center` of the text content.

### Change spinner size

Spinner size can be changed by modifying the [`width`](../api/progress-button/spinSettingsModel#width) property of [`spinSettingsModel`](../api/progress-button/spinSettingsModel). In this demo, the `width` is set to `20` to change the spinner size.

### Spinner template

You can use custom spinner by specifying the [`template`](../api/progress-button/spinSettingsModel#template) property of [`spinSettingsModel`](../api/progress-button/spinSettingsModel) with custom styles.

The following sample demonstrates the above functionalities of the spinner.

{% tab template="progress-button/getting-started", sourceFiles="app/**/*.tsx,index.html,spinner.css", isDefaultActive = "true", compileJsx=true %}

```tsx

import { ProgressButtonComponent, SpinSettingsModel } from '@syncfusion/ej2-react-splitbuttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

class App extends React.Component<{}, {}> {

  private spinSettings : SpinSettingsModel = { position: 'Right', width: 20, template: '<div class="template"></div>' };

  public render() {
    return (
      <ProgressButtonComponent content='Submit' spinSettings={this.spinSettings}/>
    );
  }
}
ReactDom.render(<App />, document.getElementById('progress-button'));

```

{% endtab %}

## Progress

### Content animation

The [`content`](../api/progress-button#content) of the ProgressButton can be animated during progress using the [`effect`](../api/progress-button/animationSettingsModel#effect) property of [`animationSettingsModel`](../api/progress-button/animationSettingsModel). You can also set custom duration and timing function using the [`duration`](../api/progress-button/animationSettingsModel#duration) and [`easing`](../api/progress-button/animationSettingsModel#easing) properties. The possible `effect` values are `None`, `SlideLeft`, `SlideRight`, `SlideUp`, `SlideDown`, `ZoomIn`, and `ZoomOut`.

{% tab template="progress-button/getting-started", sourceFiles="app/**/*.tsx,index.html", compileJsx=true %}

```tsx
import { AnimationSettingsModel, ProgressButtonComponent, SpinSettingsModel } from '@syncfusion/ej2-react-splitbuttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

class App extends React.Component<{}, {}> {

  private animationSettings: AnimationSettingsModel = { effect: 'SlideLeft',  duration: 500, easing: 'linear' };
  private spinSettings : SpinSettingsModel = { position: 'Center' };

  public render() {
    return (
      <ProgressButtonComponent content='Slide Left' enableProgress = {true} animationSettings={this.animationSettings} spinSettings={this.spinSettings}/>
    );
  }
}
ReactDom.render(<App />, document.getElementById('progress-button'));

```

{% endtab %}

### Change step of the ProgressButton

The progress can be visualized at the specified interval by changing the [`step`](../api/progress-button/progressEventArgs#step) property in the [`begin`](../api/progress-button#begin) event of the ProgressButton. In this demo, the `step` property is set to `20` to show progress at every 20% increment.

{% tab template="progress-button/getting-started", sourceFiles="app/**/*.tsx,index.html", compileJsx=true %}

```tsx
import { ProgressButtonComponent, ProgressEventArgs } from '@syncfusion/ej2-react-splitbuttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

class App extends React.Component<{}, {}> {

  public begin(args: ProgressEventArgs): void {
      args.step = 20;
  }

  public render() {
    return (
      <ProgressButtonComponent content='Progress Step' enableProgress = {true} begin={this.begin} cssClass='e-hide-spinner'/>
    );
  }
}
ReactDom.render(<App />, document.getElementById('progress-button'));

```

{% endtab %}

> The class `e-hide-spinner` hides the spinner in the ProgressButton, For more information, see [hide spinner](./how-to/hide-spinner) section.

### Change progress dynamically

The progress can be changed dynamically by modifying the [`percent`](../api/progress-button/progressEventArgs#percent) property in the ProgressButton events. In this demo, on 40% completion of progress, the `percent` property is set to `90` to show dynamic change of the progress.

{% tab template="progress-button/getting-started", sourceFiles="app/**/*.tsx,index.html", compileJsx=true %}

```tsx

import { ProgressButtonComponent, ProgressEventArgs } from '@syncfusion/ej2-react-splitbuttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

class App extends React.Component<{}, {content: string}> {
  constructor(props: any) {
    super(props);
    this.state = { content: 'Progress' };
    this.begin = this.begin.bind(this);
    this.progress = this.progress.bind(this);
    this.end = this.end.bind(this);
  }

  public render() {
    return (
      <ProgressButtonComponent content={this.state.content} enableProgress = {true} duration={15000} begin={this.begin} progress={this.progress} end={this.end} cssClass='e-hide-spinner'/>
    );
  }

  private begin(args: ProgressEventArgs): void {
    this.setState({ content: 'Progress ' + args.percent + '%' });
  }

  private progress(args: ProgressEventArgs): void {
    this.setState({ content: 'Progress ' + args.percent + '%' });
    if (args.percent === 40) {
      args.percent = 90;
    }
  }

  private end(args: ProgressEventArgs): void {
    this.setState({ content: 'Progress ' + args.percent + '%' });
  }
}
ReactDom.render(<App />, document.getElementById('progress-button'));
```

{% endtab %}

> The method [`dataBind`](../api/progress-button#databind) applies the property changes immediately to the component.

### Start and stop methods

You can pause and resume the progress using the [`stop`](../api/progress-button#start) and [`start`](../api/progress-button#stop) methods, respectively. In this demo, clicking the ProgressButton will pause and resume the progress.

{% tab template="progress-button/getting-started", sourceFiles="app/**/*.tsx,index.html,icon.css", compileJsx=true %}

```tsx

import { ProgressButtonComponent } from '@syncfusion/ej2-react-splitbuttons';
import * as React from 'react';
import * as ReactDom from 'react-dom';

class App extends React.Component<{}, {content: string, iconCss: string}> {
  private progressBtn: ProgressButtonComponent;
  constructor(props: any) {
    super(props);
    this.state = { content: 'Download', iconCss: 'e-btn-sb-icon e-download' };
    this.end = this.end.bind(this);
    this.clickHandler = this.clickHandler.bind(this);
  }

  public render() {
    return (
      <ProgressButtonComponent content={this.state.content} enableProgress = {true} duration={4000}
      iconCss={this.state.iconCss} end={this.end} cssClass='e-hide-spinner' onClick={this.clickHandler.bind(this)} ref={(scope)=>{this.progressBtn = scope as ProgressButtonComponent;}}/>
    );
  }

  private end(): void {
    this.setState({ content: 'Download', iconCss: 'e-btn-sb-icon e-download' });
  }
  
  private clickHandler(): void {
    if (this.state.content === 'Download') {
      this.setState({ content: 'Pause', iconCss: 'e-btn-sb-icon e-pause' });
    }
    else if (this.state.content === 'Pause') {
      this.setState({ content: 'Resume', iconCss: 'e-btn-sb-icon e-play' });
      this.progressBtn.stop();
    }
    else if (this.state.content === 'Resume') {
      this.setState({ content: 'Pause', iconCss: 'e-btn-sb-icon e-pause' });
      this.progressBtn.start();
    }
  }
}

ReactDom.render(<App />, document.getElementById('progress-button'));

```

{% endtab %}

## See Also

* [How to hide spinner](./how-to/hide-spinner)
* [Customize ProgressButton using cssClass](how-to/customize-progress-using-cssclass)