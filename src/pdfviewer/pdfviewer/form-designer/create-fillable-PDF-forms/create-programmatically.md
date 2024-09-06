---
title: "Create Programmatically"
component: "PDF Viewer"
description: "Learn how to Programmatically work with form field support in PDF Viewer."
---

# Create Programmatically

The PDF Viewer control provides the option to add, edit and delete the Form Fields. The Form Fields type supported by the PDF Viewer Control are:

    * Textbox
    * Password
    * CheckBox
    * RadioButton
    * ListBox
    * DropDown
    * SignatureField
    * InitialField

## Add a form field to PDF document programmatically

Using addFormField method, the form fields can be added to the PDF document programmatically. We need to pass two parameters in this method. They are Form Field Type and Properties of Form Field Type. To add form field programmatically, Use the following code.

{% tab template="pdfviewer/addformfield", isDefaultActive=true, compileJsx=true, sourceFiles="index.html,app/index.tsx" %}

```typescript

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { PdfViewerComponent, Toolbar, Magnification, Navigation, LinkAnnotation, BookmarkView,
ThumbnailView, Print, TextSelection, Annotation, TextSearch, Inject, FormDesigner, FormFields, TextFieldSettings } from '@syncfusion/ej2-react-pdfviewer';
import { RouteComponentProps } from 'react-router';

export class App extends React.Component<{}, {}> {
  render() {
    return ( <div>
        <div className='control-section'>
            {/* Render the PDF Viewer */}
            <PdfViewerComponent id="container" ref={(scope) => { this.viewer = scope; }} documentPath="FormDesigner.pdf" serviceUrl="https://ej2services.syncfusion.com/production/web-services/api/pdfviewer" documentLoad={this.documentLoaded} style={{ 'height': '640px' }}>
                <Inject services={[Toolbar, Magnification, Navigation, Annotation, LinkAnnotation, BookmarkView, ThumbnailView, Print, TextSelection, TextSearch, FormDesigner, FormFields]} />
            </PdfViewerComponent>
          </div>
        </div>
    );
  }
   documentLoaded = () => {
      this.viewer.formDesignerModule.addFormField("Textbox", { name: "Textbox", bounds: { X: 146, Y: 229, Width: 150, Height: 24 } } as TextFieldSettings);
   }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

## Edit/Update form field programmatically

Using updateFormField method, Form Field can be updated programmatically. We should get the Form Field object/Id from FormFieldCollections property that you would like to edit and pass it as a parameter to updateFormField method. The second parameter should be the properties that you would like to update for Form Field programmatically. We have updated the value and background Color properties of Textbox Form Field.

{% tab template="pdfviewer/updateformfield", isDefaultActive=true, compileJsx=true, sourceFiles="index.html,app/index.tsx" %}

```typescript

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { PdfViewerComponent, Toolbar, Magnification, Navigation, LinkAnnotation, BookmarkView,
ThumbnailView, Print, TextSelection, Annotation, TextSearch, Inject, FormDesigner, FormFields, TextFieldSettings } from '@syncfusion/ej2-react-pdfviewer';
import { RouteComponentProps } from 'react-router';

export class App extends React.Component<{}, {}> {
  render() {
    return ( <div>
        <div className='control-section'>
            {/* Render the PDF Viewer */}
            <PdfViewerComponent id="container" ref={(scope) => { this.viewer = scope; }} documentPath="FormDesigner.pdf" serviceUrl="https://ej2services.syncfusion.com/production/web-services/api/pdfviewer" documentLoad={this.documentLoaded} style={{ 'height': '640px' }}>
                <Inject services={[Toolbar, Magnification, Navigation, Annotation, LinkAnnotation, BookmarkView, ThumbnailView, Print, TextSelection, TextSearch, FormDesigner, FormFields]} />
            </PdfViewerComponent>
          </div>
        </div>
    );
  }
   documentLoaded = () => {
      this.viewer.formDesignerModule.addFormField("Textbox", { name: "Textbox", bounds: { X: 146, Y: 229, Width: 150, Height: 24 } } as TextFieldSettings);
      this.viewer.formDesignerModule.addFormField("Textbox", { name: "Textfield", bounds: { X: 300, Y: 229, Width: 150, Height: 24 } } as TextFieldSettings);
      this.viewer.formDesignerModule.updateFormField(pdfviewer.formFieldCollections[0], { backgroundColor: 'red' } as TextFieldSettings);
   }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

## Delete form field programmatically

Using deleteFormField method, the form field can be deleted programmatically. We should retrieve the Form Field object/Id from FormFieldCollections property that you would like to delete and pass it as a parameter to deleteFormField method. To delete a Form Field programmatically, use the following code.

{% tab template="pdfviewer/deleteformfield", isDefaultActive=true, compileJsx=true, sourceFiles="index.html,app/index.tsx" %}

```typescript

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { PdfViewerComponent, Toolbar, Magnification, Navigation, LinkAnnotation, BookmarkView,
ThumbnailView, Print, TextSelection, Annotation, TextSearch, Inject, FormDesigner, FormFields, TextFieldSettings } from '@syncfusion/ej2-react-pdfviewer';
import { RouteComponentProps } from 'react-router';

export class App extends React.Component<{}, {}> {
  render() {
    return ( <div>
        <div className='control-section'>
            {/* Render the PDF Viewer */}
            <PdfViewerComponent id="container" ref={(scope) => { this.viewer = scope; }} documentPath="FormDesigner.pdf" serviceUrl="https://ej2services.syncfusion.com/production/web-services/api/pdfviewer" documentLoad={this.documentLoaded} style={{ 'height': '640px' }}>
                <Inject services={[Toolbar, Magnification, Navigation, Annotation, LinkAnnotation, BookmarkView, ThumbnailView, Print, TextSelection, TextSearch, FormDesigner, FormFields]} />
            </PdfViewerComponent>
          </div>
        </div>
    );
  }
   documentLoaded = () => {
       this.viewer.formDesignerModule.addFormField("Textbox", { name: "Textbox", bounds: { X: 146, Y: 229, Width: 150, Height: 24 } } as TextFieldSettings);
       this.viewer.formDesignerModule.addFormField("Textbox", { name: "Textfield", bounds: { X: 300, Y: 229, Width: 150, Height: 24 } } as TextFieldSettings);
       this.viewer.formDesignerModule.deleteFormField(pdfviewer.formFieldCollections[0] });
   }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

## Saving the form fields

When the download icon is selected on the toolbar, the Form Fields will be saved in the PDF document and this action will not affect the original document. Refer the below GIF for further reference.

![Alt text](../../../pdfviewer/images/saveformfield.gif)

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

## Printing the form fields

When the print icon is selected on the toolbar, the PDF document will be printed along with the Form Fields added to the pages and this action will not affect the original document. Refer the below GIF for further reference.

![Alt text](../../../pdfviewer/images/printformfield.gif)

{% tab compileJsx=true%}

```tsx

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { PdfViewerComponent, Toolbar, Magnification, Navigation, LinkAnnotation, BookmarkView,
ThumbnailView, Print, TextSelection, TextSearch, Annotation, Inject } from '@syncfusion/ej2-react-pdfviewer';
import { RouteComponentProps } from 'react-router';

export class App extends React.Component<{}, {}> {
  render() {
    return ( <div>
        <div className='control-section'>
            {/* Render the PDF Viewer */}
            <PdfViewerComponent id="container" documentPath="PDF_Succinctly.pdf" enablePrint={true}
             serviceUrl="https://ej2services.syncfusion.com/production/web-services/api/pdfviewer" style={{ 'height': '640px' }}>
                <Inject services={[Toolbar, Annotation, Magnification, Navigation, LinkAnnotation, BookmarkView, ThumbnailView, Print, TextSelection, TextSearch]} />
            </PdfViewerComponent>
          </div>
        </div>
    );
  }
}
ReactDOM.render(<App />, document.getElementById('sample'));

```

{% endtab %}

## Open the existing PDF document

We can open the already saved PDF document contains Form Fields in it by clicking the open icon in the toolbar. Refer the below GIF for further reference.

![Alt text](../../../pdfviewer/images/openexistingpdf.gif)

## Validate form fields

The form fields in the PDF Document will be validated when the `enableFormFieldsValidation` is set to true and hook the validateFormFields. The validateFormFields will be triggered when the PDF document is downloaded or printed with the non-filled form fields. The non-filled fields will be obtained in the `nonFillableFields` property of the event arguments of validateFormFields.

Add the following code snippet to validate the form fields,

```tsx

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { PdfViewerComponent, Toolbar, Magnification, Navigation, LinkAnnotation, BookmarkView,
ThumbnailView, Print, TextSelection, Annotation, TextSearch, Inject, FormDesigner, FormFields, TextFieldSettings } from '@syncfusion/ej2-react-pdfviewer';
import { RouteComponentProps } from 'react-router';

export class App extends React.Component<{}, {}> {
  render() {
    return ( <div>
        <div className='control-section'>
            {/* Render the PDF Viewer */}
            <PdfViewerComponent id="container" ref={(scope) => { this.viewer = scope; }} documentPath="FormDesigner.pdf" serviceUrl="https://ej2services.syncfusion.com/production/web-services/api/pdfviewer" documentLoad={this.documentLoaded} enableFormFieldsValidation={true} ValidateFormFields= {this.validateFormFields}style={{ 'height': '640px' }}>
                <Inject services={[Toolbar, Magnification, Navigation, Annotation, LinkAnnotation, BookmarkView, ThumbnailView, Print, TextSelection, TextSearch, FormDesigner, FormFields]} />
            </PdfViewerComponent>
          </div>
        </div>
    );
  }
   documentLoaded = () => {
      this.viewer.formDesignerModule.addFormField("Textbox", { name: "Textbox", bounds: { X: 146, Y: 229, Width: 150, Height: 24 } } as TextFieldSettings);
   }
   validateFormFields = (args) =>{
     var nonfilledFormFields = args.nonFillableFields
   }

}
ReactDOM.render(<App />, document.getElementById('sample'));

```