# TZX Tape Master: Technical Documentation

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.18216179.svg)](https://doi.org/10.5281/zenodo.18216179)

This repository houses a web application designed for the creation, conversion, and export of artwork specifically for the **Sinclair ZX Spectrum**. It serves as a practical bridge between modern high-definition image formats and the unique 8-bit machine-code structures of the 1980s.

<img width="1368" height="857" alt="a TZX bitmap conversion" src="https://github.com/user-attachments/assets/a660501b-e09c-4040-ae3d-145fad8fc23d" />


> *TZX Tape Master example of bitmap conversion.*


## Rationale and Utility

The Sinclair ZX Spectrum (1982) remains a vibrant platform for retro-coding and digital art, yet its display architecture is famously idiosyncratic. This project was born from a desire to simplify the "pipeline" required to get a modern image onto original hardware. 

Developing this tool required addressing the Spectrum’s specific technical constraints—notably its non-linear memory layout and the "attribute clash" caused by its $8 \times 8$ colour blocks. The goal is to provide a reliable workflow for homebrew developers and artists to move from a modern bitmap to a genuine `.TAP` or `.TZX` tape file that is ready to be loaded via a cassette interface or SD-card reader.

<img width="1494" height="1129" alt="image" src="https://github.com/user-attachments/assets/e4693f51-a7bc-4e41-9897-a7897255222c" />

---

## System Components

### 1. The Conversion Engine (`autoConvertImage`)
This core logic translates high-resolution source images into 1-bit pixel data through two primary processes:
* **Luminance Mapping:** The system calculates the relative brightness of each pixel to determine the most appropriate "Ink" placement.
* **Colour Approximation:** The `getNearestSpeccyColor` function uses Euclidean distance mapping to match modern 24-bit RGB values to the Spectrum's hardware-native 8-colour palette (including 'Bright' variants).

### 2. The Import Engine (`parseBasic`)
A utility for reconstructing legacy data. It allows users to paste Sinclair BASIC `POKE` commands—the standard method for sharing graphics in vintage computer magazines—and renders that data back into a visual format on an HTML5 canvas for modern editing.

### 3. Binary Data Generators (`generateSpectrumMemory`)
The tool manages data exactly as the Zilog Z80 processor requires, handling the machine's specific memory constraints:
* **Non-Linear Memory Mapping:** Spectrum screen memory is fragmented into three distinct banks with an interleaved row structure. This engine correctly maps X/Y coordinates to the 6,144-byte pixel area.
* **Attribute Packing:** It manages the 768-byte "Attribute" block, which defines the Ink and Paper colours for every $8 \times 8$ pixel grid.

### 4. Tape Mastering Engines (`TAP` & `TZX`)
To ensure the output is hardware-compatible, the system includes two mastering suites:
* **TAP Generator:** Produces standard digital tape blocks with the necessary headers and checksums for ROM loading.
* **TZX Master:** A more precise engine that generates tape images incorporating specific "pause" durations and signal blocks required for reliable loading on vintage hardware.

---

## User Controls
* **PIX (Ink):** Manual manipulation of individual pixels for fine-tuning detail.
* **COL (Paper):** Block-level application of the Spectrum's background colours.
* **MOV:** Allows for the precise registration, scaling, and cropping of a reference photo before conversion.
* **Zoom & Grid:** Tools for managing attribute boundaries to identify and prevent "colour clash" early in the creative process.

## Technical Specification
* **Native Resolution:** 256 x 192 pixels.
* **Attribute Constraints:** Maximum of two colours (one Ink, one Paper) per $8 \times 8$ block.
* **Memory Layout:** 6,144 bytes (pixels) + 768 bytes (attributes).
* **Output Standards:** Binary `.tap`, `.tzx`, and raw Z80 memory fragments (.bin).
