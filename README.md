# Emergency Vehicle Detection and Video Analytics

An academic group project exploring object detection and basic video analytics for two emergency-vehicle classes: **ambulance** and **fire truck**.

## Project overview

The notebook fine-tunes a pretrained YOLOv8s model on an emergency-vehicle image dataset, then applies the trained detector to video frames using OpenCV. Detected objects are annotated with bounding boxes, class labels and confidence scores. A horizontal reference line is used for a basic line-region count.

## Technologies

- Python
- Ultralytics YOLOv8 (YOLOv8s)
- OpenCV
- Jupyter Notebook
- PyTorch (CPU training in the recorded run)

## Recorded validation results

The uploaded notebook records the following results for the best checkpoint:

| Metric | Result |
|---|---:|
| Precision | 99.5% |
| Recall | 98.9% |
| mAP@50 | 99.5% |
| mAP@50–95 | 96.1% |
| Validation images | 578 |
| Labelled instances | 649 |

Per-class results recorded in the notebook:

| Class | Images | Instances | Precision | Recall | mAP@50 | mAP@50–95 |
|---|---:|---:|---:|---:|---:|---:|
| Ambulance | 278 | 322 | 99.8% | 98.1% | 99.5% | 95.8% |
| Fire truck | 305 | 327 | 99.1% | 99.7% | 99.5% | 96.4% |

These are the notebook's recorded validation metrics, not a guarantee of performance on unseen real-world camera footage. The dataset configuration and labels should be checked before treating the results as independently reproduced.

## Repository structure

```text
emergency-vehicle-detection-yolov8/
├── notebooks/
│   └── emergency_vehicle_detection.ipynb
├── data/
│   └── README.md
├── results/
│   └── README.md
├── .gitignore
├── requirements.txt
└── README.md
```

## Getting started

1. Clone this repository.
2. Create and activate a Python virtual environment.
3. Install dependencies:

   ```bash
   pip install -r requirements.txt
   ```

4. Obtain the emergency-vehicle dataset separately, following its licence and usage terms. Place it under `data/` and adjust `DATASET_DIR` and the train/validation folder paths in the notebook to match its structure.
5. Start Jupyter with `notebooks/` as the working directory, then open `emergency_vehicle_detection.ipynb`.
6. Run the training cells. The notebook uses a pretrained `yolov8s.pt` checkpoint and trains for 50 epochs at image size 640 on CPU.
7. For video inference, set `WEIGHTS_PATH` to the generated `best.pt` checkpoint and `VIDEO_PATH` to a video file you are permitted to use.

## Important limitations

- The line-based counting code increments the count whenever a detection's centre falls within a narrow band around the line. It does **not** track object identities or confirm a one-time crossing, so the same vehicle may be counted in multiple frames.
- The notebook does not implement multi-object tracking, direction-aware counting, or duplicate suppression.
- The recorded training run used CPU and may take a long time to reproduce.
- The dataset and sample video are not included in this repository. Do not upload copyrighted or private media without permission.
- The recorded metrics should be re-evaluated after confirming that the dataset's train and validation splits and label mappings are correct.

## Academic context

This was completed as a group academic project. My contribution included model training and implementation across multiple stages of the work.

## Future improvements

- Add object tracking (for example, a tracker integrated with YOLO) to support unique-vehicle counting.
- Make line crossing direction-aware and count only confirmed crossing events.
- Add a reproducible dataset configuration and evaluation script.
- Include permitted sample frames and model-output visualizations.
- Evaluate on additional unseen video sources and report inference performance.

## Acknowledgements

Dataset attribution and any third-party resources should be added here once the original dataset source and licence are confirmed.
