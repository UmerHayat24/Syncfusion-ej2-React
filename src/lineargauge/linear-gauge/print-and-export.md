---
title: " Print and Export in React Linear Gauge component | Syncfusion "

component: "Linear Gauge"

description: "Learn here all about the Print and Export feature of Syncfusion React Linear Gauge component and more."
---

# Print and Export in React Linear Gauge

## Print

The rendered Linear Gauge can be printed directly from the browser by calling the [`print`](../api/linear-gauge/#print) method. To use the print functionality, set the [`allowPrint`](../api/linear-gauge/#allowprint) property as "**true**" and inject the **Print** module into **services**.

{% tab template="linear-gauge/print-and-export", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { LinearGaugeComponent, Print, Inject } from '@syncfusion/ej2-react-lineargauge';
class App extends React.Component<{}, {}>{
public clickHandler(){
  this.linear.print();
}
private linear: LinearGaugeComponent;
render(){
        return (<div>
        <ButtonComponent value='print' onClick= { this.clickHandler.bind(this)}>print</ButtonComponent>
        <LinearGaugeComponent id='gauge' allowPrint={true}  ref={g => this.linear = g}>
            <Inject services={[Print]} />
        </LinearGaugeComponent></div>)
        }
};
ReactDOM.render(<App />, document.getElementById('gauge'));

```

{% endtab %}

## Export

### Image Export

To use the image export functionality, set the [`allowImageExport`](../api/linear-gauge/#allowimageexport) property as "**true**" and inject the **ImageExport** module into **services**. The rendered Linear Gauge can be exported as an image using the [`export`](../api/linear-gauge/#export) method. This method requires two parameters: export type and file name. The Linear Gauge can be exported as an image with the following formats.

* JPEG
* PNG
* SVG

{% tab template="linear-gauge/print-and-export", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { LinearGaugeComponent, ImageExport, Inject } from '@syncfusion/ej2-react-lineargauge';
class App extends React.Component<{}, {}>{
public clickHandler(){
  this.linear.export('PNG','Gauge');
}
private linear: LinearGaugeComponent;
render(){
        return (<div>
        <ButtonComponent value='export' onClick= { this.clickHandler.bind(this)}>Export</ButtonComponent>
        <LinearGaugeComponent id='gauge' allowImageExport={true} ref={g => this.linear = g}>
            <Inject services={[ImageExport]} />
        </LinearGaugeComponent></div>)
        }
};
ReactDOM.render(<App />, document.getElementById('gauge'));

```

{% endtab %}

### PDF Export

To use the PDF export functionality, set the [`allowPdfExport`](../api/linear-gauge/#allowpdfexport) property as "**true**" and inject the **PdfExport** module into **services**. The rendered Linear Gauge can be exported as PDF using the [`export`](../api/linear-gauge/#export) method. The [`export`](../api/linear-gauge/#export) method requires three parameters: file type, file name, and orientation of the PDF document. The orientation of the PDF document can be set as "**Portrait**" or "**Landscape**".

{% tab template="linear-gauge/print-and-export", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { LinearGaugeComponent, PdfExport, Inject } from '@syncfusion/ej2-react-lineargauge';

class App extends React.Component<{}, {}>{

public clickHandler(){
  this.linear.export('PDF', 'Gauge');
}

private linear: LinearGaugeComponent;

render(){
        return (<div>
        <ButtonComponent value='export' onClick= { this.clickHandler.bind(this)}>print</ButtonComponent>
        <LinearGaugeComponent id='gauge' allowPdfExport={true} ref={g => this.linear = g}>
            <Inject services={[PdfExport]} />
        </LinearGaugeComponent></div>)
        }
};

ReactDOM.render(<App />, document.getElementById('gauge'));

```

{% endtab %}

### Exporting Linear Gauge as base64 string of the file

The Linear Gauge can be exported as base64 string for the JPEG, PNG and PDF formats. The rendered Linear Gauge can be exported as base64 string of the exported image or PDF document used in the [`export`](../api/linear-gauge/#export) method. The arguments that are required for this method is export type, file name, orientation of the exported PDF document and "**allowDownload**" boolean value that is set as "**false**" to return base64 string. The value for the orientation of the exported PDF document is set as "**null**" for image export and "**Portrait**" or "**Landscape**" for the PDF document.

{% tab template="linear-gauge/print-and-export", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import * as React from "react";
import * as ReactDOM from "react-dom";
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { LinearGaugeComponent, ImageExport, Inject } from '@syncfusion/ej2-react-lineargauge';
class App extends React.Component<{}, {}>{
public clickHandler(){
    this.linear.export('PNG', 'Gauge', null, false).then((data: string)=>{
        document.writeln(data);
    })
}
private linear: LinearGaugeComponent;
render(){
        return (<div>
        <ButtonComponent value='export' onClick= { this.clickHandler.bind(this)}>Export</ButtonComponent>
        <LinearGaugeComponent id='gauge' allowImageExport={true} ref={g => this.linear = g}>
            <Inject services={[ImageExport]} />
        </LinearGaugeComponent></div>)
        }
};
ReactDOM.render(<App />, document.getElementById('gauge'));

```

{% endtab %}

>Note: The exporting of the Linear Gauge as base64 string is not applicable for the SVG format.