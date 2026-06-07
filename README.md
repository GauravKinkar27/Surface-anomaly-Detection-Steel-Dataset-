# Surface-anomaly-Detection-Steel-Dataset-
Surface anomaly detection is the deep learning-based project where we trained the model to detect the anomalies for the given Dataset .

**Purpose**:Develop an AI-powered steel surface defect detection system that automates inspection, identifies subtle defects accurately, and reduces manual effort, production losses, and quality-control costs.

## Dataset summary
- **Task**: Object detection (bounding box)
- **Classes**: 10 surface defect types
- **Format**: Pascal VOC XML → converted to YOLO .txt
- **Images**: 2048×1000px, grayscale (depth=1)
- **Model**: YOLOv8s (small) & RT-DETR — best balance of speed and accuracy


## Defect classes (10 total)
| ID | Class          | Description                    |
|----|----------------|-------------------------------|
|  0 | crease         | Surface fold/crease           |
|  1 | crescent_gap   | Crescent-shaped gap           |
|  2 | inclusion      | Material inclusion            |
|  3 | oil_spot       | Oil contamination             |
|  4 | punching_hole  | Hole from punching process    |
|  5 | rolled_pit     | Pit from rolling process      |
|  6 | silk_spot      | Silk-like surface texture     |
|  7 | waist_folding  | Folding at waist area         |
|  8 | water_spot     | Water stain/spot              |
|  9 | welding_line   | Welding seam artifact         |

WHAT WE DID:

We didn't collect more data. We got creative.

→ Applied CLAHE to make dark images visible
→ Built an offline augmentation pipeline
→ Flipped, rotated, brightened, distorted images
→ Took those 11 images and generated 700 variations
→ Balanced ALL 10 classes to 500–700 samples

Total annotations went from 2,449 → 6,476
The dataset was now ready to fight. 

THE RESULT:

Trained YOLOv8s

✅ Overall mAP@50 — 91.4%
✅ Rolled Pit (the 11-sample class) — 98.3%
✅ 9 out of 10 classes above 85%
✅ Inference speed — 3ms per image


WE ALSO COMPARED TWO ARCHITECTURES:
YOLOv8s (CNN) vs RT-DETR (Transformer)

Surprise — the newer flashy Transformer lost.
73.2% vs 91.4%
Lesson: Transformers need color data and massive datasets.
For grayscale industrial images — CNN still wins.


WHAT I ACTUALLY LEARNED:

→ Data > Model. Always.
→ Class imbalance can silently kill your project
