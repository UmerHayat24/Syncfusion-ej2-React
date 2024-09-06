---
title: "Export"
component: "DocumentEditor"
description: "Learn how to export the contents of React document editor as SFDT, or DOCX document in client-side."
---

# Export

Document Editor exports the document into various known file formats in client-side such as Microsoft Word document (.docx), text document (.txt), and its own format called **Syncfusion Document Text (.sfdt)**.

## SFDT export

The following example shows how to export documents in document editor as Syncfusion document text (.sfdt).

{% tab template="document-editor/export" compileJsx=true %}

```typescript
import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { DocumentEditorComponent, SfdtExport, Selection, Editor } from '@syncfusion/ej2-react-documenteditor';

//Inject require modules.
DocumentEditorComponent.Inject(SfdtExport, Selection, Editor);
export class Default extends React.Component<{}, {}> {
    public documenteditor: DocumentEditorComponent;
    save(): void {
        //Download the document in sfdt format.
        this.documenteditor.save('sample', 'Sfdt');
    }
    render() {
        return (
            <div>
                <button onClick={this.save.bind(this)}>Save</button>
                <DocumentEditorComponent id="container" height={'330px'} ref={(scope) => { this.documenteditor = scope; }} isReadOnly={false} enableSelection={true} enableEditor={true} enableSfdtExport={true} />
            </div>
        );
    }
}
ReactDOM.render(<Default />, document.getElementById('sample'));

```

{% endtab %}

>Document Editor features are segregated into individual feature-wise modules. To use SFDT export, inject the `SfdtExport` module using `DocumentEditor.Inject( SfdtExport)`.
>
>To enable SFDT export for a document editor instance, set `enableSfdtExport` to true.

## Word export

The following example shows how to export the document as Word document (.docx).

>Note: The Syncfusion Document Editor component's document pagination (page-by-page display) can't be guaranteed for all the Word documents to match the pagination of Microsoft Word application. For more information about [why the document pagination (page-by-page display) differs from Microsoft Word](../document-editor/import/#why-the-document-pagination-differs-from-microsoft-word)

{% tab template="document-editor/export" compileJsx=true %}

```typescript
import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { DocumentEditorComponent, WordExport, SfdtExport, Selection, Editor } from '@syncfusion/ej2-react-documenteditor';

//Inject require module.
DocumentEditorComponent.Inject(SfdtExport, Selection, Editor, WordExport);
export class Default extends React.Component<{}, {}> {
    public documenteditor: DocumentEditorComponent;
    save(): void {
        //Download the document in docx format.
        this.documenteditor.save('sample', 'Docx');
    }
    render() {
        return (
            <div>
                <button onClick={this.save.bind(this)}>Save</button>
                <DocumentEditorComponent id="container" height={'330px'} ref={(scope) => { this.documenteditor = scope; }} isReadOnly={false} enableSelection={true} enableEditor={true} enableSfdtExport={true} enableWordExport={true} />
            </div>
        );
    }
}
ReactDOM.render(<Default />, document.getElementById('sample'));

```

{% endtab %}

>Document Editor features are segregated into individual feature-wise modules. To use word export, inject the `WordExport` and `SfdtExport` modules using `DocumentEditor.Inject(WordExport, SfdtExport)`.
>
>To enable word export for a document editor instance, set `enableWordExport` to true.

## Text export

The following example shows how to export document as text document (.txt).

{% tab template="document-editor/export" compileJsx=true %}

```typescript
import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { DocumentEditorComponent, SfdtExport, Selection, Editor, TextExport } from '@syncfusion/ej2-react-documenteditor';

//Inject require module.
DocumentEditorComponent.Inject(SfdtExport, Selection, Editor, TextExport);
export class Default extends React.Component<{}, {}> {
    public documenteditor: DocumentEditorComponent;
    save(): void {
        //Download the document in txt format.
        proxy.documenteditor.save('sample', 'Txt');
    }
    render() {
        return (
            <div>
                <button onClick={this.save.bind(this)}>Save</button>
                <DocumentEditorComponent id="container" height={'330px'} ref={(scope) => { this.documenteditor = scope; }} isReadOnly={false} enableSelection={true} enableEditor={true} enableSfdtExport={true} enableTextExport={true} />
            </div>
        );
    }
}
ReactDOM.render(<Default />, document.getElementById('sample'));

```

{% endtab %}

>Document Editor features are segregated into individual feature-wise modules. To use text export, inject the `TextExport` and `SfdtExport` modules using the `DocumentEditor.Inject(TextExport, SfdtExport)`.
>
>To enable text export for a document editor instance, set `enableTextExport` to true.

## Export as blob

Document Editor also supports API to store the document into a blob. Refer to the following sample to export document into blob in client-side.

{% tab compileJsx=true%}

```typescript
import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { DocumentEditorComponent, WordExport, SfdtExport } from '@syncfusion/ej2-react-documenteditor';

//Inject require modules.
DocumentEditorComponent.Inject(WordExport, SfdtExport);
export class Default extends React.Component<{}, {}> {
    public documenteditor: DocumentEditorComponent;
    save(): void {
        //Export the document as Blob object.
        this.documenteditor.saveAsBlob('Docx').then((exportedDocument: Blob) => {
            // The blob can be processed further
        });
    }
    render() {
        return (
            <div>
                <button onClick={this.save.bind(this)}>Save</button>
                <DocumentEditorComponent id="container" height={'330px'} ref={(scope) => { this.documenteditor = scope; }} enableWordExport={true} enableSfdtExport={true} enableTextExport={true} />
            </div>
        );
    }
}
ReactDOM.render(<Default />, document.getElementById('sample'));

```

{% endtab %}

For instance, to export the document as Rich Text Format file, implement an ASP.NET MVC web API controller using DocIO library by passing the DOCX blob. Refer to the following code example.

```csharp
//API controller for the conversion.
  [HttpPost]
    public HttpResponseMessage ExportAsRtf()
    {
          System.Web.HttpPostedFile data = HttpContext.Current.Request.Files[0];
          //Opens document stream
          WordDocument wordDocument = new WordDocument(data.InputStream);
          MemoryStream stream = new MemoryStream();
          //Converts document stream as RTF
          wordDocument.Save(stream, FormatType.Rtf);
          wordDocument.Close();
          stream.Position = 0;
          return new HttpResponseMessage() { Content = new StreamContent(stream) };
    }

```

In client-side, you can consume this web service and save the document as Rich Text Format (.rtf) file. Refer to the following example.

{% tab compileJsx=true%}

```typescript
  onExport(): void {
        //Export the document as Blob object.
        this.documenteditor.saveAsBlob('Docx').then((exportedDocument: Blob) => {
            // The blob can be processed further
            let formData: FormData = new FormData();
            formData.append('fileName', 'sample.docx');
            formData.append('data', exportedDocument);
            this.saveAsRtf(formData);
        });
    }

    saveAsRtf(formData: FormData): void {
        let httpRequest: XMLHttpRequest = new XMLHttpRequest();
        httpRequest.open('POST', '/api/DocumentEditor/ExportAsRtf', true);
        httpRequest.onreadystatechange = () => {
            if (httpRequest.readyState === 4) {
                if (httpRequest.status === 200 || httpRequest.status === 304) {
                    if (!!navigator.msSaveBlob) {
                        navigator.msSaveBlob(httpRequest.response, 'sample.rtf');
                    } else {
                        let downloadLink: HTMLAnchorElement = document.createElementNS(
                            'http://www.w3.org/1999/xhtml',
                            'a'
                        ) as HTMLAnchorElement;
                        download(
                            'sample.rtf',
                            'rtf',
                            httpRequest.response,
                            downloadLink,
                            'download' in downloadLink
                        );
                    }
                } else {
                    console.error(httpRequest.response);
                }
            }
        };
        httpRequest.responseType = 'blob';
        httpRequest.send(formData);
    }
    //Downlod the document in client side.
    download(fileName: string, extension: string, buffer: Blob, downloadLink: HTMLAnchorElement, hasDownloadAttribute: Boolean): void {
        if (hasDownloadAttribute) {
            downloadLink.download = fileName;
            let dataUrl: string = window.URL.createObjectURL(buffer);
            downloadLink.href = dataUrl;
            let event: MouseEvent = document.createEvent('MouseEvent');
            event.initEvent('click', true, true);
            downloadLink.dispatchEvent(event);
            setTimeout((): void => {
                window.URL.revokeObjectURL(dataUrl);
                dataUrl = undefined;
            }
            );
        } else {
            if (extension !== 'docx' && extension !== 'xlsx') {
                let url: string = window.URL.createObjectURL(buffer);
                let isPopupBlocked: Window = window.open(url, '_blank');
                if (!isPopupBlocked) {
                    window.location.href = url;
                }
            }
        }
    }
```

{% endtab %}

## See Also

* [Feature modules](../document-editor/feature-module/)