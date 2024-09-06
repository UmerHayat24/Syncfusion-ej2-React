---
title: "Drag and drop"
component: "Uploader"
description: "Explains various sources to file upload such as drag and drop (customizable), paste the images, folder selection (directory upload)."
---

# File source

## Paste to upload

The uploader component allows you to upload the files using the select or drop files option from the file
explorer.  It also supports pasting to upload the image files. You can upload any currently copied images in the clipboard.

> When you paste the image, it will be saved in the server with the filename as `image.png`. The file name can
be renamed in the server end. You can generate a random name for the file name using `getUniqueID` method.
Refer to the following example.

{% tab template="uploader/basic", sourceFiles="app/**/*.tsx" %}

```typescript

import { getUniqueID } from '@syncfusion/ej2-base';
import { UploaderComponent, UploadingEventArgs } from '@syncfusion/ej2-react-inputs';
import * as React from 'react';
import * as ReactDOM from "react-dom";

export default class App extends React.Component<{}, {}> {
    public path: object = {
        removeUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Remove',
        saveUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Save'
    }
    public onUploadBegin(args: UploadingEventArgs): void {
        // check whether the file is uploading from paste.
        if (args.fileData.fileSource === 'paste') {
            const newName: string = getUniqueID(args.fileData.name.substring(0, args.fileData.name.lastIndexOf('.'))) + '.png';
            args.customFormData = [{'fileName': newName}];
        }
    }
    public render(): JSX.Element{
        return (
            <UploaderComponent autoUpload={false}
            asyncSettings={this.path} uploading={this.onUploadBegin = this.onUploadBegin.bind(this)} />);
    }
}

ReactDOM.render(<App />, document.getElementById('fileupload'));
```

{% endtab %}

### Save action for Paste upload

```csharp
public void Save()
{
    var httpPostedFile = System.Web.HttpContext.Current.Request.Files["UploadFiles"];
    var fileSave = System.Web.HttpContext.Current.Server.MapPath("UploadedFiles");
    var fileSavePath = Path.Combine(fileSave, httpPostedFile.FileName);
    if (!System.IO.File.Exists(fileSavePath))
    {
        httpPostedFile.SaveAs(fileSavePath);
        var newName = System.Web.HttpContext.Current.Request.Form["fileName"];
        var filePath = Path.Combine(fileSavePath.Substring(0, fileSavePath.LastIndexOf("\\")), newName);
        // Rename the file
        System.IO.File.Move(fileSavePath, newName);
        HttpResponse Response = System.Web.HttpContext.Current.Response;
        Response.Clear();
        Response.ContentType = "application/json; charset=utf-8";
        Response.StatusDescription = fileSavePath;
        Response.End();
    }
}
```

## Directory upload

The uploader component allows you to upload all files in the folders to server by using
the [directoryUpload](../api/uploader/#directoryupload) property. When this property is enabled,
the uploader component processes the files by iterating through the files and sub-directories in a directory.
It allows you to select only folders instead of files to upload.

> The directory upload is available only in browsers that supports **HTML5 directory**. The uploader will
process directory upload by dragging and dropping in the Edge browser.
Refer to the following example to upload files to the server.

{% tab template="uploader/directory", sourceFiles="app/**/*.tsx" %}

```typescript

import { UploaderComponent } from '@syncfusion/ej2-react-inputs';
import * as React from 'react';
import * as ReactDOM from "react-dom";

export default class App extends React.Component<{}, {}> {
  public path: object = {
    removeUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Remove',
    saveUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Save'
  }
  public render(): JSX.Element {
    return (
        <UploaderComponent asyncSettings={this.path} directoryUpload={true} />);
  }
}

ReactDOM.render(<App />, document.getElementById('fileupload'));
```

{% endtab %}

### Save action for directory upload

```csharp
public void Save() {
    var httpPostedFile = HttpContext.Current.Request.Files["UploadFiles"];
    var fileSave = HttpContext.Current.Server.MapPath("UploadedFiles");
    // split the folders by using file name
    string[] folders = httpPostedFile.FileName.Split('/');
    string fileSavePath = "";
    if (folders.Length > 1)
    {
        for (var i = 0; i < folders.Length - 1; i++)
        {
            var newFolder = Path.Combine(fileSave, folders[i]);
            // create folder
            Directory.CreateDirectory(newFolder);
            fileSave = newFolder;
        }
        fileSavePath = Path.Combine(fileSave, folders[folders.Length - 1]);
    }
    else
    {
        fileSavePath = Path.Combine(fileSave, httpPostedFile.FileName);
    }
    if (!System.IO.File.Exists(fileSavePath))
    {
        // save file in the corresponding server location
        httpPostedFile.SaveAs(fileSavePath);
        HttpResponse Response = System.Web.HttpContext.Current.Response;
        Response.Clear();
        Response.ContentType = "application/json; charset=utf-8";
        // Sending the file path to client side
        Response.StatusDescription = fileSavePath;
        Response.End();
    }
}
```

## Drag and drop

The uploader component allows you to drag and drop the files to upload. You can drag the files from file explorer and drop into the drop area.
By default, the uploader component act as drop area element. The drop area gets highlighted when you drag the files over drop area.

### Custom drop area

The uploader component allows you to set external target element as drop area using the **dropArea** property.
The element can be represented as HTML element or element’s id.

{% tab template="uploader/drop-area", sourceFiles="app/**/*.tsx,style.css" %}

```typescript

import * as React from 'react';
import * as ReactDOM from "react-dom";
import { UploaderComponent } from '@syncfusion/ej2-react-inputs';

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
            <div id='container'>
                <div id='droparea' ref={dropAreaEle => this.dropAreaRef = dropAreaEle!}>
                Drop files here to upload
                </div>
                <div id='uploadfile'>
                    <UploaderComponent autoUpload={false}  ref = {upload => {this.uploadObj = upload !}} created={this.onCreated = this.onCreated.bind(this)} asyncSettings={this.path} />
                </div>
            </div>);
    }
}

ReactDOM.render(<App />, document.getElementById('fileupload'));
```

{% endtab %}

### Customize drop area

You can customize the appearance of drop area by overriding the default drop area styles.
The class “” and “” is available to handle this customization.

{% tab template="uploader/customize-drop", sourceFiles="app/**/*.tsx,style.css" %}

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
    private dropAreaRef: HTMLElement;
    public onCreated(): void {
        this.uploadObj.dropArea = this.dropAreaRef;
        this.uploadObj.dataBind();
    }

    public browseClick(args: React.MouseEvent): void {
        const wrapperEle: HTMLElement = select('.e-file-select-wrap button', document) as HTMLElement;
        wrapperEle.click();
        args.preventDefault();
    }
    public render(): JSX.Element {
        return (
            <div id='container'>
                <div id='dropArea'>
                    <span id='drop'> Drop files here or <a href="" id='browse' onClick={this.browseClick=this.browseClick.bind(this)}><u>Browse</u></a> </span>
                    <UploaderComponent asyncSettings={this.path}  ref = {upload => {this.uploadObj = upload!}} created={this.onCreated = this.onCreated.bind(this)}/>
                </div>
            </div>
        );
    }
}

ReactDOM.render(<App />, document.getElementById('fileupload'));
```

{% endtab %}

>You can also explore [React File Upload](https://www.syncfusion.com/react-ui-components/react-file-upload) feature tour page for its groundbreaking features. You can also explore our [React File Upload example](https://ej2.syncfusion.com/react/demos/#/material/uploader/default) to understand how to browse the files which you want to upload to the server.

## See Also

* [Achieve file upload programmatically](./how-to/achieve-file-upload-programmatically)
* [Validate image/* on drop](./how-to/validate-image-on-drop)
