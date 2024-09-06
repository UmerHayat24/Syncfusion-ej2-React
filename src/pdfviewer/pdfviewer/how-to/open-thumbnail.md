---
title: "Open Thumbnail pane programmatically"
component: "PDF Viewer"
description: "Learn how to open the thumbnail pane programmatically in PDF Viewer control."
---

# Open Thumbnail pane programmatically

The PDF Viewer library allows you to open the thumbnail pane programmatically using the [**openThumbnailPane()**](https://ej2.syncfusion.com/react/documentation/api/pdfviewer/thumbnailView/#openthumbnailpane) method.

The following steps are used to open the thumbnail.

**Step 1:** Follow the steps provided in the [link](https://ej2.syncfusion.com/react/documentation/pdfviewer/getting-started/) to create a simple PDF Viewer sample.

**Step 2:** Use the following code snippet to open thumbnail.

```html
<button onclick="openThumbnail()">Open Thumbnail Pane</button>

<script>
function openThumbnail() {
    var viewer = document.getElementById('container').ej2_instances[0];
    // Open Thumbnail pane
    viewer.thumbnailViewModule.openThumbnailPane();
}
</script>
```

Find the sample, [how to open the thumbnail pane programmatically](https://stackblitz.com/edit/react-wcs3zf?file=index.html)