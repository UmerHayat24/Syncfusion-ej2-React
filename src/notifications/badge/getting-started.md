---
title: "Getting Started For Badge"
component: "Badge"
description: "React getting started with Badge, a pure CSS component."
---

# Getting Started

The following section explains how to create a simple badge component using styles and badge’s basic usage.

## Dependencies

Install the following required dependent package to render the `Badge` component.

```javascript
|-- @syncfusion/ej2-notifications
```

## Set up your development environment

You can use [`Create-react-app`](https://github.com/facebook/create-react-app) to setup the
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

```bash

  create-react-app quickstart

  cd quickstart

```

</div>

Install the below required dependency package in order to use the `Badge` component in your application.

```bash
npm install @syncfusion/ej2-notifications --save
```

* Badge CSS files are available in the `ej2-notifications` package folder.
Import the Badge component's required CSS references as follows in `src/App.css`.

```css
@import "../node_modules/@syncfusion/ej2-base/styles/material.css";
@import "../node_modules/@syncfusion/ej2-notifications/styles/material.css";
```

> We can also use [CRG](https://crg.syncfusion.com/) to generate combined component styles.

## Initialize the Badge Component

Add an HTML span element with `e-badge` class inside any wrapper element (h1) into your return method.

{% tab compileJsx=true %}

```typescript

import * as React from 'react';
import * as ReactDOM from "react-dom";
import './App.css';

class App extends React.Component<{}, {}> {
  render() {
    return (
        <span>Badge Component <span className="e-badge">New</span></span>
    );
  }
}
ReactDOM.render(<App />, document.getElementById("element"));
```

{% endtab %}

* Run the application in the browser using the following command.

```shell
npm start
```

Output will be as follows:

{% tab template="badge/getting-started", isDefaultActive=true, compileJsx=true %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";

class App extends React.Component<{}, {}> {
  render() {
       return (
        <h1>Badge Component <span className="e-badge e-badge-primary">New</span></h1>
       );
  }
}
ReactDOM.render(<App />, document.getElementById("element"));
```

{% endtab %}

## See Also

[Types of Badge](./types)
