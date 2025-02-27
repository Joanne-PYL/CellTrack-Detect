# In-vivo Cell Segmentation through Deep Learning
In vitro and in vivo single cell migration studies are greatly limited to either the time points of analysis or the number of cells tracked. Current methods heavily rely on manual labeling which is not only time consuming but also prone to errors. We proposed a two-step deep learning model that has the ability to classify cell types while tracking individual cells across frames. To achieve single cell tracking analysis, the first step is to classify cells. We proposed to classify nuclei of the cells instead of whole cell body to prevent cells overlapping.

![p](https://user-images.githubusercontent.com/61369941/166639641-8c8bccfb-c372-403e-8a82-46960917b1ea.png)

We have chosen Detectron2, developed by Facebook, as our Mask R-CNN model. To use Detectron2, we first input the fluorescent cell image into the ResNet-FPN backbone. Follwing the ResNet-FPN extract feature, there are two stages of Mask RCNN. First, it generates proposals about the regions where there might be an object based on the input image. Then preserves exact spatial locations through a ROI align layer. Second, it predicts the class of the object, refines the bounding box and generates a mask in pixel level of the object based on the first stage proposal. Both stages are connected to the backbone structure. Finally, we arrive at a model with the output of cell nuclei instance segmentation, the bounding box region, and the classification of cells and background. 

![test_frame_24](https://user-images.githubusercontent.com/61369941/166639918-4c9cd5de-9cb0-4f9f-8928-fa8d4cb67aaa.png)
A cropped view of the predicted output using our final trained Mask R-CNN model. The score represents the accuracy between ground truth and the prediction. In cases where the merging of the two cells is presented, the model still performed highly.

## How to set up the environment for Detectron2

Requirement for running Detectron2 include:

gcc & g++ ≥ 5 \
Python ≥ 3.6 \
PyTorch ≥ 1.4 \
torchvision that matches the PyTorch installation \
OpenCV \
pycocotools: pip install -U 'git+https://github.com/cocodataset/cocoapi.git#subdirectory=PythonAPI' \
fvcore: conda install -c fvcore fvcore \
Detectron2: pip install detectron2 -f https://dl.fbaipublicfiles.com/detectron2/wheels/cu101/index.html
