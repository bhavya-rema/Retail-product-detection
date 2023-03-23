# Retail-product-detection
Object Recognition on retail products using Yolov5. Combining different detector results to attain better accuracy
Summary
Utilizing pretrained Yolov5 model, an accurate product detection model for retail products is implemented here. 
Final detector is a combination of 2 detectors trained on 2 different datasets, a general detector for all products and another for identifying products in multipack. 
Input to these detectors is a shelf image and output is bounding box coordinates of products in the shelf image

## Datasets
public Retail products dataset -  SKU 110K and another private dataset

## Architecture
General detector outputs bounding boxes for all products including those inside a multipack since SKU110 dataset lacks multipack annotations.
Multipack detector outputs multipacks bounding boxes in shelf images, but misses on many single packs. 
Therefore, bounding box coordinates from the 2 detectors are combined with the Multipack detector taking precedence.
For combining bounding box coordinates, centre points of bounding boxes from the general detector are checked against Multipack box coordinates 
to see if the centre points fall inside a multipack bounding box. If so, the boxes within a multipack are discarded to get the final set of bounding box coordinates. 

![alt text](https://github.com/bhavya-rema/Retail-product-detection/blob/main/images/Architecture.png)
## Preprocessing
YOLOv5 dataloader does not consider exif data of images, which sometimes can lead to a rotated image when it's read. 
Shelf images are therefore preprocessed to read the metadata and correct the orientation of the image before passing to the Detector module.

## Results
General Detector used pretrained YoloV5L on COCO dataset. This was further trained on the SKU110k dataset.  
Dataset was pre processed, prepared in YOLOv5 format and was trained for 50 epochs. The mAP@0.5 for this detector reached 89%


Before correcting orientation				After correcting orientation


General Detector output


Multipack Detector output
![alt text](https://github.com/bhavya-rema/E-Commerce-Recommendation/blob/main/Recommendation.png)


Combined detector’s bounding boxes


