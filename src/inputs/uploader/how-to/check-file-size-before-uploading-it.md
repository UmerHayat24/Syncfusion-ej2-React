---
title: "Check file size before uploading it"
component: "Uploader"
description: "Covers customizable features of the file upload control such as a preview image, invisible upload, progress bar, sort the file list and more."
---

# Check file size before uploading it

By using the [uploading](../../api/uploader/#uploading) event, you can get the file size before uploading it to the server.
File object contains the file size in bytes only.
You can convert the size to standard formats (`KB` or `MB`) using [bytesToSize](../../api/uploader/#bytestosize) method.

{% tab template="uploader/check-file-size", sourceFiles="app/**/*.tsx,index.css" %}

```typescript
import { UploaderComponent, UploadingEventArgs } from '@syncfusion/ej2-react-inputs';
import * as React from 'react';
import * as ReactDOM from "react-dom";

export default class App extends React.Component<{}, {}> {
  public uploadObj: UploaderComponent;
  public path: object = {
      removeUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Remove',
      saveUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Save'
  }
  public onBeforeUpload(args: UploadingEventArgs): void {
    // get the file size in bytes
    const sizeInBytes: number = args.fileData.size;
    // get the file size in standard format
    alert("File size is: " + this.uploadObj.bytesToSize(sizeInBytes));
  }
  public render(): JSX.Element {
    return (
      <UploaderComponent autoUpload={false} ref = {upload => {this.uploadObj = upload !}} asyncSettings={this.path} uploading={this.onBeforeUpload = this.onBeforeUpload.bind(this)} />
    );
  }
}

ReactDOM.render(<App />, document.getElementById('fileupload'));
```

{% endtab %}

>You can also explore [React File Upload](https://www.syncfusion.com/react-ui-components/react-file-upload) feature tour page for its groundbreaking features. You can also explore our [React File Upload example](https://ej2.syncfusion.com/react/demos/#/material/uploader/default) to understand how to browse the files which you want to upload to the server.
