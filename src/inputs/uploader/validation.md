---
title: "Validation"
component: "Uploader"
description: "Explains how to validate files before uploading it to a server such as valid file extensions, min and max file size, and duplicate files."
---

# Validation

The uploader component validate the selected files size and extension using the
**allowedExtensions**, **minFileSize** and **maxFileSize** properties.
The files can be validated before uploading to the server and can be ignored on uploading.
Also, you can validate the files by setting the HTML attributes to the original input element.
The validation process occurs on drag-and-drop the files also.

## File type

You can allow the specific files alone to upload using the **allowedExtensions**
property. The extension can be represented as collection by comma separators.
The uploader component filters the selected or dropped files to match against the specified file types and
processes the upload operation. The validation happens when you specify value to inline attribute to accept
the original input element.

{% tab template="uploader/basic", sourceFiles="app/**/*.tsx" %}

```typescript

import { UploaderComponent } from '@syncfusion/ej2-react-inputs';
import * as React from 'react';
import * as ReactDOM from "react-dom";
export default class App extends React.Component<{}, {}> {
// Uploader component
  public path: object = {
    removeUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Remove',
    saveUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Save'
  }
public render(): JSX.Element{
    return (
            <UploaderComponent asyncSettings = {this.path}
                allowedExtensions='.doc, .docx, .xls, .xlsx'/>
         );
    }
}
ReactDOM.render(<App />, document.getElementById('fileupload'));
```

{% endtab %}

## File size

The uploader component allows you to validate the files based on its size.
The validation helps to restrict uploading large files or empty files to the server.
The size can be represented in bytes. By default, the uploader component allows to
upload minimum file size as **0 byte** and maximum file size as **28.4 MB** using
`minFileSize` and `maxFileSize` properties.

{% tab template="uploader/basic", sourceFiles="app/**/*.tsx" %}

```typescript

import { UploaderComponent } from '@syncfusion/ej2-react-inputs';
import * as React from 'react';
import * as ReactDOM from "react-dom";

export default class App extends React.Component<{}, {}> {
// Uploader component
  public path: object = {
    removeUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Remove',
    saveUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Save'
  }
public render(): JSX.Element{
    return (
        <UploaderComponent asyncSettings = {this.path} minFileSize = {10000} maxFileSize= {28400000}
        />
        )
    }
}
ReactDOM.render(<App />, document.getElementById('fileupload'));
```

{% endtab %}

## Maximum files count

You can restrict the maximum number of files on uploading using the selected event.
In the selected event arguments, you can get the currently selected files details using
**getFilesData()**. You can modify the files details and assign the modified file list to **eventArgs.modifiedFilesData**.

{% tab template="uploader/basic", sourceFiles="app/**/*.tsx" %}

```typescript

import {FileInfo, SelectedEventArgs, UploaderComponent } from '@syncfusion/ej2-react-inputs';
import * as React from 'react';
import * as ReactDOM from "react-dom";

export default class App extends React.Component<{}, {}> {
  public uploadObj: UploaderComponent;
  public path: object = {
    removeUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Remove',
    saveUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Save'
  }
  public onFileSelected(args : SelectedEventArgs) : void {
    args.filesData.splice(5);
    const filesData : FileInfo[] = this.uploadObj.getFilesData();
    const allFiles : FileInfo[] = filesData.concat(args.filesData);
    if (allFiles.length > 5) {
        for (const i of allFiles) {
            if ((i as any).length > 5) {
                allFiles.shift();
            }
        }
        args.filesData = allFiles;
        args.modifiedFilesData = args.filesData;
    }
    args.isModified = true;
}
public render(): JSX.Element{
    return (
        <UploaderComponent asyncSettings = {this.path} selected={this.onFileSelected = this.onFileSelected.bind(this)} ref = {upload => {this.uploadObj = upload !}} />);
  }
}
ReactDOM.render(<App />, document.getElementById('fileupload'));
```

{% endtab %}

## Duplicate files

You can validate the duplicate files before uploading to server using the selected event.
Compare the selected files with the existing files data and filter the file list by removing the duplicate files.

{% tab template="uploader/basic", sourceFiles="app/**/*.tsx" %}

```typescript

import { isNullOrUndefined } from '@syncfusion/ej2-base';
import {FileInfo, SelectedEventArgs, UploaderComponent } from '@syncfusion/ej2-react-inputs';
import * as React from 'react';
import * as ReactDOM from "react-dom";

export default class App extends React.Component<{}, {}> {
public uploadObj: UploaderComponent;
  public path: object = {
    removeUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Remove',
    saveUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Save'
  }
  public onFileSelected(args : SelectedEventArgs) : void {
    let existingFiles: FileInfo[] = this.uploadObj.getFilesData();
     for (let i: number = 0; i < args.filesData.length; i++) {
         for(const j of existingFiles) {
             if (!isNullOrUndefined(args.filesData[i])) {
                 if (j.name === args.filesData[i].name) {
                     args.filesData.splice(i, 1);
                 }
             }
         }
     }
     existingFiles = existingFiles.concat(args.filesData);
     args.modifiedFilesData = existingFiles;
     args.isModified = true;
 }

public render(): JSX.Element{
    return (
        <UploaderComponent asyncSettings = {this.path} selected={this.onFileSelected = this.onFileSelected.bind(this)} ref = {upload => {this.uploadObj = upload !}} />);
  }
}

ReactDOM.render(<App />, document.getElementById('fileupload'));

```

{% endtab %}

>You can also explore [React File Upload](https://www.syncfusion.com/react-ui-components/react-file-upload) feature tour page for its groundbreaking features. You can also explore our [React File Upload example](https://ej2.syncfusion.com/react/demos/#/material/uploader/default) to understand how to browse the files which you want to upload to the server.

## See Also

* [Validate image/* on drop](./how-to/validate-image-on-drop)
* [Determine whether uploader has file input (required validation)](./how-to/determine-whether-uploader-has-file-input)
* [Check file size before uploading it](./how-to/check-file-size-before-uploading-it)
* [Check the MIME type of file before uploading it](./how-to/check-the-mime-type-of-file-before-upload-it)
