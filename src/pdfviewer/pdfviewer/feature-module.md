---
title: "Feature modules"
component: "PDF Viewer"
description: "Learn the feature-wise modules in ASP.NET CORE PDF Viewer and how to integrate it in your application."
---

# Feature modules

The PDF Viewer features are segregated into individual feature-wise modules to enable selectively referencing in the application. The required modules should be injected to extend its functionality. The following are the selective modules of PDF Viewer that can be included as required:

The available PdfViewer modules are:

* **Toolbar**:- Built-in toolbar for better user interaction.
* **Magnification**:- Perform zooming operation for better viewing experience.
* **Navigation**:- Easy navigation across the PDF pages.
* **LinkAnnotation**:- Easy navigation within and outside of the PDF document.
* **ThumbnailView**:- Easy navigation with in the PDF document.
* **BookmarkView**:- Easy navigation based on the bookmark content of the PDF document.
* **TextSelection**:- Select and copy text from a PDF file.
* **TextSearch**:- Search a text easily across the PDF document.
* **Print**:- Print the entire document or a specific page directly from the browser.
* **Annotation**:- Annotations can be added or edited in the PDF document.

>In addition to injecting the required modules in your application, enable corresponding properties to extend the functionality for a PDF Viewer instance.
Refer to the following table.

| Module | Property to enable the functionality for a PDF Viewer instance |
|---|---|
|Toolbar|`<PdfViewerComponent enableToolbar= {true} ></PdfViewerComponent>`|
|Magnification|`<PdfViewerComponent enableMagnification= {true} ></PdfViewerComponent>`|
|Navigation|`<PdfViewerComponent enableNavigation= {true} ></PdfViewerComponent>`|
|LinkAnnotation|`<PdfViewerComponent enableHyperlink= {true} ></PdfViewerComponent>`|
|ThumbnailView|`<PdfViewerComponent enableThumbnail= {true} ></PdfViewerComponent>`|
|BookmarkView|`<PdfViewerComponent enableBookmark= {true} ></PdfViewerComponent>`|
|TextSelection|`<PdfViewerComponent enableTextSelection= {true} ></PdfViewerComponent>`|
|TextSearch|`<PdfViewerComponent enableTextSearch= {true} ></PdfViewerComponent>`|
|Print|`<PdfViewerComponent enablePrint= {true} ></PdfViewerComponent>`|
|Annotation|`<PdfViewerComponent enableAnnotation= {true} ></PdfViewerComponent>`|

## See also

* [Toolbar items](./toolbar)
* [Toolbar customization](./how-to/toolbar-customization)