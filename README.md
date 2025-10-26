# YOLOv8 Object Detection Project

## Project Overview

This is a machine learning project using YOLOv8 for detecting refrigerators, bottles, and persons.

## Prerequisites

- Python 3.8 or higher
- pip package manager
- NVIDIA GPU with CUDA support (recommended)
- Git (for cloning the repository)

## Installation

### 1. Clone the Repository

```bash
git clone https://github.com/09078270504/YOLOV8.git
cd YOLOV8
```

### 2. Install Dependencies

```bash
pip install -r requirements.txt
```

Or install the core dependencies thru:

```bash
pip install ultralytics opencv-python pyyaml torch torchvision
```

## Project Structure

```
.
├── dataset_obj/          # Dataset directory
├── imports/              # Import utilities
├── runs/                 # Training runs and results
│   └── detect/          # Detection outputs
├── README.md            # Project documentation
├── best.pt              # Best trained model weights
├── objectval.yaml       # Dataset configuration
├── requrements.txt      # Project dependencies
└── yolo_detect.py       # Main detection script
```

## Steps to Reproduce

### 1. Activate Conda Environment

```bash
conda activate yolo-env1
```

### 2. Train the Model

**Standard Training (Recommended):**
```bash
yolo detect train model=yolo11s.pt data=C:/Projects/OBJECTVAT/objectvat.yaml imgsz=640 epochs=80 batch=16 device=0 workers=2 project=runs/detect name=objectvat_3cls
```

**If you encounter memory issues, use lower batch size:**
```bash
yolo detect train model=yolo11s.pt data=C:/Projects/OBJECTVAT/objectvat.yaml imgsz=640 epochs=80 batch=4 device=0 workers=2 amp=False project=runs/detect name=objectvat_3cls
```

**Training Parameters Explained:**
- `model=yolo11s.pt`: YOLO11 small model
- `imgsz=640`: Input image size
- `epochs=80`: Number of training epochs
- `batch=4`: Batch size (lower = less memory, slower training)
- `device=0`: Use GPU 0
- `workers=2`: Number of data loading workers
- `amp=False`: Disable Automatic Mixed Precision (for stability)

### 3. Run Object Detection

**Option A: Using best.pt in current directory**
```bash
cd C:\Projects\OBJECTVAT
python yolo_detect.py --model best.pt --source usb0 --resolution 1280x720
```

**Option B: Using full path to trained model**
```bash
python yolo_detect.py --model "C:\Users\<name>\runs\detect\objectvat_3cls8\weights\best.pt" --source usb0 --resolution 1280x720
```

**Detection Source Options:**
- `usb0` - USB webcam
- `0` - Default webcam
- `path/to/image.jpg` - Single image
- `path/to/video.mp4` - Video file
- `path/to/folder/` - Folder of images

### 4. View Training Results

Training results are saved in:
```
C:\Users\<name>\runs\detect\objectvat_3cls8\
├── weights/
│   ├── best.pt      # Best model checkpoint
│   └── last.pt      # Last epoch checkpoint
├── results.png      # Training metrics graphs
├── confusion_matrix.png
└── val_batch0_pred.jpg  # Validation predictions
```

## Usage Examples

### Real-time Webcam Detection
```bash
conda activate yolo-env1
cd C:\Projects\OBJECTVAT
python yolo_detect.py --model best.pt --source usb0 --resolution 1280x720
```

### Detect in Video File
```bash
python yolo_detect.py --model best.pt --source path/to/video.mp4
```

### Detect in Image
```bash
python yolo_detect.py --model best.pt --source path/to/image.jpg
```

### Batch Detection on Folder
```bash
python yolo_detect.py --model best.pt --source path/to/images/
```

## Model Performance

The trained YOLO11 model detects three classes:
- **Refrigerator** (Class 0)
- **Bottle** (Class 1)
- **Person** (Class 2)

Training configuration:
- Model: YOLO11s (small)
- Image size: 640x640
- Epochs: 80
- Batch size: 4 (optimized for memory)

## Troubleshooting

### Out of Memory Errors
If you get CUDA out of memory errors during training:
```bash
# Reduce batch size
yolo detect train model=yolo11s.pt data=C:/Projects/OBJECTVAT/objectvat.yaml imgsz=640 epochs=80 batch=2 device=0 workers=2 amp=False project=runs/detect name=objectvat_3cls
```

### Slow Training
- **Lower batch size**: Use `batch=4` or `batch=2`
- **Reduce workers**: Use `workers=1` or `workers=0`
- **Disable AMP**: Add `amp=False`

### Camera Not Detected
```bash
# Try different source numbers
python yolo_detect.py --model best.pt --source 0  # Default camera
python yolo_detect.py --model best.pt --source 1  # Secondary camera
```

### Module Not Found Errors
```bash
conda activate yolo-env1
pip install --upgrade ultralytics opencv-python
```

## Validation and Testing

### Validate Model Performance
```bash
yolo detect val model="C:\Users\<name>\runs\detect\objectvat_3cls8\weights\best.pt" data=C:/Projects/OBJECTVAT/objectvat.yaml
```

### Export Model for Deployment
```bash
# Export to ONNX format
yolo export model=best.pt format=onnx

# Export to TensorRT (for NVIDIA devices)
yolo export model=best.pt format=engine
```

## Additional Commands

### Resume Training from Checkpoint
```bash
yolo detect train resume model="C:\Users\<name>\runs\detect\objectvat_3cls8\weights\last.pt"
```

### Predict with CLI
```bash
yolo detect predict model=best.pt source=usb0 show=True
```

## Environment Management

### Deactivate Environment
```bash
conda deactivate
```

### Remove Environment (if needed)
```bash
conda env remove -n yolo-env1
```

### List All Environments
```bash
conda env list
```

## Credits

- Detection script: [EdjeElectronics/Train-and-Deploy-YOLO-Models](https://github.com/EdjeElectronics/Train-and-Deploy-YOLO-Models)
- YOLO11/YOLOv8 by Ultralytics
- Training performed on NVIDIA GPU with CUDA

## License

## Contact

GitHub: [@09078270504](https://github.com/09078270504)
