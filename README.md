Step 1

Make a folder called ./training-images in the current folder.

Step 2

Make subsequent folders in the above created folder by the name of the person you want to train with.
Eg.

./training-images/rishabb-yadav/
./trainging-images/will-ferrell/

Step 3

Copy images into the correct subfolders.

Step 4

Run the following from the above directory-

python align-dlib.py --dlibFacePredictor ./shape_predictor_68_face_landmarks.dat ./training-images/  align outerEyesAndNose ./aligned-images/ --size 96

This will create a new folder called ./aligned-images and produce images which are cropped and aligned for subsequent steps.

Step 5

Next, run the following from the above directory-

 ./batch-represent/main.lua -outDir ./generated-embeddings/ -data ./aligned-images/
 This will generate 128 measurements in a .csv file according to the images in aligned-images.

 Step 6

We will train your face recognition model:

./demos/classifier.py train ./generated-embeddings/

This will generate a new file called ./generated-embeddings/classifier.pkl. This file has the SVM model used to recognize new faces.

Step 7

Get a new picture with an unknown face. Pass it to the classifier script like this:

./demos/classifier.py infer ./generated-embeddings/classifier.pkl your_test_image.jpg