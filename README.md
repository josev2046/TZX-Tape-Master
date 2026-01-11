# JV's TZX Master: ZX Spectrum Art Tool

This utility is a web-based editor designed to create and convert digital artwork specifically for the **Sinclair ZX Spectrum**. Because the Spectrum had very specific technical constraints—most notably a resolution of 256 x 192 pixels and a limited colour palette—modern images cannot be displayed on it without significant modification. This tool automates that conversion and provides a manual editing suite to refine the results.

<img width="1543" height="780" alt="image" src="https://github.com/user-attachments/assets/3900eb03-c388-44ff-8e9a-5ba4501bbae0" />


## Key Features

* **Automatic Image Conversion:** You may upload a standard photograph or digital image. The tool automatically resizes it and maps the colours to the Spectrum’s hardware-native palette.
* **Attribute Management:** The Spectrum famously allowed only two colours within any $8 \times 8$ pixel block (a limitation known as 'attribute clash'). This tool manages these blocks, allowing you to paint background colours ('Paper') while drawing individual pixels ('Ink') on top.
* **BASIC Code Import:** If you possess vintage **BASIC code** (specifically `POKE` commands) from a magazine or an old project, you can paste the text into the editor. The tool will parse the code and reconstruct the image on the canvas.
* **Tape File Export:** Finished artwork can be saved as **.TAP** or **.TZX** files. These are digital replicas of the cassette tapes used by the original machine and can be loaded into Spectrum emulators or transferred to real hardware.



## Functional Overview

| Tool | Function |
| :--- | :--- |
| **PIX (Pencil)** | Draws individual black pixels (Ink). |
| **COL (Brush)** | Applies one of the eight Spectrum colours to an $8 \times 8$ attribute block. |
| **MOV (Hand)** | Adjusts the position of a reference photo for better alignment. |
| **GRID** | Toggles the $8 \times 8$ block boundaries to help manage colour placement. |
| **UNDO** | Reverses the last several actions. |

## Technical Specification

The tool renders to a standard HTML5 Canvas and processes data in the native Spectrum memory format. It generates a 6,912-byte memory map consisting of 6,144 bytes of pixel data and 768 bytes of colour attribute data.

---
