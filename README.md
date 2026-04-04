# CVAT Track Merger

A lightweight, completely client-side web tool designed to fix fragmented annotation tracks exported from CVAT (Computer Vision Annotation Tool). 

**Try it live here:** [Insert your GitHub Pages URL here]

## The Problem
When using stateless serverless AI detectors (like YOLO-Pose) via Nuclio in CVAT, the model evaluates each frame in isolation. This often results in fragmented "shape" annotations rather than continuous "track" objects, creating hundreds of broken tracks on the timeline (especially when the target moves quickly and IoU tracking fails).

## The Solution
This tool processes CVAT 1.1 XML exports directly in your browser. It automatically groups fragmented shapes by label, scores competing duplicates based on visibility confidence, and stitches them together into perfectly continuous, single-object tracks. 

### Features
* **100% Local Processing:** Uses native JavaScript `DOMParser`. No server backend, meaning your annotation data never leaves your machine.
* **Smart Visibility Scoring:** If the AI generates multiple overlapping skeletons on a single frame, the tool counts the visible keypoints (`outside="0"`) and preserves the most accurate prediction.
* **Deep Nesting Support:** Correctly handles complex, nested skeleton/keypoint structures (like `torso_coco`) without breaking CVAT's strict parent-child XML hierarchy.
* **Chronological Sorting:** Automatically sorts frames numerically to prevent playback glitches upon re-import.

## Usage Instructions

1. **Export from CVAT:** In your CVAT task, go to `Export Annotations` and select **CVAT for video 1.1**. Download the `.xml` file.
2. **Merge:** Open the [Track Merger web app](insert-your-link) and drag-and-drop your `annotations.xml` file into the drop zone.
3. **Download:** The script will instantly process the file and download a `merged_annotations.xml` file.
4. **Import to CVAT:** Back in your CVAT task, click `Upload Annotations`, select **CVAT 1.1**, and upload the merged file. Your timeline will now display clean, continuous tracks.

## Development
This is a single-file application (`index.html`). No build steps or package managers are required. Feel free to fork and modify the XML parsing logic for your specific custom label configurations.
