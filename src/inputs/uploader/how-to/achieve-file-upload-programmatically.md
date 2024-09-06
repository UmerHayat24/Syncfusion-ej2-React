---
title: "Achieve file upload programmatically"
component: "Uploader"
description: "Covers customizable features of the file upload control such as a preview image, invisible upload, progress bar, sort the file list and more."
---

# Achieve file upload programmatically

You can upload a file programmatically using the [upload](../../api/uploader/#upload) method.
Get the selected files data from the [getFilesData](../../api/uploader/#getfilesdata) public method in uploader.

* If this method receives any files as arguments, those files only start to upload.

{% tab template="uploader/dynamic-upload", sourceFiles="app/**/*.tsx,index.css" %}

```typescript

import { isNullOrUndefined } from '@syncfusion/ej2-base';
import { UploaderComponent } from '@syncfusion/ej2-react-inputs';
import * as React from 'react';
import * as ReactDOM from "react-dom";

export default class App extends React.Component<{}, {}> {
  public uploadObj: UploaderComponent;
  public path: object = {
      removeUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Remove',
      saveUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Save'
  }
  public uploadFirst(): void {
    if(!isNullOrUndefined(this.uploadObj.getFilesData()[0])) {
        this.uploadObj.upload(this.uploadObj.getFilesData()[0]);
    }
  }
  public uploadAll(): void {
    this.uploadObj.upload(this.uploadObj.getFilesData());
  }
  public render(): JSX.Element {
    return (
      <div id='container'>
        <div className="control_wrapper">
            <UploaderComponent autoUpload={false} ref = {upload => {this.uploadObj = upload !}} asyncSettings={this.path} />
        </div>
        <span className="upload-buttons">
            <button id='first' className='e-btn e-control' onClick={this.uploadFirst = this.uploadFirst.bind(this)}>Upload first file</button>
        </span>
        <span className="upload-buttons">
            <button id='full' className='e-btn e-control' onClick={this.uploadAll = this.uploadAll.bind(this)}>Upload all files</button>
        </span>
    </div>);
  }
}

ReactDOM.render(<App />, document.getElementById('fileupload'));
```

{% endtab %}

>You can also explore [React File Upload](https://www.syncfusion.com/react-ui-components/react-file-upload) feature tour page for its groundbreaking features. You can also explore our [React File Upload example](https://ej2.syncfusion.com/react/demos/#/material/uploader/default) to understand how to browse the files which you want to upload to the server.
