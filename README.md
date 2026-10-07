# Detergent Label Wrinkle Detection

HALCON / HDevelop coursework project for locating a detergent container's label and detecting label wrinkles with shape matching and a variation model.

## Overview

The latest project script is `16-gen_label_templates(test).hdev`. It localizes the detergent container, aligns its label against a reference, and highlights regions that differ from the variation model as potential label wrinkles.

Earlier experiments are preserved under [`code/`](code/). They include alternative segmentation and inspection approaches; the root script is the latest version and the recommended starting point.

### Source versions

- `code/16-gen_label_templates(new).hdev` is the earliest version. It uses Canny edges directly in the container region, selects contours of length 200–500, and uses a narrower 0.9–1.1 scale range with local polarity. Its inspection loop has no median filter or per-image error handler.
- `code/16-gen_label_templates(test).hdev` is a later version. It adds a variation-model training pass, median filtering, and per-image error handling.
- The root `16-gen_label_templates(test).hdev` is the latest version. It uses local mean-based thresholding to extract the container region, broadens contour and scale ranges, ignores local polarity, and retains filtering and error handling. It is the recommended entry point.

These are successive experiments, not required modules. Run the root `test` script for the latest version; keep the earlier scripts only as development history.

## Requirements

- HALCON / HDevelop 22.05 or a compatible version. The source file declares HALCON 22.05.
- The authorized `Cam1_01.bmp` through `Cam1_20.bmp` input images, placed beside the HDevelop script.

The 20 `Cam1_*.bmp` input images are included. The personal coursework report remains excluded because it contains personal identifiers. Selected, non-identifying result images from the report are included below.

## Usage

1. Open `16-gen_label_templates(test).hdev` in HDevelop.
2. Set HDevelop's working directory to the repository root.
3. Keep the included `Cam1_*.bmp` files beside the script.
4. Run the script. It writes `detergent_container.shm`, `region.hobj`, `label_back.shm`, and `label_back.vam` to the working directory and inspects the first eight numbered images in its loop.

The generated HALCON files are local build artifacts and are ignored by Git. The script includes interactive `stop()` calls between inspected images.

## Method

- Extracts contours and creates a scaled shape model for detergent-container localization.
- Builds an eroded label region and a second shape model for label matching.
- Uses a direct variation model to identify wrinkle-related differences after alignment.
- Filters and visualizes candidate wrinkle regions.

## Results

The coursework report describes qualitative results for the first eight images: `Cam1_01` and `Cam1_03` are labeled as having no wrinkles, while the other six show detected wrinkle regions. The examples below are selected from the original report figures and retain the HALCON inspection overlays.

**Cam1_01 — no wrinkle detected**

![HALCON inspection output for Cam1_01, reported with no wrinkle](figures/cam1-01-no-wrinkle-detected.png)

**Cam1_04 — wrinkle region highlighted**

![HALCON inspection output for Cam1_04, with a wrinkle-related region highlighted in magenta](figures/cam1-04-wrinkle-highlighted.png)

These are qualitative coursework outputs, not an independently verified accuracy evaluation. The displayed inspection times come from the original screenshots and should not be treated as benchmark measurements.

## Project structure

```text
.
├── 16-gen_label_templates(test).hdev  # Latest version
├── code/                              # Earlier HDevelop experiments
├── figures/                           # Selected inspection result screenshots
└── Cam1_*.bmp                         # Input image sequence
```

## Verification and limitations

The HDevelop application was not available for execution during repository cleanup, so runtime behavior and inspection accuracy have not been independently verified. The input images are included, and the report screenshots provide qualitative examples only; no quantitative accuracy claim is made.

## Course context

Undergraduate course design project for **Machine Vision and Machine Learning (Bilingual Course)**. The original coursework report is intentionally excluded from the public repository because it contains personal identifiers. Selected recognition result images and descriptions are included separately.
