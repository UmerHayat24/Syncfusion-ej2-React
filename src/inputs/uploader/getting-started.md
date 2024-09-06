---
title: "Getting Started"
component: "Uploader"
description: "Explains to get started with HTML5 file upload control with its key features such as asynchronous mode, handle success, fail action, etc."
---

# Getting Started

This section explains how to create and configure the simple
uploader component with its basic usage in step by step procedure.

## Dependencies

The following are the dependencies required to use the uploader component in your application:

```javascript
|-- @syncfusion/ej2-react-inputs
    |-- @syncfusion/ej2-react-base
    |-- @syncfusion/ej2-inputs
    |-- @syncfusion/ej2-base
    |-- @syncfusion/ej2-buttons

```

## Installation and Configuration

You can use [Create-react-app](https://github.com/facebookincubator/create-react-app) to setup the applications.
To install `create-react-app` run the following command.

```bash
npm install -g create-react-app
```

Start a new project using create-react-app command as follows

```bash

create-react-app quickstart --scripts-version=react-scripts-ts

cd quickstart

```

## Adding Syncfusion Packages

All the available Essential JS 2 packages are published in [npmjs.com](https://www.npmjs.com/~syncfusionorg) public registry.

To install uploader component, use the following command

```bash
npm install @syncfusion/ej2-react-inputs --save
```

## Adding CSS Reference

Import the uploader component's required CSS references as follows in `src/App.css`.

```css
@import "../node_modules/@syncfusion/ej2-base/styles/material.css";
@import "../node_modules/@syncfusion/ej2-buttons/styles/material.css";
@import "../node_modules/@syncfusion/ej2-react-inputs/styles/material.css";
```

> The [Custom Resource Generator (CRG)](https://crg.syncfusion.com/) is an online web tool, which can be used to generate the custom script and styles for a set of specific components.
> This web tool is useful to combine the required component scripts and styles in a single file.

## Adding uploader to the application

Now, you can start adding uploader component to the application. We have added uploader component in `src/App.tsx`
file using following code.

```typescript

// import uploader component
import { UploaderComponent } from '@syncfusion/ej2-react-inputs';
import * as React from 'react';
import './App.css';

export default class App extends React.Component<{}, {}> {
    public render() {
        return <UploaderComponent id="uploader" />;
    }
}

```

> From v16.2.41 version, the `Essential JS2 AJAX` library has been integrated for uploader server requests.
Hence, use the third party `promise` library like blue-bird to use the uploader in Internet Explorer.

## Run the application

After completing the configuration to render the basic uploader, run the following command to display the output in your default browser.

```cmd
npm run start
```

> From v16.2.41 version, the `Essential JS2 AJAX` library has been integrated for uploader server requests.
Hence, use the third party `promise` library like blue-bird to use the uploader in Internet Explorer.

The following code example illustrates the output in your browser.

{% tab template="uploader/basic", isDefaultActive="true", sourceFiles="app/**/*.tsx" %}

```typescript

import { UploaderComponent } from '@syncfusion/ej2-react-inputs';
import * as React from 'react';
import * as ReactDOM from "react-dom";

export default class App extends React.Component<{}, {}> {
public render(){
    return (
      <UploaderComponent />
    );
  }
}

ReactDOM.render(<App />, document.getElementById('fileupload'));
```

{% endtab %}

## Adding drop area

By default, the uploader component allows to upload files by drag the files from file explorer
and drop into the drop area.  You can configure any other external element as drop target
using **dropArea** property.

In the following sample, drop target is configured.

{% tab template="uploader/drop-area", sourceFiles="app/**/*.tsx,style.css" %}

```typescript

import { UploaderComponent } from '@syncfusion/ej2-react-inputs';
import * as React from 'react';
import * as ReactDOM from "react-dom";

export default class App extends React.Component<{}, {}> {
  public uploadObj: UploaderComponent;
  public path: object = {
    removeUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Remove',
    saveUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Save'
  }
  private dropAreaRef: HTMLElement;

  public onCreated(): void {
    this.uploadObj.dropArea = this.dropAreaRef;
    this.uploadObj.dataBind();
  }
public render(): JSX.Element {
    return (
      <div id='container'>
        <div id='droparea' ref={dropAreaEle => this.dropAreaRef = dropAreaEle!}>
            Drop files here to upload
        </div>
        <div id='uploadfile' >
            <UploaderComponent autoUpload={false}  ref = { upload => this.uploadObj = upload !} asyncSettings={this.path} created={this.onCreated = this.onCreated.bind(this)} />
        </div>
      </div>
    );
    }
}

ReactDOM.render(<App />, document.getElementById('fileupload'));
```

{% endtab %}

## Configure asynchronous settings

The uploader component processes the files to upload in Asynchronous mode by default.
Define the properties **saveUrl** and **removeUrl** to handle the save and remove
action as follows.

{% tab template="uploader/basic", sourceFiles="app/**/*.tsx" %}

```typescript

import { UploaderComponent } from '@syncfusion/ej2-react-inputs';
import * as React from 'react';
import * as ReactDOM from "react-dom";

export default class App extends React.Component<{}, {}> {
  public path: object = {
    removeUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Remove',
    saveUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Save'
}
  public render(): JSX.Element {
    return (
      <UploaderComponent autoUpload={false} asyncSettings={this.path} />
    );
  }
}

ReactDOM.render(<App />, document.getElementById('fileupload'));
```

{% endtab %}

## Handle success and failed upload

You can handle the success and failure actions using the **success** and **failure** events.
To handle these event, define the function and assign it to corresponding event as shown below.

{% tab template="uploader/basic", sourceFiles="app/**/*.tsx" %}

```typescript

import { UploaderComponent } from '@syncfusion/ej2-react-inputs';
import * as React from 'react';
import * as ReactDOM from "react-dom";

export default class App extends React.Component<{}, {}> {
  public path: object = {
    removeUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Remove',
    saveUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Save'
  }
  public onUploadSuccess(args: any): void  {
    if (args.operation === 'upload') {
      // window.console.log('File uploaded successfully');
    }
  }
  public onUploadFailure(args: any): void  {
    // window.console.log('File failed to upload');
  }
  public render(): JSX.Element {
    return (
      <UploaderComponent autoUpload={false} asyncSettings={this.path}
      success={this.onUploadSuccess=this.onUploadSuccess.bind(this)} failure={this.onUploadFailure=this.onUploadFailure.bind(this)}/>
    );
  }
}

ReactDOM.render(<App />, document.getElementById('fileupload'));
```

{% endtab %}

>You can also explore [React File Upload](https://www.syncfusion.com/react-ui-components/react-file-upload) feature tour page for its groundbreaking features. You can also explore our [React File Upload example](https://ej2.syncfusion.com/react/demos/#/material/uploader/default) to understand how to browse the files which you want to upload to the server.

## See Also

* [How to add additional data on upload](./how-to/add-additional-data-on-upload)
* [Achieve file upload programmatically](./how-to/achieve-file-upload-programmatically)
* [Achieve invisible upload](./how-to/achieve-invisible-upload)

> You can also explore [React File Upload](https://www.syncfusion.com/react-ui-components/react-file-upload) feature tour page for its groundbreaking features. You can also explore our [React File Upload example](https://ej2.syncfusion.com/react/demos/#/material/uploader/default) that shows how to render the file upload and browse the files which you want to upload to the server.