# Computer Pointer Controller
## short introduction
using gaze detection model to control the mouse pointer of a computer. You will be using the Gaze Estimation model to estimate the gaze of the user's eyes and change the mouse pointer position accordingly. This project will demonstrate your ability to run multiple models in the same machine and coordinate the flow of data between those models
all this with the help of openvino toolkit by using input image (video file or webcam feed) is sent to the face recognition model

## Project Set Up and Installation
### Setup

#### Prerequisites
  - the program will better work perfectly if you use openvinot toolkit new release versions like from 2020.2 to 2021 " You need to install openvino successfully." 
  - install the library for python all listed on the requirments.txt, Check the requirement.txt
  - check the logging basic.log file and logging time.log 

#### FAST WAY TO DOWNLOAD THE OPENVINO 

type the below command and then follow the steps in this link after 
```
wget http://registrationcenter-download.intel.com/akdlm/irc_nas/16612/l_openvino_toolkit_p_2020.2.120.tgz
```
Openvino setup process : [guide](https://docs.openvinotoolkit.org/2020.2/_docs_install_guides_installing_openvino_linux.html)
# process of excuting this program easly 
#### Step 1
Clone the all the up repository by typing on the command lines below :
```
git clone https://github.com/mohanadkoko/Computer-Pointer-Controller.git 
```
#### Step 2
Initialize the openVINO environment:-
```
source /opt/intel/openvino/bin/setupvars.sh -pyver 3.5
```
#### Step 3
go to the diractory of the downloaded repository and check the tree of the file.
```
tree
```

Download the following models by using openVINO model downloader inside saparated file like name "models":-
this my recommanded tree of the files :
```
├── bin
│   └── demo.mp4
├── log
│   ├── logging_basic.log
│   ├── logging_time.log
│ 
├── models
│   └─ FP16       
│       └─── model_precision
│               ├── all models_name.bin
│               └── all models_name.xml
│   └─ FP32
│       └─── model_precision
│               ├── all models_name.bin
│               └── all models_name.xml
├── README.md
├── requirements.txt
├── src
    ├── computer_pointer.py
    ├── face_detection.py
    ├── facial_landmarks_detection.py
    ├── gaze_estimation.py
    ├── head_pose_estimation.py
    ├── input_feeder.py
    └── mouse_controller.py
```
** Now download the needed models in the file you have selected 

**1. Face Detection Model**
```
python3 /opt/intel/openvino/deployment_tools/tools/model_downloader/downloader.py --name "face-detection-adas-binary-0001"
```
**2. Facial Landmarks Detection Model**
```
python3 /opt/intel/openvino/deployment_tools/tools/model_downloader/downloader.py --name "landmarks-regression-retail-0009"
```
**3. Head Pose Estimation Model**
```
python3 /opt/intel/openvino/deployment_tools/tools/model_downloader/downloader.py --name "head-pose-estimation-adas-0001"
```
**4. Gaze Estimation Model**
```
python3 /opt/intel/openvino/deployment_tools/tools/model_downloader/downloader.py --name "gaze-estimation-adas-0002"
```


# all set now to run the code 

#### Project directory structure



## Demo

**1. Change the directory to src directory of project repository**
```
cd <project-repo-path>
```
If you need more help for the command line arguments, try:``` python3 src/computer_pointer.py -h```
**2. running the program** with **FP16**, **CPU** 
**the face model only comes with precision FP32**
**make sure you put the path right for the downloaded models**
```
python3 src/computer_pointer.py \
--video bin/demo.mp4 \
--output_path output/demo_output.mp4 \
--fd_model models/2020.2/FP16/face-detection-adas-binary-0001 \
--fl_model models/2020.2/FP16/landmarks-regression-retail-0009 \
--hp_model models/2020.2/FP16/head-pose-estimation-adas-0001 \
--ga_model models/2020.2/FP16/gaze-estimation-adas-0002 \
--threshold 0.7 \
--input_type video \
--device CPU \
--version 2020 \
--show_image yes
```

**3.running the program** with **FP32**, **CPU** input **video**
```
python3 src/computer_pointer.py \
--video bin/demo.mp4 \
--output_path output/demo_output.mp4 \
--fd_model models/2020.2/FP32/face-detection-adas-binary-0001 \
--fl_model models/2020.2/FP32/landmarks-regression-retail-0009 \
--hp_model models/2020.2/FP32/head-pose-estimation-adas-0001 \
--ga_model models/2020.2/FP32/gaze-estimation-adas-0002 \
--threshold 0.7 \
--input_type video \
--device CPU \
--version 2020 \
--show_image yes
```

## Documentation
##### "" you will be using the model paths in running the codes make sure are arranged correctly ""
### click on the model to see the discribtion:
* [face-detection-adas-binary-0001](https://docs.openvinotoolkit.org/latest/_models_intel_face_detection_adas_binary_0001_description_face_detection_adas_binary_0001.html)
* [landmarks-regression-retail-0009](https://docs.openvinotoolkit.org/latest/_models_intel_landmarks_regression_retail_0009_description_landmarks_regression_retail_0009.html)
* [head-pose-estimation-adas-0001](https://docs.openvinotoolkit.org/latest/_models_intel_head_pose_estimation_adas_0001_description_head_pose_estimation_adas_0001.html)
* [gaze-estimation-adas-0002](https://docs.openvinotoolkit.org/latest/_models_intel_gaze_estimation_adas_0002_description_gaze_estimation_adas_0002.html)

The project needs some basic input and some optimal input. 


- input_feeder.py
 Contains InputFeeder class which initialize VideoCapture as per the user argument and return the frames one by one.

- mouse_controller.py
 Contains MouseController class which take x, y coordinates value, speed, precisions and according these values it moves the mouse pointer by using pyautogui library.




## Benchmarks
The model load time and the inference time can be found in the logging_time.log file.the program was tested with `CPU`, levels of precision. `FP32, FP16, INT8`


## Results
GPU proccesed more frames per second compared to any other hardware and specially when model precision is FP16 because GPU has severals Execution units and their instruction sets are optimized for 16bit floating point data types.
my test has the lowest load time and the total on FP16 for my device .my device is intel `CORE I5`. since I tested the application with the demo video feed only, I was unable to test the accuracy for now.
## SCREENSHOT 
<p align="center">
<img src="bin/screenshot.jpg" width=400px height=350px/>
</p>


![This is a alt text.](/Computer-Pointer-Controller/bin/screenshot.jpg.")


### Comparison: Total model load time/Inference time
### Model load time & inference time  ***FP16***
**Start time logger**
2020-11-20 22:58:50,235 INFO Facedetection load time: 188.478
2020-11-20 22:58:50,321 INFO Facial_Landmarks load time: 85.835
2020-11-20 22:58:50,436 INFO Headpose load time: 114.982
2020-11-20 22:58:50,566 INFO Gaze load time: 129.861
2020-11-20 22:58:50,566 INFO Total model load time: `519.623`
2020-11-20 22:58:50,566 INFO ##################
2020-11-20 22:58:50,844 INFO Average face inference time: 104.55894470214844
2020-11-20 22:58:50,864 INFO Average facial inference time: 2.4504661560058594
2020-11-20 22:58:50,870 INFO Average headpose inference time: 5.302667617797852
2020-11-20 22:58:50,877 INFO Average gaze inference time: 6.855010986328125
2020-11-20 22:58:50,877 INFO Total inference time: ``137.2537612915039`

### Model load time & inference time***FP32***
**Start time logger**
2020-11-20 23:03:35,814 INFO Facedetection load time: 203.3
2020-11-20 23:03:35,928 INFO Facial_Landmarks load time: 113.568
2020-11-20 23:03:36,043 INFO Headpose load time: 115.088
2020-11-20 23:03:36,169 INFO Gaze load time: 125.613
2020-11-20 23:03:36,169 INFO Total model load time: `558.112`
2020-11-20 23:03:36,169 INFO ##################
2020-11-20 23:03:36,458 INFO Average face inference time: 115.55790901184082
2020-11-20 23:03:36,477 INFO Average facial inference time: 2.2363662719726562
2020-11-20 23:03:36,483 INFO Average headpose inference time: 5.983829498291016
2020-11-20 23:03:36,491 INFO Average gaze inference time: 7.672548294067383
2020-11-20 23:03:36,491 INFO Total inference time: `148.31995964050293`
2020-11-20 23:03:36,491 INFO ----

### Model load time & inference time ***INT8***
**Start time logger**
2020-11-20 23:06:03,922 INFO Facedetection load time: 186.181
2020-11-20 23:06:04,033 INFO Facial_Landmarks load time: 110.795
2020-11-20 23:06:04,272 INFO Headpose load time: 238.407
2020-11-20 23:06:04,562 INFO Gaze load time: 289.855
2020-11-20 23:06:04,562 INFO Total model load time: `825.687`
2020-11-20 23:06:04,562 INFO ##################
2020-11-20 23:06:04,836 INFO Average face inference time: 101.85050964355469
2020-11-20 23:06:04,855 INFO Average facial inference time: 2.3262500762939453
2020-11-20 23:06:04,860 INFO Average headpose inference time: 4.399538040161133
2020-11-20 23:06:04,867 INFO Average gaze inference time: 7.376432418823242
2020-11-20 23:06:04,867 INFO Total inference time:` 133.56566429138184`
2020-11-20 23:06:04,867 INFO ----

## Stand Out Suggestions
On the code added anOutput Video` section to record the session. for the sake of practise in detection added the "nose" and the left and right "lip corners" as the output image.you can also hide the output image by changing the arguments to --show_image no. 
## Edge Cases
- in case of more than one face detected in the frame then model takes the first detected face for control the mouse pointer by changing the threshold or take another precision `FP32, FP16, INT8` .
- if no head detected it will skip the frame 
I tested the application with the demo video feed only, I was unable to test the accuracy for now
