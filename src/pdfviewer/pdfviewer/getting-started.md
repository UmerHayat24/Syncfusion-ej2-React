---
title: "Getting Started"
component: "PDF Viewer"
description: "Learn how to get started using React PDF Viewer component through simple steps."
---

# Getting Started

This section explains the steps required to create a simple Essential JS 2 PDF Viewer and demonstrates the basic usage of the PDF Viewer control in a React application.

## Dependencies

The following are the list of minimum dependencies required to use the PDF Viewer.

```javascript
|-- @syncfusion/ej2-react-pdfviewer
|-- @syncfusion/ej2-react-base
    |-- @syncfusion/ej2-pdfviewer
    |-- @syncfusion/ej2-base
    |-- @syncfusion/ej2-buttons
    |-- @syncfusion/ej2-data
    |-- @syncfusion/ej2-dropdowns
    |-- @syncfusion/ej2-inputs
    |-- @syncfusion/ej2-lists
    |-- @syncfusion/ej2-navigations
    |-- @syncfusion/ej2-popups
    |-- @syncfusion/ej2-splitbuttons
    |-- @syncfusion/ej2-notifications
```

## Setup for Local Development

You can use [`create-react-app`](https://github.com/facebookincubator/create-react-app) to setup the applications.
To install `create-react-app` run the following command.

```sh
npm install -g create-react-app
```

* To setup basic `React` sample use following commands.

<div class='tsx'>

```sh
create-react-app quickstart --scripts-version=react-scripts-ts

cd quickstart

npm install

```

</div>

<div class='jsx'>

```sh
create-react-app quickstart

cd quickstart

npm install

```

</div>

## Adding Syncfusion packages

All the available Essential JS 2 packages are published in [`npmjs.com`](https://www.npmjs.com/~syncfusionorg) public registry.
To install PDF Viewer component, use the following command

```sh
npm install @syncfusion/ej2-react-pdfviewer --save
```

## Adding CSS reference

 Add components style as given below in `src/App.css`.

```css
@import '../node_modules/@syncfusion/ej2-base/styles/material.css';  
@import '../node_modules/@syncfusion/ej2-buttons/styles/material.css';  
@import '../node_modules/@syncfusion/ej2-dropdowns/styles/material.css';  
@import '../node_modules/@syncfusion/ej2-inputs/styles/material.css';  
@import '../node_modules/@syncfusion/ej2-navigations/styles/material.css';
@import '../node_modules/@syncfusion/ej2-popups/styles/material.css';
@import '../node_modules/@syncfusion/ej2-splitbuttons/styles/material.css';
@import "../node_modules/@syncfusion/ej2-react-pdfviewer/styles/material.css";
@import "../node_modules/@syncfusion/ej2-notifications/styles/material.css";
```

> To refer `App.css` in the application then import it in the `src/App.tsx` file.

## Adding PDF Viewer component

Now, you can start adding PDF Viewer component in the application. For getting started, add the PDF Viewer component in `src/App.tsx` file
using following code.

Place the following pdfviewer code in the `src/App.tsx`.

{% tab compileJsx=true%}

```tsx

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { PdfViewerComponent, Toolbar, Magnification, Navigation, LinkAnnotation, BookmarkView,
ThumbnailView, Print, TextSelection, Annotation, TextSearch, Inject } from '@syncfusion/ej2-react-pdfviewer';

import './App.css';
class App extends React.Component<{}, {}>{
    render() {
        return    <PdfViewerComponent id="container" documentPath="PDF_Succinctly.pdf" serviceUrl="https://ej2services.syncfusion.com/production/web-services/api/pdfviewer" style={{ 'height': '640px' }}>
                <Inject services={[Toolbar, Magnification, Navigation, Annotation, LinkAnnotation, BookmarkView, ThumbnailView, Print, TextSelection, TextSearch]} />
            </PdfViewerComponent>
    }
};
ReactDOM.render(<App />, document.getElementById('container'));

```

{% endtab %}

> For PDF Viewer serviceUrl creation, follow the steps provided in the [link](https://ej2.syncfusion.com/documentation/pdfviewer/how-to/create-pdfviewer-service/)

## Run the application

The [`create-react-app`](https://github.com/facebookincubator/create-react-app) will pre-configure the project to compile and
run the application in browser. Use the following command to run the application.

```sh

npm start

```

Output will be appears as follows.

{% tab template="pdfviewer/base", isDefaultActive=true, compileJsx=true, es5Template="started" , sourceFiles="index.html,app/index.tsx" %}

```tsx

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { PdfViewerComponent, Toolbar, Magnification, Navigation, LinkAnnotation, BookmarkView,
ThumbnailView, Print, TextSelection, Annotation, TextSearch, Inject } from '@syncfusion/ej2-react-pdfviewer';
import { RouteComponentProps } from 'react-router';

export class App extends React.Component<{}, {}> {
  render() {
    return ( <div>
        <div className='control-section'>
            {/* Render the PDF Viewer */}
            <PdfViewerComponent id="container" documentPath="PDF_Succinctly.pdf" serviceUrl="https://ej2services.syncfusion.com/production/web-services/api/pdfviewer" style={{ 'height': '640px' }}>
                <Inject services={[Toolbar, Magnification, Navigation, Annotation, LinkAnnotation, BookmarkView, ThumbnailView, Print, TextSelection, TextSearch]} />
            </PdfViewerComponent>
          </div>
        </div>
    );
  }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

> You can refer to our [React PDF Viewer](https://www.syncfusion.com/react-ui-components/react-pdf-viewer) feature tour page for its groundbreaking feature representations. You can also explore our [React PDF Viewer example](https://ej2.syncfusion.com/react/demos/#/material/pdfviewer/default) to understand how to explains core features of PDF Viewer.