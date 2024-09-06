---
title: "Trigger click event of input file from external button"
component: "Uploader"
description: "Covers customizable features of the file upload control such as a preview image, invisible upload, progress bar, sort the file list and more."
---

# Trigger click event of input file from external button

Click event of input file from the external button can be triggered using the `click` event of button.
In the following sample, you can find the triggered click event of input file from `Essential JavaScript 2 Button`.

{% tab template="uploader/external-click", sourceFiles="app/**/*.tsx" %}

```typescript
import { select } from '@syncfusion/ej2-base';
import { UploaderComponent } from '@syncfusion/ej2-react-inputs';
import * as React from 'react';
import * as ReactDOM from "react-dom";

export default class App extends React.Component<{}, {}> {
  public uploadObj: UploaderComponent;
  public path: object = {
      removeUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Remove',
      saveUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Save'
  }
  public browseClick(): void {
    const wrapperEle: HTMLElement = select('.e-file-select-wrap button', document) as HTMLElement;
    wrapperEle.click();
  }
  public render(): JSX.Element {
    return (
        <div className="control_wrapper">
            <div id="dropArea">
                <span id="drop"> Drop image (JPG, PNG) files here or <button className='e-btn e-control' id="browse" onClick = {this.browseClick = this.browseClick.bind(this)}>Browse</button></span>
            </div>
            <UploaderComponent ref={uplaod => {this.uploadObj = uplaod !}} asyncSettings={this.path} />
        </div>
    );
  }
}

ReactDOM.render(<App />, document.getElementById('fileupload'));
```

{% endtab %}

>You can also explore [React File Upload](https://www.syncfusion.com/react-ui-components/react-file-upload) feature tour page for its groundbreaking features. You can also explore our [React File Upload example](https://ej2.syncfusion.com/react/demos/#/material/uploader/default) to understand how to browse the files which you want to upload to the server.
