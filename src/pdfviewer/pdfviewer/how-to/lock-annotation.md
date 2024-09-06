---
title: "Lock square or rectangle annotations"
component: "PDF Viewer"
description: "Learn how to lock square or rectangle annotations in the PDF Viewer control."
---

# Lock square or rectangle annotations

The PDF Viewer library allows you to lock the rectangle or square annotations using the **isLock** property in the **rectangleSettings**.

**Step 1:** Follow the steps provided in the [link](https://ej2.syncfusion.com/react/documentation/pdfviewer/getting-started/) to create simple PDF Viewer sample in React.

**Step 2:** Add the following code snippet to lock the rectangle or square annotations.

```javascript

<PdfViewerComponent
   id="container"
   documentPath="PDF_Succinctly.pdf"
   serviceUrl="https://ej2services.syncfusion.com/production/web-services/api/pdfviewer"
    // lock annotation
   rectangleSettings={{ isLock: true }}
   style={{ height: '640px' }}
>

```

Find the Sample [how to lock square or rectangle annotations](https://stackblitz.com/edit/react-mngaa3?file=index.js)