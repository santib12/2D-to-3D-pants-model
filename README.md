# 2D-to-3D-pants-model

## Project Overview
This project aims to develop an AI model that converts 2D images of isolated garments (specifically pants) into 3D models. The focus is on training and evaluating models using cropped images of pants, with the goal of generating accurate 3D reconstructions for individual clothing items. The project will start by leveraging existing state-of-the-art solutions and progress toward custom or fine-tuned models.

---

## Project Structure

The following folder structure has been created to organize the project:

```
2D-to-3D-pants-model/
│
├── data/                # Datasets: 2D images and 3D models (isolated pants)
│   ├── images/          # Cropped images of pants for training/testing
│   └── models/          # Corresponding 3D models (e.g., .obj, .ply)
├── notebooks/           # Jupyter notebooks for experiments and prototyping
├── src/                 # Source code for model, training, and utilities
├── pretrained_models/   # Downloaded or fine-tuned existing models
├── outputs/             # Generated 3D models and visualizations
├── pifuhd/              # PIFuHD model and scripts
├── requirements.txt     # Python dependencies
└── README.md            # Project documentation
```

---

## Running PIFuHD on Custom Images

1. **Prepare your images:**
   - Place your cropped pants images in `pifuhd/sample_images/`.
   - Images should be in `.png` or `.jpg` format (lowercase extensions are safest).
   - Images must be exactly **512x512 pixels**.
   - Remove any non-image or hidden files from the folder.

2. **Activate your virtual environment:**
   - In your terminal, from the project root:
     - Git Bash: `source venv/Scripts/activate`
     - Command Prompt: `venv\Scripts\activate`

3. **Run the inference from inside the `pifuhd` directory:**
   ```bash
   cd pifuhd
   python -m apps.simple_test
   ```
   - The script will process all valid images in `sample_images/` and save results in `pifuhd/results/`.

---

## Troubleshooting: PIFuHD Not Detecting Images

If you see `test data size: 0`:
- **Check image size:** All images must be 512x512 pixels. Resize if needed.
- **Check file extensions:** Use `.png` or `.jpg` (all lowercase is safest).
- **Check for hidden or non-image files:** Only valid images should be in `sample_images/`.
- **Check the folder path:** Images must be directly in `pifuhd/sample_images/` (not in subfolders).
- **Check PIFuHD’s file pattern:**
  - Open `pifuhd/lib/data/EvalWPoseDataset.py` and look for the file pattern (e.g., `*.png` or `*.jpg`).
  - Rename your images to match the expected extension if needed.
- **Debug with Python:**
  - From inside `pifuhd`, run:
    ```python
    import os
    img_dir = 'sample_images'
    img_files = [f for f in os.listdir(img_dir) if f.lower().endswith(('jpg', 'jpeg', 'png'))]
    print("Detected image files:", img_files)
    print("Total:", len(img_files))
    ```
  - This will show which files Python can see in the folder.

---

## Common Issues and Solutions

- **Images not detected:**
  - Ensure correct size, extension, and folder location.
  - Rename files to `.png` or `.jpg` if needed.
- **Default sample image processed:**
  - Remove any default images from `sample_images/` to process only your own.
- **Output is not as expected:**
  - PIFuHD is trained on full-body humans; results on isolated garments may be poor. Consider fine-tuning or using a model designed for single garments.

---

## Notes
- Start simple, iterate, and use existing models as learning tools.
- Document your process and any issues for reproducibility.
- For further debugging or custom training, inspect and modify the PIFuHD code as needed.