# JV's TZX Master: Technical Documentation

This repository houses my humble web app for creating, converting, and exporting artwork specifically for the **Sinclair ZX Spectrum**. I am hoping it serves as a sophisticated bridge between modern high-definition image formats and the intricate 8-bit machine-code structures of the 1980s.

## Why on Earth am I doing this?

The Sinclair ZX Spectrum is a cornerstone of computing nostalgia—at least for those of us of a certain demographic and age—but its unique display architecture makes creating modern artwork for it an arduous task. This project was born from a desire to simplify that "pipeline," get on with the job, and have a pint. 

I must confess I've been pulling my hair a bit with this one. Polishing it required overcoming the Spectrum’s notorious technical hurdles—specifically its non-linear memory layout and "attribute clash." The goal is to provide a seamless workflow for digital preservationists, homebrew developers, and retro-artists to move from a modern JPEG to a genuine `.TZX` tape file that can be loaded on 40-year-old hardware. It isn't perfect, but surely it must've been worth the effort.

<img width="1543" height="780" alt="JV's TZX Master Interface" src="https://github.com/user-attachments/assets/24125d65-37b2-4dd8-9cce-5d742fd6bd09" />

---

## System Components

### 1. The Conversion Engine (`autoConvertImage`)
This is the core logic that translates high-resolution photographs into 1-bit pixel data. 
* **Luminance Mapping:** It calculates the relative brightness of each pixel to determine the "Ink" placement.
* **Colour Approximation:** The `getNearestSpeccyColor` function uses Euclidean distance mapping to match modern 24-bit RGB values to the Spectrum's hardware-native 8-colour palette.

### 2. The Import Engine (`parseBasic`)
A "reverse-engineering" feature. It allows the user to paste Sinclair BASIC `POKE` commands—the primary way graphics were shared in 1980s computer magazines—and reconstructs that data into a visual format on a modern HTML5 canvas.

### 3. Binary Data Generators (`generateSpectrumMemory`)
The tool manages data exactly as the Zilog Z80 processor would.
* **Non-Linear Memory Mapping:** Unlike modern displays, the Spectrum's screen memory is fragmented. This engine correctly maps coordinates to the 6,144-byte pixel area.

* **Attribute Packing:** It handles the 768-byte "Attribute" block, which dictates the colour for every $8 \times 8$ pixel grid.

### 4. Tape Mastering Engines (`TAP` & `TZX`)
To ensure the output is "hardware-ready," the system includes two mastering suites:
* **TAP Generator:** Produces standard digital tape blocks with necessary headers and checksums.
* **TZX Master:** A more advanced engine that generates high-fidelity tape images. It includes specific "pause" durations and signal blocks required to bypass the limitations of vintage loading routines.


---

## User Controls
* **PIX (Ink):** Manual manipulation of individual pixels.
* **COL (Paper):** Block-level application of the Spectrum's background colours.
* **MOV:** Allows for the precise registration and scaling of a reference photo before the conversion engine is triggered.
* **Zoom & Grid:** High-magnification tools for "pixel-peeping" and managing attribute boundaries.

## Technical Specification
* **Native Resolution:** 256 x 192 pixels.
* **Attribute Constraints:** Maximum of two colours (one Ink, one Paper) per $8 \times 8$ block.
* **Output Standard:** Binary .tap, .tzx, and raw Z80 memory fragments.
