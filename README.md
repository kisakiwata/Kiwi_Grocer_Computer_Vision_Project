# PPOCR_text_recognition

Testing out Paddle Paddle OCR text recognition model.
See details of PPOCR here:

For this, I was testing out an image of food for the project of fridge image recognition project I was running for Kiwi Grocer: http://thekiwigrocer.com
For this project, I would be running following models:
1. Object Detection
   - EfficientDet ('efficientdet_d0_coco17_tpu-32')
     - This model was used due to the lightness and accuracy of detection 
     - http://download.tensorflow.org/models/object_detection/tf2/20200711/efficientdet_d0_coco17_tpu-32.tar.gz
2. Text Regonition
   - Paddle Paddle Model: https://github.com/PaddlePaddle/PaddleOCR
   - Cleaning up and inferring the output file (PPOCR model successfully identified the texts from the images, but the next challenge is to read the result (JSON format) from the model output and infer the product from the output texts.)
   - Following methods were used to calculate the relationship (closeness of the bounding boxes of each word) to identify which text belongs to which food item
       - centeroid distances
       - K-means clustering
       - hierachical clustering
       - sort by (xmin, ymin) combinations of the box location
       - As a conclusiong, the soring by combination of x-min and y-min was the fastest and least computationally method to identify the closest text
       - Next challenge is to group texts by a food item
         
Example of result image:
![fridge_image_2023-07-14 14_07_31 397384_](https://github.com/kisakiwata/PPOCR_text_recognition/assets/46466783/1d1c8547-0247-4e2f-bfda-42b1a834210f)


3. Barcode Scanning Model
