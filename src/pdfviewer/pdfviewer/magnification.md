---
title: "Magnification"
component: "PDF Viewer"
description: "Learn about the Magnification support in PDF Viewer."
---

# Magnification

The magnification tools of the PDF Viewer contains ZoomIn, ZoomOut, Zoom, FitPage, and FitWidth tools in the
default toolbar. The PDF Viewer also has an option to show or hide the magnification tools in the
default toolbar.

The following code snippet describes how to enable the magnification in PDF Viewer.

{% tab compileJsx=true%}

```tsx

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { PdfViewerComponent, Toolbar, Magnification, Navigation, LinkAnnotation, BookmarkView,
ThumbnailView, Print, TextSelection, TextSearch, Annotation, Inject } from '@syncfusion/ej2-react-pdfviewer';
import { RouteComponentProps } from 'react-router';

export class App extends React.Component<{}, {}> {
  render() {
    return ( <div>
        <div className='control-section'>
            {/* Render the PDF Viewer */}
            <PdfViewerComponent id="container" documentPath="PDF_Succinctly.pdf" enableMagnification={true}
             serviceUrl="https://ej2services.syncfusion.com/production/web-services/api/pdfviewer" style={{ 'height': '640px' }}>
                <Inject services={[Toolbar, Annotation, Magnification, Navigation, LinkAnnotation, BookmarkView, ThumbnailView, Print, TextSelection, TextSearch]} />
            </PdfViewerComponent>
          </div>
        </div>
    );
  }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

The following magnification options are available in the default toolbar of PDF Viewer,

* [**ZoomIn**](https://ej2.syncfusion.com/vue/documentation/api/pdfviewer/magnification/#zoomin):- Zoom in from the current zoom value of PDF pages.
* [**ZoomOut**](https://ej2.syncfusion.com/vue/documentation/api/pdfviewer/magnification/#zoomout):- Zoom out from the current zoom value of PDF pages.
* [**Zoom**](https://ej2.syncfusion.com/vue/documentation/api/pdfviewer/magnification/#zoomto):- Zoom to specific zoom value of PDF pages.
* [**FitPage**](https://ej2.syncfusion.com/vue/documentation/api/pdfviewer/magnification/#fittopage):- Fits the page width with in the available view port size.
* [**FitWidth**](https://ej2.syncfusion.com/vue/documentation/api/pdfviewer/magnification/#fittowidth):- Fits the view port width based on the page content size.

![Alt text ](./images/zoom.png)

>PDF Viewer can support the zoom value ranges from 50 to 400.

## See also

* [Toolbar items](./toolbar)
* [Feature Modules](./feature-module)