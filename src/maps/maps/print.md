---
title: " Print And Export in React Maps control | Syncfusion "

component: "Maps"

description: "Learn here all about Print And Export feature of Syncfusion React Maps control and more."
---

# Print and Export in React Maps control

## Print

The rendered Maps can be printed directly from the browser by calling the [`print`](../api/maps/#print) method. To use the print functionality, the **Print** module must be injected into the Maps using **Inject services={[]}** tag and set the [`allowPrint`](../api/maps/#allowprint) property to **true**.

```tsx
<MapsComponent id="maps">
    <Inject services={[Print]}/>
<MapsComponent>
```

{% tab template="maps/default-map", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import { world_map } from 'world-map.ts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { MapsComponent, LayersDirective, LayerDirective, Inject, Print, DataLabel } from '@syncfusion/ej2-react-maps';
class App extends React.Component<{}, {}>{
    private maps: MapsComponent;
    public clickHandler(){
        this.maps.print();
    }
render(){
        return (<div>
        <ButtonComponent value='export' onClick= { this.clickHandler.bind(this)}>print</ButtonComponent>
            <MapsComponent id="maps" allowPrint={true} ref={g => this.maps = g}>
                <Inject services={[DataLabel, Print]} />
                <LayersDirective>
                    <LayerDirective shapeData={world_map}
                     dataLabelSettings={ {
                            visible: true,
                            labelPath: 'name',
                            smartLabelMode: 'Trim'
                        } }>
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent></div>)
        }
};
ReactDOM.render(<App />, document.getElementById('maps'));

```

{% endtab %}

## Export

### Image Export

To use the image export functionality in Maps, **ImageExport** module must be injected into the Maps using **Inject services={[ImageExport]}** tag and set the [`allowImageExport`](../api/maps/#allowimageexport) property to **true**.

```tsx
<MapsComponent id="maps">
    <Inject services={[ImageExport]}/>
<MapsComponent>
```

The rendered Maps can be exported as an image using the [`export`](../api/maps/#export) method. This method requires two parameters: image type and file name. The Maps can be exported as an image in the following formats.

* JPEG
* PNG
* SVG

{% tab template="maps/default-map", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import { world_map } from 'world-map.ts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { MapsComponent, LayersDirective, LayerDirective, DataLabel, Inject, ImageExport } from '@syncfusion/ej2-react-maps';

class App extends React.Component<{}, {}>{
    private maps: MapsComponent;
    public clickHandler(){
        this.maps.export('PNG', 'Maps');
    }
render(){
        return (<div>
        <ButtonComponent value='export' onClick= { this.clickHandler.bind(this)}>Export</ButtonComponent>
            <MapsComponent id="maps" allowImageExport={true} ref={g => this.maps = g}>
                <Inject services={[DataLabel, ImageExport]} />
                <LayersDirective>
                    <LayerDirective shapeData={world_map}
                     dataLabelSettings={ {
                            visible: true,
                            labelPath: 'name',
                            smartLabelMode: 'Trim'
                        } }>
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent></div>)
        }
};
ReactDOM.render(<App />, document.getElementById('maps'));
```

{% endtab %}

### Exporting Maps as base 64 string of the file

The image can be exported as base64 string for the JPEG and PNG formats. The rendered Maps can be exported to image as a base64 string using the [`export`](../api/maps/#export) method. There are four parameters required: image type, file name, orientation of the exported PDF document which must be set as **null** for image export and finally **allowDownload** which should be set as **false** to return base64 string.

{% tab template="maps/default-map", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import { world_map } from 'world-map.ts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { MapsComponent, LayersDirective, LayerDirective, DataLabel, Inject, ImageExport } from '@syncfusion/ej2-react-maps';

class App extends React.Component<{}, {}>{
    private maps: MapsComponent;
    public clickHandler(){
        this.maps.export('PNG', 'Maps', null, false).then((data: string)=>{
            document.getElementById('data').innerHTML = data;
        })
    }
render(){
        return (<div>
        <ButtonComponent value='export' onClick= { this.clickHandler.bind(this)}>Export</ButtonComponent>
            <MapsComponent id="maps" allowImageExport={true} ref={g => this.maps = g}>
                <Inject services={[DataLabel, ImageExport]} />
                <LayersDirective>
                    <LayerDirective shapeData={world_map}
                     dataLabelSettings={ {
                            visible: true,
                            labelPath: 'name',
                            smartLabelMode: 'Trim'
                        } }>
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent><div id="data"></div></div>)
        }
};
ReactDOM.render(<App />, document.getElementById('maps'));
```

{% endtab %}

### PDF Export

To use the PDF export functionality, **PdfExport** module must be injected into the Maps using **Inject services={[PdfExport]}** method and set the [`allowPdfExport`](../api/maps/#allowpdfexport) property to **true**.

```tsx
<MapsComponent id="maps">
    <Inject services={[PdfExport]}/>
<MapsComponent>
```

The rendered Maps can be exported as PDF using the [`export`](../api/maps/#export) method. The [`export`](../api/maps/#export) method requires three parameters: file type, file name and orientation of the PDF document. The orientation setting is optional and **0** indicates portrait and **1** indicates landscape.

{% tab template="maps/default-map", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx

import { world_map } from 'world-map.ts';
import * as React from "react";
import * as ReactDOM from "react-dom";
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { MapsComponent, LayersDirective, LayerDirective, DataLabel, Inject, PdfExport } from '@syncfusion/ej2-react-maps';

class App extends React.Component<{}, {}>{
    private maps: MapsComponent;
    public clickHandler(){
        this.maps.export('PDF', 'Maps');
    }
render(){
        return (<div>
        <ButtonComponent value='export' onClick= { this.clickHandler.bind(this)}>Export</ButtonComponent>
            <MapsComponent id="maps" allowPdfExport={true} ref={g => this.maps = g}>
                <Inject services={[DataLabel, PdfExport]} />
                <LayersDirective>
                    <LayerDirective shapeData={world_map}
                     dataLabelSettings={ {
                            visible: true,
                            labelPath: 'name',
                            smartLabelMode: 'Trim'
                        } }>
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent></div>)
        }
};
ReactDOM.render(<App />, document.getElementById('maps'));
```

{% endtab %}

>The exporting of the Maps as base64 string is not supported for the PDF export.

### Export the tile Maps

The rendered Maps with providers such as OSM, Bing and Google static Maps can be exported using the [`export`](../api/maps/#export) method. It supports the following export formats.

* JPEG
* PNG
* PDF

{% tab template="maps/default-map", compileJsx=true, sourceFiles="app/**/*.tsx" %}

```tsx
import * as React from "react";
import * as ReactDOM from "react-dom";
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { MapsComponent, LayersDirective, LayerDirective, Inject, ImageExport } from '@syncfusion/ej2-react-maps';

class App extends React.Component<{}, {}>{
    private maps: MapsComponent;
    public clickHandler(){
        this.maps.export('PNG', 'Maps');
    }
render() {
        return (<div>
        <ButtonComponent value='export' onClick= { this.clickHandler.bind(this)}>Export</ButtonComponent>
            <MapsComponent id="maps" allowImageExport={true}
                                     ref={g => this.maps = g}
                                     titleSettings={ { text: 'OSM' } }>
                <Inject services={[ImageExport]} />
                <LayersDirective>
                    <LayerDirective layerType='OSM'>
                    </LayerDirective>
                </LayersDirective>
            </MapsComponent></div>)
        }
};
ReactDOM.render(<App />, document.getElementById('maps'));
```

{% endtab %}