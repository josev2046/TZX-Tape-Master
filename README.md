# JV's TZX Master: Technical Documentation

This repository contains a specialised web application for creating, converting, and exporting artwork for the Sinclair ZX Spectrum. It functions not just as a drawing tool, but as a bridge between modern image formats and 1980s machine-code data structures.

<img width="1543" height="780" alt="image" src="https://github.com/user-attachments/assets/24125d65-37b2-4dd8-9cce-5d742fd6bd09" />


## System Components

### 1. The Conversion Engine (`autoConvertImage`)
This is the core logic that translates high-resolution photographs into 1-bit pixel data. 
* **Luminance Mapping:** It calculates the brightness (luminance) of each pixel to decide whether to place a 'black' ink pixel or a blank space.
* **Colour Approximation:** The `getNearestSpeccyColor` function uses Euclidean distance mapping to find the closest match between a modern 24-bit colour and the Spectrum's original 8-colour palette.

### 2. The Import Engine (`parseBasic`)
A unique feature that allows users to 'reverse-engineer' artwork. It parses a list of Sinclair BASIC `POKE` commands—the traditional method for loading graphics in the 1980s—and reconstructs the image on a modern HTML5 canvas.

### 3. Binary Data Generators (`generateSpectrumMemory`)
The tool manages data exactly as the Spectrum's Z80 processor would.
* **Screen Memory Mapping:** It accounts for the Spectrum's notoriously non-linear screen memory, where the vertical rows are not stored sequentially.
* **Attribute Packing:** It packs colour information into the 768-byte 'Attribute' memory block that sits behind the main 6KB pixel display.

### 4. Tape Mastering Engines (`TAP` & `TZX`)
To make the art usable on real hardware, the code includes two mastering engines:
* **TAP Generator:** Creates a standard digital tape file with appropriate headers and checksums for error detection.
* **TZX Master:** Generates a more complex 'Tape Image' format, complete with specific 'pause' intervals and signal blocks to ensure compatibility with vintage tape-loading routines.

## User Controls
* **PIX (Ink):** Manual pixel manipulation.
* **COL (Paper):** Block-based background colour application.
* **MOV:** Precision positioning of the reference image before conversion.
* **Zoom & Grid:** Visual aids for high-precision 'pixel-peeping'.

---

### Technical Specification
* **Target Resolution:** 256 x 192 pixels.
* **Attribute Density:** One colour pair (Ink/Paper) per $8 \times 8$ pixel grid.
* **Output Formats:** Binary .tap, .tzx, and raw Z80 memory dumps.
