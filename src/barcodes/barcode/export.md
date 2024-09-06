---
title: "Export"
component: "BarcodeGenerator"
description: "The BarcodeGenerator component is a pure JavaScript library which will convert a string to barcode and show it to the user. This supports the major 1D and 2D barcodes including the coda bar, code 128, QR Code."
---

# Export

Export barcode as an image and base64 string is common for barcode,QRcode and datamatrix. The following code samples explain how to export the barcode as an image and base64 string.

## Export

Barcode provides the support to export its content as an image in the specified image type and downloads it in the browser.
The following code example shows how to export the barcode as an image

```tsx

let barcodeInstance;
ReactDOM.render(
  <BarcodeGeneratorComponent
  id="barcode"
  ref={barcode => (barcodeInstance = barcode)}
  width={"200px"}
  height={"150px"}
  type='Code39'
  value='SYNCFUSION'
  ></BarcodeGeneratorComponent>,
document.getElementById("barcode")
);
let filename = 'Export';
barcodeInstance.exportImage(filename,'JPG');

```

The filename specifies the name of the file to be downloaded

### Export As Base64String

Barcode provides support to export its content as an image in the specified image type and returns it as base64 string.
The following code example illustrates how to export the barcode as a base64 string

```tsx

let barcodeInstance;
ReactDOM.render(
  <BarcodeGeneratorComponent
    id="barcode"
    ref={barcode => (barcodeInstance = barcode)}
    width={"200px"}
    height={"150px"}
    type='Code39'
    value='SYNCFUSION'
    ></BarcodeGeneratorComponent>,
document.getElementById("barcode")
);
base64string();
async function base64string() {
let base64 = await barcodeInstance.exportAsBase64Image('JPG');
console.log(base64);
};

```

>**Note:**
>Format is to specify the type or format of the exported file. You can export the barcode to the following formats:
>* JPG.
>* PNG.