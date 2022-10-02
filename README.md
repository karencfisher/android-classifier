# android-classifier
First attempt to deploy an image classifier on Android device

![Screenshot](Screenshot.jpg)

This project is to go through the basic process from building an image classifier using transfer learning, convert the trained model to Tensorflow Lite format, and then deploy the model for inference on a mobile device. For me this is a learning process, also, in building an Android application in Kotlin, on Android Studio. 

Looking at a couple of examples of real time inference using the devices camera, they made predictions asynchronously/continuously. This is not what I wanted. My preference instead is to get a subject in the camera frame, and touch a button to make an inference on that image. So to accomplish this I used the image capture use case with CameraX instead of the analyze use case. I capture an image into a buffer, preprocess the captured image (scaling, reformatting bitmap to expected 3d array of pixel values, and normalizing), and run it through the classifier.

To use perhaps a more useful model (i.e., do more than classifying everything as either a cat or a dog), one should simply be able replace the tflite model file and the accompanying text file containing the labels, and (at this point) modify two lines in the Classifier class definition as necessary.

```
class Classifier(assetManager: AssetManager) {
    //...
    private val modelPath: String = "CatsVsDogs.tflite"
    private val labelPath: String = "label.txt"
```

