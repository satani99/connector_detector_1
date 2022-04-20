# Prepare the data 

The first step to train a model is to have good quality data. To build my dataset I
labeled all of them by hand using [makesense.ai](https://www.makesense.ai/). In that case,
I chose just one class, but the software can be used to annotate multiple classes as well.
It generated an XML file per image that contains all annotations and bounding boxes.
Then converted the XML to TF.record format using [create_tfrecords_from_xml.py](https://github.com/satani99/connector_detector_1/blob/main/create_tfrecords_from_xml.py).
Then I created a labelmap file to define the classes that were going to be used.In my case
Connector was the only one.


# Choosing the model

This project was based on one-class object detection problem, so I chose SSD MobileNet v2
320x320 from [Tensorflow 2 Detection Model Zoo](https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/tf2_detection_zoo.md).


# Configure training 
Defined training parameters as below:
num_classes = 1
batch_size = 96
num_steps = 7500
num_eval_steps = 1000

With the parameters set, started training.

# Exporting the model

After training is complpeted, I exported the model. Converted the training checkpoints to
a protobuf(pb) file.

# Deploying the model

The model needed to be deployed on the web so that anyone can open a PC or mobile camera
and perform inferences in real-time through a web browser. To do that, I converted the
saved model to the Tensorflow.js layers format, loaded the model in a javascript application
and made everything available on [Glitch](https://glitch.com/).
