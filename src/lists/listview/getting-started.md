---
title: "ListView Getting Started"
component: "ListView"
description: "Getting started with ListView component."
---

# Getting Started

The following section explains the required steps to build the simple ListView component with its basic usage in step by step procedure.

## Dependencies

Install the below required dependent packages to render the ListView component.

```javascript
+-- @syncfusion/ej2-react-lists
    |-- @syncfusion/ej2-react-base
    |-- @syncfusion/ej2-lists
        |-- @syncfusion/ej2-base
        |-- @syncfusion/ej2-data
```

## Installation and Configuration

You can use [`create-react-app`](https://github.com/facebookincubator/create-react-app) to setup the
applications.

To install `create-react-app` run the following command.

```bash
npm install -g create-react-app
```

Start a new project using `create-react-app` command as follows

<div class='tsx'>

```bash

create-react-app quickstart --typescript

cd quickstart

```

</div>

<div class='jsx'>

```sh

create-react-app quickstart

cd quickstart

```

</div>

## Adding Syncfusion packages

All the available Essential JS 2 packages are published in
[`npmjs.com`](https://www.npmjs.com/~syncfusionorg) public registry. Now, we are going to render
`ListView` component from these packages.

To install `ListView` component, use the following command.

```bash
npm install @syncfusion/ej2-react-lists --save
```

The above command installs [ListView dependencies](#dependencies)
which are required to render the component in the `React` environment.

## Adding ListView component

Now, you can add `ListView` component in the application.
For getting started, add `ListView` component in `src/App.tsx` file using the following code snippet.

{% tab compileJsx=true%}

```typescript

import * as React from 'react';
import { ListViewComponent } from '@syncfusion/ej2-react-lists';
import './App.css';

export default class App extends React.Component<{}, {}> {
  render() {
    return (
      //specifies the tag to render the ListView component
      <ListViewComponent id='list' />
    );
  }
}

```

{% endtab %}

## Adding CSS Reference

Import `ListView` component required theme references at the top of `src/App.css`.

```css

/* import the ListView dependency styles */

@import "../node_modules/@syncfusion/ej2-base/styles/material.css";
@import "../node_modules/@syncfusion/ej2-react-lists/styles/material.css";

```

* If you are using `CheckList` behavior in ListView, we need to add `Button` component's styles as given below in `src/App.css` file

```css
@import "../node_modules/@syncfusion/ej2-buttons/styles/material.css";
```

## Bind dataSource

Populate the data in ListView using `dataSource` property. Here, an array of JSON values passed to
`ListView` component.

{% tab compileJsx=true%}

```typescript

import * as React from 'react';
import { ListViewComponent } from '@syncfusion/ej2-react-lists';
import './App.css';

export default class App extends React.Component<{}, {}> {
  // define the array of Json
  private arts: { [key: string]: string }[] = [
    { text: 'Artwork', id: '01' },
    { text: 'Abstract', id: '02' },
    { text: 'Modern Painting', id: '03' },
    { text: 'Ceramics', id: '04' },
    { text: 'Animation Art', id: '05' },
    { text: 'Oil Painting', id: '06' }];
  render() {
    return (
      // specifies the tag to render the ListView component
      <ListViewComponent id="list" dataSource={this.arts} />
    );
  }
}


```

{% endtab %}

## Running the application

Now use the `npm start` command to run the application in the browser.

```cmd
npm start
```

{% tab template="listview/getting-started", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```typescript

import * as React from 'react';
import * as ReactDOM from "react-dom";
import { ListViewComponent } from '@syncfusion/ej2-react-lists';

export default class App extends React.Component<{}, {}> {
  // define the array of Json
  private arts: { [key: string]: string }[] = [
    { text: 'Artwork', id: '01' },
    { text: 'Abstract', id: '02' },
    { text: 'Modern Painting', id: '03' },
    { text: 'Ceramics', id: '04' },
    { text: 'Animation Art', id: '05' },
    { text: 'Oil Painting', id: '06' }];
  render() {
    return (
      // specifies the tag to render the ListView component
      <ListViewComponent id='list' dataSource={this.arts} ></ListViewComponent>
    );
  }
}

ReactDOM.render(<App />, document.getElementById('element'));
```

{% endtab %}

## See Also

[Data Binding Types](./data-binding)

[ListView customization](./customizing-templates)

[Virtualization](./virtualization)
