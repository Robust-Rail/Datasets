# Datasets
This repository contains the data and annotations used by Robust Rail Projects. 

The datasets in this repo are used for a research. This research focuses on the automatic detection and reading of hazardous material (hazmat) plates on freight trains and trucks using computer vision.

## Project Overview

The research paper's goal is to enhance the safety and efficiency of freight transport by automating the identification of hazardous materials. This is achieved by detecting and reading the orange RID/ADR plates on transport vehicles. The paper benchmarks various object detection and optical character recognition (OCR) models to create a robust pipeline for this task.

The system utilizes a two-step process:
1.  **Placard Detection:** Identifying the location of the hazmat plate in an image.
2.  **Optical Character Recognition (OCR):** Extracting the RID/ADR and UN numbers from the detected plate.

## Dataset Description

The data used in this project is split into two main datasets: a private dataset of freight trains (`prorail_datasets`) and a public dataset of trucks (`haztruck_dataset`).

### `prorail_datasets`

This dataset contains data from videos of freight trains. Due to privacy constraints, the raw video and image files are not publicly available. However, the annotations are provided in COCO format.

*   **`coco_datasets/`**: This directory contains the annotations for the hazmat plates in COCO JSON format.
    *   `instances_train.json`: Annotations for the training set.
    *   `instances_val.json`: Annotations for the validation set.
    *   `instances_test.json`: Annotations for the test set.
    *   `instances_aug.json`: Annotations for the augmented training set.

    **COCO Annotation Format:**
    Each JSON file contains information about the images, annotations, and categories. The annotations include bounding box coordinates (`bbox`), the area of the bounding box, the image ID it belongs to, a unique annotation ID, and the category ID.

*   **`video_data_info.csv`**: This file provides metadata for the videos from which the frames were extracted. The columns include:
    *   `filename`: The name of the video file.
    *   `fps`: Frames per second of the video.
    *   `frame_count`: Total number of frames in the video.
    *   `width`, `height`, `resolution`: Video dimensions.
    *   `duration_seconds`: The duration of the video in seconds.
    *   `file_size_mb`: The size of the video file in megabytes.
    *   `hash`: A unique identifier for the video file.
    *   `train_detected`, `confidence`: Output from an initial, untrained YOLO model to pre-select videos containing trains. This was part of an early filtering step and the final selection was done manually.

### `haztruck_dataset`

This dataset consists of images of trucks with hazmat plates, sourced from the internet. The images used for the last two entries were taken by the authors and free to use for anybody.

*   **`images/`**: This directory contains the two images that were captured by the authors. Other images are not provided due to copyright restrictions, but their sources are listed in the CSV file.
    *   `282.jpg`
    *   `283.jpg`

*   **`haztruck_dataset.csv`**: This file contains the annotations and metadata for the truck images. The columns are:
    *   `image_id`: A unique identifier for the image.
    *   `link`: The URL where the image was sourced from.
    *   `website`: The name of the website hosting the image.
    *   `author`: The author of the image, if known.
    *   `resolution`: The resolution of the image.
    *   `date_accessed`: The date when the image was accessed.
    *   `added_by`: The person who added the image to the dataset.
    *   `image_name`: The corresponding filename in the local dataset.
    *   `box_label`: The label for the annotation, which is `hazmat_sign`.
    *   `box_xtl`, `box_ytl`, `box_xbr`, `box_ybr`: The top-left and bottom-right coordinates of the bounding box for the hazmat plate.
    *   `issue`: Any specific notes about the image, such as "rotated", "low quality", or "damaged".
    *   `code`: The RID/ADR and UN numbers on the plate, separated by a forward slash.

## Models and Regulations

The research paper evaluates several computer vision models for both object detection and OCR.

### Object Detection Models

*   **YOLOv11x**: A state-of-the-art, real-time object detection model known for its speed and efficiency. It comes in various sizes to suit different computational constraints.
*   **Faster R-CNN**: A two-stage object detection model that is known for its accuracy. It uses a Region Proposal Network (RPN) to first identify regions of interest and then classifies the objects within those regions.

### OCR Models

*   **Tesseract**: An open-source OCR engine originally developed by Hewlett-Packard and now supported by Google. It can recognize over 100 languages.
*   **EasyOCR**: A Python library for OCR that is designed to be user-friendly and can read text from natural scenes and documents. It supports over 80 languages.
*   **Idefics2**: A multimodal model that can process both images and text to generate text-based responses. It has strong OCR capabilities, which makes it suitable for extracting text from images and documents.


## How to Use This Data

Developers and researchers interested in this project can use the provided annotation files to train and evaluate their own object detection and OCR models.

1.  **Object Detection**: The  `haztruck_dataset.csv` provide the bounding box annotations necessary to train object detection models like YOLOv11x or Faster R-CNN to locate hazmat plates.

2.  **OCR**: Once a plate is detected, the cropped image of the plate can be used to test or fine-tune OCR models like Tesseract, EasyOCR, or Idefics2. The `code` column in `haztruck_dataset.csv` provides the ground truth text for the truck images.

## Disclaimer and Contact

Please note that due to privacy and copyright restrictions, the raw video and image data for the `prorail_datasets` and the majority of the `haztruck_dataset` are not included in this repository.

For access to the full `prorail_datasets` for research purposes, please contact the authors of the paper. The `haztruck_dataset` images can be downloaded online.

We hope this dataset and the accompanying information are valuable for your research in computer vision and intelligent transportation systems.