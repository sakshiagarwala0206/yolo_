
# 🦾 Train YOLOv10 on Your Custom Dataset

This guide helps you train YOLOv10 (from Ultralytics) on a custom dataset in YOLO format.

---

## 🧱 1. Dataset Structure

Organize your dataset like this:

```
dataset/
├── images/
│   ├── train/
│   └── val/
├── labels/
│   ├── train/
│   └── val/
```

- `labels/*.txt` → Each file corresponds to an image and contains:
  ```
  class_id x_center y_center width height
  ```
  (All values are **normalized** between 0 and 1)

---

## 📝 2. data.yaml

Create a config file like this:

```yaml
path: ./dataset
train: images/train
val: images/val

nc: 3  # number of classes
names: ['class1', 'class2', 'class3']
```

---

## ⚙️ 3. Install YOLOv10

```bash
pip install ultralytics
```

---

## 🚀 4. Train YOLOv10

```bash
yolo detect train model=yolov10n.pt data=data.yaml epochs=100 imgsz=640 name=yolov10-custom
```

> Models: `yolov10n.pt`, `yolov10s.pt`, `yolov10m.pt`, `yolov10l.pt`, `yolov10x.pt`

The first time, YOLOv10 will **automatically download** the model.

---

## 📊 5. Validate

```bash
yolo detect val model=runs/detect/yolov10-custom/weights/best.pt data=data.yaml
```

---

## 🔎 6. Predict on New Images

```bash
yolo detect predict model=runs/detect/yolov10-custom/weights/best.pt source=path/to/image_or_folder
```

---

## 📈 7. Results

After training:

```
runs/detect/yolov10-custom/
├── weights/
│   ├── best.pt
│   └── last.pt
├── results.png
├── confusion_matrix.png
```



