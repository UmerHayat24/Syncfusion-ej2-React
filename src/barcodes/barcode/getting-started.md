---
title: " barcode Getting Started | React "

component: "barcode"

description: "Getting started file explains how to configure and install barcode packages and also how to create basic barcode."
---
<!-- markdownlint-disable MD036 -->

# Getting Started

This section explains you the steps required to create a simple barcode and demonstrate the basic usage of the barcode control.

## Dependencies

Below is the list of minimum dependencies required to use the barcode component.

```javascript

|-- @syncfusion/ej2-react-barcodegenerator
    |-- @syncfusion/ej2-base
    |-- @syncfusion/ej2-data
    |-- @syncfusion/ej2-barcodegenerator
    |-- @syncfusion/ej2-react-base
    |-- @syncfusion/ej2-pdf-export
    |-- @syncfusion/ej2-file-utils
    |-- @syncfusion/ej2-compression
    |-- @syncfusion/ej2-svg-base
```

## Installation and configuration

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

```

</div>

* Install Syncfusion packages using below command.

```sh
npm install @syncfusion/ej2-react-barcodegenerator --save
```

## Adding Barcode Generator control

You can start adding Essential JS 2 barcode-generator component to the application. To get started, add the barcode component in `app.ts` and `index.html` files using the following code.

Place the following barcode-generator  code in the `app.ts`.

{% tab template="barcode/getting-started/initialize", compileJsx=true,  isDefaultActive=true%}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
 import { BarcodeGeneratorComponent  } from '@syncfusion/ej2-react-barcode-generator';


ReactDOM.render(
 <BarcodeGeneratorComponent
    id="barcode"
    width={"200px"}
    height={"150px"}
    type='Codabar'
    value='123456789'
    ></BarcodeGeneratorComponent>,
  document.getElementById("barcode")
);
```

{% endtab %}

## Adding QR Generator control

You can add the QR code in our barcode generator component.

{% tab template="barcode/getting-started/qrcode", compileJsx=true,  isDefaultActive=true%}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
 import { QRCodeGeneratorComponent  } from '@syncfusion/ej2-react-barcode-generator';


ReactDOM.render(
 <QRCodeGeneratorComponent
    id="barcode"
    width={"200px"}
    height={"150px"}
    value='Syncfusion'
    ></QRCodeGeneratorComponent>,
  document.getElementById("barcode")
);
```

{% endtab %}

## Adding Datamatrix Generator control

You can add the datamatrix code in our barcode generator component.

{% tab template="barcode/getting-started/dataMatrix", compileJsx=true,  isDefaultActive=true%}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
 import { DataMatrixGeneratorComponent  } from '@syncfusion/ej2-react-barcode-generator';


ReactDOM.render(
 <DataMatrixGeneratorComponent
    id="barcode"
    width={"200px"}
    height={"150px"}
     value='Syncfusion'
    ></DataMatrixGeneratorComponent>,
  document.getElementById("barcode")
);
```

{% endtab %}