---
title: "Load PDF documents dynamically"
component: "PDF Viewer"
description: "Learn how to load PDF documents dynamically in PDF Viewer control."
---

# Load PDF documents dynamically

The PDF Viewer library allows to switch or load PDF documents dynamically after the initial load operation. To achieve this, load the PDF document as a base64 string or the file name into the PDF Viewer control using the  [**Load()**](https://ej2.syncfusion.com/react/documentation/api/pdfviewer/#load) method dynamically.

The following steps are used to load the PDF document dynamically.

**Step 1:** Follow the steps provided in the [link](https://ej2.syncfusion.com/react/documentation/pdfviewer/getting-started/) to create a simple PDF Viewer sample.

**Step 2:** Use the following code snippet to load the PDF document using a base64 string.

```html
<button id='load1'>LoadDocumentFromBase64</button>

<script>
// Load PDF document from Base64 string
function load_1(){
    var viewer = document.getElementById('container').ej2_instances[0];
    viewer.load('data:application/pdf;base64,'+ AddBase64String, null);
}
</script>
```

**Step 3:** Use the following code snippet to the load PDF document the using document name.

```html
<button id='load2'>LoadDocument</button>

<script>
// Load PDF document using file name
function load_2(){
    var viewer = document.getElementById('container').ej2_instances[0];
    viewer.load('PDF_Succinctly.pdf', null);
}
</script>
```

Find the sample, [how to load PDF documents dynamically](https://stackblitz.com/edit/react-4w9zpt?file=index.html)