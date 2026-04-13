---
slug: /platform/key-concepts/nodes/built-in/base64-decode
title: Base64 Decode
---

The Base64 Decode node in APPSe AI is a built-in node that allows you to convert a Base64 string back into its original format. Many applications and APIs return files in a Base64 string format. This node helps decode that data into a text format that can be used in other nodes in your workflow.


1. From the selection screen, choose the Base64 Decode node.
<img src="\img\platform\key-concepts\nodes\built-in\base64-decode\selection-screen.png" alt="selection screen" width="700"/>

2. Connect it with a desired node that provides a Base64 string.
<img src="\img\platform\key-concepts\nodes\built-in\base64-decode\select-a-desired-node.png" alt="select a desired node" width="700"/>

## Configuration

### Type

Select the type of file you want to decode.

1. [PDF](#pdf)
2. [Image](#image)

## Steps to Use the Base64 Node for PDF Files {#pdf}

3. Under Type, select the format of the file you want to decode.
<img src="\img\platform\key-concepts\nodes\built-in\base64-decode\select-type.jpg" alt="select type" width="700"/>

### Base64 String
Enter or map the field containing the Base64-encoded string that you want to decode. Make sure the string is properly encoded — invalid or incomplete Base64 data will result in an error.

4. In the Base64 String field, enter or map the field that contains the Base64 string.
<img src="\img\platform\key-concepts\nodes\built-in\base64-decode\Base64N-PLD4.jpg" width="700"/>

### Example Input PDF file 

5. Based on the requirement, please select the PDF as shown below, encode it into Base64 by following the process outlined below, and save the output as a file (e.g., “PDFName.pdf”).
<img src="\img\platform\key-concepts\nodes\built-in\base64-decode\Input of PDF.jpg" width="700" />

6. Click Continue, then Run the node to decode the data.
<img src="\img\platform\key-concepts\nodes\built-in\base64-decode\continue.jpg" alt="continue" width="700"/>

7. After execution, the original file content will be available as output for the next node in your workflow.
<img src="\img\platform\key-concepts\nodes\built-in\base64-decode\PDF-Output.jpg" alt="output" width="700"/>

----------

## Steps to Use the Base64 Node for Image Files {#image}


3. Under Type, select the format of the file you want to decode.
<img src="\img\platform\key-concepts\nodes\built-in\base64-decode\Base64N-IMGSLCT3.jpg" width="700" />

### Base64 String
Enter or map the field containing the Base64-encoded string that you want to decode. Make sure the string is properly encoded — invalid or incomplete Base64 data will result in an error.

4. In the Base64 String field, enter or map the field that contains the Base64 string.
<img src="\img\platform\key-concepts\nodes\built-in\base64-decode\Base64N-PLD4.jpg" width="700" />

### Example Input Image file

5. Based on the requirement, please select the image as shown below, encode it into Base64 by following the process outlined below, and save the output as a file (e.g., “filename.png”).
<img src="\img\platform\key-concepts\nodes\built-in\base64-decode\Image-Input.jpg" width="700" />

6. Click Continue, then Run the node to decode the data.
<img src="\img\platform\key-concepts\nodes\built-in\base64-decode\Base64N-CNTNUE5.jpg" width="700" />

7. After execution, the original file content will be available as output for the next node in your workflow.
<img src="\img\platform\key-concepts\nodes\built-in\base64-decode\Base64N-Result6.jpg" width="700" />

:::note

The Base64 node currently supports only the PDF files that are **NOT** protected by a password.

:::
