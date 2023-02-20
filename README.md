Source code for the paper:
# Detecting and Monitoring Rodents Using Camera Traps and Machine Learning Versus Live Trapping for Occupancy Modeling
Authors: Jaran Hopkins, Gabriel Marcelo Santos-Elizondo, Francis Villablanca

Available at: Pending

![Species_ID](https://user-images.githubusercontent.com/52707386/127080011-22a3a9d5-acd3-4adb-afb5-0318b1cde7cf.GIF)

## Project Summary 
An artificial-intelligence machine-learning model was developed to process camera trap images for rodent species level identification using YoloV5.  We took a common monitoring method for mammals, camera traps, and combined such with ML image processing to provide a drastically lower-effort methodology for monitoring.  We were able to use our results from our ML model to perform informative statistical analysis on both rodent detection and occurrence.  Our findings showed that cameras, compared to commonly used live traps, provide far greater detection of rodents and more accurate insight into their occurrence.  Given the success of cameras for rodent detection and occurrence estimates, we further found that combining cameras with ML image processing, requires much lower effort and can provide a practical and sustainable methodology for conservation efforts and researchers.  

### Untrained models vs. pre-trained models vs. transfer learning
Untrained models are neural networks that have seen no data, we specify this since most readily available open-source models have been pre-trained on a large dataset. This pre-training is what allows them to learn new objects faster and more efficiently. Taking a model like this and introducing it to a new set of images is called transfer learning. We are taking what the model already knows and using that information to learn the new images more effectively.

In our project, we used [Yolov5](https://github.com/ultralytics/yolov5) pre-trained on the [COCO dataset](https://cocodataset.org/#home). We then used transfer learning to train the pre-trained Yolov5 model on a set of rodent images.

Below we will outline the steps for using a pre-trained Yolov5 model with new images.

## Outline for Model Building/Training

### Step 1: Image Annotation (CVAT or Roboflow)
The first step in training an image recognition model is to annotate a set of images that will be used. Annotation tools like CVAT and Roboflow facilitate the drawing, naming, and formating of bounding boxes around the target within an image.

![Annotating with Roboflow](https://github.com/rodentid-draft/project-draft/blob/main/AnnotatingWRoboflow.gif)
Example with [Roboflow](https://docs.roboflow.com/annotate)

Once we finished annotating an initial set of images, vetting out images with targets that were blurry or cut-off, we checked to see there was sufficient representation of each target species. This value changes depending on the total amount of images annotated.

### Step 2: Image Preparation
Models 'see' images as a matrix of pre-determined size. We need to make sure the size of the image being passed to the model is the same as that which the model is expecting. In our case, we resized our images to 640x640 using OpenCV (Open Source Computer Vision Library). This can also be accomplished automatically through Roboflow's app. If resizing manually, make sure that the resulting bounding box has been resized and relocated correctly.

[Image resizing example in Google Colab](https://github.com/rodentid-draft/project-draft/blob/main/Example_Resize_bb_and_image.ipynb)
