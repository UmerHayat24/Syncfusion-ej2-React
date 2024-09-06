---
title: "Avatar Getting Started"
component: "Avatar"
description: "React getting started with Avatar, a pure CSS component."
---

# Getting Started

This section explains how to create a simple **Avatar** using Styles in the React Framework

## Dependencies

The Avatar Component is pure CSS component so no specific dependencies to render the avatar.

## Installation and configuration

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

Install the below required dependency package in order to use the `Avatar` component in your application.

```bash
npm install @syncfusion/ej2-layouts --save
```

* The Avatar CSS files are available in the `ej2-layouts` package folder.
This can be referenced in your application using the following code.

`[src/styles/styles.css]`

```css
@import '../../node_modules/@syncfusion/ej2-base/styles/material.css';
@import '../../node_modules/@syncfusion/ej2-layouts/styles/material.css';
```

## Adding a simple Avatar

* Add the HTML `div` element with `e-avatar` class into your `index.html`.

`[src/index.html]`

```html
  <div className="e-avatar">AJ</div>
```

```shell
npm start
```

Output will be as follows:

{% tab template="avatar/getting-started", isDefaultActive=true, sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";

class ReactApp extends React.Component<{}, {}> {
  render() {
       return (
        <div>
            <span className="e-avatar e-avatar-xlarge"></span>
            <span className="e-avatar e-avatar-large"></span>
            <span className="e-avatar"></span>
            <span className="e-avatar e-avatar-small"></span>
            <span className="e-avatar e-avatar-xsmall"></span>
        </div>
       );
  }
}
ReactDOM.render(<ReactApp/>, document.getElementById("element"));
```

{% endtab %}

## See Also

[Types of Avatar](./types)
