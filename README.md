# Object Detection and Image Classification using coreML
The purpose of this mini-project/demo is to demonstrate the use of Apple's framework to integrate machine learning models into apps. The focus of this particular example is on the setup and the use of Create ML to train custom models to recognize objects in images. As this is a demo, the training is incomplete and thus is not perfect. :) A lot of the steps here are similar to those that you would perform when training on Google Colab or Jupyter Notebook. The original plan was to train the models in Google Colab or Jupyter Notebook but converting the resulting models to compatible CoreML models lead to a lot of issues with missing labels which I decided I did not have the time to debug.

<p float = "left" align = "center">
<img src="https://github.com/domdavid/objectDetectionCoreMLDemo/blob/main/gifs/detectCars.gif" width="400" height="300" />
<img src="https://github.com/domdavid/objectDetectionCoreMLDemo/blob/main/gifs/detectDog.gif" width="400" height="300" />
</p>
<p align = "center">Fig. 1. The animations show the model identifying the objects (outlined by the rectangular bounding box) it was trained on.</p>

## Description

Using Create ML, this project outlines the necessary steps in training custom models with your data! This is from the perspective of a high school / junior college computer science instructor. I will be sharing my experience labeling image data and training models using Create ML. Labeling your data correctly and training a model will allow you to use the model to detect objects in images such as stills or videos.

I decided to focus on using Core ML as it can be a quick way for me to introduce these topics to my students in the context of iOS app development. Using this framework would allow my students to play around with many important concepts in deep learning while giving them practical applications that will run on their devices immediately.

## Getting Started

### Dependencies

* Since this demo uses Create ML, you will need to run a MacOS operating system that is compatible with the latest versions by downloading the latest copy of [XCode](https://developer.apple.com/xcode/). You can find this easily on the Apple App Store.
* On that note, the steps in labeling images are transferrable to training models using other methods such as [Google Collab](https://colab.research.google.com/) or [Jupyter Notebook](https://jupyter.org/). 

### Installs

* [labelme](https://github.com/labelmeai/labelme?tab=readme-ov-file#starter-guide)
* You will need to install _labelme_ as a way to easily label your data to train models. Please see the instructions in the link.

### Data Files
* Have a handful of images you will label for detection in a folder you can easily locate on your computer. Or use the provided images in the repository linked [here](https://github.com/TBSDrJ/YOLO-Attempt-1). 

### Executing program

* Please run label me using the instructions [here](https://github.com/labelmeai/labelme?tab=readme-ov-file#usage). In a terminal window, run the command below once label me is installed. 
```
labelme  # just open gui
```
Once the program executes, click the Open Dir button and direct it to the folder containing your images. 
<p align = "center">
<img src = "https://github.com/domdavid/objectDetectionCoreMLDemo/blob/main/images/open.png" width = "400px" height = "300px"></img>
</p>

### Labeling Your Data

* Use the Next Image and Prev Image buttons to go through your image data. For each image, create Polygons that surround the objects you are trying to label. Label these accordingly. For example, if you're labeling a bunch of bananas then you will likely use banana as a label as you draw polygons.
* Unless you're going to be segmenting images (separating objects and cutting them out), you can just draw rectangles!
<p align = "center">
<img src="https://github.com/domdavid/objectDetectionCoreMLDemo/blob/main/examplePolygon.jpg" width="300" height="250" />
</p>

### Encode to COCO Format

While labelme simplifies adding labels to image data, COCO is a much more popular format for the annotations. Download the [script](https://github.com/fcakyon/labelme2coco/blob/master/labelme2coco/labelme2coco.py) to your image folder (the one with annotations). The folder that contained your original image files should now have a bunch of .json files. Once the script is in the same folder as your images, you can run the command below in your terminal. This will create a new folder called result. The folder will contain a .json file (with your annotations), a jpeg folder, and a visualization folder (containing your images with the overlayed labels).

```
python labelme2coco.py ./ result --labels labels.txt
```
### Generate Create ML .json File

Lastly, you will need to convert the .json files to a single file that will be used in Create ML. You can use the provided [script](https://github.com/domdavid/objectDetectionCoreMLDemo/blob/main/convert.py). Run it in the terminal similar to the previous step. 

```
python labelme2coco.py ./ result --labels labels.txt
```
### Ready?! 
Your folder structure after annotating your data should look like the following. 
<p align = "center">
   <img src = "https://github.com/domdavid/objectDetectionCoreMLDemo/blob/main/images/folderStructure.png" width = "400px" height = "300px"></img>
</p>

### Start Create ML

Start Create ML by opening XCode and going to the developer tools as shown in the image below. 
<p align = "center">
   <img src = "https://github.com/domdavid/objectDetectionCoreMLDemo/blob/main/images/startCML.png" width = "300px" height = "300px"> </img>
</p>

### Create a new Object Detection Project

<p align = "center">
   <img src = "https://github.com/domdavid/objectDetectionCoreMLDemo/blob/main/images/cmlCreate.png" width = "300px" height = "300px"> </img>
</p>

### Reference the training folder

You can drag and drop the folder into the training Data Box in Create ML or you can click on the + button and direct it to the folder. This is why you need to know where your folders are located. Take the time now to get organized if you need to so you can navigate your project files easily.
<p align = "center">
   <img src = "https://github.com/domdavid/objectDetectionCoreMLDemo/blob/main/images/train.png" width = "300px" height = "300px"> </img>
</p>

### Train!
You are all set to start training. 

At this point, read up on how to train models for object detection so you can play around with the different parameters you can fine tune! 

## Help

One hiccup that you might run into is that Create ML may not find classes for the annotations you made. Open the .json file and make sure the labels are correct. Your file format and structure should be similar to [mine](https://github.com/domdavid/objectDetectionCoreMLDemo/blob/main/result/annotations.createml.json)

## Authors

[@DomDavid](https://x.com/dom_david)

## Version History

* 0.1
    * Initial Release

## License

Feel free to use...

## Acknowledgments

Inspiration, code snippets, etc.
* [labelme](https://github.com/labelmeai/labelme)
* [coremltools](https://apple.github.io/coremltools/docs-guides/)
