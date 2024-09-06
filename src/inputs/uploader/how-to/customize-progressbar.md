---
title: "Customize progressbar"
component: "Uploader"
description: "Covers customizable features of the file upload control such as a preview image, invisible upload, progress bar, sort the file list and more."
---

# Customize progressbar

You can customize the progress bar’s size, color, and background by overriding the styles in uploader component. Refer to the following example.

{% tab template="uploader/progress-customize", sourceFiles="app/**/*.tsx,style.css" %}

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
        <div className = 'control-pane' ref={dropAreaEle => this.dropAreaRef = dropAreaEle!}>
            <div className='control-section row uploadpreview'>
            <div className='col-lg-9'>
            <div className='upload_wrapper custom_progress' id="container">
                {/* Render Uploader */}
                <UploaderComponent id='fileUpload' type='file' ref = {upload => {this.uploadObj = upload !}}
                asyncSettings = {this.path} created={this.onCreated = this.onCreated.bind(this)}
                />
            </div>
            </div>
            </div>
        </div>
        )
    }
}

ReactDOM.render(<App />, document.getElementById('fileupload'));
```

{% endtab %}

>You can also explore [React File Upload](https://www.syncfusion.com/react-ui-components/react-file-upload) feature tour page for its groundbreaking features. You can also explore our [React File Upload example](https://ej2.syncfusion.com/react/demos/#/material/uploader/default) to understand how to browse the files which you want to upload to the server.
