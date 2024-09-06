---
title: "Getting Started"
component: "SpreadSheet"
description: "This section helps to learn how to create the Spreadsheet component in React application with its basic features like selection, editing, formatting, importing and exporting to Excel."
---

# Getting Started

This section explains the steps to create a simple Spreadsheet component in a React application.

## Dependencies

The following list of dependencies are required to use the Spreadsheet component in your application:

```js
|-- @syncfusion/ej2-react-spreadsheet
      |-- @syncfusion/ej2-react-base
      |-- @syncfusion/ej2-spreadsheet
      |-- @syncfusion/ej2-base
      |-- @syncfusion/ej2-dropdowns
      |-- @syncfusion/ej2-navigations
      |-- @syncfusion/ej2-grids

```

## Setup for Local Development

You can use [`create-react-app`](https://github.com/facebookincubator/create-react-app) to setup the applications and run the following command to install create-react-app.

```sh
npm install -g create-react-app
```

Run the following command to setup the basic `React` samples.

```sh
create-react-app quickstart --scripts-version=react-scripts-ts

cd quickstart

npm install

```

## Adding Syncfusion packages

All the available Essential JS 2 packages are published in [`npmjs.com`](https://www.npmjs.com/~syncfusionorg) public registry.
To install Spreadsheet component use the following command.

```sh
npm install @syncfusion/ej2-react-spreadsheet --save
```

## Adding CSS reference

 Add components style as given below in `src/App.css`.

```css
@import '../node_modules/@syncfusion/ej2-base/styles/material.css';
@import '../node_modules/@syncfusion/ej2-inputs/styles/material.css';
@import '../node_modules/@syncfusion/ej2-buttons/styles/material.css';
@import '../node_modules/@syncfusion/ej2-splitbuttons/styles/material.css';
@import '../node_modules/@syncfusion/ej2-lists/styles/material.css';
@import '../node_modules/@syncfusion/ej2-navigations/styles/material.css';
@import '../node_modules/@syncfusion/ej2-popups/styles/material.css';
@import '../node_modules/@syncfusion/ej2-dropdowns/styles/material.css';
@import '../node_modules/@syncfusion/ej2-grids/styles/material.css';
@import '../node_modules/@syncfusion/ej2-react-spreadsheet/styles/material.css';
```

> To refer `App.css` in the application then import it in the `src/App.tsx` file.

## Adding Spreadsheet component

Now, you can import the spreadsheet component into your `src/App.tsx` file.

```typescript
import * as React from 'react';
import { SpreadsheetComponent } from '@syncfusion/ej2-react-spreadsheet';
import './App.css';
export default class App extends React.Component {
     render() {
        return  (<SpreadsheetComponent/>);
    }
}
```

## Run the application

The [create-react-app](https://github.com/facebookincubator/create-react-app) will pre-configure the project to compile and run the application in browser. Use the following command to run the application.

```sh

npm start

```

The following example shows a basic spreadsheet component.

{% tab template="spreadsheet/getting-started", sourceFiles="app/**/*.tsx,index.html", iframeHeight="450px", isDefaultActive=true, compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { SpreadsheetComponent } from '@syncfusion/ej2-react-spreadsheet';
export default class App extends React.Component<{}, {}> {
     render() {
        return  (<SpreadsheetComponent/>);
    }
}
ReactDOM.render(<App />, document.getElementById('root'));
```

{% endtab %}

## Note

You can refer to our [React Spreadsheet](https://www.syncfusion.com/react-ui-components/react-spreadsheet) feature tour page for its groundbreaking feature representations. You can also explore our [React Spreadsheet example](https://ej2.syncfusion.com/react/demos/#/material/spreadsheet/default) to knows how to present and manipulate data.

## See Also

* [Data Binding](./data-binding)
* [Open and Save](./open-save)