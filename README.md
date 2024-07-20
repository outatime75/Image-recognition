# **Image Recognition** :pizza:

The objective of this assignment was to build a model that can locate and identify specific pizza toppings from an image. This assignment was a requirement within the study unit *Advanced Computer Vision for Artificial Intelligence* offered by the University of Malta as part of its undergraduate course in Artificial Intelligence. 

The first task involved using pre-trained models to classify images as those containing a pizza and those that do not. The second task focused on building a dataset for training an object detector for this project. The third part involved the training of object detectors to locate a pizza in the input image and also identify its toppings.

## Task 1: Object Classification 🍕

### Dataset
A modified version of the Food-101 dataset, containing 983 images of pizza and 983 non-pizza images, was used. Images were rescaled to a maximum side length of 512 pixels.

This repository contains two datasets containg images used to train a Faster R-CNN model and a YOLOv8 model to detect pizza and 4 pizza toppings (black olives, mushrooms, pepperoni and peppers). There are two versions of this dataset:
- one in COCO json format (to be used with the Faster R-CNN model training)
- one in YOLOv8 format.


### Methodology
- **Model**: MobileNet_v2 with 'imagenet' weights.
- **Data Split**: Training (80%), Validation (10%), Testing (10%).
- **Techniques**: AUTOTUNE for performance optimization, data augmentation (random flip and rotation), preprocessing with `preprocessing_input` from MobileNet_v2.

### Results
- **Training Accuracy**: 90.97%
- **Validation Accuracy**: 93.23%

**Training and Validation Results**:

![output_38_0](https://github.com/user-attachments/assets/41be9e2d-495a-415c-8d0a-31638d7464fe)

## Task 2: Building a Dataset 🛠️

### Dataset Creation
A curated dataset was built focusing on four pizza toppings: black olives, pepperoni, mushrooms, and peppers. The dataset was sourced from the 'Pizza Topping Image Dataset' on Kaggle, containing 9213 annotated images.

### Process
- **Selection**: 100 images per topping, resulting in a total of 566 images after removing duplicates.
- **Annotation**: Images were annotated and classes were created in Roboflow for 'pizza', 'black_olives', 'pepperoni', 'mushrooms', and 'peppers'.
- **Storage**: The dataset was uploaded to a GitHub repository.

## Task 3: Object Detection/Localization 🔍

### Model 1: Faster R-CNN

#### Architecture
- **Components**: Region Proposal Network (RPN), Region of Interest (RoI) Pooling, CNN Backbone (ResNet), Fully Connected Layers.
- **Implementation**: Custom implementation using PyTorch.

![faster_cnn](https://github.com/user-attachments/assets/ce4dab52-8a75-4d3d-bff2-9385e5cb382a)

*Faster R-CNN Architecture (Image by Neeraj Krishna)*

#### Training
- **Optimizer**: AdamW with a weight decay of 0.0005.
- **Learning Rate**: 1e-3 for 15 epochs.
- **Results**: Training and validation loss were plotted, indicating the model performance over epochs.

#### Inference
- **Precision and Recall**: Various metrics were calculated, indicating limited success in object detection with this model.

![faster_cnn_results](https://github.com/user-attachments/assets/1bde1e8d-dd4b-46c8-a9cc-83f954cea4d2)

![faster_cnn_predictions](https://github.com/user-attachments/assets/835bee5d-0542-47ed-93f7-2694a00253e9)

### Model 2: YOLO V8

#### Architecture
- **Components**: The latest version of YOLO from Ultralytics.
- **Implementation**: Roboflow has inbuilt export support for YOLOv8 and hence the dataset configuration was performed seamlessly with the data.yaml configuration file being automatically generated by Roboflow. This file includes details of the training, validation and test set locations together with their annotations.
  
#### Training and Results
- **Training**: The training part of the model can be performed with basic, pre-set hyperparameters but a number of configurations are possible. For this task the model was trained for 50 epochs, using a learning rate of 1e-2, with a dropout ratio of 0.1, freezing zero layers and a batch size of 24. The model, with setting plots=True can save plots and images generated during training in a specific folder. It also generated a results.csv file which contains metrics generated at every epoch. These were loaded into a pandas dataframe and plotted against the number of epochs.
- **Results**: 

![yolov8_val_metrics](https://github.com/user-attachments/assets/e3fc1743-07fe-45b9-b61d-dc880a98ebe9)

*Example of multiple detections*

![multiple_detections_yolov8](https://github.com/user-attachments/assets/074915ee-f1a5-4b09-87c2-aea265da73b8)



## References
- [Kaggle Food-101 Dataset](https://www.kaggle.com/datasets/carlosrunner/food-101)
- [Pizza Topping Image Dataset](https://www.kaggle.com/datasets)
- [Roboflow](https://roboflow.com)
- [Faster R-CNN Paper](https://arxiv.org/abs/1506.01497)
- [YOLO V8 by Ultralytics](https://ultralytics.com/yolov8)

---

