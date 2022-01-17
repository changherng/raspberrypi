# Object Detection using custom dataset on the Raspberrypi
## Introduction
This guide provides step-by-step instructions for how to set up TensorFlow Lite on the Raspberry Pi and use it to run object detection models. It also shows how to set up the Coral USB Accelerator on the Pi and run Edge TPU detection models. It works for the Raspberry Pi 3 and Raspberry Pi 4 running either Rasbpian Buster or Rasbpian Stretch.
## Setting Up
First, the Raspberry Pi needs to be fully updated. Open a terminal and issue:

    sudo apt-get update
    sudo apt-get dist-upgrade
Next, clone this GitHub repository by issuing the following command. The repository contains the scripts we'll use to run TensorFlow Lite, as well as a shell script that will make installing everything easier. Issue:

    git clone https://github.com/EdjeElectronics/TensorFlow-Lite-Object-Detection-on-Android-and-Raspberry-Pi.git
This downloads everything into a folder called TensorFlow-Lite-Object-Detection-on-Android-and-Raspberry-Pi. That's a little long to work with, so rename the folder to "tflite1" and then cd into it:

    mv TensorFlow-Lite-Object-Detection-on-Android-and-Raspberry-Pi tflite1
    cd tflite1
I'm using a virtual environment for this guide because it prevents any conflicts between versions of package libraries that may already be installed on your Pi. Keeping TensorFlow installed in its own environment allows us to avoid version conflicts.

    sudo pip3 install virtualenv
Then, create the "tflite1-env" virtual environment by issuing:
    
    python3 -m venv tflite1-env
This will create a folder called tflite1-env inside the tflite1 directory. The tflite1-env folder will hold all the package libraries for this environment. Next, activate the environment by issuing:

    source tflite1-env/bin/activate
### You'll need to issue the source tflite1-env/bin/activate command from inside the /home/pi/tflite1 directory to reactivate the environment every time you open a new terminal window.
## Install TensorFlow Lite dependencies and OpenCV
Next, we'll install TensorFlow, OpenCV, and all the dependencies needed for both packages. OpenCV is not needed to run TensorFlow Lite, but the object detection scripts in this repository use it to grab images and draw detection results on them.

    bash get_pi_requirements.sh
This downloads about 400MB worth of installation files, so it will take a while. Go grab a cup of coffee while it's working! If you'd like to see everything that gets installed, simply open get_pi_dependencies.sh to view the list of packages.
## Set up TensorFlow Lite detection model
Next, we'll set up the detection model that will be used with TensorFlow Lite. A detection model has two files associated with it: a detect.tflite file (which is the model itself) and a labelmap.txt file (which provides a labelmap for the model). My preferred way to organize the model files is to create a folder (such as "BirdSquirrelRaccoon_TFLite_model") and keep both the detect.tflite and labelmap.txt in that folder. This is also how Google's downloadable sample TFLite model is organized.
