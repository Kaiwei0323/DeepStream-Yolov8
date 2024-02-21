# DeepStream-Yolov8 for Jetson Orin

## Hardware Requirements
  * NVIDIA Jetson Orin NX 16GB

## Software Requirements
  * Ubuntu 20.04
  * CUDA 11.4
  * JetPack: 5.1.2
  * NVIDIA DeepStream SDK 6.2

## Environment Setup
```
  sudo apt update
  sudo apt install -y python3-pip
  pip3 install --upgrade pip
```
```
  pip3 install -r requirements.txt
```

## DeepStream Configuration for Yolov8
### Export Model
```
  python3 utils/export_yoloV8.py -w best_m.pt
```
```
  cp utils/best_m.onnx
  cp utils/labels.txt
```
### Compile Library
```
  CUDA_VER=11.4 make -C nvdsinfer_custom_impl_Yolo
```
### Edit Configuration Files
#### Edit `config_infer_primary_yoloV8.txt`
```
  [property]
  ...
  onnx-file=best_m.onnx
  ...
  num-detected-classes=2
  ...
```
#### Edit `deepstream_app_config.txt`
##### Video Source
```
  ...
  [source0]
  ...
  uri=file:///home/aim/Downloads/pills.mp4
```
##### Webcam
```
  ...
  [source0]
  ...
  camera-width=640
  camera-height=480
  camera-fps-n=10
  camera-fps-d=1
  camera-v412-dev-node=0
```
### Run Inference
```
  deepstream-app -c deepstream_app_config.txt
```

### Result
![Screenshot from 2024-02-21 07-42-46](https://github.com/Kaiwei0323/DeepStream-Yolov8/assets/91507316/ab77f5e9-f3aa-4444-8c49-6e21dd159377)

## Reference
* https://wiki.seeedstudio.com/YOLOv8-DeepStream-TRT-Jetson/
* https://github.com/marcoslucianops/DeepStream-Yolo?tab=readme-ov-file
  





