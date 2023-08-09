# Fridge Image Detection POC Repo

I was testing out some images of food items inside the fridge for the Computer Vision project I was running for Kiwi Grocer: http://thekiwigrocer.com
For this project, I would be running the following models:
1. Object Detection
   - EfficientDet ('efficientdet_d0_coco17_tpu-32')
     - This model was used due to the lightness and accuracy of the detection 
     - http://download.tensorflow.org/models/object_detection/tf2/20200711/efficientdet_d0_coco17_tpu-32.tar.gz
     - Running the inferences via Fast API
3. Text Recognition
   -  The difficulty of simply running an object detection model is that it doesn't recognize packaged items as food products and just identifies them as a generic "bottle" etc. Hence, I decided to run a text recognition model on top of it.
   - Paddle Paddle Model was selected because of its accuracy and availability: https://github.com/PaddlePaddle/PaddleOCR
   - PPOCR model successfully identified the texts from the images, but the next challenge is to read the result (JSON format) from the model output and infer the product from the output texts to showcase which product on the market is actually inside the fridge.
   - Following methods were used to calculate the relationship (closeness of the bounding boxes of each word) to identify which text belongs to which food item
       - centroid distances
       - K-means clustering
       - hierarchical clustering
       - sort by (xmin, ymin) combinations of the box location
       - In conclusion, soring by a combination of x-min and y-min was the fastest and least computationally heavy method to identify the closest text among each other.
       - Next challenge is to group texts by a food item
         
Example of result image:
![fridge_image_2023-07-14 14_07_31 397384_](https://github.com/kisakiwata/PPOCR_text_recognition/assets/46466783/1d1c8547-0247-4e2f-bfda-42b1a834210f)


3. Barcode Scanning Model
