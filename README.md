### Conda (Recommended)

```bash
conda env create -f conda-gpu.yml
conda activate yolov4-gpu
```

## Running the Tracker with YOLOv4

- Convert darknet .weights -> TensorFlow model (saved to /checkpoints) 
- Run object_tracker.py

```bash
# Convert darknet weights to tensorflow model
python save_model.py --model yolov4

# Run yolov4 deep sort object tracker on video
python object_tracker.py --video ./data/video/test.mp4 --output ./outputs/demo.avi --model yolov4
```

Use --output [insert path] to save video.

## Filter Classes that are Tracked by Object Tracker

To filter a custom selection of classes all you need to do is comment out line 159 and uncomment out line 162 of object_tracker.py. Within the list ``allowed_classes`` just add whichever classes you want the tracker to track. The classes can be any of the 80 that the model is trained on, see which classes you can track in the file [data/classes/coco.names](https://github.com/theAIGuysCode/yolov4-deepsort/blob/master/data/classes/coco.names)

## Command Line Args Reference

```bash
save_model.py:
  --weights: path to weights file
  --output: path to output
  --[no]tiny: yolov4 or yolov4-tiny
  --input_size: define input size of export model
  --framework: what framework to use (tf, trt, tflite)
  --model: yolov3 or yolov4

 object_tracker.py:
  --video: path to input video (use 0 for webcam)
  --output: path to output video (remember to set right codec for given format. e.g. XVID for .avi)
  --output_format: codec used in VideoWriter when saving video to file
  --[no]tiny: yolov4 or yolov4-tiny
  --weights: path to weights file
  --framework: what framework to use (tf, trt, tflite)
  --model: yolov3 or yolov4
  --size: resize images to
  --iou: iou threshold
  --score: confidence threshold
  --dont_show: dont show video output
  --info: print detailed info about tracked objects
```

### References  
* [tensorflow-yolov4-tflite](https://github.com/hunglc007/tensorflow-yolov4-tflite)
* [Deep SORT Repository](https://github.com/nwojke/deep_sort)
