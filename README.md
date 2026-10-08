# DataOpen Dataset Files

This package contains example data for strawberry harvesting sequence planning, including scene images, depth arrays, detection annotations, structured attributes, and input–output samples for LLM fine-tuning. It covers 8 scenes.

## Directory Structure

```text
dataopen/
├── raw/
│   ├── rgb/                 # RGB scene images (.png)
│   └── depth/               # Depth arrays (.npy)
├── annotations/
│   ├── yolo/                # Object detection annotations (.txt)
│   ├── structured/          # Scene attributes and picking labels (.json)
│   └── occlusion/           # Occlusion information and data splits (.json)
└── finetune/
    └── planner/
        └── items/           # LLM planning samples (.json)
```

## File Descriptions

| Directory | Contents |
| --- | --- |
| `raw/rgb/` | RGB images of strawberry scenes, with a resolution of 640 × 480 pixels. |
| `raw/depth/` | Depth arrays for the corresponding scenes, with a shape of `(480, 640)`. These files can be loaded using NumPy. |
| `annotations/yolo/` | YOLO annotations. Each row contains a class ID and normalized bounding-box center coordinates, width, and height. In the current annotations, class `0` corresponds to ripe strawberries and class `1` to unripe strawberries. |
| `annotations/structured/` | Complete scene records, including the initial robot arm position, fruit positions, size-related fields, ripeness, occlusion, cluster assignments, picking order, and summary statistics. |
| `annotations/occlusion/` | Fruit-level occlusion information, scene IDs, source records, and `train`, `val`, or `test` split labels. The four directional occlusion fields in this package are replicated from a scalar occlusion value. |
| `finetune/planner/items/` | Planning samples for LLM fine-tuning. Each file contains a task description, scene input, and target output. |

## Fine-Tuning Sample Structure

Each fine-tuning JSON file contains three top-level fields:

| Field | Description |
| --- | --- |
| `introduction` | Task description and harvesting sequence planning instructions. |
| `input` | Initial robot arm position (`arm_position`), cluster assignments (`clusters`), and fruit attributes (`fruits`). |
| `output` | Picking order for ripe strawberries (`pick_order`) and a textual explanation (`reason`). |

## File Correspondence

Files belonging to the same scene are linked by their scene number. For example, scene 0007 corresponds to:

```text
raw/rgb/dataopen_scene_0007.png
raw/depth/dataopen_scene_0007.npy
annotations/yolo/7.txt
annotations/structured/dataopen_scene_0007.json
annotations/occlusion/dataopen_scene_0007.json
finetune/planner/items/dataopen_scene_0007.json
```

The scene numbers are `0007`, `0008`, `0009`, `0010`, `0011`, `0013`, `0014`, and `0015`. The first six are training samples; `0014` is the validation sample, and `0015` is the test sample.
