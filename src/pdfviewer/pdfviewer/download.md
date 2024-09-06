---
title: "Download"
component: "PDF Viewer"
description: "Learn about download option in PDF Viewer to download the loaded document."
---
# Download

The PDF Viewer supports downloading the loaded PDF file. You can enable/disable the download using the following code snippet.

![Alt text](./images/download.png)

You can invoke download action using following code snippet.,

{% tab compileJsx=true%}

```tsx

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { PdfViewerComponent, Toolbar, Magnification, Navigation, LinkAnnotation, BookmarkView,
ThumbnailView, Print, TextSelection, Annotation, TextSearch, Inject } from '@syncfusion/ej2-react-pdfviewer';
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { RouteComponentProps } from 'react-router';

export class App extends React.Component<{}, {}> {
  public viewer: PdfViewerComponent;
  render() {
    return ( <div>
        <div className='control-section'>
            {/* Render the PDF Viewer */}
            <ButtonComponent id="downloadBtn" onClick={this.downloadClicked.bind(this)}>Download</ButtonComponent>
            <PdfViewerComponent ref={(scope) => { this.viewer = scope; }}  id="container" documentPath="PDF_Succinctly.pdf" serviceUrl="https://ej2services.syncfusion.com/production/web-services/api/pdfviewer" style={{ 'height': '640px' }}>
                <Inject services={[Toolbar, Magnification, Navigation, LinkAnnotation, Annotation, BookmarkView, ThumbnailView, Print, TextSelection, TextSearch]} />
            </PdfViewerComponent>
          </div>
        </div>
    );
  }
  downloadClicked() {
      this.viewer.download();
  }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

## See also

* [Toolbar items](./toolbar)
* [Feature Modules](./feature-module)