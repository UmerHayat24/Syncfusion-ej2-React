---
title: "Hide default drop area"
component: "Uploader"
description: "Covers customizable features of the file upload control such as a preview image, invisible upload, progress bar, sort the file list and more."
---

# Hide default drop area

You can achieve this behavior by overriding the corresponding uploader styles. Override the following styles to hide the default drop area behavior.

    * .e-upload.e-control
    * .e-upload .e-file-select
    * .e-upload .e-file-drop

{% tab template="uploader/hide-drop", sourceFiles="app/**/*.tsx,style.css" %}

```typescript
import * as React from 'react';
import * as ReactDOM from "react-dom";
import { UploaderComponent } from '@syncfusion/ej2-react-inputs';

export default class App extends React.Component<{}, {}> {
// Uploader component
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
        <div className = 'control-pane'>
            <div className='control-section row uploadpreview'  ref={dropAreaEle => this.dropAreaRef = dropAreaEle!}>
            <div className='col-lg-9'>
            <div className='upload_wrapper'>
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
