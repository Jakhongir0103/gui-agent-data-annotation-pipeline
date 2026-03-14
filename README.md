# GUI Agent Data Annotation Pipeline

<p align="center">
    <img src="./annotation_pipeline.png" alt="Pipeline diagram" style="max-width:80%; height:auto;" />
</p>

This is a data collection pipeline that converts freely available YouTube tutorials into annotated training data for GUI Grounding, with each UI element annotated with *label*, *task* and *bounding-box coordinates*. More info can be found in the [poster](./poster.pdf) and the [presentation video](./presentation.mp4).

The annotation pipeline consists of 4 steps: (1) extraction of unique frames from a video, (2) image-level annotation of UI elements, (3) deduplication of UI elements, (4) element-level annotation of UI elements.
1. Unique Frames Extraction: A video goes through a min-max algorithm using image-hashing to keep only unique frames, which are then passed to a CNN-based classifier to filter out non-screenshot images.
2. Image-Level-Annotation: The UI elements in an image are detected using OmniParser and Claude-sonnet-4.5. We then take the overlapping bounding boxes as the final output.
3. Deduplication: Deduplication is carried out using an OCR text and the coordinates of the UI elements within an image. OCR text is detected using olmOCR-7B model.
4. Element-level Relabeling: We use Gemini-3-flash to relabel individual UI elements (optional step).