---
title: "Check the MIME type of file before upload it"
component: "Uploader"
description: "Covers customizable features of the file upload control such as a preview image, invisible upload, progress bar, sort the file list and more."
---

# Check the MIME type of file before upload it

By using the [uploading](../../api/uploader/#uploading) event, you can get the file MIME type before uploading it to the server.
In the following sample, file MIME type is shown in the alert box before the file starts to upload.

{% tab template="uploader/mime-type", sourceFiles="app/**/*.tsx" %}

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
    // get the file MIME type
    alert("File MIME type is: " + (args.fileData.rawFile as Blob).type);
  }
  public render() {
    return (
     <UploaderComponent autoUpload={false} ref = {upload => {this.uploadObj = upload !}} asyncSettings={this.path} uploading={this.onBeforeUpload = this.onBeforeUpload.bind(this)} />
    );
  }
}

ReactDOM.render(<App />, document.getElementById('fileupload'));
```

{% endtab %}

>You can also explore [React File Upload](https://www.syncfusion.com/react-ui-components/react-file-upload) feature tour page for its groundbreaking features. You can also explore our [React File Upload example](https://ej2.syncfusion.com/react/demos/#/material/uploader/default) to understand how to browse the files which you want to upload to the server.
